---
name: nextjs-app-router
description: >-
  Especialista em arquitetura Next.js App Router (Next 15/16) e React 19.
  Aplica padrões estritos de Data Access Layer (DAL), Server Components por padrão,
  Server Actions validadas com Zod, streaming de UI com Suspense e prevenção de vazamento de estado.
---

# ⚡ Next.js App Router & Architecture Standards

Esta skill estabelece os padrões modernos de arquitetura para aplicações construídas com **Next.js App Router** e **TypeScript Estrito**.

---

## 🏛️ Princípios Arquiteturais

1. **Server Components por Padrão**: Todos os componentes são Server Components (`async function Component()`), a menos que precisem explicitamente de hooks de estado (`useState`, `useEffect`, `useActionState`) ou eventos de browser (`onClick`), onde `'use client'` deve ser colocado na primeira linha.
2. **Data Access Layer (DAL) Obrigatório**: Componentes de UI NUNCA fazem chamadas diretas soltas ao banco de dados ou `fetch` dispersos. Toda interação de dados reside estritamente em funções tipadas em `src/lib/<modulo>/` ou Server Actions dedicadas.
3. **Validação de Input Rígida**: Qualquer Server Action ou API Route que receba payload do usuário DEVE validar os dados com schemas **Zod** antes de qualquer processamento ou persistência.
4. **Sem Layout Shift (CLS)**: Todas as páginas que realizam carregamento de dados assíncronos devem envolver blocos assíncronos em `<Suspense fallback={<SkeletonComponent />}>`. Proibido telas em branco ou spinners soltos no meio do nada.

---

## 📂 Estrutura de Camadas Recomendada

```text
src/
├── app/                      # Rotas e páginas (App Router)
│   ├── (auth)/               # Grupo de rotas públicas / autenticação
│   ├── (dashboard)/          # Rotas autenticadas do sistema
│   └── layout.tsx            # Layout raiz com fontes e providers globais
├── components/
│   ├── ui/                   # Componentes atômicos do Design System (shadcn)
│   └── features/             # Componentes de negócio compostos
├── lib/                      # Data Access Layer (DAL) & Utilitários
│   ├── auth/                 # Sessão, validação de permissões
│   ├── financeiro/           # Queries e mutações do módulo financeiro
│   └── supabase/             # Clientes Supabase seguros (server.ts / client.ts)
└── types/                    # Tipagens TypeScript compartilhadas
```

---

## 📝 Padrão de Server Action Segura

```typescript
'use server';

import { z } from 'zod';
import { revalidatePath } from 'next/cache';
import { createServerClient } from '@/lib/supabase/server';

const CreateItemSchema = z.object({
  title: z.string().min(3, 'Título muito curto').max(100),
  amount: z.number().positive('O valor deve ser maior que zero'),
});

export type ActionState = {
  success: boolean;
  error?: string;
  data?: any;
};

export async function createItemAction(
  prevState: ActionState,
  formData: FormData
): Promise<ActionState> {
  const supabase = await createServerClient();
  const { data: { user } } = await supabase.auth.getUser();

  if (!user) {
    return { success: false, error: 'Acesso não autorizado.' };
  }

  const rawData = {
    title: formData.get('title'),
    amount: Number(formData.get('amount')),
  };

  const validation = CreateItemSchema.safeParse(rawData);
  if (!validation.success) {
    return {
      success: false,
      error: validation.error.errors.map(e => e.message).join(', '),
    };
  }

  const { error } = await supabase
    .from('items')
    .insert({ ...validation.data, user_id: user.id });

  if (error) {
    return { success: false, error: 'Erro ao salvar registro no banco.' };
  }

  revalidatePath('/dashboard');
  return { success: true };
}
```

---

## ✅ Checklist de Entrega para o Agente

- [ ] Arquivo TypeScript passa sem erros com `npx tsc --noEmit`?
- [ ] Server Actions contêm `'use server'` e validação com Zod?
- [ ] Não há `console.log` de debug ou tokens expostos?
- [ ] Skeleton condizente exibido durante carregamentos (`loading.tsx` ou `<Suspense>`)?
- [ ] Touch targets móveis com pelo menos 44x44px nos elementos interativos?
