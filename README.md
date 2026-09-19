# 🧠 Agent Skills Hub (`agent-skills`)

> Repositório central e versionado de **Skills Especializadas para Agentes de IA**.  
> Projetado para ser consumido de forma modular e reutilizável por qualquer projeto (como `meuplantao`, `mkdigital` e futuros ecossistemas).

---

## 🎯 Objetivo

Eliminar a necessidade de manter dezenas de agentes com papéis fixos. Em vez disso, adotamos a **Arquitetura JIT (Just-in-Time)**:
1. Qualquer agente inteligente (Orca, Codex, Claude Code, Antigravity, etc.) pode executar tarefas em qualquer domínio.
2. Na issue do Linear, especificamos a skill obrigatória localizada neste repositório.
3. O agente lê o `SKILL.md` correspondente e carrega todo o repertório técnico, heurísticas e diretrizes necessárias.

---

## 📂 Catálogo de Skills Ativas por Setor

```text
agent-skills/
├── skills/
│   ├── frontend/
│   │   ├── impeccable/               # Polimento estético, tipografia, contraste e anti-slop
│   │   └── design-motion-principles/ # Animações suaves, microinterações e springs
│   ├── backend/
│   │   ├── supabase-rls-guard/       # Auditoria de RLS, isolamento auth.uid() e RPCs atômicas
│   │   └── nextjs-app-router/        # Server Components, DAL pattern e Server Actions com Zod
│   ├── marketing/
│   │   ├── high-converting-copy/     # Copywriting persuasivo (PAS, AIDA) e ganchos de conversão
│   │   └── carousel-storytelling/    # Roteirização de carrosséis de 5-7 slides de alta retenção
│   ├── qa/
│   │   └── playwright-e2e/           # Testes ponta a ponta mobile-first (360px-430px) e POM
│   └── product/
│       └── linear-issue-spec/        # Especificação cirúrgica de issues com critérios Gherkin
```

---

## 🚀 Como Consumir em Novos Projetos

### Método 1: Como Git Submodule (Recomendado)
Para vincular este hub ao seu projeto e manter tudo sincronizado com um comando:

```bash
# Na raiz do seu projeto (ex: meuplantao ou mkdigital)
git submodule add https://github.com/lMaick/agent-skills.git .agents/skills

# Para atualizar todas as skills para a versão mais recente da main:
git submodule update --remote --merge
```

### Método 2: Referência Direta em Issues do Linear
Ao despachar uma tarefa no Linear, indique o caminho relativo da skill:

```markdown
## 🛠️ Skill Requerida
* **Skill Principal:** `skills/frontend/impeccable/SKILL.md`
* **Skill Complementar:** `skills/frontend/design-motion-principles/SKILL.md`
* **Repositório Central:** [lMaick/agent-skills](https://github.com/lMaick/agent-skills)
```

---

## 📋 Padrão de uma Nova Skill (`SKILL.md`)

Toda nova skill adicionada a este repositório deve conter um arquivo `SKILL.md` contendo:
* **YAML Frontmatter**: `name` e `description` clara para indexação.
* **Objetivo & Escopo**: Quando usar e quando NÃO usar.
* **Invariantes & Regras Rígidas**: Princípios inegociáveis de qualidade.
* **Exemplos de Entrada/Saída**: Padrões "Antes vs. Depois".
* **Scripts & Referências (opcional)**: Ferramentas auxiliares ou links de documentação.

---

## 🛡️ Licença & Manutenção
Mantido por **Maick Campos** (@lMaick).  
Distribuído sob licença MIT para uso em todos os projetos da organização.
