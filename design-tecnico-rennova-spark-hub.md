# Design Técnico — Portal de Gestão da Inovação Rennova

> Documento técnico objetivo para orientar implementação, revisão e manutenção do Rennova Spark Hub.

---

<a id="sumario"></a>
## Sumário

- [1. Identificação do projeto](#dt-1-identificacao-do-projeto)
- [2. Resumo técnico da solução](#dt-2-resumo-tecnico-da-solucao)
- [3. Arquitetura geral](#dt-3-arquitetura-geral)
  - [3.1 Visão de alto nível](#dt-3-1-visao-de-alto-nivel)
  - [3.2 Componentes da solução](#dt-3-2-componentes-da-solucao)
- [4. Stack tecnológica](#dt-4-stack-tecnologica)
- [5. Decisões técnicas](#dt-5-decisoes-tecnicas)
  - [DT001 - Lovable como fonte principal do front-end](#dt-dt001-lovable-como-fonte-principal-do-front-end)
  - [DT002 - Supabase como fonte de verdade do portal](#dt-dt002-supabase-como-fonte-de-verdade-do-portal)
  - [DT003 - Chamadas externas somente via Edge Functions](#dt-dt003-chamadas-externas-somente-via-edge-functions)
  - [DT004 - Asana como ferramenta operacional, não fonte de governança](#dt-dt004-asana-como-ferramenta-operacional-nao-fonte-de-governanca)
  - [DT005 - Dashboard baseado em `asana_sync`](#dt-dt005-dashboard-baseado-em-asana-sync)
  - [DT006 - Webhook + cron para sincronização Asana](#dt-dt006-webhook-cron-para-sincronizacao-asana)
  - [DT007 - Provider de IA configurável](#dt-dt007-provider-de-ia-configuravel)
  - [DT008 - Escala de priorização 1–5](#dt-dt008-escala-de-priorizacao-1-5)
  - [DT009 - Não usar custom fields de projeto no Asana](#dt-dt009-nao-usar-custom-fields-de-projeto-no-asana)
  - [DT010 - Logs funcionais em `activity_log`](#dt-dt010-logs-funcionais-em-activity-log)
- [6. Modelo de dados](#dt-6-modelo-de-dados)
  - [6.1 Entidade: `profiles`](#dt-6-1-entidade-profiles)
  - [6.2 Entidade: `departments`](#dt-6-2-entidade-departments)
  - [6.3 Entidade: `ideas`](#dt-6-3-entidade-ideas)
  - [6.4 Entidade: `projects`](#dt-6-4-entidade-projects)
  - [6.5 Entidade: `project_phases`](#dt-6-5-entidade-project-phases)
  - [6.6 Entidade: `project_phase_tasks`](#dt-6-6-entidade-project-phase-tasks)
  - [6.7 Entidade: `project_metrics`](#dt-6-7-entidade-project-metrics)
  - [6.8 Entidade: `project_comments`](#dt-6-8-entidade-project-comments)
  - [6.9 Entidade: `asana_sync`](#dt-6-9-entidade-asana-sync)
  - [6.10 Entidade: `triage_sessions`](#dt-6-10-entidade-triage-sessions)
  - [6.11 Entidade: `activity_log`](#dt-6-11-entidade-activity-log)
  - [6.12 Entidade recomendada: `asana_webhooks`](#dt-6-12-entidade-recomendada-asana-webhooks)
  - [6.13 Enums e valores controlados](#dt-6-13-enums-e-valores-controlados)
- [7. Contratos de API](#dt-7-contratos-de-api)
  - [API001 - GET `/functions/v1/public-departments`](#dt-api001-get-functions-v1-public-departments)
  - [API002 - POST `/functions/v1/submit-idea`](#dt-api002-post-functions-v1-submit-idea)
  - [API003 - POST `/functions/v1/ai-assist-block`](#dt-api003-post-functions-v1-ai-assist-block)
  - [API004 - POST `/functions/v1/ai-summarize-idea`](#dt-api004-post-functions-v1-ai-summarize-idea)
  - [API005 - POST `/functions/v1/approve-idea-summary`](#dt-api005-post-functions-v1-approve-idea-summary)
  - [API006 - POST `/functions/v1/asana-create-project`](#dt-api006-post-functions-v1-asana-create-project)
  - [API007 - POST `/functions/v1/asana-webhook`](#dt-api007-post-functions-v1-asana-webhook)
  - [API008 - POST `/functions/v1/asana-sync`](#dt-api008-post-functions-v1-asana-sync)
  - [API009 - POST `/functions/v1/ai-generate-insight`](#dt-api009-post-functions-v1-ai-generate-insight)
- [8. Integrações externas](#dt-8-integracoes-externas)
  - [INT001 - Asana](#dt-int001-asana)
  - [INT002 - Provedor de IA](#dt-int002-provedor-de-ia)
- [9. Autenticação e autorização](#dt-9-autenticacao-e-autorizacao)
  - [9.1 Estratégia de autenticação](#dt-9-1-estrategia-de-autenticacao)
  - [9.2 Sessão e expiração](#dt-9-2-sessao-e-expiracao)
  - [9.3 Perfis e permissões](#dt-9-3-perfis-e-permissoes)
  - [9.4 Regras de acesso](#dt-9-4-regras-de-acesso)
- [10. Tratamento de erros](#dt-10-tratamento-de-erros)
  - [10.1 Erros de frontend](#dt-10-1-erros-de-frontend)
  - [10.2 Erros de backend](#dt-10-2-erros-de-backend)
  - [10.3 Erros de integração](#dt-10-3-erros-de-integracao)
- [11. Logs e observabilidade](#dt-11-logs-e-observabilidade)
  - [11.1 Eventos que devem gerar log](#dt-11-1-eventos-que-devem-gerar-log)
  - [11.2 Informações que devem constar no log](#dt-11-2-informacoes-que-devem-constar-no-log)
  - [11.3 Informações que não devem constar no log](#dt-11-3-informacoes-que-nao-devem-constar-no-log)
- [12. Segurança técnica](#dt-12-seguranca-tecnica)
- [13. Estratégia de deploy](#dt-13-estrategia-de-deploy)
  - [13.1 Ambientes](#dt-13-1-ambientes)
  - [13.2 Processo de deploy](#dt-13-2-processo-de-deploy)
  - [13.3 Rollback](#dt-13-3-rollback)
- [14. Variáveis de ambiente e configurações](#dt-14-variaveis-de-ambiente-e-configuracoes)
- [15. Riscos técnicos](#dt-15-riscos-tecnicos)
- [16. Pendências técnicas](#dt-16-pendencias-tecnicas)
- [17. Aprovação técnica](#dt-17-aprovacao-tecnica)
---

<a id="dt-1-identificacao-do-projeto"></a>
## 1. Identificação do projeto

### Nome do projeto

**Rennova Spark Hub — Portal de Gestão da Inovação**

### Responsável técnico

**Nome:** Phablo Tavares  
**Área/Time:** Inovação / Desenvolvimento de Agentes e Soluções de IA  
**Data:** 2026-07-08  
**Versão:** 0.2

---

<a id="dt-2-resumo-tecnico-da-solucao"></a>
## 2. Resumo técnico da solução

Aplicação web em React/Vite, evoluída prioritariamente via Lovable, com Supabase para autenticação, Postgres, RLS e Edge Functions. O portal terá uma rota pública para submissão de ideias e rotas internas autenticadas para gestão do portfólio. Chamadas a IA e Asana serão feitas exclusivamente por Supabase Edge Functions. O Supabase será a fonte de verdade de governança; o Asana será usado para execução operacional de tarefas e sprints.

---

<a id="dt-3-arquitetura-geral"></a>
## 3. Arquitetura geral

<a id="dt-3-1-visao-de-alto-nivel"></a>
### 3.1 Visão de alto nível

```text
Colaborador externo ao portal interno
  ↓
/canvas público — React/Lovable
  ↓
Supabase Edge Functions: submit-idea, ai-assist-block, ai-summarize-idea
  ↓
Supabase Postgres: ideas, departments

Usuário interno: Diretoria / Inovação
  ↓
Portal interno — React/Lovable + Supabase Client
  ↓
Supabase Auth + RLS
  ↓
Supabase Postgres: profiles, ideas, projects, phases, metrics, comments, asana_sync

Portal interno
  ↓
Supabase Edge Functions
  ├── IA: OpenAI ou Claude
  └── Asana API: criar projeto, webhook, sync

Asana
  ↓ webhook
Supabase Edge Function: asana-webhook
  ↓
Supabase Postgres: asana_sync, activity_log

Supabase Scheduled Function / cron
  ↓
Edge Function: asana-sync
  ↓
Asana API + asana_sync
```

<a id="dt-3-2-componentes-da-solucao"></a>
### 3.2 Componentes da solução

| Componente | Tecnologia | Responsabilidade | Observações |
|---|---|---|---|
| Frontend | React, Vite, TypeScript, Tailwind, shadcn/Radix, Recharts | Interface pública e interna | Evolução principal via Lovable |
| Backend / API | Supabase Edge Functions | Regras sensíveis, integrações, IA, Asana, submissão pública | Não expor tokens no front-end |
| Banco de dados | Supabase Postgres | Persistência de ideias, projetos, usuários, governança e cache Asana | RLS habilitado |
| Autenticação | Supabase Auth | Login, sessão e identidade | E-mail/senha no MVP |
| Autorização | Supabase RLS + validação nas Edge Functions | Controle por `diretoria` e `inovacao` | Não depender só do front-end |
| IA | OpenAI ou Claude via Edge Function | Sugestões, resumo, notas IA e insights | Provider configurável por secret |
| Asana | Asana REST API + webhooks | Projeto operacional, tarefas e sprints | Portal lê cache em `asana_sync` |
| Logs | `activity_log` + logs das Edge Functions | Auditoria funcional e troubleshooting | Sem dados sensíveis |
| Deploy frontend | Lovable | Publicação do app web | Confirmar domínio/ambientes |
| Deploy backend | Supabase | Edge Functions, DB, Auth, cron | Configurar secrets por ambiente |

---

<a id="dt-4-stack-tecnologica"></a>
## 4. Stack tecnológica

| Camada | Tecnologia | Versão | Justificativa / observação |
|---|---|---|---|
| Frontend | React | 18.3.1 | Stack atual do projeto |
| Build | Vite | 8.0.0 | Stack atual do projeto |
| Linguagem | TypeScript | 5.8.3 | Tipagem e manutenção |
| UI | Tailwind CSS + shadcn/Radix | Tailwind 3.4.17 | Base visual atual do Lovable |
| Gráficos | Recharts | 2.15.4 | Matriz e indicadores |
| Estado/queries | TanStack React Query | 5.83.0 | Cache e queries client-side |
| Backend | Supabase Edge Functions | A confirmar | Integrações e lógica sensível |
| Banco de dados | Supabase Postgres | Managed | Fonte de verdade do portal |
| Autenticação | Supabase Auth | Managed | Login e sessão |
| ORM / Query builder | Supabase JS Client | A incluir | Acesso tipado ao Supabase pelo front-end |
| Integração Asana | Asana REST API | v1 | Criação, webhook e sync |
| IA | OpenAI ou Claude | Configurável | Provider via `AI_PROVIDER` |
| Hospedagem | Lovable + Supabase | A confirmar | Front no Lovable; backend no Supabase |
| CI/CD | Lovable GitHub sync / Supabase CLI | A definir | Evitar edição manual ampla do front |
| Monitoramento / logs | Supabase logs + `activity_log` | A definir | Diagnóstico mínimo |

---

<a id="dt-5-decisoes-tecnicas"></a>
## 5. Decisões técnicas

<a id="dt-dt001-lovable-como-fonte-principal-do-front-end"></a>
### DT001 - Lovable como fonte principal do front-end

#### Decisão

O front-end será evoluído prioritariamente pelo Lovable. Edições externas diretas em componentes React devem ser evitadas ou feitas apenas com controle e validação.

#### Contexto

O projeto foi criado no Lovable e há risco de perda de continuidade caso o código seja alterado externamente de forma incompatível.

#### Alternativas consideradas

- Editar tudo localmente com VS Code/Codex.
- Usar Lovable apenas para protótipos e migrar para desenvolvimento manual.
- Manter Lovable como fonte principal e isolar lógica crítica em Supabase.

#### Justificativa

Preserva a capacidade de evolução rápida no Lovable e reduz risco de quebra do fluxo de desenvolvimento.

#### Impactos

- Prompts para Lovable devem ser claros e incrementais.
- Backend crítico deve ser isolado em Edge Functions.
- Mudanças manuais no front exigem cautela.

<a id="dt-dt002-supabase-como-fonte-de-verdade-do-portal"></a>
### DT002 - Supabase como fonte de verdade do portal

#### Decisão

Ideias, triagem, projetos, governança, métricas, usuários e cache do Asana serão armazenados no Supabase.

#### Contexto

O portal precisa de dados estruturados, RLS, autenticação e regras de acesso.

#### Alternativas consideradas

- Usar apenas Asana como base.
- Usar banco próprio fora do Supabase.
- Usar Supabase com Postgres e RLS.

#### Justificativa

Supabase integra banco, Auth, RLS e Edge Functions com baixa complexidade operacional.

#### Impactos

- Modelagem deve ser bem definida.
- RLS deve ser revisada antes da produção.
- Edge Functions usam `service_role` apenas quando necessário.

<a id="dt-dt003-chamadas-externas-somente-via-edge-functions"></a>
### DT003 - Chamadas externas somente via Edge Functions

#### Decisão

Asana, IA e operações públicas sensíveis serão acessadas apenas por Edge Functions.

#### Contexto

Front-end não pode expor tokens de IA, Asana ou Supabase service role.

#### Alternativas consideradas

- Chamar APIs externas diretamente do front-end.
- Criar backend separado em Node.js.
- Usar Supabase Edge Functions.

#### Justificativa

Edge Functions reduzem superfície de ataque e mantêm arquitetura simples.

#### Impactos

- Toda função deve validar entrada e permissão.
- Secrets devem ser configurados por ambiente.
- Logs não podem incluir tokens.

<a id="dt-dt004-asana-como-ferramenta-operacional-nao-fonte-de-governanca"></a>
### DT004 - Asana como ferramenta operacional, não fonte de governança

#### Decisão

Asana gerencia tarefas, sprints e execução. O portal gerencia ideias, priorização, métricas, fases executivas e governança.

#### Contexto

O Asana já possui template operacional e custom fields de tarefa.

#### Alternativas consideradas

- Duplicar tarefas no portal.
- Criar custom fields de projeto no Asana para dados estratégicos.
- Separar governança no portal e operação no Asana.

#### Justificativa

Evita duplicidade operacional e mantém cada ferramenta no seu papel.

#### Impactos

- O portal exibe Asana em modo leitura.
- Dados estratégicos ficam apenas no Supabase.
- Conversão deve preencher descrição inicial no Asana.

<a id="dt-dt005-dashboard-baseado-em-asana-sync"></a>
### DT005 - Dashboard baseado em `asana_sync`

#### Decisão

Dashboard e detalhe do projeto lerão dados do Asana apenas de `asana_sync`.

#### Contexto

Chamadas ao Asana em tempo real podem causar lentidão, falha de tela e rate limit.

#### Alternativas consideradas

- Chamar Asana ao carregar Dashboard.
- Atualizar manualmente dados do Asana.
- Usar cache `asana_sync` com webhook e cron.

#### Justificativa

Garante performance e resiliência.

#### Impactos

- Pode haver pequena defasagem nos dados.
- Webhook e cron precisam ser monitorados.
- UI deve exibir data de última sincronização.

<a id="dt-dt006-webhook-cron-para-sincronizacao-asana"></a>
### DT006 - Webhook + cron para sincronização Asana

#### Decisão

Usar webhook para atualização próxima do tempo real e cron diário para reconciliação.

#### Contexto

Eventos de webhook podem falhar ou ser perdidos; cron garante consistência.

#### Alternativas consideradas

- Apenas webhook.
- Apenas cron.
- Webhook mais cron.

#### Justificativa

Combina rapidez e consistência.

#### Impactos

- Criar webhook por projeto convertido.
- Armazenar metadados/segredo do webhook com segurança.
- Tratar rate limit e retries.

<a id="dt-dt007-provider-de-ia-configuravel"></a>
### DT007 - Provider de IA configurável

#### Decisão

Usar variável `AI_PROVIDER` para alternar entre OpenAI e Claude.

#### Contexto

A escolha de provedor pode mudar por custo, qualidade, disponibilidade ou política interna.

#### Alternativas consideradas

- Fixar OpenAI.
- Fixar Claude.
- Abstrair provider por configuração.

#### Justificativa

Evita acoplamento e facilita troca futura.

#### Impactos

- Edge Functions devem normalizar respostas.
- Prompt e JSON schema devem ser compatíveis.
- Testes devem cobrir resposta inválida.

<a id="dt-dt008-escala-de-priorizacao-1-5"></a>
### DT008 - Escala de priorização 1–5

#### Decisão

Impacto e esforço usarão escala inteira de 1 a 5.

#### Contexto

O schema Supabase e a especificação do gerente usam escala 1–5; o protótipo atual usa 0–10.

#### Alternativas consideradas

- Manter escala 0–10.
- Usar escala qualitativa.
- Usar escala 1–5.

#### Justificativa

Escala 1–5 é simples, suficiente e alinhada ao schema.

#### Impactos

- Ajustar matriz atual.
- Validar check constraints.
- Deixar claro se nota é IA ou final.

<a id="dt-dt009-nao-usar-custom-fields-de-projeto-no-asana"></a>
### DT009 - Não usar custom fields de projeto no Asana

#### Decisão

Não criar custom fields de projeto no Asana para impacto, esforço e áreas.

#### Contexto

A especificação Asana define que esses dados vivem no Supabase.

#### Alternativas consideradas

- Duplicar dados estratégicos no Asana.
- Armazenar tudo no Asana.
- Armazenar governança no Supabase.

#### Justificativa

Evita divergência e simplifica o modelo.

#### Impactos

- Portal deve ser a fonte de dados estratégicos.
- Asana recebe apenas contexto descritivo e tarefas operacionais.

<a id="dt-dt010-logs-funcionais-em-activity-log"></a>
### DT010 - Logs funcionais em `activity_log`

#### Decisão

Ações relevantes serão registradas em `activity_log`.

#### Contexto

Conversões, mudanças de status e falhas precisam ser rastreáveis.

#### Alternativas consideradas

- Depender apenas de logs técnicos da plataforma.
- Criar tabela de auditoria funcional.
- Não registrar auditoria no MVP.

#### Justificativa

Aumenta rastreabilidade com baixo custo.

#### Impactos

- Definir ações padronizadas.
- Não registrar dados sensíveis.
- Logs técnicos continuam nas Edge Functions.

---

<a id="dt-6-modelo-de-dados"></a>
## 6. Modelo de dados

<a id="dt-6-1-entidade-profiles"></a>
### 6.1 Entidade: `profiles`

#### Descrição

Perfil interno vinculado ao usuário do Supabase Auth.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | auth.users.id | Identificador do usuário |
| nome | text | Sim | Não | '' | Nome exibido |
| email | text | Sim | Não | - | E-mail do usuário |
| role | app_role | Sim | Não | diretoria | Perfil funcional |
| ativo | boolean | Sim | Não | true | Controle de acesso |
| created_at | timestamptz | Sim | Não | now() | Criação |
| updated_at | timestamptz | Sim | Não | now() | Atualização |

#### Relacionamentos

- Pertence a `auth.users`.
- Pode ser owner de `projects`.
- Pode ser author de `project_comments`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| profiles_pkey | id | primary | Identificação |
| idx_profiles_role | role | recomendado | Filtros administrativos |

<a id="dt-6-2-entidade-departments"></a>
### 6.2 Entidade: `departments`

#### Descrição

Áreas de origem e áreas impactadas pelas ideias/projetos.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| nome | text | Sim | Sim | - | Nome do departamento |
| ativo | boolean | Sim | Não | true | Disponível para seleção |
| created_at | timestamptz | Sim | Não | now() | Criação |

#### Relacionamentos

- Referenciado por `ideas` e `projects`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| departments_nome_key | nome | unique | Evitar duplicidade |

<a id="dt-6-3-entidade-ideas"></a>
### 6.3 Entidade: `ideas`

#### Descrição

Submissões do Canvas público e itens do funil de inovação.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| nome_ideia | text | Sim | Não | - | Título da ideia |
| autor_nome | text | Sim | Não | - | Nome do autor |
| autor_email | text | Sim | Não | - | E-mail do autor |
| departamento_origem_id | uuid | Não | Não | - | Área de origem |
| departamento_impactado_id | uuid | Não | Não | - | Área impactada |
| problema | text | Não | Não | - | Bloco obrigatório no app |
| indicadores | text | Não | Não | - | Indicadores de sucesso |
| resolver_sem_ia | text | Não | Não | - | Solução sem IA |
| resolver_com_ia | text | Não | Não | - | Solução com IA |
| para_quem | text | Não | Não | - | Personas/público |
| dados | text | Não | Não | - | Dados e fontes |
| ferramentas | text | Não | Não | - | Ferramentas |
| resumo_ia | text | Não | Não | - | Resumo gerado por IA |
| resumo_aprovado | boolean | Sim | Não | false | Aprovação do autor |
| comentario_autor | text | Não | Não | - | Complemento do autor |
| impacto_ia | int | Não | Não | - | Nota IA 1–5 |
| esforco_ia | int | Não | Não | - | Nota IA 1–5 |
| impacto_final | int | Não | Não | - | Nota triagem 1–5 |
| esforco_final | int | Não | Não | - | Nota triagem 1–5 |
| status | idea_status | Sim | Não | rascunho | Status da ideia |
| triagem_mes | date | Não | Não | - | Mês de triagem |
| converted_project_id | uuid | Não | Recomendado | - | Projeto gerado |
| submitted_at | timestamptz | Não | Não | - | Data de envio |
| created_at | timestamptz | Sim | Não | now() | Criação |
| updated_at | timestamptz | Sim | Não | now() | Atualização |

#### Relacionamentos

- Referencia `departments`.
- Pode gerar um `project`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_ideas_status | status | btree | Filtros por status |
| idx_ideas_triagem | triagem_mes | btree | Triagem mensal |
| ideas_converted_project_unique | converted_project_id | unique recomendado | Idempotência |

<a id="dt-6-4-entidade-projects"></a>
### 6.4 Entidade: `projects`

#### Descrição

Projetos de inovação aprovados, com governança no portal e execução no Asana.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| origin_idea_id | uuid | Não | Recomendado | - | Ideia de origem |
| nome | text | Sim | Não | - | Nome do projeto |
| objetivo | text | Não | Não | - | Objetivo |
| problema | text | Não | Não | - | Problema |
| descricao | text | Não | Não | - | Descrição |
| resumo_ia | text | Não | Não | - | Resumo executivo |
| departamento_origem_id | uuid | Não | Não | - | Área origem |
| departamento_impactado_id | uuid | Não | Não | - | Área impactada |
| owner_id | uuid | Não | Não | - | Responsável interno |
| status | project_status | Sim | Não | ativo | Ativo/pausado/encerrado |
| progress_pct | int | Sim | Não | 0 | Progresso calculado |
| impacto | int | Não | Não | - | Nota final herdada |
| esforco | int | Não | Não | - | Nota final herdada |
| asana_project_gid | text | Não | Recomendado | - | ID Asana |
| asana_permalink | text | Não | Não | - | Link Asana |
| encerrado_em | timestamptz | Não | Não | - | Data de encerramento |
| encerrado_na_fase | project_phase | Não | Não | - | Fase de encerramento |
| created_at | timestamptz | Sim | Não | now() | Criação |
| updated_at | timestamptz | Sim | Não | now() | Atualização |

#### Relacionamentos

- Pode originar de uma `idea`.
- Referencia `departments` e `profiles`.
- Possui fases, métricas, comentários e `asana_sync`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_projects_status | status | btree | Dashboard/filtros |
| idx_projects_owner | owner_id | btree | Consulta por responsável |
| projects_origin_idea_unique | origin_idea_id | unique recomendado | Idempotência |
| projects_asana_project_gid_unique | asana_project_gid | unique recomendado | Evitar duplicidade Asana |

<a id="dt-6-5-entidade-project-phases"></a>
### 6.5 Entidade: `project_phases`

#### Descrição

Cinco fases fixas do ciclo de vida do projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| project_id | uuid | Sim | Não | - | Projeto |
| phase | project_phase | Sim | Não | - | Fase |
| ordem | int | Sim | Não | - | Ordem 1–5 |
| status | phase_status | Sim | Não | pendente | Estado da fase |
| observacao | text | Não | Não | - | Observação |
| concluida_em | timestamptz | Não | Não | - | Conclusão |
| updated_at | timestamptz | Sim | Não | now() | Atualização |

#### Relacionamentos

- Pertence a `projects`.
- Possui `project_phase_tasks`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| project_phases_project_phase_key | project_id, phase | unique | Uma fase por projeto |
| idx_phases_project | project_id | btree | Carregar detalhe |

<a id="dt-6-6-entidade-project-phase-tasks"></a>
### 6.6 Entidade: `project_phase_tasks`

#### Descrição

Checklist executivo de cada fase do projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| phase_id | uuid | Sim | Não | - | Fase |
| descricao | text | Sim | Não | - | Item do checklist |
| concluida | boolean | Sim | Não | false | Estado |
| ordem | int | Sim | Não | 0 | Ordenação |
| created_at | timestamptz | Sim | Não | now() | Criação |

#### Relacionamentos

- Pertence a `project_phases`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_phase_tasks_phase | phase_id | btree | Carregar checklist |

<a id="dt-6-7-entidade-project-metrics"></a>
### 6.7 Entidade: `project_metrics`

#### Descrição

Indicadores, metas, resultados e insights do projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| project_id | uuid | Sim | Não | - | Projeto |
| indicador | text | Sim | Não | - | Nome do indicador |
| meta_texto | text | Não | Não | - | Meta qualitativa |
| meta_valor | numeric | Não | Não | - | Meta numérica |
| unidade | text | Não | Não | - | Unidade |
| resultado_valor | numeric | Não | Não | - | Resultado numérico |
| resultado_texto | text | Não | Não | - | Resultado qualitativo |
| insight_ia | text | Não | Não | - | Insight gerado por IA |
| fase | project_phase | Não | Não | - | Fase associada |
| medido_em | timestamptz | Não | Não | - | Data da medição |
| created_at | timestamptz | Sim | Não | now() | Criação |
| updated_at | timestamptz | Sim | Não | now() | Atualização |

#### Relacionamentos

- Pertence a `projects`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_metrics_project | project_id | btree | Carregar métricas |

<a id="dt-6-8-entidade-project-comments"></a>
### 6.8 Entidade: `project_comments`

#### Descrição

Comentários de governança do projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| project_id | uuid | Sim | Não | - | Projeto |
| author_id | uuid | Sim | Não | - | Autor |
| corpo | text | Sim | Não | - | Comentário |
| created_at | timestamptz | Sim | Não | now() | Criação |

#### Relacionamentos

- Pertence a `projects`.
- Referencia `profiles`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_comments_project | project_id | btree | Carregar comentários |

<a id="dt-6-9-entidade-asana-sync"></a>
### 6.9 Entidade: `asana_sync`

#### Descrição

Cache de leitura dos dados operacionais do Asana por projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| project_id | uuid | Sim | Sim | - | Projeto |
| num_tasks | int | Não | Não | 0 | Total de tarefas |
| num_incomplete | int | Não | Não | 0 | Tarefas abertas |
| num_completed | int | Não | Não | 0 | Tarefas concluídas |
| status_distribution | jsonb | Não | Não | - | Contagem por status |
| last_status_update | text | Não | Não | - | Último status update |
| last_activity_at | timestamptz | Não | Não | - | Última atividade Asana |
| last_synced_at | timestamptz | Não | Não | - | Última sincronização |

#### Relacionamentos

- Pertence a `projects` como relação 1:1.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| asana_sync_pkey | project_id | primary | Consulta por projeto |

<a id="dt-6-10-entidade-triage-sessions"></a>
### 6.10 Entidade: `triage_sessions`

#### Descrição

Sessões mensais de triagem de ideias.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| mes | date | Sim | Sim | - | Mês da triagem |
| realizada_em | timestamptz | Não | Não | - | Data da realização |
| notas | text | Não | Não | - | Observações |
| created_at | timestamptz | Sim | Não | now() | Criação |

#### Relacionamentos

- Relacionamento lógico com `ideas.triagem_mes`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| triage_sessions_mes_key | mes | unique | Uma sessão por mês |

<a id="dt-6-11-entidade-activity-log"></a>
### 6.11 Entidade: `activity_log`

#### Descrição

Auditoria funcional de ações relevantes.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| entity_type | text | Sim | Não | - | Tipo da entidade |
| entity_id | uuid | Sim | Não | - | Registro afetado |
| action | text | Sim | Não | - | Ação executada |
| actor_id | uuid | Não | Não | - | Usuário, se aplicável |
| detalhe | jsonb | Não | Não | - | Detalhes não sensíveis |
| created_at | timestamptz | Sim | Não | now() | Criação |

#### Relacionamentos

- Pode referenciar `profiles` como ator.
- Relacionamento polimórfico por `entity_type` + `entity_id`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| idx_activity_entity | entity_type, entity_id | btree | Consulta por entidade |

<a id="dt-6-12-entidade-recomendada-asana-webhooks"></a>
### 6.12 Entidade recomendada: `asana_webhooks`

#### Descrição

Tabela recomendada para armazenar metadados de webhooks Asana por projeto.

#### Campos

| Campo | Tipo | Obrigatório? | Único? | Valor padrão | Descrição |
|---|---|---:|---:|---|---|
| id | uuid | Sim | Sim | gen_random_uuid() | Identificador |
| project_id | uuid | Sim | Não | - | Projeto portal |
| asana_project_gid | text | Sim | Não | - | Projeto Asana |
| webhook_gid | text | Sim | Sim | - | Webhook Asana |
| hook_secret | text | Sim | Não | - | Segredo de validação |
| active | boolean | Sim | Não | true | Estado do webhook |
| created_at | timestamptz | Sim | Não | now() | Criação |
| last_success_at | timestamptz | Não | Não | - | Último sucesso |
| last_failure_at | timestamptz | Não | Não | - | Última falha |

#### Relacionamentos

- Pertence a `projects`.

#### Índices necessários

| Índice | Campo(s) | Tipo | Finalidade |
|---|---|---|---|
| asana_webhooks_webhook_gid_key | webhook_gid | unique | Identificar webhook |
| idx_asana_webhooks_project | project_id | btree | Buscar por projeto |

---

<a id="dt-6-13-enums-e-valores-controlados"></a>
### 6.13 Enums e valores controlados

#### Enum: `app_role`

| Valor | Descrição |
|---|---|
| diretoria | Acesso interno somente leitura |
| inovacao | Gestão completa do portal |

#### Enum: `idea_status`

| Valor | Descrição |
|---|---|
| rascunho | Autor ainda preenchendo ou estado inicial interno |
| enviada | Ideia enviada, aguardando resumo IA |
| resumo_gerado | Resumo gerado, aguardando aprovação do autor |
| aprovada_autor | Autor aprovou, entra em matriz/triagem |
| em_triagem | Ideia em avaliação pela Inovação |
| virou_projeto | Ideia convertida em projeto |
| backlog | Ideia mantida para futuro |
| arquivada | Ideia descartada |

#### Enum: `project_phase`

| Valor | Descrição |
|---|---|
| ideacao | Ideação |
| validacao | Validação |
| mvp | MVP |
| implantacao | Implantação |
| producao | Produção |

#### Enum: `phase_status`

| Valor | Descrição |
|---|---|
| pendente | Ainda não iniciada |
| em_andamento | Fase atual/em execução |
| concluida | Fase concluída |

#### Enum: `project_status`

| Valor | Descrição |
|---|---|
| ativo | Projeto em andamento |
| pausado | Projeto temporariamente suspenso |
| encerrado | Projeto encerrado |

---

<a id="dt-7-contratos-de-api"></a>
## 7. Contratos de API

> As APIs abaixo serão Supabase Edge Functions. Leituras e CRUD simples autenticados podem usar Supabase Client respeitando RLS.

<a id="dt-api001-get-functions-v1-public-departments"></a>
### API001 - GET `/functions/v1/public-departments`

#### Descrição

Retornar departamentos ativos para o Canvas público.

#### Autenticação necessária

- [ ] Sim
- [x] Não

#### Permissões necessárias

Pública, apenas leitura de departamentos ativos.

#### Request

##### Parâmetros de rota

| Parâmetro | Tipo | Obrigatório? | Descrição |
|---|---|---:|---|
| - | - | - | - |

##### Query params

| Parâmetro | Tipo | Obrigatório? | Descrição |
|---|---|---:|---|
| - | - | - | - |

##### Body

Não aplicável.

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "departments": [
    { "id": "uuid", "nome": "Comercial" }
  ]
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 500 | Erro interno | `DEPARTMENTS_FETCH_FAILED` |

#### Requisitos relacionados

- RF003

#### Regras de negócio relacionadas

- RN004, RN006

---

<a id="dt-api002-post-functions-v1-submit-idea"></a>
### API002 - POST `/functions/v1/submit-idea`

#### Descrição

Receber submissão pública do Canvas, validar dados, aplicar anti-spam e gravar ideia.

#### Autenticação necessária

- [ ] Sim
- [x] Não

#### Permissões necessárias

Pública, com validação e proteção anti-spam.

#### Request

##### Body

```json
{
  "nome_ideia": "Automação de atendimento",
  "autor_nome": "Nome do autor",
  "autor_email": "autor@rennova.com.br",
  "departamento_origem_id": "uuid",
  "departamento_impactado_id": "uuid",
  "problema": "Texto",
  "indicadores": "Texto",
  "resolver_sem_ia": "Texto",
  "resolver_com_ia": "Texto",
  "para_quem": "Texto",
  "dados": "Texto opcional",
  "ferramentas": "Texto opcional",
  "honeypot": ""
}
```

#### Response de sucesso

**Status:** `201 Created`

```json
{
  "idea_id": "uuid",
  "status": "enviada"
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Dados inválidos | `VALIDATION_ERROR` |
| 429 | Rate limit | `RATE_LIMITED` |
| 500 | Erro interno | `IDEA_SUBMIT_FAILED` |

#### Requisitos relacionados

- RF003

#### Regras de negócio relacionadas

- RN004, RN006, RN007, RN028

---

<a id="dt-api003-post-functions-v1-ai-assist-block"></a>
### API003 - POST `/functions/v1/ai-assist-block`

#### Descrição

Gerar sugestão de preenchimento para um bloco do Canvas.

#### Autenticação necessária

- [ ] Sim
- [x] Não

#### Permissões necessárias

Pública, limitada por rate limit.

#### Request

##### Body

```json
{
  "block": "problema",
  "context": {
    "nome_ideia": "Texto",
    "area_origem": "Comercial",
    "area_impactada": "Atendimento",
    "campos_preenchidos": {
      "problema": "Texto parcial"
    }
  }
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "suggestion": "Sugestão editável para o bloco."
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Bloco inválido | `INVALID_BLOCK` |
| 429 | Rate limit | `RATE_LIMITED` |
| 502 | IA indisponível | `AI_PROVIDER_ERROR` |
| 500 | Erro interno | `AI_ASSIST_FAILED` |

#### Requisitos relacionados

- RF004

#### Regras de negócio relacionadas

- RN008, RN009, RN028

---

<a id="dt-api004-post-functions-v1-ai-summarize-idea"></a>
### API004 - POST `/functions/v1/ai-summarize-idea`

#### Descrição

Gerar resumo, impacto IA e esforço IA para uma ideia.

#### Autenticação necessária

- [ ] Sim
- [x] Não, se usado no fluxo público logo após submissão com token/controle

#### Permissões necessárias

Acesso restrito ao fluxo da própria ideia ou acionamento server-side após submissão.

#### Request

##### Body

```json
{
  "idea_id": "uuid",
  "approval_token": "token-temporario-se-aplicavel"
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "idea_id": "uuid",
  "resumo_ia": "Resumo consolidado da ideia.",
  "status": "resumo_gerado"
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Dados inválidos | `VALIDATION_ERROR` |
| 403 | Token inválido | `FORBIDDEN` |
| 404 | Ideia não encontrada | `IDEA_NOT_FOUND` |
| 502 | IA indisponível | `AI_PROVIDER_ERROR` |
| 500 | Erro interno | `AI_SUMMARY_FAILED` |

#### Requisitos relacionados

- RF005

#### Regras de negócio relacionadas

- RN008, RN009, RN010, RN011, RN028

---

<a id="dt-api005-post-functions-v1-approve-idea-summary"></a>
### API005 - POST `/functions/v1/approve-idea-summary`

#### Descrição

Registrar aprovação do resumo pelo autor.

#### Autenticação necessária

- [ ] Sim
- [x] Não, quando usado com token público temporário

#### Permissões necessárias

Token temporário válido da submissão ou sessão imediata.

#### Request

##### Body

```json
{
  "idea_id": "uuid",
  "approval_token": "token-temporario",
  "comentario_autor": "Comentário opcional"
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "idea_id": "uuid",
  "status": "aprovada_autor"
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Dados inválidos | `VALIDATION_ERROR` |
| 403 | Token inválido/expirado | `FORBIDDEN` |
| 404 | Ideia não encontrada | `IDEA_NOT_FOUND` |
| 409 | Status incompatível | `INVALID_STATUS_TRANSITION` |
| 500 | Erro interno | `SUMMARY_APPROVAL_FAILED` |

#### Requisitos relacionados

- RF005

#### Regras de negócio relacionadas

- RN005, RN011

---

<a id="dt-api006-post-functions-v1-asana-create-project"></a>
### API006 - POST `/functions/v1/asana-create-project`

#### Descrição

Converter ideia em projeto e criar projeto correspondente no Asana a partir de template.

#### Autenticação necessária

- [x] Sim
- [ ] Não

#### Permissões necessárias

Perfil `inovacao`.

#### Request

##### Body

```json
{
  "idea_id": "uuid",
  "triage_session_id": "uuid"
}
```

#### Response de sucesso

**Status:** `201 Created`

```json
{
  "project_id": "uuid",
  "asana_project_gid": "121...",
  "asana_permalink": "https://app.asana.com/...",
  "idea_status": "virou_projeto"
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Ideia sem notas finais | `VALIDATION_ERROR` |
| 401 | Não autenticado | `UNAUTHENTICATED` |
| 403 | Sem permissão | `FORBIDDEN` |
| 404 | Ideia não encontrada | `IDEA_NOT_FOUND` |
| 409 | Ideia já convertida | `IDEA_ALREADY_CONVERTED` |
| 502 | Erro Asana | `ASANA_PROVIDER_ERROR` |
| 500 | Erro interno | `ASANA_CREATE_PROJECT_FAILED` |

#### Requisitos relacionados

- RF008, RF009

#### Regras de negócio relacionadas

- RN016, RN017, RN018, RN019, RN028

---

<a id="dt-api007-post-functions-v1-asana-webhook"></a>
### API007 - POST `/functions/v1/asana-webhook`

#### Descrição

Receber handshake e eventos de webhook do Asana.

#### Autenticação necessária

- [ ] Sim
- [x] Não, endpoint público validado por segredo/assinatura

#### Permissões necessárias

Validação de headers do Asana.

#### Request

##### Headers

| Header | Tipo | Obrigatório? | Descrição |
|---|---|---:|---|
| X-Hook-Secret | string | No handshake | Segredo enviado pelo Asana |
| X-Hook-Signature | string | Em eventos | Assinatura para validação |

##### Body

```json
{
  "events": [
    {
      "resource": { "gid": "asana_project_gid" },
      "action": "changed",
      "created_at": "2026-07-07T12:00:00Z"
    }
  ]
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "ok": true
}
```

No handshake, responder também o header `X-Hook-Secret`.

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Payload inválido | `INVALID_WEBHOOK_PAYLOAD` |
| 403 | Assinatura inválida | `INVALID_WEBHOOK_SIGNATURE` |
| 500 | Erro interno | `ASANA_WEBHOOK_FAILED` |

#### Requisitos relacionados

- RF016

#### Regras de negócio relacionadas

- RN024, RN028

---

<a id="dt-api008-post-functions-v1-asana-sync"></a>
### API008 - POST `/functions/v1/asana-sync`

#### Descrição

Executar reconciliação de dados do Asana para todos os projetos ativos integrados ou para projeto específico.

#### Autenticação necessária

- [x] Sim para acionamento manual
- [x] Secret interno para cron

#### Permissões necessárias

Perfil `inovacao` ou secret de job agendado.

#### Request

##### Body

```json
{
  "project_id": "uuid opcional"
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "synced": 3,
  "failed": 0
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 401 | Não autenticado | `UNAUTHENTICATED` |
| 403 | Sem permissão | `FORBIDDEN` |
| 502 | Erro Asana | `ASANA_PROVIDER_ERROR` |
| 500 | Erro interno | `ASANA_SYNC_FAILED` |

#### Requisitos relacionados

- RF013, RF016

#### Regras de negócio relacionadas

- RN012, RN013, RN024, RN028

---

<a id="dt-api009-post-functions-v1-ai-generate-insight"></a>
### API009 - POST `/functions/v1/ai-generate-insight`

#### Descrição

Gerar insight de IA para uma métrica com meta e resultado.

#### Autenticação necessária

- [x] Sim
- [ ] Não

#### Permissões necessárias

Perfil `inovacao`.

#### Request

##### Body

```json
{
  "metric_id": "uuid"
}
```

#### Response de sucesso

**Status:** `200 OK`

```json
{
  "metric_id": "uuid",
  "insight_ia": "Análise objetiva da meta versus resultado."
}
```

#### Respostas de erro

| Status | Situação | Resposta / mensagem esperada |
|---|---|---|
| 400 | Métrica sem resultado | `MISSING_RESULT` |
| 401 | Não autenticado | `UNAUTHENTICATED` |
| 403 | Sem permissão | `FORBIDDEN` |
| 404 | Métrica não encontrada | `METRIC_NOT_FOUND` |
| 502 | IA indisponível | `AI_PROVIDER_ERROR` |
| 500 | Erro interno | `AI_INSIGHT_FAILED` |

#### Requisitos relacionados

- RF012

#### Regras de negócio relacionadas

- RN008, RN009, RN023, RN028

---

<a id="dt-8-integracoes-externas"></a>
## 8. Integrações externas

<a id="dt-int001-asana"></a>
### INT001 - Asana

#### Sistema externo

Asana — Workspace Rennova.

#### Objetivo

Criar projetos operacionais a partir de ideias aprovadas e sincronizar indicadores de tarefas para visão executiva no portal.

#### Direção da comunicação

- [x] Sistema envia dados para serviço externo
- [x] Sistema recebe dados de serviço externo
- [x] Comunicação bidirecional

#### Protocolo / método

REST API Asana + webhooks.

#### Autenticação

Personal Access Token ou OAuth token armazenado em Supabase Secrets como `ASANA_TOKEN`. Não registrar token neste documento.

#### Payload enviado / recebido

Criação por template:

```json
{
  "data": {
    "name": "INV | Nome do projeto",
    "public": false
  }
}
```

Atualização de projeto:

```json
{
  "data": {
    "owner": "1211426908652574",
    "html_notes": "<body><strong>Resumo IA</strong><p>...</p></body>"
  }
}
```

Cache recebido/processado:

```json
{
  "num_tasks": 10,
  "num_completed": 4,
  "num_incomplete": 6,
  "status_distribution": { "Em andamento": 3, "Bloqueada": 1 }
}
```

#### Tratamento de erro

- Erros devem ser registrados em logs técnicos e `activity_log` quando relevantes.
- Falha na conversão não deve confirmar sucesso ao usuário.
- Falha de webhook deve ser compensada pelo cron.
- Rate limit deve usar retry/backoff quando possível.

#### Limites conhecidos

- Limite aproximado de 1.500 req/min por token, conforme spec interna.
- Webhooks podem perder eventos; cron diário é obrigatório.
- Criação a partir de template retorna job assíncrono.
- Endpoint de webhook precisa responder rapidamente ao handshake/eventos.

<a id="dt-int002-provedor-de-ia"></a>
### INT002 - Provedor de IA

#### Sistema externo

OpenAI ou Claude.

#### Objetivo

Apoiar preenchimento do Canvas, gerar resumo/nota inicial e produzir insights sobre métricas.

#### Direção da comunicação

- [x] Sistema envia dados para serviço externo
- [x] Sistema recebe dados de serviço externo
- [ ] Comunicação bidirecional contínua

#### Protocolo / método

REST API do provedor via Edge Function.

#### Autenticação

Chave de API armazenada em secret (`OPENAI_API_KEY` ou `ANTHROPIC_API_KEY`). Provider selecionado por `AI_PROVIDER`.

#### Payload enviado / recebido

Exemplo de saída esperada para resumo:

```json
{
  "resumo": "Resumo executivo da ideia.",
  "impacto": 4,
  "esforco": 2,
  "justificativa": "Justificativa curta."
}
```

#### Tratamento de erro

- Validar JSON antes de persistir.
- Em falha, permitir continuidade manual quando possível.
- Registrar erro sem payload sensível.
- Exibir mensagem amigável ao usuário.

#### Limites conhecidos

- Latência variável.
- Custo por chamada.
- Possibilidade de resposta inválida ou fora do schema.
- Necessidade de revisão humana para decisões.

---

<a id="dt-9-autenticacao-e-autorizacao"></a>
## 9. Autenticação e autorização

<a id="dt-9-1-estrategia-de-autenticacao"></a>
### 9.1 Estratégia de autenticação

Login com e-mail e senha via Supabase Auth. O Canvas público não exige login, mas operações de escrita passam por Edge Function com validação.

<a id="dt-9-2-sessao-e-expiracao"></a>
### 9.2 Sessão e expiração

A sessão será gerenciada pelo Supabase Auth. Quando expirar, o usuário deve ser redirecionado para `/login`. Logout deve limpar sessão local e retornar para login.

<a id="dt-9-3-perfis-e-permissoes"></a>
### 9.3 Perfis e permissões

| Perfil | Permissões | Restrições |
|---|---|---|
| diretoria | Ler dashboard, matriz, ideias elegíveis e detalhes de projeto | Não pode editar, triar, converter, administrar ou comentar |
| inovacao | Gestão total do portal, triagem, conversão, projetos, fases, métricas, comentários, admin | Não deve burlar RLS; ações críticas logadas |
| público | Enviar ideia e usar IA no Canvas | Sem acesso ao portal interno e sem leitura direta do banco |

<a id="dt-9-4-regras-de-acesso"></a>
### 9.4 Regras de acesso

- Usuário `diretoria` pode consultar dados internos em modo leitura.
- Usuário `diretoria` não pode alterar ideias, projetos, fases, métricas, comentários ou usuários.
- Usuário `inovacao` pode gerir dados internos.
- Público pode usar apenas `/canvas` e funções públicas controladas.
- Escrita em `ideas` pelo público deve ocorrer somente via Edge Function.
- Tokens e service role nunca são acessíveis ao usuário final.

---

<a id="dt-10-tratamento-de-erros"></a>
## 10. Tratamento de erros

<a id="dt-10-1-erros-de-frontend"></a>
### 10.1 Erros de frontend

- Campos inválidos: exibir mensagem próxima ao campo e impedir envio.
- Falha de rede: exibir mensagem geral e permitir tentar novamente.
- Erro inesperado: exibir mensagem genérica sem detalhes técnicos.
- Falta de permissão: exibir acesso negado e ocultar ações proibidas.
- Integrações demoradas: exibir loading e bloquear duplo clique.

<a id="dt-10-2-erros-de-backend"></a>
### 10.2 Erros de backend

Formato padrão:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Mensagem clara sobre o erro"
  }
}
```

Códigos recomendados:

| Código | Uso |
|---|---|
| VALIDATION_ERROR | Entrada inválida |
| UNAUTHENTICATED | Usuário não autenticado |
| FORBIDDEN | Usuário sem permissão |
| NOT_FOUND | Registro inexistente |
| CONFLICT | Duplicidade ou estado incompatível |
| AI_PROVIDER_ERROR | Erro no provedor de IA |
| ASANA_PROVIDER_ERROR | Erro no Asana |
| INTERNAL_ERROR | Erro inesperado |

<a id="dt-10-3-erros-de-integracao"></a>
### 10.3 Erros de integração

Falhas de IA devem permitir continuidade manual quando possível. Falhas de Asana durante conversão devem impedir confirmação de sucesso e registrar estado para diagnóstico. Falhas de webhook devem ser compensadas pelo cron. Logs devem conter contexto técnico mínimo sem secrets.

---

<a id="dt-11-logs-e-observabilidade"></a>
## 11. Logs e observabilidade

<a id="dt-11-1-eventos-que-devem-gerar-log"></a>
### 11.1 Eventos que devem gerar log

- [x] Login realizado, quando viável por logs da plataforma.
- [x] Falha de login, quando viável por logs da plataforma.
- [x] Criação de ideia.
- [x] Aprovação de resumo pelo autor.
- [x] Alteração de status de ideia.
- [x] Decisão de triagem.
- [x] Conversão de ideia em projeto.
- [x] Falha em integração Asana.
- [x] Falha em integração IA.
- [x] Encerramento de projeto.
- [x] Alteração de perfil/role.
- [x] Erro interno inesperado.

<a id="dt-11-2-informacoes-que-devem-constar-no-log"></a>
### 11.2 Informações que devem constar no log

- Data e hora.
- Usuário, quando aplicável.
- Ação executada.
- Tipo e identificador do registro afetado.
- Código do erro, quando aplicável.
- Mensagem técnica suficiente para diagnóstico.
- Identificador Asana quando aplicável.

<a id="dt-11-3-informacoes-que-nao-devem-constar-no-log"></a>
### 11.3 Informações que não devem constar no log

- Senhas.
- Tokens.
- Chaves de API.
- Supabase service role.
- Payload integral enviado ao provedor de IA quando contiver dados sensíveis.
- Headers de autenticação.
- Stack trace exibido ao usuário.

---

<a id="dt-12-seguranca-tecnica"></a>
## 12. Segurança técnica

- [x] Validação de entrada no backend.
- [x] Controle de autorização no backend.
- [x] Proteção contra exposição de credenciais.
- [x] Uso de HTTPS.
- [x] Sanitização de dados exibidos no frontend.
- [x] Configuração segura de variáveis de ambiente.
- [x] Proteção contra acesso indevido a arquivos ou registros.
- [x] RLS habilitado em tabelas do Supabase.
- [x] Rate limit/honeypot/captcha leve no Canvas público.
- [x] Validação de webhook Asana.
- [x] Idempotência na conversão de ideia.
- [x] Revisão da policy de `profiles` para impedir autoelevação de role.

---

<a id="dt-13-estrategia-de-deploy"></a>
## 13. Estratégia de deploy

<a id="dt-13-1-ambientes"></a>
### 13.1 Ambientes

| Ambiente | URL / Identificação | Finalidade | Observações |
|---|---|---|---|
| Desenvolvimento | Lovable preview / Supabase dev | Evolução e testes iniciais | Evitar dados reais sensíveis |
| Homologação | A definir | Validação antes da produção | Usar workspace/projeto Asana controlado se possível |
| Produção | A definir | Uso real | Secrets e políticas revisadas |

<a id="dt-13-2-processo-de-deploy"></a>
### 13.2 Processo de deploy

1. Atualizar especificação/prompt e aplicar mudanças incrementais no Lovable.
2. Aplicar migrations SQL no Supabase do ambiente alvo.
3. Deployar Edge Functions e configurar secrets.
4. Validar build do front-end.
5. Executar Plano de Validação.
6. Publicar em produção após aceite.

<a id="dt-13-3-rollback"></a>
### 13.3 Rollback

- Front-end: voltar para versão anterior no Lovable/GitHub conforme mecanismo disponível.
- Banco: migrations devem ser versionadas com scripts reversíveis quando possível.
- Edge Functions: manter versão anterior para redeploy rápido.
- Integração Asana: se falhar, desativar conversão temporariamente e manter portal em modo leitura/triagem.

---

<a id="dt-14-variaveis-de-ambiente-e-configuracoes"></a>
## 14. Variáveis de ambiente e configurações

| Variável | Obrigatória? | Descrição | Exemplo seguro |
|---|---|---|---|
| SUPABASE_URL | Sim | URL do projeto Supabase | `https://<ref>.supabase.co` |
| SUPABASE_ANON_KEY | Sim | Chave pública anon do Supabase | `ey...` sem service role |
| SUPABASE_SERVICE_ROLE_KEY | Sim, backend | Chave service role para Edge Functions | Secret, não registrar valor |
| AI_PROVIDER | Sim | Provedor de IA | `openai` ou `claude` |
| OPENAI_API_KEY | Condicional | Chave OpenAI | Secret |
| ANTHROPIC_API_KEY | Condicional | Chave Claude | Secret |
| ASANA_TOKEN | Sim | Token Asana | Secret |
| ASANA_TEMPLATE_GID | Sim | Template de projeto | `1215808313871106` |
| ASANA_PORTFOLIO_GID | Sim | Portfólio Inovação | `1213936811318686` |
| ASANA_WORKSPACE_GID | Sim | Workspace Rennova | `1202773865285599` |
| ASANA_DEFAULT_OWNER | Sim | Owner padrão | `1211426908652574` |
| ASANA_WEBHOOK_TARGET_URL | Sim | URL pública do webhook | `https://<ref>.supabase.co/functions/v1/asana-webhook` |
| INTERNAL_CRON_SECRET | Sim | Secret para scheduled functions | Secret |
| PUBLIC_FORM_RATE_LIMIT_WINDOW | Não | Janela de rate limit | `60` |
| PUBLIC_FORM_RATE_LIMIT_MAX | Não | Limite por janela | `5` |

---

<a id="dt-15-riscos-tecnicos"></a>
## 15. Riscos técnicos

| ID | Risco | Impacto | Probabilidade | Mitigação |
|---|---|---|---|---|
| RT001 | Alterações externas quebrarem continuidade no Lovable | Alto | Média | Manter Lovable como fonte principal do front; mudanças externas só controladas |
| RT002 | Token Asana exposto no front-end ou logs | Alto | Baixa | Usar apenas secrets em Edge Functions e revisar logs |
| RT003 | Conversão duplicada de ideia em projeto | Alto | Média | Idempotência, constraints únicas e lock/transação |
| RT004 | Falha parcial na criação Asana | Médio | Média | Estados de recuperação, logs e reexecução segura |
| RT005 | Webhook Asana perder eventos | Médio | Média | Cron diário de reconciliação |
| RT006 | Resposta inválida da IA | Médio | Alta | JSON schema, validação e fallback manual |
| RT007 | RLS permitir autoelevação de role | Alto | Média | Revisar policy `profiles_self_update` e restringir alteração de role |
| RT008 | Canvas público sofrer spam | Médio | Média | Rate limit, honeypot e captcha leve |
| RT009 | Departamentos não acessíveis no Canvas público por RLS | Médio | Alta | Criar `public-departments` ou policy pública controlada |
| RT010 | Asana API/rate limit indisponível | Médio | Baixa | Retry/backoff, cache e mensagens claras |

---

<a id="dt-16-pendencias-tecnicas"></a>
## 16. Pendências técnicas

| ID | Pendência | Responsável | Decisão / encaminhamento | Status |
|---|---|---|---|---|
| PT001 | Definir homologação e produção no Supabase | Técnico / Gestão | Criar ambientes ou definir fluxo seguro no mesmo projeto | Aberta |
| PT002 | Criar tabela `asana_webhooks` | Técnico | Recomendado para suportar webhook por projeto | Aberta |
| PT003 | Revisar RLS de `profiles_self_update` | Técnico | Impedir autoalteração de `role` e `ativo` | Aberta |
| PT004 | Definir estratégia de departamentos públicos no Canvas | Técnico | Edge Function `public-departments` recomendada | Aberta |
| PT005 | Definir token de aprovação do autor | Produto / Técnico | Token temporário com hash recomendado | Aberta |
| PT006 | Definir uso de Supabase Scheduled Functions para cron | Técnico | Implementar `asana-sync` diário | Aberta |
| PT007 | Definir provider inicial de IA | Gestão / Técnico | OpenAI ou Claude via `AI_PROVIDER` | Aberta |
| PT008 | Ajustar escala da matriz atual para 1–5 | Lovable / Técnico | Alterar UI e validações | Aberta |
| PT009 | Gerar tipos Supabase para o front-end | Técnico | Usar Supabase CLI quando estabilizar schema | Aberta |
| PT010 | Definir estratégia de monitoramento de Edge Functions | Técnico | Supabase logs + alertas mínimos | Aberta |

---

<a id="dt-17-aprovacao-tecnica"></a>
## 17. Aprovação técnica

| Papel | Nome | Data | Aprovação |
|---|---|---|---|
| Responsável técnico | Phablo Tavares | 2026-07-07 | Em revisão |
| Desenvolvimento | A definir |  |  |
| Solicitante / Dono do produto | A definir |  |  |
