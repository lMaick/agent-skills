# 🧠 Agent Skills Hub (`agent-skills`)

> Repositório central, padronizado e versionado de **Skills Especializadas para Agentes de IA**.  
> Projetado para alimentar ecossistemas multi-agentes (como `meuplantao`, `mkdigital` e novas ferramentas) através de carregamento dinâmico (*Just-in-Time*).

---

## 🎯 Filosofia de Orquestração

Em vez de manter dezenas de agentes com papéis fixos e personas duplicadas:
1. **Workers Versáteis**: Agentes de execução (Orca, Claude Code, Codex, Antigravity) executam qualquer tarefa.
2. **Despacho via Linear**: Cada issue no Linear define o escopo, critérios de aceite e a **Skill Obrigatória** deste repositório.
3. **Execução Especializada**: O agente lê o `SKILL.md` designado, assimila instantaneamente as regras inegociáveis, padrões de código e heurísticas daquele domínio, e realiza a entrega.

---

## 📂 Catálogo Completo de Skills por Setor (43 Skills)

### 🎨 1. Frontend & UI/UX (6 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`frontend/impeccable`** | Polimento estético avançado, hierarquia, tipografia, contraste e anti-UI-slop. | Hub / Community |
| **`frontend/design-motion-principles`** | Animações suaves, microinterações, easing, springs e acessibilidade vestibular. | Emil Kowalski / Hub |
| **`frontend/web-design-guidelines`** | Boas práticas de UI/UX, responsividade, formulários e navegação moderna. | `vercel-labs/agent-skills` |
| **`frontend/react-best-practices`** | Performance React, data fetching, bundle optimization e eliminação de waterfalls. | `vercel-labs/agent-skills` |
| **`frontend/composition-patterns`** | Arquitetura de componentes React, composição e eliminação de props drilling. | `vercel-labs/agent-skills` |
| **`frontend/frontend-design`** | Direção visual forte, evitando interfaces genéricas produzidas por IA. | `anthropics/skills` |

---

### 🗄️ 2. Backend & Banco de Dados (5 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`backend/supabase-rls-guard`** | RLS estrito, isolamento `auth.uid()`, RPCs atômicas e imutabilidade financeira. | Camada Própria do Hub |
| **`backend/nextjs-app-router`** | Padrões de Server Components, Camada DAL (`src/lib/<modulo>`) e Server Actions com Zod. | Camada Própria do Hub |
| **`backend/supabase`** | Operação geral: Auth, Postgres, Storage, Edge Functions e SDK. | `supabase/agent-skills` |
| **`backend/supabase-postgres-best-practices`** | Otimização de queries, índices, concorrência e boas práticas de banco. | `supabase/agent-skills` |
| **`backend/postgresql-code-review`** | Auditoria de SQL/Postgres para schemas, consultas e segurança antes do merge. | `github/awesome-copilot` |

---

### 📣 3. Marketing & Growth (12 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`marketing/copywriting`** | Copy de alta conversão para landing pages, anúncios, headlines e CTAs. | `coreyhaines31/marketingskills` |
| **`marketing/copy-editing`** | Revisão, polimento e fortalecimento de textos já existentes. | `coreyhaines31/marketingskills` |
| **`marketing/carousel-storytelling`** | Roteirização de carrosséis de 5 a 7 slides para Instagram e LinkedIn. | Camada Própria do Hub |
| **`marketing/social`** | Estratégia de redes sociais, formatos, plataformas e adaptação de conteúdo. | `coreyhaines31/marketingskills` |
| **`marketing/content-strategy`** | Planejamento de conteúdo, pilares editoriais, temas e visão de longo prazo. | `coreyhaines31/marketingskills` |
| **`marketing/product-marketing`** | Posicionamento, proposta de valor, messaging e diferenciação de SaaS. | `coreyhaines31/marketingskills` |
| **`marketing/marketing-plan`** | Plano de marketing tático estruturado a partir das metas do produto. | `coreyhaines31/marketingskills` |
| **`marketing/launch`** | Estratégia e checklist de lançamento de produtos e features. | `coreyhaines31/marketingskills` |
| **`marketing/pricing`** | Estratégias de preço, planos, tiers e estrutura comercial de SaaS. | `coreyhaines31/marketingskills` |
| **`marketing/onboarding`** | Otimização da jornada inicial do usuário para aceleração do "Aha! Moment". | `coreyhaines31/marketingskills` |
| **`marketing/seo-audit`** | Auditoria técnica e semântica de SEO para busca orgânica. | `coreyhaines31/marketingskills` |
| **`marketing/analytics`** | Instrumentação de eventos, funis de conversão e métricas de retenção. | `coreyhaines31/marketingskills` |

