---
name: linear-orchestrator
description: >-
  Protocolo universal de orquestração de tarefas para qualquer setor via Linear.
  Define o modo exato de executar: alinhamento com o usuário, especificação e criação da issue no Linear,
  atribuição de skills especializadas, execução pelo agente trabalhador, entrega estruturada diretamente no card,
  revisão visual pelo usuário na coluna In Review e finalização pós-aprovação.
---

# 🧭 Linear Orchestrator — Protocolo Operacional Padrão (SOP)

Este protocolo define o modo exato de orquestrar e executar qualquer tipo de tarefa (desenvolvimento de código, design/UI, marketing, QA, infraestrutura ou produto) utilizando o **Linear** como central de controle e aprovação.

---

## 🔄 Fluxo de Execução Passo a Passo

```text
[1. Alinhamento] ➔ [2. Criação da Issue] ➔ [3. Execução pelo Worker] ➔ [4. Entrega no Card] ➔ [5. In Review] ➔ [6. Decisão do Usuário] ➔ [7. Conclusão]
                                                                                                        │
                                                                                                [Needs Rework]
```

---

### Etapa 1: Alinhamento & Especificação (Orquestrador)
1. Receber o objetivo ou pedido do usuário em linguagem natural.
2. Identificar o setor da tarefa (`dev`, `marketing`, `design`, `qa`, `devops` ou `product`).
3. Selecionar a skill especializada correspondente no repositório `agent-skills`.
4. Criar a Issue no Linear contendo:
   * **Título**: claro e objetivo, seguindo Conventional Commits (ex: `feat:`, `fix:`, `mkt:`, `design:`).
   * **Objetivo & Contexto**: o resultado esperado e o valor para o produto.
   * **Skill do Hub**: caminho relativo da skill que orienta o trabalhador.
   * **Escopo do Entregável**: lista exata dos itens a serem produzidos.
   * **Critérios de Aceite**: checklist objetivo de validação.
   * **Template de Entrega**: seção reservada no card para o trabalhador preencher.
5. Manter a issue no status **`Todo`** e informar ao usuário no chat apenas a confirmação com o link do card criado.

---

### Etapa 2: Execução Especializada (Agente Trabalhador)
1. Assumir a Issue no Linear e alterar seu status para **`In Progress`**.
2. Carregar e seguir as diretrizes contidas no `SKILL.md` indicado na issue.
3. Executar o trabalho de acordo com os padrões daquela especialidade:
   * **Tarefas de Código / Dev**: criar branch dedicada, implementar código com testes e garantir CI verde.
   * **Tarefas de Marketing / Conteúdo**: produzir arte/criativo visual, legenda persuasiva, hashtags e programar data/horário.
   * **Tarefas de Design / UI**: prototipar ou ajustar componentes com foco em acessibilidade e ergonomia mobile.
   * **Tarefas de QA / Infra**: rodar auditorias, testes E2E ou scripts de infraestrutura.

---

### Etapa 3: Entrega Estruturada Dentro do Card (Agente Trabalhador)
O trabalhador preenche a entrega **diretamente no corpo da Issue no Linear**, organizando as informações para visualização imediata pelo usuário:

```markdown
---
### 📦 Entregável para Aprovação

#### Detalhes da Entrega:
* **Resumo**: [O que foi produzido e resultado obtido]
* **Arquivos / Links**: [Branch, PR no GitHub, Imagem anexada ou arquivos gerados]
* **Evidências de Validação**: [Testes executados, prints ou links de preview]

#### Checklist de Decisão:
- [ ] Aprovado para finalização
- [ ] Ajustes necessários (comentar no card)
---
```

Após preencher o card, alterar o status da Issue para **`In Review`**.

---

### Etapa 4: Revisão & Decisão no Linear (Usuário)
1. O usuário abre o Linear (aplicativo móvel ou versão web) e visualiza os cards na coluna **`In Review`**.
2. O usuário examina o entregável direto no card e define a ação:
   * **Aprovação**: o usuário marca o checkbox de aprovação e move o card para **`Done`**.
   * **Solicitação de Ajustes**: o usuário escreve os ajustes desejados nos comentários do card e move para **`Needs Rework`**.

---

### Etapa 5: Ciclo de Retrabalho (quando houver ajustes)
1. O trabalhador lê o feedback deixado nos comentários da Issue.
2. Realiza os ajustes solicitados com base na skill da tarefa.
3. Atualiza os dados no corpo do card com a versão revisada.
4. Move o card novamente para **`In Review`**.

---

### Etapa 6: Finalização & Pós-Aprovação (Orquestrador)
Assim que a Issue atinge o status **`Done`**, executar o encerramento operacional:
* **Marketing**: disparar agendamento ou publicação automática via API do Postiz.
* **Desenvolvimento**: notificar que a PR está verde e pronta para merge humano.
* **Design / Produto**: homologar e consolidar documentação.
* Registrar confirmação final no Linear e notificar o usuário com resumo de 1 linha.
