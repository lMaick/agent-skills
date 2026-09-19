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

## 📂 Estrutura de Setores

```text
agent-skills/
├── skills/
│   ├── frontend/        # UI/UX, Design Systems, Acessibilidade, Motion e Frameworks
│   │   ├── impeccable/               # Polimento estético, tipografia, contraste e anti-slop
│   │   └── design-motion-principles/ # Animações suaves, microinterações e springs
│   ├── backend/         # Arquitetura de APIs, Banco de Dados, RLS e Performance
│   ├── marketing/       # Copywriting, Storytelling, Calendário Editorial e Redes Sociais
│   ├── qa/              # Testes E2E, TDD, Testes de Mutação e Auditoria de Qualidade
│   ├── product/         # PRDs, Critérios de Aceite, Análise de Requisitos e User Stories
│   └── devops/          # CI/CD, Docker, Observabilidade, Infra e Segurança
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
* **Skill:** `.agents/skills/skills/frontend/impeccable/SKILL.md`
* **Referência:** [agent-skills/frontend/impeccable](https://github.com/lMaick/agent-skills/tree/main/skills/frontend/impeccable)
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