---

### 🛡️ 4. QA & Confiabilidade (8 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`qa/playwright-e2e`** | Testes ponta a ponta mobile-first (360px-430px), Page Objects e sem flakiness. | Camada Própria do Hub |
| **`qa/webapp-testing`** | Exploração e validação funcional completa de aplicações web. | `anthropics/skills` |
| **`qa/test-driven-development`** | Ciclo TDD rigoroso: teste primeiro, implementação mínima e refatoração. | `obra/superpowers` |
| **`qa/systematic-debugging`** | Diagnóstico metódico de causa-raiz antes de tocar em qualquer linha de código. | `obra/superpowers` |
| **`qa/verification-before-completion`** | Obriga a IA a apresentar provas de execução antes de finalizar uma tarefa. | `obra/superpowers` |
| **`qa/requesting-code-review`** | Padroniza o handoff e a solicitação formal de code review. | `obra/superpowers` |
| **`qa/playwright-explore-website`** | Exploração autônoma de fluxos antes da escrita de asserções. | `github/awesome-copilot` |
| **`qa/playwright-generate-test`** | Geração de especificações Playwright a partir de casos reais. | `github/awesome-copilot` |

---

### 📐 5. Produto & Engenharia de Requisitos (8 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`product/linear-orchestrator`** | Protocolo universal de orquestração de tarefas e aprovação no Linear. | Camada Própria do Hub |
| **`product/linear-issue-spec`** | Manual de decomposição cirúrgica de issues e critérios Gherkin. | Camada Própria do Hub |
| **`product/to-spec`** | Transforma ideias brutas ou vagas em especificações técnicas claras. | `mattpocock/skills` |
| **`product/to-tickets`** | Decompõe especificações em tarefas atômicas e executáveis. | `mattpocock/skills` |
| **`product/domain-modeling`** | Modelagem de entidades, invariantes, estados e regras de negócio. | `mattpocock/skills` |
| **`product/research`** | Pesquisa técnica estruturada antes de definir arquiteturas ou dependências. | `mattpocock/skills` |
| **`product/create-specification`** | Elaboração formal de especificações funcionais de engenharia. | `github/awesome-copilot` |
| **`product/create-implementation-plan`** | Conversão de especificação em plano de arquivos, etapas e dependências. | `github/awesome-copilot` |

---

### ⚙️ 6. DevOps & Segurança (4 Skills)
| Skill | Descrição / Foco | Fonte / Referência |
| :--- | :--- | :--- |
| **`devops/security-review`** | Auditoria de segurança de código e vetores de ataque antes do deploy. | `github/awesome-copilot` |
| **`devops/secret-scanning`** | Detecção de chaves privadas, tokens de API e credenciais expostas. | `github/awesome-copilot` |
| **`devops/multi-stage-dockerfile`** | Construção de imagens Docker multi-stage enxutas para produção. | `github/awesome-copilot` |
| **`devops/incident-postmortem`** | Relatórios pós-incidente, análise de causa-raiz e planos de remediação. | `github/awesome-copilot` |

---

## 🚀 Como Integrar nos Projetos da Organização

### Método 1: Como Git Submodule (Recomendado)
Para conectar este repositório central em qualquer projeto (`meuplantao`, `mkdigital`, etc.):

```bash
# Na raiz do seu projeto:
git submodule add https://github.com/lMaick/agent-skills.git .agents/skills

# Para atualizar todas as skills para a versão mais recente da main:
git submodule update --remote --merge
```

### Método 2: Referência em Despachos no Linear
Quando o Orquestrador criar uma issue, ele referencia a skill necessária:

```markdown
## 🛠️ Skill Obrigatória
* **Skill:** `skills/frontend/web-design-guidelines/SKILL.md`
* **Repositório Central:** [lMaick/agent-skills](https://github.com/lMaick/agent-skills)
```

---

## 🛡️ Licença & Manutenção
Mantido por **Maick Campos** (@lMaick).  
Distribuído sob licença MIT para uso em todos os projetos da organização.
