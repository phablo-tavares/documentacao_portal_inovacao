# Especificação Funcional — Portal de Gestão da Inovação Rennova

> Fonte funcional para orientar construção, aceite e evolução do Rennova Spark Hub.  
> Esta versão reduz redundâncias entre requisitos, regras, fluxos e telas sem remover comportamento, restrições ou critérios necessários para implementação e validação.

---

<a id="sumario"></a>
## Sumário

- [1. Identificação do projeto](#ef-1-identificacao-do-projeto)
- [2. Visão geral](#ef-2-visao-geral)
  - [2.1 Contexto](#ef-2-1-contexto)
  - [2.2 Objetivo](#ef-2-2-objetivo)
  - [2.3 Público-alvo / usuários](#ef-2-3-publico-alvo-usuarios)
- [3. Escopo](#ef-3-escopo)
  - [3.1 Escopo incluído](#ef-3-1-escopo-incluido)
  - [3.2 Fora de escopo](#ef-3-2-fora-de-escopo)
  - [3.3 Premissas](#ef-3-3-premissas)
  - [3.4 Restrições](#ef-3-4-restricoes)
- [4. Requisitos funcionais](#ef-4-requisitos-funcionais)
  - [RF001 - Autenticação no portal interno](#ef-rf001-autenticacao-no-portal-interno)
  - [RF002 - Controle de acesso por perfil](#ef-rf002-controle-de-acesso-por-perfil)
  - [RF003 - Submissão de ideia pelo Canvas público](#ef-rf003-submissao-de-ideia-pelo-canvas-publico)
  - [RF004 - Sugestão de IA por bloco do Canvas](#ef-rf004-sugestao-de-ia-por-bloco-do-canvas)
  - [RF005 - Resumo de IA e aprovação pelo autor](#ef-rf005-resumo-de-ia-e-aprovacao-pelo-autor)
  - [RF006 - Dashboard executivo](#ef-rf006-dashboard-executivo)
  - [RF007 - Matriz Impacto × Esforço](#ef-rf007-matriz-impacto-x-esforco)
  - [RF008 - Triagem mensal de ideias](#ef-rf008-triagem-mensal-de-ideias)
  - [RF009 - Conversão de ideia em projeto](#ef-rf009-conversao-de-ideia-em-projeto)
  - [RF010 - Detalhe e governança do projeto](#ef-rf010-detalhe-e-governanca-do-projeto)
  - [RF011 - Gestão de fases e checklist executivo](#ef-rf011-gestao-de-fases-e-checklist-executivo)
  - [RF012 - Métricas, resultados e insight de IA](#ef-rf012-metricas-resultados-e-insight-de-ia)
  - [RF013 - Bloco Asana no projeto](#ef-rf013-bloco-asana-no-projeto)
  - [RF014 - Comentários de governança](#ef-rf014-comentarios-de-governanca)
  - [RF015 - Administração de departamentos e usuários](#ef-rf015-administracao-de-departamentos-e-usuarios)
  - [RF016 - Sincronização Asana → Portal](#ef-rf016-sincronizacao-asana-portal)
  - [RF017 - Auditoria de ações relevantes](#ef-rf017-auditoria-de-acoes-relevantes)
- [5. Regras de negócio](#ef-5-regras-de-negocio)
- [6. Fluxos de usuário](#ef-6-fluxos-de-usuario)
- [7. Mapa de navegação](#ef-7-mapa-de-navegacao)
- [8. Telas e comportamento visual](#ef-8-telas-e-comportamento-visual)
  - [Tela 1 - Canvas público](#ef-tela-1-canvas-publico)
  - [Tela 2 - Login](#ef-tela-2-login)
  - [Tela 3 - Dashboard](#ef-tela-3-dashboard)
  - [Tela 4 - Matriz Impacto × Esforço](#ef-tela-4-matriz-impacto-x-esforco)
  - [Tela 5 - Triagem](#ef-tela-5-triagem)
  - [Tela 6 - Detalhe do projeto](#ef-tela-6-detalhe-do-projeto)
  - [Tela 7 - Admin](#ef-tela-7-admin)
- [9. Requisitos não funcionais](#ef-9-requisitos-nao-funcionais)
- [10. Mensagens do sistema](#ef-10-mensagens-do-sistema)
- [11. Pendências e dúvidas funcionais](#ef-11-pendencias-e-duvidas-funcionais)
- [12. Controle de mudanças de escopo](#ef-12-controle-de-mudancas-de-escopo)
- [13. Aprovação funcional](#ef-13-aprovacao-funcional)

---

<a id="ef-1-identificacao-do-projeto"></a>
## 1. Identificação do projeto

| Campo | Valor |
|---|---|
| Nome do projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável pelo documento | Phablo Tavares |
| Área/Time | Inovação / Desenvolvimento de Agentes e Soluções de IA |
| Data | 2026-07-08 |
| Versão | 0.3 |

---

<a id="ef-2-visao-geral"></a>
## 2. Visão geral

<a id="ef-2-1-contexto"></a>
### 2.1 Contexto

A área de Inovação da Rennova recebe ideias de diferentes áreas, avalia potencial, prioriza iniciativas e acompanha projetos aprovados. Parte desse processo hoje fica dispersa entre conversas, documentos, planilhas e ferramentas operacionais. O portal deve centralizar entrada de ideias, triagem, priorização, conversão em projetos e acompanhamento executivo.

Já existe um protótipo visual no Lovable/GitHub, com Dashboard, Projetos, Detalhe de Projeto e Ideias usando dados mockados. A entrega alvo deve transformar o protótipo em produto funcional com Supabase, autenticação, banco real, IA e integração com Asana.

<a id="ef-2-2-objetivo"></a>
### 2.2 Objetivo

Construir um portal interno para centralizar a gestão da inovação na Rennova, permitindo que colaboradores submetam ideias, a Inovação qualifique e priorize iniciativas, a diretoria acompanhe o portfólio e projetos aprovados sejam integrados ao Asana para execução operacional.

<a id="ef-2-3-publico-alvo-usuarios"></a>
### 2.3 Público-alvo / usuários

| Ator / Perfil | Responsabilidade | Principais ações |
|---|---|---|
| Colaborador / Autor da ideia | Submeter ideia pelo Canvas público | Preencher Canvas, solicitar sugestões de IA, revisar resumo e aprovar submissão |
| Inovação | Gerir funil e governança da inovação | Triar ideias, ajustar impacto/esforço, converter ideias, gerir projetos, fases, métricas, comentários e cadastros |
| Diretoria | Acompanhar portfólio em visão executiva | Consultar dashboard, matriz e detalhes dos projetos sem editar dados |
| Administrador funcional | Gerir cadastros básicos | Gerenciar departamentos e perfis de usuários |
| Sistema / Integrações | Executar automações | Gerar sugestões/resumos/insights, criar projetos no Asana, sincronizar dados e registrar logs |

---

<a id="ef-3-escopo"></a>
## 3. Escopo

<a id="ef-3-1-escopo-incluido"></a>
### 3.1 Escopo incluído

- [x] Base visual inicial com tema escuro, dashboard, projetos, detalhes e ideias usando `mockData`.
- [ ] Canvas público sem login para submissão de ideias.
- [ ] Sugestões de IA por bloco do Canvas.
- [ ] Resumo consolidado da ideia por IA.
- [ ] Aprovação ou ajuste do resumo pelo autor.
- [ ] Login com Supabase Auth por e-mail e senha.
- [ ] Controle de acesso por perfis `diretoria` e `inovacao`.
- [ ] Dashboard executivo com indicadores do portfólio e dados cacheados do Asana.
- [ ] Matriz Impacto × Esforço para ideias elegíveis.
- [ ] Triagem mensal de ideias pela Inovação.
- [ ] Conversão de ideia em projeto no portal e no Asana.
- [ ] Detalhe do projeto com fases, checklist executivo, métricas, resultados, insights de IA e comentários de governança.
- [ ] Bloco Asana somente leitura no detalhe do projeto.
- [ ] Sincronização Asana → portal por webhook e cron de reconciliação.
- [ ] Administração de departamentos e usuários.
- [ ] Logs de auditoria para ações relevantes.

<a id="ef-3-2-fora-de-escopo"></a>
### 3.2 Fora de escopo

- Substituir o Asana como ferramenta operacional de tarefas.
- Editar tarefas Asana dentro do portal.
- SSO corporativo na primeira versão.
- Aplicativo mobile nativo.
- Gestão financeira detalhada de orçamento, custos ou CAPEX/OPEX.
- Workflow completo de aprovação multinível fora da triagem de Inovação.
- BI avançado fora dos indicadores previstos no dashboard.
- Migração automática de dados históricos não estruturados.
- Integrações com ERP, CRM, e-mail ou sistemas internos além do Asana.
- Acompanhamento da evolução da ideia pelo autor após aprovação, salvo definição em nova fase.

<a id="ef-3-3-premissas"></a>
### 3.3 Premissas

- Lovable continuará sendo a principal ferramenta de evolução do front-end.
- Supabase será usado para Auth, Postgres, RLS e Edge Functions.
- Asana será a fonte operacional de tarefas e sprints.
- Supabase será a fonte de verdade para ideias, triagem, governança, métricas, usuários e visão executiva.
- Tokens de Asana e IA ficarão somente em secrets nas Edge Functions.
- Workspace, template, portfólio e owner padrão do Asana já foram identificados.
- Respostas de IA serão estruturadas em JSON e validadas antes de gravação.
- A primeira versão priorizará desktop e responsividade básica para web.

<a id="ef-3-4-restricoes"></a>
### 3.4 Restrições

- Não expor chaves, tokens ou `service_role` no front-end.
- Não chamar Asana nem provedores de IA diretamente pelo browser.
- Evitar edição manual ampla do front-end fora do Lovable.
- Proteger o formulário público contra spam.
- Não exibir impacto/esforço ao autor da ideia.
- Aplicar permissões no front-end e reforçar por RLS/Edge Functions.
- Não depender de chamada ao Asana em tempo real no dashboard.

---

<a id="ef-4-requisitos-funcionais"></a>
## 4. Requisitos funcionais

> Cada RF abaixo consolida comportamento, exceções e aceite. As regras detalhadas estão na seção [5. Regras de negócio](#ef-5-regras-de-negocio).

<a id="ef-rf001-autenticacao-no-portal-interno"></a>
### RF001 - Autenticação no portal interno

| Item | Especificação |
|---|---|
| Descrição | Permitir login no portal interno por e-mail e senha via Supabase Auth. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário cadastrado no Supabase Auth; perfil correspondente em `profiles`; usuário ativo. |
| Fluxo principal | 1. Acessar `/login`.<br>2. Informar e-mail e senha.<br>3. Autenticar no Supabase.<br>4. Consultar perfil/permissões.<br>5. Redirecionar para Dashboard. |
| Exceções | `FA001` credenciais inválidas: mensagem genérica.<br>`FA002` usuário inativo: bloquear acesso e orientar contato com Inovação.<br>`FA003` perfil inexistente: bloquear e registrar erro técnico.<br>`FA004` sessão expirada: redirecionar para `/login`. |
| Critérios de aceite | Usuário ativo com credenciais válidas acessa Dashboard; usuário inativo é bloqueado; usuário não autenticado em rota interna é enviado para `/login`. |
| Regras | RN001, RN002, RN003. |
| Observação | SSO não faz parte da primeira versão. |

<a id="ef-rf002-controle-de-acesso-por-perfil"></a>
### RF002 - Controle de acesso por perfil

| Item | Especificação |
|---|---|
| Descrição | Restringir funcionalidades conforme perfil `diretoria` ou `inovacao`. |
| Ator | Sistema. |
| Pré-condições | Usuário autenticado; `profiles.role` definido. |
| Fluxo principal | 1. Usuário acessa rota interna.<br>2. Sistema carrega perfil.<br>3. UI exibe apenas menus/ações permitidos.<br>4. RLS/Edge Functions reforçam a permissão. |
| Exceções | Diretoria em `/triagem` ou `/admin`: acesso negado.<br>Diretoria tentando alteração por chamada direta: bloqueio por RLS/Edge Function.<br>Perfil ausente/desconhecido: bloqueio por segurança. |
| Critérios de aceite | Diretoria consulta dashboard/matriz/detalhe em leitura; não edita dados; Inovação acessa triagem/admin e ações de gestão. |
| Regras | RN001, RN002, RN003, RN027. |
| Observação | Ocultar botão no front-end não substitui validação server-side. |

<a id="ef-rf003-submissao-de-ideia-pelo-canvas-publico"></a>
### RF003 - Submissão de ideia pelo Canvas público

| Item | Especificação |
|---|---|
| Descrição | Permitir que colaborador envie ideia pela rota pública `/canvas`, sem login. |
| Ator | Colaborador. |
| Pré-condições | Rota pública disponível; departamentos ativos disponíveis; Edge Function `submit-idea` configurada. |
| Fluxo principal | 1. Acessar `/canvas`.<br>2. Preencher dados do solicitante, departamentos e 7 blocos do Canvas.<br>3. Enviar ideia.<br>4. Sistema valida dados e anti-spam.<br>5. Sistema grava `ideas.status = enviada`.<br>6. Sistema inicia/chama geração de resumo por IA. |
| Exceções | Campos obrigatórios vazios: bloquear e destacar campos.<br>E-mail inválido: bloquear.<br>Rate limit/honeypot: bloquear com mensagem genérica.<br>Falha de gravação: exibir erro e permitir nova tentativa.<br>Departamentos indisponíveis: exibir alternativa ou indisponibilidade temporária. |
| Critérios de aceite | Colaborador sem login acessa `/canvas`; Canvas incompleto é bloqueado; submissão válida cria registro em `ideas` com status `enviada`. |
| Regras | RN004, RN005, RN006, RN007, RN028, RN030. |
| Observação | Escrita pública no banco deve ocorrer somente via Edge Function com `service_role`. |

<a id="ef-rf004-sugestao-de-ia-por-bloco-do-canvas"></a>
### RF004 - Sugestão de IA por bloco do Canvas

| Item | Especificação |
|---|---|
| Descrição | Permitir que o autor solicite sugestão de IA para cada bloco do Canvas. |
| Ator | Colaborador. |
| Pré-condições | `/canvas` aberto; `ai-assist-block` configurada; provider de IA configurado por secret. |
| Fluxo principal | 1. Clicar em “Sugestão IA” em um bloco.<br>2. Enviar bloco e contexto para Edge Function.<br>3. IA retorna sugestão objetiva.<br>4. Sistema exibe sugestão para aceitar, editar ou ignorar. |
| Exceções | IA indisponível: manter edição manual.<br>Resposta inválida: ignorar resposta, registrar erro e exibir mensagem genérica.<br>Conteúdo insuficiente: IA pode retornar pergunta orientadora ou sugestão genérica. |
| Critérios de aceite | Sugestão retorna texto editável; falha de IA não impede preenchimento manual. |
| Regras | RN008, RN009, RN028, RN030. |
| Observação | Enviar ao provider somente o contexto necessário. |

<a id="ef-rf005-resumo-de-ia-e-aprovacao-pelo-autor"></a>
### RF005 - Resumo de IA e aprovação pelo autor

| Item | Especificação |
|---|---|
| Descrição | Gerar resumo consolidado da ideia e permitir aprovação/complemento pelo autor antes da triagem. |
| Ator | Autor da ideia. |
| Pré-condições | Ideia com status `enviada`; `ai-summarize-idea` configurada. |
| Fluxo principal | 1. Enviar blocos da ideia para Edge Function.<br>2. IA retorna JSON com resumo, impacto sugerido e esforço sugerido.<br>3. Gravar `resumo_ia`, `impacto_ia`, `esforco_ia` e `status = resumo_gerado`.<br>4. Exibir resumo ao autor, sem notas.<br>5. Autor aprova ou complementa.<br>6. Gravar aprovação/comentário e `status = aprovada_autor`. |
| Exceções | IA falha: permitir submissão com resumo pendente para Inovação.<br>JSON inválido: não gravar pontuações e registrar erro.<br>Autor edita/comenta: gravar ajuste e seguir para aprovação.<br>Autor abandona tela: manter `resumo_gerado` ou aplicar fluxo de expiração definido. |
| Critérios de aceite | Resumo válido é exibido antes da triagem; aprovação muda status para `aprovada_autor`; impacto/esforço nunca aparecem ao autor. |
| Regras | RN005, RN008, RN009, RN010, RN011, RN028, RN030. |
| Observação | Retomada após abandono ainda depende de definição funcional. |

<a id="ef-rf006-dashboard-executivo"></a>
### RF006 - Dashboard executivo

| Item | Especificação |
|---|---|
| Descrição | Exibir visão executiva do portfólio de inovação. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; dados de `projects`, `ideas` e `asana_sync` disponíveis. |
| Fluxo principal | 1. Acessar `/`.<br>2. Exibir KPIs: projetos ativos, progresso médio, tarefas abertas e ideias em triagem.<br>3. Exibir lista de projetos com área, status, progresso e última atualização.<br>4. Permitir filtro por área/status e acesso ao detalhe. |
| Exceções | Sem projetos: estado vazio.<br>Sem dados Asana: indicar indisponível/pendente conforme regra.<br>Erro de carregamento: exibir erro e opção de tentar novamente. |
| Critérios de aceite | KPIs calculados com dados do Supabase; filtros funcionam; indisponibilidade do Asana não quebra a tela nem gera chamada Asana ao vivo. |
| Regras | RN001, RN012, RN013, RN030. |
| Observação | Tela já existe em protótipo com dados mockados; substituir por consultas reais. |

<a id="ef-rf007-matriz-impacto-x-esforco"></a>
### RF007 - Matriz Impacto × Esforço

| Item | Especificação |
|---|---|
| Descrição | Exibir ideias elegíveis em matriz de priorização impacto×esforço. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; ideias elegíveis com pontuações. |
| Fluxo principal | 1. Acessar `/matriz`.<br>2. Buscar ideias `aprovada_autor`, `em_triagem` e `backlog`.<br>3. Plotar esforço no eixo X e impacto no eixo Y.<br>4. Diferenciar pontuação IA e pontuação final de triagem.<br>5. Permitir clique para detalhe. |
| Exceções | Ideia sem pontuação: não plotar ou listar como pendente de triagem.<br>Sem elegíveis: estado vazio.<br>Diretoria: leitura sem ações de decisão. |
| Critérios de aceite | Ideias elegíveis aparecem nos quadrantes corretos; ideias convertidas/arquivadas não aparecem; diretoria não altera decisão. |
| Regras | RN010, RN014, RN015. |
| Observação | Protótipo atual usa escala 0–10; versão final deve usar 1–5. |

<a id="ef-rf008-triagem-mensal-de-ideias"></a>
### RF008 - Triagem mensal de ideias

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação realize triagem mensal, ajuste notas e registre decisão. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; ideias em `aprovada_autor` ou `em_triagem`. |
| Fluxo principal | 1. Acessar `/triagem`.<br>2. Listar ideias elegíveis do mês.<br>3. Revisar resumo e Canvas.<br>4. Ajustar `impacto_final` e `esforco_final`.<br>5. Decidir: Vira Projeto, Backlog ou Arquivar.<br>6. Atualizar status, registrar sessão em `triage_sessions` e log em `activity_log`. |
| Exceções | Notas fora de 1–5: bloquear.<br>“Vira Projeto” sem notas finais: bloquear.<br>Falha ao converter no Asana: manter ideia em estado seguro e exibir erro.<br>Usuário sem permissão: bloquear. |
| Critérios de aceite | Notas válidas são salvas; Backlog permanece na matriz; Arquivar sai da matriz; Vira Projeto converte com sucesso quando elegível. |
| Regras | RN001, RN010, RN015, RN016, RN017, RN029, RN030. |
| Observação | Triagem pode ser simples na primeira versão, sem aprovação multinível. |

<a id="ef-rf009-conversao-de-ideia-em-projeto"></a>
### RF009 - Conversão de ideia em projeto

| Item | Especificação |
|---|---|
| Descrição | Converter uma ideia aprovada em projeto no portal e instanciar projeto correspondente no Asana. |
| Ator | Inovação. |
| Pré-condições | Ideia com decisão “Vira Projeto”; notas finais válidas; secrets Asana configurados; template e portfólio disponíveis. |
| Fluxo principal | 1. Confirmar “Vira Projeto”.<br>2. Chamar `asana-create-project`.<br>3. Verificar idempotência.<br>4. Criar/preparar projeto no Supabase.<br>5. Instanciar template no Asana e aguardar job.<br>6. Adicionar ao portfólio.<br>7. Atualizar descrição e owner no Asana.<br>8. Gravar `asana_project_gid`, `asana_permalink` e vínculo da ideia.<br>9. Registrar log e marcar ideia como `virou_projeto`. |
| Exceções | Ideia já convertida: retornar conflito.<br>Job Asana falha: registrar e não confirmar conversão.<br>Falha ao adicionar ao portfólio: registrar pendência de sync.<br>Falha parcial após criar Asana: registrar estado de recuperação manual.<br>Token inválido: erro controlado e log técnico. |
| Critérios de aceite | Ideia não convertida gera projeto no portal e no Asana; tentativa duplicada é impedida; falha Asana não gera sucesso falso. |
| Regras | RN016, RN017, RN018, RN019, RN028, RN029, RN030. |
| Observação | Idempotência e falhas parciais são obrigatórias. |

<a id="ef-rf010-detalhe-e-governanca-do-projeto"></a>
### RF010 - Detalhe e governança do projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir e permitir gestão das informações executivas do projeto aprovado. |
| Ator | Inovação; Diretoria em leitura. |
| Pré-condições | Usuário autenticado; projeto existente. |
| Fluxo principal | 1. Acessar `/projetos/:id`.<br>2. Exibir título, status, progresso, área, owner e datas.<br>3. Exibir resumo IA, objetivo, problema e descrição.<br>4. Exibir fases, checklist, métricas, Asana e comentários.<br>5. Permitir edição apenas para `inovacao`. |
| Exceções | Projeto inexistente: “Projeto não encontrado”.<br>Usuário sem permissão: ocultar/bloquear ações editáveis.<br>Dados Asana ausentes: bloco vazio/indisponível. |
| Critérios de aceite | Detalhe exibe seções executivas; diretoria não edita; Inovação gere fases, checklist, métricas e comentários. |
| Regras | RN001, RN012, RN020, RN021, RN022, RN025. |
| Observação | Tela já existe em protótipo com dados mockados e deve ser preservada visualmente quando possível. |

<a id="ef-rf011-gestao-de-fases-e-checklist-executivo"></a>
### RF011 - Gestão de fases e checklist executivo

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação acompanhe cinco fases fixas e checklist executivo por fase. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; projeto existente; fases semeadas em `project_phases`. |
| Fluxo principal | 1. Acessar detalhe do projeto.<br>2. Exibir stepper de cinco fases.<br>3. Marcar checklist da fase atual.<br>4. Marcar fase como concluída.<br>5. Atualizar status da fase.<br>6. Trigger recalcula `progress_pct`. |
| Exceções | Fase anterior pendente: impedir avanço, salvo regra futura.<br>Projeto encerrado: bloquear alteração de fases/checklist.<br>Falha ao salvar: exibir erro e manter estado anterior. |
| Critérios de aceite | Fase concluída recalcula progresso; cinco fases concluídas resultam em 100%; projeto encerrado bloqueia alteração. |
| Regras | RN020, RN021, RN022. |
| Observação | Checklist do portal é executivo e não substitui tarefas do Asana. |

<a id="ef-rf012-metricas-resultados-e-insight-de-ia"></a>
### RF012 - Métricas, resultados e insight de IA

| Item | Especificação |
|---|---|
| Descrição | Permitir registrar métricas, resultados e gerar insight de IA comparando meta e realizado. |
| Ator | Inovação. |
| Pré-condições | Projeto existente; métricas cadastradas ou derivadas da ideia; `ai-generate-insight` configurada. |
| Fluxo principal | 1. Acessar métricas no detalhe.<br>2. Exibir indicador, meta, unidade e resultado.<br>3. Preencher resultado.<br>4. Acionar “Gerar insight”.<br>5. Chamar Edge Function.<br>6. Gravar `insight_ia`. |
| Exceções | Resultado vazio: bloquear insight.<br>IA indisponível: manter resultado salvo e informar falha.<br>Resposta inválida: não gravar insight e registrar erro. |
| Critérios de aceite | Métrica com resultado gera insight salvo; falha da IA não perde resultado. |
| Regras | RN008, RN009, RN023, RN028, RN030. |
| Observação | Insight apoia governança; não decide automaticamente. |

<a id="ef-rf013-bloco-asana-no-projeto"></a>
### RF013 - Bloco Asana no projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir dados operacionais do Asana no detalhe do projeto em modo somente leitura. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Projeto com `asana_project_gid`; dados em `asana_sync` ou estado vazio. |
| Fluxo principal | 1. Acessar detalhe.<br>2. Consultar `asana_sync`.<br>3. Exibir total de tarefas, abertas, concluídas, distribuição de status e última atualização.<br>4. Exibir “Abrir no Asana”. |
| Exceções | Projeto sem Asana: indicar não integrado.<br>Cache vazio: “Aguardando sincronização”.<br>Permalink ausente: ocultar botão ou marcar indisponível. |
| Critérios de aceite | Dados vêm de `asana_sync`; botão abre projeto no Asana; nenhuma edição de tarefa Asana é possível no portal. |
| Regras | RN012, RN013, RN018, RN024. |
| Observação | Portal não deve consultar Asana ao vivo durante renderização. |

<a id="ef-rf014-comentarios-de-governanca"></a>
### RF014 - Comentários de governança

| Item | Especificação |
|---|---|
| Descrição | Permitir registrar comentários de governança no projeto. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; projeto existente. |
| Fluxo principal | 1. Acessar detalhe.<br>2. Exibir comentários existentes.<br>3. Adicionar comentário.<br>4. Salvar com autor e data.<br>5. Registrar log quando aplicável. |
| Exceções | Comentário vazio: bloquear.<br>Diretoria: leitura sem criação.<br>Falha ao salvar: exibir erro e manter texto digitado. |
| Critérios de aceite | Comentário válido aparece no histórico; diretoria não adiciona comentários. |
| Regras | RN001, RN025, RN029, RN030. |
| Observação | Comentários operacionais de tarefas permanecem no Asana. |

<a id="ef-rf015-administracao-de-departamentos-e-usuarios"></a>
### RF015 - Administração de departamentos e usuários

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação gerencie departamentos e perfis de usuários. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao` autenticado. |
| Fluxo principal | 1. Acessar `/admin`.<br>2. Exibir departamentos e usuários.<br>3. Criar, editar ou inativar departamento.<br>4. Alterar nome, papel ou status de usuário.<br>5. Salvar e registrar log. |
| Exceções | Departamento duplicado: bloquear.<br>Departamento em uso: preferir inativação.<br>Tentativa de autoelevação de papel: bloquear.<br>Usuário sem permissão: bloquear. |
| Critérios de aceite | Departamento único é criado; departamento em uso pode ser inativado sem quebrar histórico; diretoria recebe acesso negado em `/admin`. |
| Regras | RN001, RN026, RN027, RN029, RN030. |
| Observação | Revisar policy de `profiles` para impedir autoelevação de perfil. |

<a id="ef-rf016-sincronizacao-asana-portal"></a>
### RF016 - Sincronização Asana → Portal

| Item | Especificação |
|---|---|
| Descrição | Manter dados operacionais do Asana sincronizados em `asana_sync` por webhook e cron. |
| Ator | Sistema. |
| Pré-condições | Projeto com `asana_project_gid`; `asana-webhook` e `asana-sync` configuradas; token Asana válido. |
| Fluxo principal | 1. Criar webhook na conversão do projeto.<br>2. Receber handshake do Asana e responder protocolo.<br>3. Receber eventos e atualizar/sinalizar `asana_sync`.<br>4. Executar cron diário de reconciliação.<br>5. Dashboard/detalhe leem apenas `asana_sync`. |
| Exceções | Webhook perdido: cron corrige depois.<br>Handshake inválido: não criar webhook e registrar erro.<br>Token inválido: registrar erro.<br>Rate limit: aplicar retry/backoff quando necessário. |
| Critérios de aceite | Alterações Asana atualizam cache por webhook ou cron; falhas são reconciliadas; front-end não chama API Asana. |
| Regras | RN012, RN013, RN018, RN024, RN028, RN030. |
| Observação | Validação de assinatura/segredo pertence ao design técnico, mas é obrigatória para aceite funcional da integração. |

<a id="ef-rf017-auditoria-de-acoes-relevantes"></a>
### RF017 - Auditoria de ações relevantes

| Item | Especificação |
|---|---|
| Descrição | Registrar ações relevantes em `activity_log`. |
| Ator | Sistema. |
| Pré-condições | Tabela `activity_log` disponível. |
| Fluxo principal | 1. Usuário ou sistema executa ação relevante.<br>2. Sistema identifica entidade, ação, ator e detalhes não sensíveis.<br>3. Sistema grava log.<br>4. Inovação consulta logs quando necessário. |
| Exceções | Falha ao gravar log não crítico: não bloquear fluxo principal, mas registrar erro técnico quando possível.<br>Dados sensíveis no detalhe: remover/mascarar antes de gravar. |
| Critérios de aceite | Conversão registra `action = convert`; alteração de status relevante gera log; logs não contêm tokens, senhas ou chaves. |
| Regras | RN029, RN030. |
| Observação | Log funcional não substitui monitoramento técnico das Edge Functions. |

---

<a id="ef-5-regras-de-negocio"></a>
## 5. Regras de negócio

| ID | Regra | Aplicável em | Critério / observação |
|---|---|---|---|
| RN001 | O portal terá perfis `diretoria` e `inovacao`. | RF001, RF002, RF006–RF017 | Diretoria tem leitura; Inovação executa gestão. Novos perfis exigem mudança de escopo. |
| RN002 | Permissões devem ser reforçadas por RLS e/ou Edge Functions. | RF002, RF008, RF010, RF015 | Ocultar ação na UI não basta; chamadas diretas indevidas devem ser bloqueadas. |
| RN003 | Usuário com `profiles.ativo = false` não acessa áreas internas. | RF001, RF002 | Bloqueio pode ocorrer após autenticação, ao carregar perfil. |
| RN004 | Campos obrigatórios do Canvas: nome, e-mail, departamentos, Problema, Indicadores, Como resolver sem IA, Como resolver com IA e Para quem/personas. Dados/fontes e Ferramentas são opcionais. | RF003 | Envio deve ser bloqueado se qualquer obrigatório estiver ausente. |
| RN005 | Ideias devem seguir status controlados: `rascunho`, `enviada`, `resumo_gerado`, `aprovada_autor`, `em_triagem`, `virou_projeto`, `backlog`, `arquivada`. | RF003, RF005, RF007, RF008, RF009 | Transições inválidas devem ser bloqueadas na aplicação. |
| RN006 | O front público não deve inserir diretamente em `ideas`; toda submissão passa por `submit-idea`. | RF003 | Insert anônimo direto deve ser bloqueado por RLS. |
| RN007 | Submissões públicas devem ter proteção anti-spam. | RF003 | Usar honeypot, rate limit e/ou captcha leve; mensagens ao usuário devem ser genéricas. |
| RN008 | IA é apoio, não autoridade final. | RF004, RF005, RF012 | Sugestões, resumo, notas e insights podem ser revisados pela Inovação. |
| RN009 | Edge Functions de IA devem solicitar e validar JSON estruturado antes de gravar campos controlados. | RF004, RF005, RF012 | Resposta não JSON não deve gravar campos críticos indevidamente. |
| RN010 | Impacto e esforço usam escala inteira de 1 a 5. | RF005, RF007, RF008, RF009 | Valores fora da escala devem ser bloqueados; matriz mockada 0–10 deve ser ajustada. |
| RN011 | Impacto e esforço não devem aparecer no fluxo público do autor. | RF005 | As notas são internas ao processo da Inovação. |
| RN012 | Asana é fonte operacional de tarefas, sprints, responsáveis e status; portal exibe espelho de leitura. | RF006, RF013, RF016 | Tarefas não são editadas no portal; comentários operacionais permanecem no Asana. |
| RN013 | Dashboard e detalhe leem dados Asana apenas de `asana_sync`. | RF006, RF013, RF016 | Reduz latência, rate limit e exposição de token. |
| RN014 | Matriz exibe apenas ideias `aprovada_autor`, `em_triagem` ou `backlog`. | RF007 | Ideias `virou_projeto` e `arquivada` não aparecem. |
| RN015 | `impacto_final` e `esforco_final`, quando existirem, prevalecem sobre notas IA. | RF007, RF008, RF009 | UI deve diferenciar nota sugerida de nota confirmada. |
| RN016 | Somente ideias com decisão explícita “Vira Projeto” podem ser convertidas. | RF008, RF009 | Conversão sem triagem é bloqueada, salvo nova regra formal. |
| RN017 | Conversão deve ser idempotente: uma ideia não pode gerar mais de um projeto no portal ou no Asana. | RF009 | Duplo clique/retry deve retornar projeto existente ou bloquear duplicidade. |
| RN018 | Impacto, esforço, área de origem e área impactada ficam no Supabase; não criar custom fields de projeto no Asana. | RF009, RF013, RF016 | Custom fields de tarefas do template Asana podem ser mantidos. |
| RN019 | Projeto criado no Asana deve receber descrição inicial com resumo IA e blocos principais do Canvas em `html_notes` permitido pela API. | RF009 | HTML deve ser sanitizado antes do envio. |
| RN020 | Todo projeto terá cinco fases fixas: Ideação, Validação, MVP, Implantação e Produção. | RF010, RF011 | Adicionar/remover fase é mudança de escopo. |
| RN021 | `progress_pct` é calculado por fases concluídas sobre o total de cinco fases. | RF010, RF011 | Exemplo: 2 fases concluídas = 40%. Cálculo por trigger no banco. |
| RN022 | Projeto pode ser encerrado em qualquer fase, registrando `encerrado_em` e `encerrado_na_fase`. | RF010, RF011 | Projeto encerrado não deve permitir alterações operacionais no portal. |
| RN023 | Insight de IA sobre métrica exige resultado preenchido. | RF012 | Meta qualitativa pode ser usada junto com resultado textual. |
| RN024 | Sincronização Asana deve ser resiliente: webhook para atualização rápida e cron diário para reconciliação. | RF013, RF016 | Não depender exclusivamente de webhook. |
| RN025 | Comentários do portal são de governança; comentários de tarefas permanecem no Asana. | RF014 | Evita duplicidade entre gestão executiva e operação. |
| RN026 | Departamentos em uso devem ser inativados, não excluídos. | RF015 | Inativos não aparecem em novos formulários e preservam histórico. |
| RN027 | Usuário não pode alterar o próprio `role` para ganhar permissões. | RF015 | Requer policy segura ou função controlada. |
| RN028 | Tokens Asana, chaves de IA e `service_role` devem existir somente em backend/Edge Functions. | RF003, RF004, RF005, RF009, RF012, RF016 | Também não registrar secrets em logs. |
| RN029 | Logs devem conter ação, entidade, ator e detalhes úteis, sem senhas, tokens, chaves ou dados pessoais desnecessários. | RF017 | Dados sensíveis devem ser minimizados/mascarados. |
| RN030 | Mensagens ao usuário devem ser claras e não expor stack trace, payload interno ou detalhe de credenciais. | Todos os RFs | Detalhes técnicos ficam nos logs. |

---

<a id="ef-6-fluxos-de-usuario"></a>
## 6. Fluxos de usuário

| Fluxo | Ator | Passos essenciais | Resultado | Atenção |
|---|---|---|---|---|
| Envio de ideia pelo Canvas | Colaborador | Acessa `/canvas`; preenche dados e blocos obrigatórios; pode usar sugestões IA; envia ideia; revisa/aprova resumo. | Ideia registrada como `aprovada_autor` e pronta para matriz/triagem. | Não exibir notas ao autor; proteger contra spam; permitir preenchimento manual se IA falhar. |
| Triagem e priorização | Inovação | Acessa `/triagem`; revisa resumo/Canvas; ajusta impacto/esforço finais; decide Vira Projeto, Backlog ou Arquivar. | Ideia classificada e direcionada. | Notas finais prevalecem; Backlog permanece na matriz; conversão é idempotente. |
| Conversão para projeto Asana | Inovação / Sistema | Confirma Vira Projeto; cria projeto no portal; instancia template no Asana; adiciona ao portfólio; grava vínculo; cria webhook/sync. | Projeto disponível no portal e no Asana. | Tratar falhas parciais; evitar duplicidade; manter tokens fora do front-end. |
| Acompanhamento executivo | Diretoria / Inovação | Login; Dashboard; filtro por status/área; detalhe do projeto; consulta resumo, progresso, fases, métricas, Asana e comentários. | Visão única e atualizada do portfólio. | Diretoria somente leitura; dashboard lê cache do Asana. |
| Gestão de governança do projeto | Inovação | Atualiza fases/checklist; preenche métricas/resultados; gera insights; comenta; encerra projeto quando aplicável. | Projeto com governança executiva atualizada. | Checklist do portal não é tarefa Asana; projeto encerrado bloqueia alterações relevantes. |

---

<a id="ef-7-mapa-de-navegacao"></a>
## 7. Mapa de navegação

```text
/canvas                       Canvas público, sem login
/login                        Login do portal interno
/                             Dashboard executivo
├── /projetos                 Lista de projetos
│   └── /projetos/:id         Detalhe do projeto
├── /matriz                   Matriz Impacto × Esforço
├── /triagem                  Triagem mensal, somente Inovação
├── /ideias                   Backlog/lista de ideias, se mantido como módulo separado
└── /admin                    Gestão de departamentos e usuários, somente Inovação
```

---

<a id="ef-8-telas-e-comportamento-visual"></a>
## 8. Telas e comportamento visual

> Esta seção complementa os RFs. Regras de negócio, permissões e critérios de aceite prevalecem quando houver dúvida.

<a id="ef-tela-1-canvas-publico"></a>
### Tela 1 - Canvas público

| Aspecto | Especificação |
|---|---|
| Objetivo | Coletar ideias de colaboradores de forma estruturada. |
| Campos | Nome, e-mail, área de origem, área impactada, Problema, Indicadores de sucesso, Como resolver sem IA, Como resolver com IA, Para quem/personas, Dados/fontes, Ferramentas. |
| Obrigatórios | Nome, e-mail, áreas e blocos definidos na RN004. |
| Ações | Sugestão IA; Enviar ideia; Aprovar resumo; Editar/comentar resumo. |
| Estados | Inicial com orientações; carregamento com botões desabilitados; erro por campo ou geral; sucesso com confirmação. |
| Referência visual | Lovable; tema escuro Rennova com acento dourado. |

<a id="ef-tela-2-login"></a>
### Tela 2 - Login

| Aspecto | Especificação |
|---|---|
| Objetivo | Autenticar usuários internos. |
| Campos | E-mail e senha, ambos obrigatórios. |
| Ações | Entrar; Sair em áreas internas. |
| Estados | Inicial; loading; erro de credencial/usuário inativo; sucesso redirecionando para Dashboard. |
| Referência visual | A definir no Lovable. |

<a id="ef-tela-3-dashboard"></a>
### Tela 3 - Dashboard

| Aspecto | Especificação |
|---|---|
| Objetivo | Fornecer visão executiva do portfólio. |
| Dados exibidos | Projetos ativos, progresso médio, tarefas abertas, ideias em triagem e lista/cards de projetos. |
| Ações | Filtrar por área/status; abrir projeto. |
| Estados | KPIs/lista carregados; loading; vazio sem projetos; erro de consulta; sucesso com dados renderizados. |
| Referência visual | Protótipo atual Lovable/GitHub com dados mockados. |

<a id="ef-tela-4-matriz-impacto-x-esforco"></a>
### Tela 4 - Matriz Impacto × Esforço

| Aspecto | Especificação |
|---|---|
| Objetivo | Priorizar ideias visualmente. |
| Dados exibidos | Ideia, impacto 1–5, esforço 1–5, status, origem e área impactada. |
| Ações | Clicar no ponto para detalhe; filtros se implementados. |
| Estados | Matriz com pontos; loading; vazio sem ideias elegíveis; erro de carregamento. |
| Referência visual | Tela Ideias atual contém matriz mockada; ajustar escala de 0–10 para 1–5. |

<a id="ef-tela-5-triagem"></a>
### Tela 5 - Triagem

| Aspecto | Especificação |
|---|---|
| Objetivo | Permitir decisão mensal sobre ideias. |
| Dados exibidos | Ideia, resumo IA, impacto final, esforço final e decisão. |
| Ações | Salvar notas; Vira Projeto; Backlog; Arquivar. |
| Estados | Lista do mês; vazio sem ideia elegível; erro ao salvar/converter; sucesso com decisão registrada. |
| Referência visual | A definir no Lovable. |

<a id="ef-tela-6-detalhe-do-projeto"></a>
### Tela 6 - Detalhe do projeto

| Aspecto | Especificação |
|---|---|
| Objetivo | Concentrar governança executiva do projeto. |
| Dados exibidos | Nome, status, progresso, área, owner, datas, resumo IA, objetivo, problema, descrição, fases, checklist, métricas, Asana e comentários. |
| Ações | Marcar checklist; concluir fase; registrar resultado; gerar insight; adicionar comentário; encerrar projeto; abrir Asana. |
| Estados | Dados do projeto; loading; projeto não encontrado; erro de consulta/salvamento; sucesso após ação. |
| Referência visual | Protótipo atual Lovable/GitHub com dados mockados. |

<a id="ef-tela-7-admin"></a>
### Tela 7 - Admin

| Aspecto | Especificação |
|---|---|
| Objetivo | Gerenciar cadastros básicos e permissões. |
| Dados exibidos | Departamentos e usuários. |
| Ações | Criar/editar/inativar departamento; alterar papel de usuário; ativar/inativar usuário. |
| Estados | Listas carregadas; vazio sem registros; erro ao salvar; sucesso com feedback. |
| Referência visual | A definir no Lovable. |

---

<a id="ef-9-requisitos-nao-funcionais"></a>
## 9. Requisitos não funcionais

| Categoria | Requisitos |
|---|---|
| Segurança | Autenticação em áreas restritas; controle por perfil; RLS nas tabelas; validação de inputs públicos no backend; proteção anti-spam; tokens/IA/Asana/`service_role` apenas em secrets; dados sensíveis fora do front-end, logs e mensagens. |
| Performance | Telas internas principais devem carregar em até 3 segundos em condições normais; dashboard lê Supabase/cache, sem Asana ao vivo; listagens devem suportar pelo menos 500 ideias e 100 projetos na primeira versão; IA/Asana devem exibir loading sem travar UI. |
| Usabilidade | Campos obrigatórios identificados; mensagens claras; feedback visual após ações importantes; conteúdos gerados por IA identificados; badges, progresso e stepper seguindo padrão visual Rennova. |
| Compatibilidade | Chrome, Edge e Safari atuais; desktop/notebook; responsividade básica para tablet; resolução mínima recomendada 1366×768; mobile não é foco, mas fluxos básicos não devem quebrar. |
| Logs e auditoria | Erros críticos, ações sensíveis, conversões, alterações de status e falhas de integração devem gerar log; logs não devem conter secrets, senhas ou dados sensíveis desnecessários. |

---

<a id="ef-10-mensagens-do-sistema"></a>
## 10. Mensagens do sistema

| Código | Situação | Mensagem sugerida |
|---|---|---|
| MSG001 | Operação realizada com sucesso | Alterações salvas com sucesso. |
| MSG002 | Campo obrigatório vazio | Preencha os campos obrigatórios antes de continuar. |
| MSG003 | Login inválido | E-mail ou senha inválidos. |
| MSG004 | Usuário inativo | Seu acesso está inativo. Procure a área de Inovação. |
| MSG005 | Sem permissão | Você não tem permissão para executar esta ação. |
| MSG006 | Ideia enviada | Ideia enviada com sucesso. Revise o resumo gerado para concluir a submissão. |
| MSG007 | Resumo aprovado | Resumo aprovado. Sua ideia foi enviada para avaliação da Inovação. |
| MSG008 | IA indisponível | Não foi possível gerar a sugestão agora. Você pode continuar preenchendo manualmente. |
| MSG009 | Conversão iniciada | A conversão da ideia em projeto foi iniciada. |
| MSG010 | Conversão concluída | Projeto criado com sucesso no portal e no Asana. |
| MSG011 | Conversão duplicada | Esta ideia já foi convertida em projeto. |
| MSG012 | Falha no Asana | Não foi possível concluir a integração com o Asana. Tente novamente ou acione o suporte técnico. |
| MSG013 | Sincronização pendente | Dados do Asana ainda não sincronizados. |
| MSG014 | Projeto encerrado | Projeto encerrado com sucesso. |
| MSG015 | Erro inesperado | Ocorreu um erro inesperado. Tente novamente. |

---

<a id="ef-11-pendencias-e-duvidas-funcionais"></a>
## 11. Pendências e dúvidas funcionais

| ID | Pendência | Responsável | Encaminhamento | Status |
|---|---|---|---|---|
| P001 | Definir se o autor poderá retomar aprovação do resumo por link/token após sair da tela. | Inovação / Técnico | Recomendado token temporário ou aprovação na mesma sessão. | Aberta |
| P002 | Definir se haverá notificação por e-mail ao autor após submissão. | Inovação | Fora do MVP salvo decisão contrária. | Aberta |
| P003 | Definir lista final de departamentos. | Inovação | Usar seed inicial e ajustar em Admin. | Aberta |
| P004 | Definir se `/ideias` será mantida separada de `/matriz` e `/triagem`. | Produto / Técnico | Manter se agregar valor de backlog/listagem. | Aberta |
| P005 | Definir política de edição de projeto após encerramento. | Inovação | Recomendado bloquear alterações, exceto comentários administrativos. | Aberta |
| P006 | Definir visual final da tela de triagem. | Produto / Lovable | Criar no Lovable com base nesta especificação. | Aberta |

---

<a id="ef-12-controle-de-mudancas-de-escopo"></a>
## 12. Controle de mudanças de escopo

| Data | Solicitação | Impacto | Aprovado por | Status |
|---|---|---|---|---|
| 2026-07-07 | Criação da especificação inicial | Define escopo funcional base | A definir | Em revisão |
| 2026-07-08 | Revisão de objetividade e redução de redundâncias | Mantém escopo e melhora uso pelo desenvolvimento | A definir | Em revisão |

---

<a id="ef-13-aprovacao-funcional"></a>
## 13. Aprovação funcional

| Papel | Nome | Data | Aprovação |
|---|---|---|---|
| Solicitante / Dono do produto | A definir |  |  |
| Desenvolvimento | Phablo Tavares | 2026-07-08 | Em revisão |
