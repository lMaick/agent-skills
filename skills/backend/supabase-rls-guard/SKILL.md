---
name: supabase-rls-guard
description: >-
  Especialista em segurança, integridade e arquitetura de dados no Supabase e PostgreSQL.
  Aplica regras estritas de Row Level Security (RLS), isolamento por tenant/user via auth.uid(),
  transações atômicas com RPCs e prevenção de vazamento de dados.
---

# 🛡️ Supabase RLS Guard & Database Integrity

Esta skill define as regras inegociáveis de segurança e integridade de dados em bancos de dados Supabase/Postgres consumidos por aplicações modernas.

---

## 🔒 Invariantes Não Negociáveis

1. **RLS Sempre Ativo**: Toda tabela exposta na API pública (`public.*`) DEVE ter `ALTER TABLE ... ENABLE ROW LEVEL SECURITY;`.
2. **Isolamento por Usuário**: Nenhuma query de leitura ou mutação pode rodar sem filtrar pelo usuário autenticado (`auth.uid() = user_id`).
3. **Imutabilidade Financeira e Contratos**: Proibido delete físico de registros que possuam dependências financeiras (ex: pagamentos, repasses, notas). Utilize cancelamento lógico auditável (`status = 'cancelled'`, `canceled_at = now()`).
4. **Valores Derivados vs Campos Manuais**: Saldos, juros e atrasos devem ser calculados com base nos dados reais ou funções imutáveis, nunca persistidos via input manual solto do frontend.
5. **RPCs com Contexto Seguro**: Funções Postgres `SECURITY DEFINER` devem obrigatoriamente definir `SET search_path = public, pg_temp;` para evitar ataques de injeção de schema.

---

## 📐 Template de Tabela & Policies Seguras

```sql
-- 1. Criação da tabela
CREATE TABLE IF NOT EXISTS public.orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
    title TEXT NOT NULL,
    amount NUMERIC(12, 2) NOT NULL CHECK (amount >= 0),
    created_at TIMESTAMPTZ NOT NULL DEFAULT timezone('utc'::text, now()),
    updated_at TIMESTAMPTZ NOT NULL DEFAULT timezone('utc'::text, now())
);

-- 2. Ativação obrigatória de RLS
ALTER TABLE public.orders ENABLE ROW LEVEL SECURITY;

-- 3. Policy de Leitura (SELECT)
CREATE POLICY "Users can only view their own orders"
    ON public.orders FOR SELECT
    USING (auth.uid() = user_id);

-- 4. Policy de Inserção (INSERT)
CREATE POLICY "Users can only insert their own orders"
    ON public.orders FOR INSERT
    WITH CHECK (auth.uid() = user_id);

-- 5. Policy de Atualização (UPDATE)
CREATE POLICY "Users can only update their own orders"
    ON public.orders FOR UPDATE
    USING (auth.uid() = user_id)
    WITH CHECK (auth.uid() = user_id);
```

---

## ⚡ Transações Atômicas via RPC (Remote Procedure Call)

Para operações multi-tabela (ex: salvar um pedido e debitar um saldo), utilize sempre funções atômicas em PL/pgSQL para evitar inconsistência por concorrência:

```sql
CREATE OR REPLACE FUNCTION public.process_transaction(
    p_amount NUMERIC,
    p_description TEXT
)
RETURNS UUID
LANGUAGE plpgsql
SECURITY DEFINER
SET search_path = public, pg_temp
AS $$
DECLARE
    v_user_id UUID;
    v_new_id UUID;
BEGIN
    -- Captura o usuário da sessão Supabase
    v_user_id := auth.uid();
    IF v_user_id IS NULL THEN
        RAISE EXCEPTION 'Não autenticado' USING ERRCODE = '42501';
    END IF;

    -- Executa operações atômicas
    INSERT INTO public.transactions (user_id, amount, description)
    VALUES (v_user_id, p_amount, p_description)
    RETURNING id INTO v_new_id;

    RETURN v_new_id;
END;
$$;
```

---

## ✅ Checklist de Auditoria para o Agente

Antes de finalizar qualquer tarefa de banco de dados, verifique:
- [ ] O RLS foi explicitamente ativado na tabela criada?
- [ ] As 4 políticas básicas (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) cobrem apenas `auth.uid() = user_id`?
- [ ] A migration foi salva em `supabase/migrations/` com timestamp cronológico?
- [ ] Não há `service_role_key` vazando no código client-side?
- [ ] Nenhum componente React chama o banco diretamente (tudo passa pelo DAL em `src/lib/<modulo>`)?
