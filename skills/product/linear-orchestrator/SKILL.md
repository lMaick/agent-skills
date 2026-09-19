---
name: linear-orchestrator
description: >-
  Protocolo de orquestração do MeuPlantão (Maick + Gravity + Linear + Braço Executor).
  Define a divisão em 4 papéis, o fluxo padrão de tarefas para qualquer setor, o formato de prompt em 5 blocos
  e a gestão de entregas via Linear até a aprovação final do dono.
---

# 🧭 Time de Operação com IA (Maick + Gravity + Linear + Executor)

Este protocolo define a engenharia de operação e orquestração para todos os setores do MeuPlantão e ferramentas da organização.

---

## 👥 Os 4 Papéis

* **Você (Maick)** = **O Dono**. Define os pedidos, avalia as entregas e tem a palavra final de aprovação.
* **Gravity** = **O Gerente / Orquestrador**. Entende o pedido, alinha a viabilidade, cria as tarefas no Linear com regras e skills, aciona o braço executor, audita a qualidade e apresenta a entrega.
* **Linear** = **O Mural**. A única fonte de verdade. Nenhuma tarefa existe fora do mural. Guarda status, prioridades, links e histórico.
* **O Braço Executor (Orca / Workers)** = **O Executor Isolado**. Cada tarefa ganha um ambiente isolado (worktree para código, worker para marketing/conteúdo) para produzir a entrega e abrir PR ou formatar o entregável.

---

## 🔄 Fluxo Padrão

1. **Pedido do Dono**: Maick traz o objetivo em linguagem natural.
2. **Tarefa no Linear (O Mural)**: Gravity cria a issue no Linear via MCP com título claro, prioridade, setor e a skill obrigatória de `agent-skills`.
3. **Disparar o Executor**:
   * *Para Código / Dev*: disparar via Orca CLI em worktree isolada:
     ```bash
     orca worktree create --repo name:meuplantao --name nome-da-task --base-branch main --agent claude --prompt "..." --activate
     ```
   * *Para Marketing / Design / Outros*: despachar para o worker correspondente com a skill indicada.
4. **Acompanhar**: verificar commit na worktree (`git log --oneline -3`), status do card no Linear ou logs de execução.
5. **Revisão Técnica do Gerente (Gravity)**:
   * Se código: auditar diff (`gh pr diff`), testes e lint verdes (`gh pr checks`).
   * Se marketing/conteúdo: checar tom de voz, imagem e legenda no card.
6. **Aprovação do Dono (Maick)**: Maick visualiza o PR ou o card no Linear na coluna `In Review` e dá o veredito.
7. **Finalização**:
   * Se código aprovado: merge via squash e branch deletada (`gh pr merge --squash --delete-branch`).
   * Se post aprovado: agendamento disparado no Postiz (`node ops/marketing/postiz-client.mjs`).
   * Fechar a tarefa no Linear (`Done`).

---

## 📝 O Prompt do Executor (Estrutura em 5 Blocos)

Toda tarefa delegada ao executor deve conter exatamente estes 5 blocos:

1. **TAREFA**: objetivo numerado, direto e específico (quais arquivos ou telas criar/modificar).
2. **CONTEXTO**: o que já existe no projeto, bibliotecas usadas e padrão arquitetural.
3. **FRONTEIRAS**: o que pertence a esta tarefa e o que NÃO deve ser tocado (evita colisão de arquivos e permite paralelismo).
4. **REGRAS & SKILLS**: indicação da skill obrigatória em `.agents/skills-hub/skills/...` e regras do `AGENTS.md`.
5. **ENTREGA**: formato esperado (branch própria + PR para `main` sem mergear, ou preenchimento no card do Linear).

---

## 🏆 Regras de Ouro

* **Paralelismo por Dono de Arquivo**: Nunca dois executores ativos alterando os mesmos arquivos ao mesmo tempo.
* **Deploy e Merge são do Dono**: Gravity e os executores nunca fazem merge em produção sem o OK de Maick.
* **Zero Segredos**: Chaves, tokens e URLs privadas nunca aparecem em prompts, commits ou issues.
* **Nada entra quebrado**: CI vermelho nunca mergeia; testes e typecheck são barreiras obrigatórias.
* **Mural Atualizado**: O card no Linear sempre reflete o estado real da tarefa (`Todo` ➔ `In Progress` ➔ `In Review` ➔ `Done`).
