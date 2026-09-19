---
name: linear-issue-spec
description: >-
  Especialista em decomposição de produto e escrita de issues no Linear para orquestração de IAs e humanos.
  Padroniza especificações com escopo cirúrgico, não-escopo explícito, critérios de aceite Gherkin
  e vinculação de skills do repositório agent-skills.
---

# 📐 Linear Issue Specification Standard

Esta skill rege a criação e refinamento de issues no Linear para garantir que qualquer agente ou desenvolvedor entenda exatamente o que deve ser entregue, sem ambiguidades ou alucinações.

---

## 🏛️ Princípios de uma Boa Issue para Agentes

1. **Contexto Antes do Código**: Explique o "porquê" (a dor do usuário final) antes do "o quê".
2. **Não-Escopo Explícito**: Declarar o que **NÃO** deve ser feito é tão importante quanto o que deve ser feito. Isso previne que a IA tente refatorar o projeto inteiro.
3. **Skill Obrigatória Indicada**: Toda issue técnica ou de marketing deve apontar explicitamente qual skill de `agent-skills` guia a execução.
4. **Critérios de Aceite Verificáveis**: Use formato checklist objetivo ou sintaxe Gherkin (`Dado que... Quando... Então...`).

---

## 📋 Template Padrão de Issue no Linear

```markdown
### 🎯 Objetivo
[Descrição em 1 ou 2 frases do resultado esperado e valor entregue].

---

### 🏥 Contexto de Negócio / Clínico
[Qual é a dor real do usuário que motivou essa demanda? Onde isso impacta a rotina?].

---

### 🛠️ Skills Obrigatórias (`agent-skills`)
* **Skill Principal:** `skills/frontend/impeccable/SKILL.md`
* **Skill Complementar:** `skills/frontend/design-motion-principles/SKILL.md`

---

### 📂 Escopo Técnico & Arquivos Impactados
* **Criar:** `src/components/features/NovoComponente.tsx`
* **Modificar:** `src/lib/modulo/dal.ts` (adicionar função `getResumoFinanceiro`)
* **Testes:** `tests/e2e/novo-fluxo.spec.ts`

---

### 🚫 Não-Escopo (O que NÃO fazer)
* NÃO alterar schemas de banco de dados ou migrations existentes.
* NÃO modificar a navegação global (`Navbar.tsx` ou `Sidebar.tsx`).
* NÃO instalar dependências externas sem alinhamento prévio.

---

### ✅ Critérios de Aceite (Definition of Done)
- [ ] **Critério 1**: Dado um usuário logado com plantões pendentes, quando abrir a tela, deve ver o card com saldo recalculado em tempo real.
- [ ] **Critério 2**: Em conexões lentas, deve exibir skeleton screen proporcional (sem spinner isolado ou tela branca).
- [ ] **Critério 3**: Área de toque móvel nos botões de ação possui no mínimo 44x44px.
- [ ] **Critério 4**: CI passa 100% verde (`npm run lint`, `npx tsc --noEmit`, `npm test`).

---

### 📦 Protocolo de Retorno
Ao concluir, comente nesta issue no formato:
`[DELIVERY] @Orquestrador: Resumo da entrega, branch/PR criada e status dos testes.`
```

---

## ✅ Checklist do Orquestrador antes de Publicar a Issue

- [ ] O título segue Conventional Commits (ex: `feat(financeiro): card de saldo`, `fix(auth): redirect mobile`)?
- [ ] Os labels corretos de Setor (`setor:dev`, `setor:marketing`) e Prioridade foram aplicados?
- [ ] A skill necessária do `agent-skills` foi linkada?
- [ ] Os critérios de aceite são testáveis de forma binária (passou ou não passou)?
