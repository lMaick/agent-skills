---
name: linear-content-pipeline
description: >-
  Protocolo estrito de orquestração de conteúdo e social media via Linear.
  Define as fronteiras do Orquestrador (Gravity), a execução por workers especializados,
  a aprovação visual 100% dentro do Linear (coluna In Review) e o agendamento no Postiz.
---

# 🎯 Linear Content & Approval Pipeline

Esta skill estabelece as regras permanentes para o fluxo de planejamento, produção, revisão e agendamento de conteúdos sociais do MeuPlantão via Linear.

---

## 🚫 1. Separação Rígida de Papéis (Regra Inegociável)

1. **O Orquestrador (Gravity):**
   * **NUNCA** redige o texto final da postagem nem gera imagens diretamente no chat com o usuário.
   * **NUNCA** pede aprovação de textos longos dentro da conversa.
   * **FUNÇÃO EXCLUSIVA**: Entender a intenção do Maick, abrir/organizar as issues no Linear com as especificações técnicas, indicar as skills necessárias da estante (`copywriting`, `marketing-config`, etc.), e monitorar o status do quadro.
2. **O Trabalhador Especialista (Worker Agent):**
   * Lê a issue e as skills designadas no repositório.
   * Produz o criativo visual e a legenda persuasiva.
   * **Entrega o resultado formatado DENTRO da própria Issue no Linear** (anexando imagem e preenchendo o card).
   * Move o status da issue para **`In Review`**.
3. **O Aprovador (Maick):**
   * Abre o Linear (pelo celular ou computador) na coluna **`In Review`**.
   * Avalia a arte, a legenda e a data.
   * Se aprovado: marca o checkbox e move para **`Done`**.
   * Se precisar de ajustes: comenta no próprio card e move para **`Needs Rework`**.

---

## 📋 2. Estrutura do Card no Linear (A Mesa de Aprovação)

O trabalhador deve formatar o corpo da Issue no Linear para que o Maick tenha uma experiência executiva e limpa:

```markdown
### 🗓️ Data & Horário Sugerido
* **Data:** Segunda-feira, 22/09/2026 às 12h30
* **Canais:** Instagram (`@meuplantao.pro`) e Facebook

---

### 🖼️ Criativo Visual
![Mockup do Post](link-ou-anexo-da-imagem)

---

### 📝 Legenda Proposta
> [Texto completo da postagem aqui, com quebras de linha e emojis moderados]

**Hashtags:**
#medicina #plantonista #repassemedico #meuplantao

---

### ⚖️ Checklist de Aprovação do Maick
- [ ] Aprovado para agendamento automático no Postiz
- [ ] Ajustes solicitados (ver comentários abaixo)
```

---

## 🔄 3. Ciclo de Estados no Linear

```text
[Todo] ➔ [In Progress] ➔ [In Review] ➔ [Done] (Disparo no Postiz)
                               │
                        [Needs Rework] (Se Maick pedir ajustes)
```

1. **`Todo`**: Demanda criada pelo Orquestrador, com especificações e skills vinculadas.
2. **`In Progress`**: Worker especialista assumiu e está produzindo a arte e a copy.
3. **`In Review`**: O post está pronto e formatado dentro do card aguardando o Maick.
4. **`Needs Rework`**: Maick deixou comentários no card pedindo mudanças. O worker ajusta e devolve para `In Review`.
5. **`Done`**: Post aprovado pelo Maick. Aciona automaticamente o script do Postiz (`ops/marketing/postiz-client.mjs`).

---

## ⚙️ 4. Agendamento Automático (Postiz)

Assim que o card atinge o estado **`Done`**, a postagem é enviada para a API local do Postiz (`http://localhost:4007`) usando:
* **Canal padrão:** `MeuPlantão.App (@meuplantao.pro)`
* **Mídia:** Imagem aprovada.
* **Data/Hora:** Programada conforme definido no card.

---

## ✅ Checklist do Orquestrador antes de falar com o Usuário

- [ ] Eu NÃO produzi o post no chat?
- [ ] O card foi criado no projeto correto do Linear?
- [ ] As skills de marketing necessárias foram referenciadas?
- [ ] Apenas avisei o usuário com o link do card no Linear para ele avaliar?
