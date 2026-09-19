---
name: linear-orchestrator
description: "Protocolo canônico de orquestração do MeuPlantão (Maick + Gravity + Linear + Orca). Define o modelo dos 4 papéis, o template rígido de 5 blocos, especificação de skills obrigatórias, template de comentário no Linear e economia de tokens no terminal."
---

# 🧭 Linear Orchestrator — Protocolo dos 4 Papéis (MeuPlantão)

Este skill é a **fonte canônica de operação** para criação, estruturação, delegação e acompanhamento de tarefas entre o Dono, o Gerente (IA), o Mural (Linear) e os Executores (Orca/Workers).

---

## 👥 1. Os 4 Papéis

- **Você (Maick) = O Dono:** Dá os pedidos em linguagem natural, aciona os workers no Orca e tem a palavra final de aprovação e merge dos PRs.
- **Gravity = O Gerente / Orquestrador:** Alinha a viabilidade, estrutura as tarefas no Linear em `Todo` com a label `Orca Ready` seguindo estritamente o template de 5 blocos. Gravity **NUNCA** dispara workers nem executa tarefas de produção sozinho no chat.
- **Linear = O Mural Canônico:** A fonte única da verdade. Nenhuma tarefa existe fora do mural. Guarda status, prioridades, links de PRs e histórico de entrega.
- **Orca / Workers = O Braço Executor:** O Maick abre o Orca (**Tasks → Linear**), filtra por `Orca Ready`, seleciona a issue e cria o workspace para o worker executar o ciclo completo (código/arte + commit + push + PR + relatório no Linear).

---

## 🔄 2. Como Usar Este Skill (Fluxo Passo a Passo)

### Passo 1: Alinhamento do Pedido
1. O Dono (Maick) envia o objetivo (ex: "preciso de um post sobre repasses atrasados" ou "quero suporte a dark mode").
2. Gravity analisa a viabilidade técnica/clínica, propõe o escopo e confirma com o Dono.

### Passo 2: Criação da Issue no Linear (via Gravity)
Gravity usa o Linear MCP para criar a issue aplicando o seguinte checklist obrigatório:
- **Projeto:** `MeuPlantao - Novo Fluxo` (`bd99b748-a38d-4355-bf1c-057ec9b1d398`).
- **Status Inicial:** `Todo`.
- **Labels:** `Orca Ready` + tag da área (`Dev`, `Marketing`, `Bug`, `Feature`, `Infra`).
- **Prioridade:** 1 (Urgente), 2 (Alta) ou 3 (Média).
- **Corpo da Issue:** Preenchido obrigatoriamente com o **Template Canônico dos 5 Blocos** abaixo.

### Passo 3: Ativação do Worker (via Maick no Orca)
1. Maick abre o app **Orca** ➔ vai em **Tasks** ➔ **Linear**.
2. Filtra pelas issues com label **`Orca Ready`**.
3. Clica na issue e cria o workspace para o worker iniciar.

### Passo 4: Execução Isolada pelo Worker
1. O worker lê a issue no Linear, identifica as **Skills Obrigatórias** e trabalha no branch correspondente.
2. Executa a suíte de testes e linters locais (`npm test && npm run lint && npx tsc --noEmit && npm run build`).
3. Executa o ciclo de Git: `git add .`, commit convencional, `git push` e `gh pr create` para `main`.
4. Publica o **relatório completo estruturado como comentário no Linear**.
5. **Economia de Tokens:** Responde no terminal do Orca apenas uma linha:
   `Concluído: PR #X aberta e relatório postado no Linear.`

### Passo 5: Revisão e Merge do Dono
1. Maick visualiza o PR no GitHub ou o card no Linear na coluna `In Review`.
2. Após aprovação do Dono, o PR é mergeado via squash (`gh pr merge --squash --delete-branch`).
3. A issue no Linear é atualizada para `Done`.
4. *Para tarefas de marketing:* o disparo/agendamento no Postiz é executado imediatamente após o merge.

---

## 📝 3. Template Canônico do Briefing (5 Blocos Rígidos)

Toda issue criada para o Orca DEVE usar exatamente esta estrutura:

```markdown
---
**Skills Obrigatórias:** `[ex: design-motion-principles, impeccable, frontend-developer]`
**Modelo Recomendado:** `[Codex / Claude Sonnet / GPT-4o]` (High Effort)
**Branch Base:** `main` ➔ `[feat|fix|docs]/[mai-XXX-slug]`
---

### 1. TAREFA & OBJETIVO
[Descrição numerada, clara e precisa do que deve ser construído, corrigido ou gerado]

### 2. CONTEXTO & PADRÕES DO REPO
[Arquivos existentes, contratos, design system, paleta de cores ou regras clínicas envolvidas]

### 3. FRONTEIRAS & ARQUIVOS PERMITIDOS
- **Arquivos permitidos para alteração/criação:** `[lista explícita]`
- **NÃO TOCAR:** `[arquivos fora do escopo para evitar regressões ou conflitos de merge]`

### 4. REGRAS & CRITÉRIOS DE ACEITE
- [Critério funcional/clínico 1]
- [Critério de UX/Motion 2]
- Testes 100% verdes (`npm test && npm run lint && npx tsc --noEmit && npm run build`).
- Respeito estrito ao `AGENTS.md` (RLS Supabase, dados derivados, sem segredos em código).

### 5. ENTREGA & TEMPLATE OBRIGATÓRIO (Git + Linear)
1. Executar no terminal do worktree:
   ```bash
   git add .
   git commit -m "[feat|fix|docs]([escopo]): [mensagem] (MAI-XXX)"
   git push -u origin [branch]
   gh pr create --base main --title "[feat|fix|docs]([escopo]): [mensagem] (MAI-XXX)" --body "Fixes #MAI-XXX"
   ```
2. **Comentário Obrigatório no Linear:** Publicar este template preenchido no card da issue:
   ```markdown
   🚀 **Entrega Concluída — MAI-XXX:**
   - **Pull Request:** https://github.com/lMaick/meuplantao/pull/XXX
   - **Branch:** [branch]
   - **Commit:** [SHA]
   - **O que foi feito:**
     - [Item 1]
     - [Item 2]
   - **Status dos Testes:** Todos os testes passando (npm test / typecheck / lint verdes).
   ```
3. **Economia de Tokens no Terminal Orca:** Ao terminar, responda no terminal APENAS uma linha:
   `Concluído: PR aberta e relatório postado no Linear.`
```

---

## 🏆 4. Regras de Ouro Não Negociáveis

1. **Paralelismo por Dono de Arquivo:** Nunca dois workers ativos alterando os mesmos arquivos simultaneamente.
2. **Deploy e Merge são do Dono:** Gravity e workers nunca fazem merge em `main` sem o OK explícito de Maick.
3. **Zero Segredos:** Chaves privadas, tokens e senhas pertencem unicamente a `.env.local` e secrets de CI.
4. **Nada entra quebrado:** CI vermelho barra o merge.
5. **Economia de Tokens no Orca:** Workers reportam detalhadamente apenas no Linear; o terminal recebe apenas a confirmação de uma linha.
