# Especificação Funcional — Portal de Gestão da Inovação Rennova

> Documento objetivo para orientar construção, aceite e evolução do Portal de Gestão da Inovação da Rennova.

---

<a id="sumario"></a>
## Sumário

- [1. Identificação do projeto](#ef-1-identificacao-do-projeto)
- [2. Visão geral](#ef-2-visao-geral)
  - [2.1 Contexto](#ef-2-1-contexto)
  - [2.2 Objetivo do projeto](#ef-2-2-objetivo-do-projeto)
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
  - [RN001 - Perfis do portal](#ef-rn001-perfis-do-portal)
  - [RN002 - Autorização reforçada no backend](#ef-rn002-autorizacao-reforcada-no-backend)
  - [RN003 - Usuário inativo não acessa o portal](#ef-rn003-usuario-inativo-nao-acessa-o-portal)
  - [RN004 - Campos obrigatórios do Canvas](#ef-rn004-campos-obrigatorios-do-canvas)
  - [RN005 - Status da ideia](#ef-rn005-status-da-ideia)
  - [RN006 - Formulário público sem insert direto no banco](#ef-rn006-formulario-publico-sem-insert-direto-no-banco)
  - [RN007 - Proteção anti-spam](#ef-rn007-protecao-anti-spam)
  - [RN008 - IA como apoio, não autoridade final](#ef-rn008-ia-como-apoio-nao-autoridade-final)
  - [RN009 - Respostas de IA estruturadas](#ef-rn009-respostas-de-ia-estruturadas)
  - [RN010 - Escala de impacto e esforço](#ef-rn010-escala-de-impacto-e-esforco)
  - [RN011 - Pontuação não visível ao autor](#ef-rn011-pontuacao-nao-visivel-ao-autor)
  - [RN012 - Asana como fonte operacional](#ef-rn012-asana-como-fonte-operacional)
  - [RN013 - Dashboard baseado em cache](#ef-rn013-dashboard-baseado-em-cache)
  - [RN014 - Elegibilidade da matriz](#ef-rn014-elegibilidade-da-matriz)
  - [RN015 - Notas finais prevalecem sobre notas IA](#ef-rn015-notas-finais-prevalecem-sobre-notas-ia)
  - [RN016 - Conversão exige decisão explícita](#ef-rn016-conversao-exige-decisao-explicita)
  - [RN017 - Conversão idempotente](#ef-rn017-conversao-idempotente)
  - [RN018 - Sem custom fields de projeto no Asana](#ef-rn018-sem-custom-fields-de-projeto-no-asana)
  - [RN019 - Descrição inicial do projeto Asana](#ef-rn019-descricao-inicial-do-projeto-asana)
  - [RN020 - Fases fixas do projeto](#ef-rn020-fases-fixas-do-projeto)
  - [RN021 - Progresso por fases concluídas](#ef-rn021-progresso-por-fases-concluidas)
  - [RN022 - Encerramento de projeto](#ef-rn022-encerramento-de-projeto)
  - [RN023 - Insight de IA exige resultado](#ef-rn023-insight-de-ia-exige-resultado)
  - [RN024 - Sincronização Asana resiliente](#ef-rn024-sincronizacao-asana-resiliente)
  - [RN025 - Comentários de governança separados da operação](#ef-rn025-comentarios-de-governanca-separados-da-operacao)
  - [RN026 - Departamentos inativáveis](#ef-rn026-departamentos-inativaveis)
  - [RN027 - Perfil não pode autoelevar papel](#ef-rn027-perfil-nao-pode-autoelevar-papel)
  - [RN028 - Secrets somente no backend](#ef-rn028-secrets-somente-no-backend)
  - [RN029 - Logs de auditoria não sensíveis](#ef-rn029-logs-de-auditoria-nao-sensiveis)
  - [RN030 - Mensagens claras e não técnicas](#ef-rn030-mensagens-claras-e-nao-tecnicas)
- [6. Fluxos de usuário](#ef-6-fluxos-de-usuario)
  - [Fluxo 1 - Envio de ideia pelo Canvas](#ef-fluxo-1-envio-de-ideia-pelo-canvas)
  - [Fluxo 2 - Triagem e priorização](#ef-fluxo-2-triagem-e-priorizacao)
  - [Fluxo 3 - Conversão para projeto Asana](#ef-fluxo-3-conversao-para-projeto-asana)
  - [Fluxo 4 - Acompanhamento executivo](#ef-fluxo-4-acompanhamento-executivo)
  - [Fluxo 5 - Gestão de governança do projeto](#ef-fluxo-5-gestao-de-governanca-do-projeto)
- [7. Mapa de navegação](#ef-7-mapa-de-navegacao)
- [8. Telas, wireframes e comportamento visual](#ef-8-telas-wireframes-e-comportamento-visual)
  - [Tela 1 - Canvas público](#ef-tela-1-canvas-publico)
  - [Tela 2 - Login](#ef-tela-2-login)
  - [Tela 3 - Dashboard](#ef-tela-3-dashboard)
  - [Tela 4 - Matriz Impacto × Esforço](#ef-tela-4-matriz-impacto-x-esforco)
  - [Tela 5 - Triagem](#ef-tela-5-triagem)
  - [Tela 6 - Detalhe do projeto](#ef-tela-6-detalhe-do-projeto)
  - [Tela 7 - Admin](#ef-tela-7-admin)
- [9. Requisitos não funcionais](#ef-9-requisitos-nao-funcionais)
  - [9.1 Segurança](#ef-9-1-seguranca)
  - [9.2 Performance](#ef-9-2-performance)
  - [9.3 Usabilidade](#ef-9-3-usabilidade)
  - [9.4 Compatibilidade](#ef-9-4-compatibilidade)
  - [9.5 Logs e auditoria funcional](#ef-9-5-logs-e-auditoria-funcional)
- [10. Mensagens do sistema](#ef-10-mensagens-do-sistema)
- [11. Pendências e dúvidas funcionais](#ef-11-pendencias-e-duvidas-funcionais)
- [12. Controle de mudanças de escopo](#ef-12-controle-de-mudancas-de-escopo)
- [13. Aprovação funcional](#ef-13-aprovacao-funcional)
---

<a id="ef-1-identificacao-do-projeto"></a>
## 1. Identificação do projeto

### Nome do projeto

**Rennova Spark Hub — Portal de Gestão da Inovação**

### Responsável pelo documento

**Nome:** Phablo Tavares  
**Área/Time:** Inovação / Desenvolvimento de Agentes e Soluções de IA  
**Data:** 2026-07-08  
**Versão:** 0.2

---

<a id="ef-2-visao-geral"></a>
## 2. Visão geral

<a id="ef-2-1-contexto"></a>
### 2.1 Contexto

A área de Inovação da Rennova recebe ideias de diferentes áreas, avalia potencial, prioriza iniciativas e acompanha projetos aprovados. Hoje, parte desse processo fica dispersa entre conversas, documentos, planilhas e ferramentas operacionais. A gestão precisa de uma visão única para entrada de ideias, triagem, priorização, conversão em projetos e acompanhamento executivo.

Já existe um protótipo visual do portal no Lovable/GitHub, com telas de Dashboard, Projetos, Detalhe de Projeto e Ideias usando dados mockados. O sistema a ser construído deve transformar esse protótipo em produto funcional com Supabase, autenticação, banco real, IA e integração com Asana.

<a id="ef-2-2-objetivo-do-projeto"></a>
### 2.2 Objetivo do projeto

Construir um portal interno para centralizar a gestão da inovação na Rennova, permitindo que colaboradores submetam ideias, a área de Inovação qualifique e priorize iniciativas, a diretoria acompanhe o portfólio e projetos aprovados sejam integrados ao Asana para execução operacional.

<a id="ef-2-3-publico-alvo-usuarios"></a>
### 2.3 Público-alvo / usuários

| Ator / Perfil | Descrição | Principais ações no sistema |
|---|---|---|
| Colaborador | Pessoa da Rennova que envia uma ideia pelo Canvas público | Preencher Canvas, solicitar sugestões de IA, revisar resumo, aprovar submissão |
| Autor da ideia | Colaborador que submeteu uma ideia | Aprovar ou ajustar o resumo gerado por IA antes da triagem |
| Inovação | Time responsável por gerir o funil de inovação | Triar ideias, ajustar impacto/esforço, converter ideias em projetos, gerir fases, métricas, comentários e cadastros |
| Diretoria | Usuários com visão executiva | Consultar dashboard, matriz e detalhes dos projetos sem editar dados |
| Administrador funcional | Usuário da Inovação com atribuição de gestão | Gerenciar departamentos e perfis de usuários |
| Sistema / Integrações | Edge Functions, IA e Asana | Gerar sugestões, criar projetos no Asana, sincronizar dados operacionais e registrar logs |

---

<a id="ef-3-escopo"></a>
## 3. Escopo

<a id="ef-3-1-escopo-incluido"></a>
### 3.1 Escopo incluído

- [x] Base visual inicial com tema escuro, dashboard, projetos, detalhes e ideias usando mockData.
- [ ] Form Canvas público sem login para submissão de ideias.
- [ ] Sugestões de IA por bloco do Canvas.
- [ ] Geração de resumo consolidado da ideia por IA.
- [ ] Aprovação ou ajuste do resumo pelo autor da ideia.
- [ ] Login com Supabase Auth por e-mail e senha.
- [ ] Controle de acesso por perfis `diretoria` e `inovacao`.
- [ ] Dashboard executivo com indicadores do portfólio, progresso e dados do Asana cacheados.
- [ ] Matriz Impacto × Esforço para ideias elegíveis.
- [ ] Triagem mensal de ideias pela área de Inovação.
- [ ] Conversão de ideia em projeto no portal e no Asana.
- [ ] Detalhe do projeto com fases, checklist executivo, métricas, resultados, insights de IA e comentários de governança.
- [ ] Bloco de tarefas Asana somente leitura no detalhe do projeto.
- [ ] Sincronização Asana → portal por webhook e cron de reconciliação.
- [ ] Administração de departamentos e usuários.
- [ ] Logs de auditoria para ações relevantes.

<a id="ef-3-2-fora-de-escopo"></a>
### 3.2 Fora de escopo

- Substituir o Asana como ferramenta operacional de gestão de tarefas.
- Edição de tarefas Asana dentro do portal.
- SSO corporativo na primeira versão.
- Aplicativo mobile nativo.
- Gestão financeira detalhada de orçamento, custos ou CAPEX/OPEX.
- Workflow completo de aprovação multinível fora da triagem de Inovação.
- Relatórios avançados de BI fora dos indicadores previstos no dashboard.
- Migração automática de dados históricos não estruturados.
- Integração com ERP, CRM, e-mail ou sistemas internos além do Asana.
- Permitir que o autor acompanhe a evolução da ideia após aprovação, salvo se isso for definido em nova fase.

<a id="ef-3-3-premissas"></a>
### 3.3 Premissas

- O Lovable continuará sendo a principal ferramenta de evolução do front-end do portal.
- O projeto usará Supabase para Auth, Postgres, RLS e Edge Functions.
- O Asana será a fonte operacional de tarefas e sprints.
- O Supabase será a fonte de verdade para ideias, triagem, governança, métricas, usuários e visão executiva.
- Tokens de Asana e IA serão armazenados somente como secrets nas Edge Functions.
- O workspace, template, portfólio e owner padrão do Asana já foram identificados.
- A IA retornará respostas estruturadas em JSON e sempre passará por validação antes de gravar dados.
- A primeira versão priorizará desktop/responsividade básica para web.

<a id="ef-3-4-restricoes"></a>
### 3.4 Restrições

- Não expor chaves, tokens ou service role no front-end.
- Não chamar Asana nem provedores de IA diretamente pelo browser.
- Evitar edição manual ampla do código fora do Lovable para não comprometer a continuidade de evolução no Lovable.
- O formulário público deve ter proteção anti-spam mínima.
- A nota de impacto/esforço não deve ser exibida ao autor da ideia.
- Perfis de usuários e permissões devem ser aplicados no front-end e reforçados por RLS/Edge Functions.
- O dashboard não deve depender de chamada ao Asana em tempo real.

---

<a id="ef-4-requisitos-funcionais"></a>
## 4. Requisitos funcionais

<a id="ef-rf001-autenticacao-no-portal-interno"></a>
### RF001 - Autenticação no portal interno

#### Descrição

O sistema deve permitir login no portal interno por e-mail e senha usando Supabase Auth.

#### Ator principal

Diretoria e Inovação.

#### Pré-condições

- Usuário cadastrado no Supabase Auth.
- Usuário possui linha correspondente em `profiles`.
- Usuário está ativo.

#### Fluxo principal

1. Usuário acessa `/login`.
2. Sistema exibe formulário de e-mail e senha.
3. Usuário informa credenciais válidas.
4. Sistema autentica no Supabase.
5. Sistema consulta perfil e permissões.
6. Sistema redireciona para o Dashboard.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Credenciais inválidas | Exibir mensagem de login inválido sem detalhar se e-mail existe |
| FA002 | Usuário inativo | Bloquear acesso e orientar contato com Inovação |
| FA003 | Perfil inexistente | Bloquear acesso e registrar erro técnico |
| FA004 | Sessão expirada | Redirecionar para `/login` |

#### Regras de negócio relacionadas

- RN001, RN002, RN003

#### Critérios de aceite

- Dado um usuário ativo, quando informar credenciais válidas, então acessa o Dashboard.
- Dado um usuário inativo, quando tentar login, então o acesso é bloqueado.
- Dado um usuário não autenticado, quando acessar rota interna, então é redirecionado para `/login`.

#### Observações

Não haverá SSO na primeira versão.

---

<a id="ef-rf002-controle-de-acesso-por-perfil"></a>
### RF002 - Controle de acesso por perfil

#### Descrição

O sistema deve restringir funcionalidades conforme o perfil do usuário: `diretoria` ou `inovacao`.

#### Ator principal

Sistema.

#### Pré-condições

- Usuário autenticado.
- Perfil definido em `profiles.role`.

#### Fluxo principal

1. Usuário acessa uma rota interna.
2. Sistema carrega o perfil do usuário.
3. Sistema exibe apenas menus e ações permitidas.
4. Banco/Edge Functions reforçam a permissão.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Diretoria tenta acessar `/triagem` ou `/admin` | Exibir acesso negado |
| FA002 | Diretoria tenta alterar dados por chamada direta | RLS ou Edge Function bloqueia a operação |
| FA003 | Perfil desconhecido | Bloquear acesso por segurança |

#### Regras de negócio relacionadas

- RN001, RN002

#### Critérios de aceite

- Dado um usuário `diretoria`, quando acessar dashboard, matriz e detalhe, então visualiza os dados em modo leitura.
- Dado um usuário `diretoria`, quando tentar editar projeto, então a ação não está disponível e é bloqueada no backend.
- Dado um usuário `inovacao`, quando acessar triagem e admin, então pode executar ações de gestão.

#### Observações

A restrição visual no front-end não substitui RLS e validações nas Edge Functions.

---

<a id="ef-rf003-submissao-de-ideia-pelo-canvas-publico"></a>
### RF003 - Submissão de ideia pelo Canvas público

#### Descrição

O sistema deve permitir que qualquer colaborador envie uma ideia pela rota pública `/canvas`, sem login.

#### Ator principal

Colaborador.

#### Pré-condições

- Rota pública disponível.
- Departamentos ativos disponíveis para seleção.
- Edge Function `submit-idea` configurada.

#### Fluxo principal

1. Colaborador acessa `/canvas`.
2. Sistema exibe formulário com dados do solicitante e 7 blocos do Canvas.
3. Colaborador preenche campos obrigatórios.
4. Colaborador envia a ideia.
5. Sistema valida os dados e executa proteção anti-spam.
6. Sistema grava a ideia com status `enviada`.
7. Sistema inicia ou chama geração de resumo por IA.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Campos obrigatórios vazios | Bloquear envio e destacar campos pendentes |
| FA002 | E-mail inválido | Bloquear envio e solicitar correção |
| FA003 | Rate limit ou honeypot acionado | Bloquear envio com mensagem genérica |
| FA004 | Falha de gravação | Exibir erro e permitir nova tentativa |
| FA005 | Departamentos indisponíveis | Exibir campo alternativo ou mensagem de indisponibilidade temporária |

#### Regras de negócio relacionadas

- RN004, RN005, RN006, RN007

#### Critérios de aceite

- Dado um colaborador sem login, quando acessar `/canvas`, então consegue preencher e enviar uma ideia válida.
- Dado um Canvas incompleto, quando tentar enviar, então o sistema bloqueia o envio.
- Dado uma submissão válida, quando enviada, então a ideia é registrada em `ideas` com status `enviada`.

#### Observações

A rota é pública, mas a escrita no banco deve ocorrer somente via Edge Function com `service_role`.

---

<a id="ef-rf004-sugestao-de-ia-por-bloco-do-canvas"></a>
### RF004 - Sugestão de IA por bloco do Canvas

#### Descrição

O sistema deve permitir que o autor solicite uma sugestão de IA para cada bloco do Canvas.

#### Ator principal

Colaborador.

#### Pré-condições

- Formulário `/canvas` aberto.
- Edge Function `ai-assist-block` configurada.
- Provider de IA configurado por secret.

#### Fluxo principal

1. Colaborador clica em “Sugestão IA” em um bloco.
2. Sistema envia contexto do Canvas e nome do bloco para a Edge Function.
3. IA retorna uma sugestão objetiva.
4. Sistema exibe a sugestão para o usuário aceitar, editar ou ignorar.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | IA indisponível | Informar indisponibilidade e manter edição manual |
| FA002 | Resposta inválida | Ignorar resposta, registrar erro e exibir mensagem genérica |
| FA003 | Conteúdo insuficiente | IA pode retornar pergunta orientadora ou sugestão genérica |

#### Regras de negócio relacionadas

- RN008, RN009

#### Critérios de aceite

- Dado um bloco do Canvas, quando clicar em “Sugestão IA”, então o sistema retorna uma sugestão editável.
- Dado falha da IA, quando solicitar sugestão, então o usuário continua podendo preencher manualmente.

#### Observações

A sugestão não deve enviar dados sensíveis desnecessários ao provedor de IA.

---

<a id="ef-rf005-resumo-de-ia-e-aprovacao-pelo-autor"></a>
### RF005 - Resumo de IA e aprovação pelo autor

#### Descrição

O sistema deve gerar um resumo consolidado da ideia e permitir que o autor aprove ou complemente o resumo antes da triagem.

#### Ator principal

Autor da ideia.

#### Pré-condições

- Ideia enviada com status `enviada`.
- Edge Function `ai-summarize-idea` configurada.

#### Fluxo principal

1. Sistema envia os blocos da ideia para a Edge Function.
2. IA retorna resumo, impacto sugerido e esforço sugerido em JSON estruturado.
3. Sistema grava `resumo_ia`, `impacto_ia`, `esforco_ia` e status `resumo_gerado`.
4. Sistema exibe o resumo ao autor.
5. Autor aprova ou complementa com comentário/ajuste.
6. Sistema marca `resumo_aprovado = true` e status `aprovada_autor`.
7. Sistema exibe confirmação.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | IA falha | Permitir submissão com resumo pendente para tratamento pela Inovação |
| FA002 | JSON inválido | Não gravar pontuações, registrar erro e exibir mensagem genérica |
| FA003 | Autor edita/comenta | Gravar comentário/ajuste e seguir para aprovação |
| FA004 | Autor abandona tela | Ideia permanece em `resumo_gerado` ou fluxo definido de expiração |

#### Regras de negócio relacionadas

- RN005, RN008, RN010, RN011

#### Critérios de aceite

- Dado uma ideia enviada, quando a IA gerar resumo válido, então o autor visualiza o resumo antes da triagem.
- Dado o resumo exibido ao autor, quando ele aprovar, então a ideia passa para `aprovada_autor`.
- Dado o autor na tela de aprovação, então impacto e esforço não são exibidos.

#### Observações

A forma exata de retomada do fluxo pelo autor após abandono deve ser definida antes da produção.

---

<a id="ef-rf006-dashboard-executivo"></a>
### RF006 - Dashboard executivo

#### Descrição

O sistema deve exibir uma visão executiva do portfólio de inovação.

#### Ator principal

Diretoria e Inovação.

#### Pré-condições

- Usuário autenticado.
- Dados de projetos, ideias e `asana_sync` disponíveis.

#### Fluxo principal

1. Usuário acessa `/`.
2. Sistema exibe KPIs de projetos ativos, progresso médio, tarefas abertas e ideias em triagem.
3. Sistema exibe lista de projetos ativos com área, status, progresso e última atualização.
4. Usuário filtra por área e status.
5. Usuário acessa detalhe de um projeto.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Sem projetos cadastrados | Exibir estado vazio |
| FA002 | Sem dados de Asana | Exibir contagem como indisponível ou zero conforme regra definida |
| FA003 | Erro de carregamento | Exibir erro e opção de tentar novamente |

#### Regras de negócio relacionadas

- RN001, RN012, RN013

#### Critérios de aceite

- Dado um usuário autenticado, quando acessar o Dashboard, então visualiza KPIs calculados com dados do Supabase.
- Dado filtros selecionados, quando aplicados, então a lista de projetos é filtrada corretamente.
- Dado indisponibilidade do Asana, quando acessar o Dashboard, então a tela não chama Asana ao vivo e permanece funcional.

#### Observações

A tela atual já existe em protótipo com dados mockados; a implementação final deve substituir mocks por consultas reais.

---

<a id="ef-rf007-matriz-impacto-x-esforco"></a>
### RF007 - Matriz Impacto × Esforço

#### Descrição

O sistema deve exibir ideias elegíveis em uma matriz de priorização impacto×esforço.

#### Ator principal

Diretoria e Inovação.

#### Pré-condições

- Usuário autenticado.
- Ideias com status elegível e pontuações disponíveis.

#### Fluxo principal

1. Usuário acessa `/matriz`.
2. Sistema busca ideias com status `aprovada_autor`, `em_triagem` e `backlog`.
3. Sistema plota ideias em gráfico de dispersão com esforço no eixo X e impacto no eixo Y.
4. Sistema diferencia pontuação IA de pontuação final de triagem.
5. Usuário clica em uma ideia para abrir detalhes.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Ideia sem pontuação | Não plotar ou exibir em lista de pendências de triagem |
| FA002 | Sem ideias elegíveis | Exibir estado vazio |
| FA003 | Usuário diretoria | Permitir leitura sem ações de decisão |

#### Regras de negócio relacionadas

- RN010, RN014, RN015

#### Critérios de aceite

- Dado ideias elegíveis com notas, quando acessar `/matriz`, então elas aparecem nos quadrantes corretos.
- Dado uma ideia convertida ou arquivada, quando acessar a matriz, então ela não aparece.
- Dado usuário diretoria, quando abrir detalhe da ideia, então não consegue alterar decisão.

#### Observações

A tela atual de Ideias já contém matriz em protótipo com escala 0–10; a versão final deve usar escala 1–5.

---

<a id="ef-rf008-triagem-mensal-de-ideias"></a>
### RF008 - Triagem mensal de ideias

#### Descrição

O sistema deve permitir que a Inovação realize triagem mensal de ideias, ajuste notas e registre decisão.

#### Ator principal

Inovação.

#### Pré-condições

- Usuário autenticado com perfil `inovacao`.
- Ideias em `aprovada_autor` ou `em_triagem`.

#### Fluxo principal

1. Usuário acessa `/triagem`.
2. Sistema lista ideias elegíveis do mês.
3. Usuário abre resumo e dados do Canvas.
4. Usuário ajusta `impacto_final` e `esforco_final`.
5. Usuário escolhe decisão: Vira Projeto, Backlog ou Arquivar.
6. Sistema atualiza status da ideia.
7. Sistema registra sessão em `triage_sessions` e log em `activity_log`.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Notas fora de 1–5 | Bloquear salvamento |
| FA002 | Decisão “Vira Projeto” sem notas finais | Bloquear conversão |
| FA003 | Falha ao converter no Asana | Manter ideia em estado seguro e exibir erro |
| FA004 | Usuário sem permissão | Bloquear acesso |

#### Regras de negócio relacionadas

- RN001, RN010, RN015, RN016, RN017

#### Critérios de aceite

- Dado usuário `inovacao`, quando ajustar notas válidas, então o sistema salva impacto/esforço final.
- Dado decisão Backlog, quando confirmada, então a ideia permanece visível na matriz.
- Dado decisão Arquivar, quando confirmada, então a ideia sai da matriz.
- Dado decisão Vira Projeto, quando concluída com sucesso, então a ideia é convertida em projeto.

#### Observações

Triagem pode ser simples na primeira versão, sem workflow formal de aprovação em múltiplas etapas.

---

<a id="ef-rf009-conversao-de-ideia-em-projeto"></a>
### RF009 - Conversão de ideia em projeto

#### Descrição

O sistema deve converter uma ideia aprovada em projeto no portal e instanciar o projeto correspondente no Asana.

#### Ator principal

Inovação.

#### Pré-condições

- Ideia elegível com decisão “Vira Projeto”.
- Notas finais válidas.
- Secrets do Asana configurados.
- Template e portfólio Asana disponíveis.

#### Fluxo principal

1. Usuário confirma “Vira Projeto”.
2. Sistema chama Edge Function `asana-create-project`.
3. Função verifica idempotência.
4. Função cria registro de projeto no Supabase ou prepara conversão transacional.
5. Função instancia template no Asana.
6. Função aguarda job de criação concluir.
7. Função adiciona projeto ao portfólio de Inovação.
8. Função atualiza descrição e owner no Asana.
9. Função grava `asana_project_gid`, `asana_permalink` e vínculo da ideia.
10. Função registra log e atualiza status da ideia para `virou_projeto`.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Ideia já convertida | Bloquear nova conversão e retornar conflito |
| FA002 | Job Asana falha | Registrar erro e não marcar conversão como concluída |
| FA003 | Falha ao adicionar ao portfólio | Registrar erro e sinalizar pendência de sincronização |
| FA004 | Falha parcial após criar projeto Asana | Registrar estado de recuperação manual |
| FA005 | Token Asana inválido | Retornar erro controlado e registrar log técnico |

#### Regras de negócio relacionadas

- RN016, RN017, RN018, RN019

#### Critérios de aceite

- Dado uma ideia não convertida, quando for aprovada como projeto, então um projeto é criado no portal e no Asana.
- Dado uma ideia já convertida, quando tentar converter novamente, então o sistema impede duplicidade.
- Dado falha do Asana, quando converter, então o erro é registrado e não há confirmação falsa ao usuário.

#### Observações

A implementação deve tratar idempotência e falhas parciais explicitamente.

---

<a id="ef-rf010-detalhe-e-governanca-do-projeto"></a>
### RF010 - Detalhe e governança do projeto

#### Descrição

O sistema deve exibir e permitir gerir informações executivas do projeto aprovado.

#### Ator principal

Inovação; Diretoria em modo leitura.

#### Pré-condições

- Usuário autenticado.
- Projeto existente.

#### Fluxo principal

1. Usuário acessa `/projetos/:id`.
2. Sistema exibe título, status, progresso, área, owner e datas.
3. Sistema exibe resumo IA, objetivo, problema e descrição.
4. Sistema exibe fases, checklist, métricas, Asana e comentários.
5. Usuário `inovacao` pode editar itens permitidos.
6. Usuário `diretoria` apenas consulta.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Projeto inexistente | Exibir “Projeto não encontrado” |
| FA002 | Usuário sem permissão de edição | Ocultar/bloquear ações editáveis |
| FA003 | Dados de Asana ausentes | Exibir bloco Asana em estado vazio/indisponível |

#### Regras de negócio relacionadas

- RN001, RN012, RN020, RN021

#### Critérios de aceite

- Dado um projeto existente, quando acessar detalhe, então todas as seções executivas são exibidas.
- Dado usuário diretoria, quando acessar detalhe, então nenhuma ação de edição está disponível.
- Dado usuário inovação, quando acessar detalhe, então pode gerir fases, checklist, métricas e comentários.

#### Observações

A tela atual já existe em protótipo com dados mockados e deve ser mantida visualmente sempre que possível.

---

<a id="ef-rf011-gestao-de-fases-e-checklist-executivo"></a>
### RF011 - Gestão de fases e checklist executivo

#### Descrição

O sistema deve permitir que a Inovação acompanhe cinco fases fixas do projeto e checklist executivo por fase.

#### Ator principal

Inovação.

#### Pré-condições

- Usuário `inovacao` autenticado.
- Projeto existente.
- Fases semeadas em `project_phases`.

#### Fluxo principal

1. Usuário acessa detalhe do projeto.
2. Sistema exibe stepper de cinco fases.
3. Usuário marca checklist da fase atual.
4. Usuário marca fase como concluída.
5. Sistema atualiza status da fase.
6. Trigger recalcula `progress_pct`.
7. Sistema reflete novo progresso.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Fase anterior pendente | Impedir avanço, salvo regra futura de exceção |
| FA002 | Projeto encerrado | Bloquear alteração de fases/checklist |
| FA003 | Falha ao salvar | Exibir erro e manter estado anterior |

#### Regras de negócio relacionadas

- RN020, RN021, RN022

#### Critérios de aceite

- Dado uma fase marcada como concluída, quando salvar, então o progresso do projeto é recalculado.
- Dado cinco fases concluídas, quando visualizar projeto, então progresso é 100%.
- Dado projeto encerrado, quando tentar alterar fase, então ação é bloqueada.

#### Observações

Checklist do portal é executivo e não substitui tarefas do Asana.

---

<a id="ef-rf012-metricas-resultados-e-insight-de-ia"></a>
### RF012 - Métricas, resultados e insight de IA

#### Descrição

O sistema deve permitir registrar métricas do projeto, resultados e gerar insight de IA comparando meta e realizado.

#### Ator principal

Inovação.

#### Pré-condições

- Projeto existente.
- Métricas cadastradas ou derivadas dos indicadores da ideia.
- Edge Function `ai-generate-insight` configurada.

#### Fluxo principal

1. Usuário acessa métricas no detalhe do projeto.
2. Sistema exibe indicador, meta, unidade e resultado.
3. Usuário preenche resultado.
4. Usuário clica em “Gerar insight”.
5. Sistema chama Edge Function.
6. IA retorna análise objetiva.
7. Sistema grava `insight_ia`.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Resultado vazio | Bloquear geração de insight |
| FA002 | IA indisponível | Manter resultado salvo e informar falha do insight |
| FA003 | Resposta inválida | Não gravar insight e registrar erro |

#### Regras de negócio relacionadas

- RN008, RN023

#### Critérios de aceite

- Dado uma métrica com resultado preenchido, quando gerar insight, então o sistema grava uma análise da IA.
- Dado falha da IA, quando gerar insight, então o resultado não é perdido.

#### Observações

Insights são apoio à governança, não decisão automática.

---

<a id="ef-rf013-bloco-asana-no-projeto"></a>
### RF013 - Bloco Asana no projeto

#### Descrição

O sistema deve exibir dados operacionais do Asana no detalhe do projeto, em modo somente leitura.

#### Ator principal

Diretoria e Inovação.

#### Pré-condições

- Projeto possui `asana_project_gid`.
- `asana_sync` possui dados sincronizados ou estado vazio.

#### Fluxo principal

1. Usuário acessa detalhe do projeto.
2. Sistema consulta `asana_sync`.
3. Sistema exibe total de tarefas, abertas, concluídas, distribuição de status e última atualização.
4. Sistema exibe botão “Abrir no Asana”.
5. Usuário clica e é direcionado ao Asana.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Projeto sem Asana | Exibir “Projeto ainda não integrado ao Asana” |
| FA002 | Cache vazio | Exibir estado “Aguardando sincronização” |
| FA003 | Permalink ausente | Ocultar botão ou exibir indisponível |

#### Regras de negócio relacionadas

- RN012, RN018, RN024

#### Critérios de aceite

- Dado projeto integrado ao Asana, quando abrir detalhe, então o bloco exibe dados vindos de `asana_sync`.
- Dado usuário clica em “Abrir no Asana”, então abre o projeto Asana em nova aba.
- Dado qualquer usuário, então não é possível editar tarefa Asana pelo portal.

#### Observações

O portal nunca deve consultar o Asana ao vivo durante renderização da tela.

---

<a id="ef-rf014-comentarios-de-governanca"></a>
### RF014 - Comentários de governança

#### Descrição

O sistema deve permitir registrar comentários de governança no projeto.

#### Ator principal

Inovação.

#### Pré-condições

- Usuário `inovacao` autenticado.
- Projeto existente.

#### Fluxo principal

1. Usuário acessa detalhe do projeto.
2. Sistema exibe comentários existentes.
3. Usuário adiciona comentário.
4. Sistema salva comentário com autor e data.
5. Sistema registra log quando aplicável.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Comentário vazio | Bloquear envio |
| FA002 | Usuário diretoria | Permitir leitura, bloquear criação |
| FA003 | Falha ao salvar | Exibir erro e manter texto digitado |

#### Regras de negócio relacionadas

- RN001, RN025

#### Critérios de aceite

- Dado usuário `inovacao`, quando publicar comentário válido, então ele aparece no histórico do projeto.
- Dado usuário `diretoria`, quando visualizar comentários, então não consegue adicionar novos.

#### Observações

Comentários operacionais de tarefas devem permanecer no Asana.

---

<a id="ef-rf015-administracao-de-departamentos-e-usuarios"></a>
### RF015 - Administração de departamentos e usuários

#### Descrição

O sistema deve permitir que a Inovação gerencie departamentos e perfis de usuários.

#### Ator principal

Inovação.

#### Pré-condições

- Usuário `inovacao` autenticado.

#### Fluxo principal

1. Usuário acessa `/admin`.
2. Sistema exibe departamentos e usuários.
3. Usuário cria, edita ou inativa departamento.
4. Usuário altera nome, papel ou status de usuário.
5. Sistema salva alterações e registra log.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Departamento duplicado | Bloquear criação |
| FA002 | Tentativa de excluir departamento em uso | Preferir inativação |
| FA003 | Usuário tenta alterar próprio papel indevidamente | Bloquear se não for fluxo autorizado |
| FA004 | Usuário sem permissão | Bloquear acesso |

#### Regras de negócio relacionadas

- RN001, RN026, RN027

#### Critérios de aceite

- Dado usuário `inovacao`, quando criar departamento com nome único, então ele fica disponível para seleção.
- Dado departamento em uso, quando quiser remover, então o sistema permite inativar sem quebrar histórico.
- Dado usuário diretoria, quando acessar `/admin`, então recebe acesso negado.

#### Observações

Deve ser revisada a política de atualização de `profiles` para impedir autoelevação de perfil.

---

<a id="ef-rf016-sincronizacao-asana-portal"></a>
### RF016 - Sincronização Asana → Portal

#### Descrição

O sistema deve manter dados operacionais do Asana sincronizados em `asana_sync` por webhook e cron.

#### Ator principal

Sistema.

#### Pré-condições

- Projeto possui `asana_project_gid`.
- Edge Functions `asana-webhook` e `asana-sync` configuradas.
- Token Asana válido.

#### Fluxo principal

1. Na conversão, sistema cria webhook para o projeto Asana.
2. Asana envia handshake para `asana-webhook`.
3. Função responde conforme protocolo do Asana.
4. Eventos do Asana atualizam ou sinalizam atualização de `asana_sync`.
5. Cron diário executa reconciliação completa.
6. Dashboard e detalhe leem apenas `asana_sync`.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Webhook perdido | Cron diário corrige dados posteriormente |
| FA002 | Handshake inválido | Não criar webhook e registrar erro |
| FA003 | Token inválido | Registrar erro de integração |
| FA004 | Rate limit | Aplicar retry/backoff quando necessário |

#### Regras de negócio relacionadas

- RN012, RN018, RN024, RN028

#### Critérios de aceite

- Dado projeto integrado, quando Asana atualizar tarefas, então `asana_sync` é atualizado por webhook ou cron.
- Dado falha de webhook, quando cron rodar, então dados são reconciliados.
- Dado dashboard carregado, então nenhuma chamada direta ao Asana é feita pelo front-end.

#### Observações

A validação de assinatura/segredo do webhook deve ser parte do design técnico.

---

<a id="ef-rf017-auditoria-de-acoes-relevantes"></a>
### RF017 - Auditoria de ações relevantes

#### Descrição

O sistema deve registrar ações relevantes em `activity_log`.

#### Ator principal

Sistema.

#### Pré-condições

- Tabela `activity_log` disponível.

#### Fluxo principal

1. Usuário ou sistema executa ação relevante.
2. Sistema identifica entidade, ação, ator e detalhes não sensíveis.
3. Sistema grava log.
4. Inovação pode consultar logs quando necessário.

#### Fluxos alternativos e exceções

| Código | Situação | Comportamento esperado |
|---|---|---|
| FA001 | Falha ao gravar log não crítico | Não bloquear fluxo principal, mas registrar erro técnico quando possível |
| FA002 | Dados sensíveis no detalhe | Remover/mascarar antes de gravar |

#### Regras de negócio relacionadas

- RN029, RN030

#### Critérios de aceite

- Dado conversão de ideia, quando concluída, então há log com `action = convert`.
- Dado alteração de status relevante, quando salva, então há log de auditoria.
- Dado qualquer log, então não contém tokens, senhas ou chaves.

#### Observações

Log não substitui monitoramento técnico das Edge Functions.

---

<a id="ef-5-regras-de-negocio"></a>
## 5. Regras de negócio

<a id="ef-rn001-perfis-do-portal"></a>
### RN001 - Perfis do portal

#### Descrição

O sistema terá dois perfis funcionais: `diretoria` e `inovacao`.

#### Aplicável em

- RF001, RF002, RF006 a RF017

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Usuário `diretoria` acessa Dashboard | Acesso permitido em leitura |
| Inválido | Usuário `diretoria` acessa Admin | Acesso negado |

#### Observações

Novos perfis exigem mudança de escopo.

<a id="ef-rn002-autorizacao-reforcada-no-backend"></a>
### RN002 - Autorização reforçada no backend

#### Descrição

Permissões devem ser aplicadas por RLS e/ou Edge Functions, não apenas por ocultação de botões no front-end.

#### Aplicável em

- RF002, RF008, RF010, RF015

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Inovação atualiza fase | Operação permitida |
| Inválido | Diretoria tenta atualizar fase via API | Operação bloqueada |

#### Observações

Toda operação sensível deve ser validada server-side.

<a id="ef-rn003-usuario-inativo-nao-acessa-o-portal"></a>
### RN003 - Usuário inativo não acessa o portal

#### Descrição

Usuários com `profiles.ativo = false` não devem acessar áreas internas.

#### Aplicável em

- RF001, RF002

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Usuário inativo realiza login | Acesso bloqueado |

#### Observações

O bloqueio pode ser aplicado após autenticação, ao carregar o perfil.

<a id="ef-rn004-campos-obrigatorios-do-canvas"></a>
### RN004 - Campos obrigatórios do Canvas

#### Descrição

Os blocos obrigatórios são: Problema, Indicadores de sucesso, Como resolver sem IA, Como resolver com IA e Para quem/personas. Dados/fontes e Ferramentas são opcionais.

#### Aplicável em

- RF003

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Todos os obrigatórios preenchidos | Envio permitido |
| Inválido | Problema vazio | Envio bloqueado |

#### Observações

Nome, e-mail e departamentos também são obrigatórios.

<a id="ef-rn005-status-da-ideia"></a>
### RN005 - Status da ideia

#### Descrição

Ideias devem seguir os status controlados: `rascunho`, `enviada`, `resumo_gerado`, `aprovada_autor`, `em_triagem`, `virou_projeto`, `backlog`, `arquivada`.

#### Aplicável em

- RF003, RF005, RF007, RF008, RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Autor aprova resumo | Status `aprovada_autor` |
| Válido | Triagem decide arquivar | Status `arquivada` |

#### Observações

Transições inválidas devem ser bloqueadas na camada de aplicação.

<a id="ef-rn006-formulario-publico-sem-insert-direto-no-banco"></a>
### RN006 - Formulário público sem insert direto no banco

#### Descrição

O front-end público não deve inserir diretamente em `ideas`; toda submissão deve passar por `submit-idea`.

#### Aplicável em

- RF003

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Submit via Edge Function | Registro criado |
| Inválido | Insert anônimo direto | Bloqueado por RLS |

#### Observações

A Edge Function deve aplicar rate limit/honeypot/captcha leve.

<a id="ef-rn007-protecao-anti-spam"></a>
### RN007 - Proteção anti-spam

#### Descrição

Submissões públicas devem ter proteção mínima contra abuso.

#### Aplicável em

- RF003

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Muitas submissões do mesmo IP em curto período | Bloqueio temporário |
| Inválido | Honeypot preenchido | Envio rejeitado |

#### Observações

A mensagem ao usuário deve ser genérica.

<a id="ef-rn008-ia-como-apoio-nao-autoridade-final"></a>
### RN008 - IA como apoio, não autoridade final

#### Descrição

Sugestões, resumos, impactos, esforços e insights gerados por IA são apoio ao processo e podem ser revisados pela Inovação.

#### Aplicável em

- RF004, RF005, RF012

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | IA sugere impacto 4 | Inovação pode alterar para 3 |

#### Observações

O sistema deve identificar claramente conteúdos gerados por IA.

<a id="ef-rn009-respostas-de-ia-estruturadas"></a>
### RN009 - Respostas de IA estruturadas

#### Descrição

Edge Functions de IA devem solicitar e validar JSON estruturado antes de gravar campos controlados.

#### Aplicável em

- RF004, RF005, RF012

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | JSON com campos esperados | Gravação permitida |
| Inválido | Texto livre em vez de JSON | Gravação bloqueada/parcial |

#### Observações

Campos textuais podem ser tratados separadamente quando seguro.

<a id="ef-rn010-escala-de-impacto-e-esforco"></a>
### RN010 - Escala de impacto e esforço

#### Descrição

Impacto e esforço devem usar escala inteira de 1 a 5.

#### Aplicável em

- RF005, RF007, RF008, RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Impacto 5, esforço 2 | Aceito |
| Inválido | Impacto 7 | Bloqueado |

#### Observações

A matriz atual em mock usa escala 0–10 e deve ser ajustada.

<a id="ef-rn011-pontuacao-nao-visivel-ao-autor"></a>
### RN011 - Pontuação não visível ao autor

#### Descrição

Impacto e esforço, sejam sugeridos por IA ou confirmados na triagem, não devem aparecer no fluxo público do autor.

#### Aplicável em

- RF005

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Tela de aprovação mostra impacto/esforço | Deve ser corrigido |

#### Observações

As notas são internas ao processo de Inovação.

<a id="ef-rn012-asana-como-fonte-operacional"></a>
### RN012 - Asana como fonte operacional

#### Descrição

O Asana deve armazenar e operar tarefas, sprints, responsáveis e status operacionais. O portal deve exibir somente um espelho de leitura.

#### Aplicável em

- RF006, RF013, RF016

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Tarefa alterada no Asana | Portal atualiza cache |
| Inválido | Usuário edita tarefa pelo portal | Não permitido |

#### Observações

Comentários operacionais permanecem no Asana.

<a id="ef-rn013-dashboard-baseado-em-cache"></a>
### RN013 - Dashboard baseado em cache

#### Descrição

Dashboard e detalhe do projeto devem ler dados do Asana somente a partir de `asana_sync`.

#### Aplicável em

- RF006, RF013, RF016

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Acessar Dashboard | Consulta Supabase |
| Inválido | Front chama API Asana | Não permitido |

#### Observações

Reduz latência, risco de rate limit e exposição de token.

<a id="ef-rn014-elegibilidade-da-matriz"></a>
### RN014 - Elegibilidade da matriz

#### Descrição

A matriz deve exibir apenas ideias com status `aprovada_autor`, `em_triagem` ou `backlog`.

#### Aplicável em

- RF007

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Ideia em `backlog` | Aparece na matriz |
| Inválido | Ideia em `virou_projeto` | Não aparece |

#### Observações

Ideias arquivadas e convertidas saem da matriz.

<a id="ef-rn015-notas-finais-prevalecem-sobre-notas-ia"></a>
### RN015 - Notas finais prevalecem sobre notas IA

#### Descrição

Quando `impacto_final` e `esforco_final` existirem, elas devem prevalecer sobre `impacto_ia` e `esforco_ia`.

#### Aplicável em

- RF007, RF008, RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | IA=4, final=3 | Matriz usa 3 |

#### Observações

A UI deve diferenciar nota rascunho de nota confirmada.

<a id="ef-rn016-conversao-exige-decisao-explicita"></a>
### RN016 - Conversão exige decisão explícita

#### Descrição

Somente ideias com decisão “Vira Projeto” na triagem podem ser convertidas em projeto.

#### Aplicável em

- RF008, RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Ideia sem triagem tenta converter | Bloqueado |

#### Observações

A exceção manual deve ser registrada como nova regra se necessária.

<a id="ef-rn017-conversao-idempotente"></a>
### RN017 - Conversão idempotente

#### Descrição

Uma ideia não pode gerar mais de um projeto no portal ou no Asana.

#### Aplicável em

- RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Reenvio por duplo clique | Retorna projeto já existente ou bloqueia duplicidade |

#### Observações

Deve haver constraint e validação transacional.

<a id="ef-rn018-sem-custom-fields-de-projeto-no-asana"></a>
### RN018 - Sem custom fields de projeto no Asana

#### Descrição

Impacto, esforço, área de origem e área impactada devem ficar no Supabase. O Asana não terá custom fields de projeto para esses dados.

#### Aplicável em

- RF009, RF013, RF016

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Projeto criado no Asana | Dados estratégicos permanecem no portal |

#### Observações

Custom fields de tarefa do template são mantidos no Asana.

<a id="ef-rn019-descricao-inicial-do-projeto-asana"></a>
### RN019 - Descrição inicial do projeto Asana

#### Descrição

Ao criar projeto no Asana, a descrição deve conter resumo IA e blocos principais do Canvas em `html_notes` permitido pela API.

#### Aplicável em

- RF009

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Ideia convertida | Projeto Asana tem descrição preenchida |

#### Observações

Sanitizar HTML antes de enviar.

<a id="ef-rn020-fases-fixas-do-projeto"></a>
### RN020 - Fases fixas do projeto

#### Descrição

Todo projeto terá cinco fases fixas: Ideação, Validação, MVP, Implantação e Produção.

#### Aplicável em

- RF010, RF011

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Projeto criado | Cinco fases semeadas |

#### Observações

Adicionar/remover fases é mudança de escopo.

<a id="ef-rn021-progresso-por-fases-concluidas"></a>
### RN021 - Progresso por fases concluídas

#### Descrição

`progress_pct` deve ser calculado por fases concluídas sobre o total de cinco fases.

#### Aplicável em

- RF010, RF011

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | 2 fases concluídas | Progresso 40% |

#### Observações

O cálculo é feito por trigger no banco.

<a id="ef-rn022-encerramento-de-projeto"></a>
### RN022 - Encerramento de projeto

#### Descrição

Projeto pode ser encerrado em qualquer fase, registrando `encerrado_em` e `encerrado_na_fase`.

#### Aplicável em

- RF010, RF011

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Encerrar na fase MVP | Projeto fica `encerrado` e guarda fase |

#### Observações

Projeto encerrado não deve permitir alterações operacionais no portal.

<a id="ef-rn023-insight-de-ia-exige-resultado"></a>
### RN023 - Insight de IA exige resultado

#### Descrição

Insight de IA sobre métrica só deve ser gerado quando houver resultado preenchido.

#### Aplicável em

- RF012

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Resultado vazio | Bloquear geração |

#### Observações

Meta qualitativa pode ser usada junto com resultado textual.

<a id="ef-rn024-sincronizacao-asana-resiliente"></a>
### RN024 - Sincronização Asana resiliente

#### Descrição

Webhook deve atualizar dados próximos do tempo real e cron diário deve reconciliar perdas ou falhas.

#### Aplicável em

- RF013, RF016

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Evento perdido | Cron corrige cache |

#### Observações

Não depender exclusivamente de webhook.

<a id="ef-rn025-comentarios-de-governanca-separados-da-operacao"></a>
### RN025 - Comentários de governança separados da operação

#### Descrição

Comentários no portal devem registrar decisões, pareceres e governança. Comentários de tarefas permanecem no Asana.

#### Aplicável em

- RF014

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Comentário sobre decisão executiva | Salvo no portal |

#### Observações

Evita duplicidade com gestão operacional.

<a id="ef-rn026-departamentos-inativaveis"></a>
### RN026 - Departamentos inativáveis

#### Descrição

Departamentos devem ser inativados em vez de excluídos quando já houver relacionamento histórico.

#### Aplicável em

- RF015

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Departamento em uso | Inativação permitida, exclusão evitada |

#### Observações

Departamentos inativos não aparecem em novos formulários.

<a id="ef-rn027-perfil-nao-pode-autoelevar-papel"></a>
### RN027 - Perfil não pode autoelevar papel

#### Descrição

Usuário não deve conseguir alterar o próprio `role` para ganhar permissões.

#### Aplicável em

- RF015

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Usuário edita próprio role | Bloqueado |

#### Observações

Requer ajuste/revisão de policy ou uso de função controlada.

<a id="ef-rn028-secrets-somente-no-backend"></a>
### RN028 - Secrets somente no backend

#### Descrição

Tokens Asana, chaves de IA e service role devem existir apenas como secrets de backend/Edge Functions.

#### Aplicável em

- RF003, RF004, RF005, RF009, RF012, RF016

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Token no código front-end | Correção obrigatória |

#### Observações

Também não registrar secrets em logs.

<a id="ef-rn029-logs-de-auditoria-nao-sensiveis"></a>
### RN029 - Logs de auditoria não sensíveis

#### Descrição

Logs devem conter ação, entidade, ator e detalhes úteis, mas nunca senhas, tokens ou chaves.

#### Aplicável em

- RF017

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Válido | Log de conversão | Sem token Asana |

#### Observações

Dados pessoais devem ser minimizados.

<a id="ef-rn030-mensagens-claras-e-nao-tecnicas"></a>
### RN030 - Mensagens claras e não técnicas

#### Descrição

Mensagens ao usuário devem ser claras e não expor stack trace, payloads internos ou detalhes de credenciais.

#### Aplicável em

- Todos os RFs

#### Exemplos

| Caso | Entrada / condição | Resultado esperado |
|---|---|---|
| Inválido | Erro exibe stack trace | Deve ser corrigido |

#### Observações

Detalhes técnicos ficam nos logs.

---

<a id="ef-6-fluxos-de-usuario"></a>
## 6. Fluxos de usuário

<a id="ef-fluxo-1-envio-de-ideia-pelo-canvas"></a>
### Fluxo 1 - Envio de ideia pelo Canvas

#### Objetivo do fluxo

Permitir que colaborador submeta uma ideia estruturada para avaliação da Inovação.

#### Ator

Colaborador.

#### Passos

1. Usuário acessa `/canvas`.
2. Sistema exibe formulário público.
3. Usuário preenche dados pessoais, áreas e blocos obrigatórios.
4. Usuário pode solicitar sugestões de IA por bloco.
5. Usuário envia a ideia.
6. Sistema grava a ideia e gera resumo.
7. Usuário aprova/complementa o resumo.
8. Sistema confirma submissão para triagem.

#### Resultado esperado

Ideia registrada com status `aprovada_autor` e pronta para matriz/triagem.

#### Pontos de atenção

- Não exibir impacto/esforço ao autor.
- Proteger contra spam.
- Permitir edição manual mesmo se IA falhar.

<a id="ef-fluxo-2-triagem-e-priorizacao"></a>
### Fluxo 2 - Triagem e priorização

#### Objetivo do fluxo

Permitir que a Inovação avalie ideias e decida destino.

#### Ator

Inovação.

#### Passos

1. Usuário acessa `/triagem`.
2. Sistema lista ideias elegíveis.
3. Usuário revisa resumo e Canvas.
4. Usuário ajusta impacto e esforço finais.
5. Usuário decide entre Vira Projeto, Backlog ou Arquivar.
6. Sistema atualiza status e registra logs.

#### Resultado esperado

Ideia classificada e direcionada corretamente.

#### Pontos de atenção

- Notas finais prevalecem sobre IA.
- Conversão deve ser idempotente.
- Backlog permanece na matriz.

<a id="ef-fluxo-3-conversao-para-projeto-asana"></a>
### Fluxo 3 - Conversão para projeto Asana

#### Objetivo do fluxo

Transformar uma ideia aprovada em projeto gerenciável operacionalmente no Asana e governável no portal.

#### Ator

Inovação / Sistema.

#### Passos

1. Usuário confirma “Vira Projeto”.
2. Sistema cria projeto no portal.
3. Edge Function instancia template no Asana.
4. Edge Function adiciona projeto ao portfólio.
5. Edge Function preenche descrição e owner.
6. Sistema grava vínculo Asana no Supabase.
7. Sistema cria webhook e inicia sincronização.

#### Resultado esperado

Projeto disponível no portal e no Asana, com link e dados de sincronização.

#### Pontos de atenção

- Tratar falhas parciais.
- Não criar duplicidade.
- Manter tokens fora do front-end.

<a id="ef-fluxo-4-acompanhamento-executivo"></a>
### Fluxo 4 - Acompanhamento executivo

#### Objetivo do fluxo

Permitir que diretoria e Inovação acompanhem portfólio e projetos.

#### Ator

Diretoria e Inovação.

#### Passos

1. Usuário faz login.
2. Acessa Dashboard.
3. Filtra projetos por status/área.
4. Abre detalhe de projeto.
5. Consulta resumo, progresso, fases, métricas, Asana e comentários.

#### Resultado esperado

Usuário tem visão única e atualizada do portfólio.

#### Pontos de atenção

- Diretoria em modo somente leitura.
- Dashboard lê cache do Asana, não API ao vivo.

<a id="ef-fluxo-5-gestao-de-governanca-do-projeto"></a>
### Fluxo 5 - Gestão de governança do projeto

#### Objetivo do fluxo

Permitir que Inovação mantenha informações executivas do projeto atualizadas.

#### Ator

Inovação.

#### Passos

1. Usuário acessa detalhe do projeto.
2. Atualiza fases e checklist.
3. Preenche métricas e resultados.
4. Gera insights de IA.
5. Adiciona comentários de governança.
6. Encerra projeto quando aplicável.

#### Resultado esperado

Projeto com governança atualizada no portal.

#### Pontos de atenção

- Checklist do portal não é tarefa Asana.
- Projeto encerrado bloqueia alterações relevantes.

---

<a id="ef-7-mapa-de-navegacao"></a>
## 7. Mapa de navegação

```text
/canvas                       Form Canvas público, sem login
/login                        Login do portal interno
/                             Dashboard executivo
├── /projetos                 Lista de projetos
│   └── /projetos/:id         Detalhe do projeto
├── /matriz                   Matriz Impacto × Esforço
├── /triagem                  Triagem mensal, somente inovação
├── /ideias                   Backlog/lista de ideias, se mantido como módulo separado
└── /admin                    Gestão de departamentos e usuários, somente inovação
```

---

<a id="ef-8-telas-wireframes-e-comportamento-visual"></a>
## 8. Telas, wireframes e comportamento visual

<a id="ef-tela-1-canvas-publico"></a>
### Tela 1 - Canvas público

#### Objetivo da tela

Coletar ideias de colaboradores de forma estruturada.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Nome do solicitante | Texto | Sim | Não vazio |
| E-mail | E-mail | Sim | Formato válido |
| Área de origem | Select | Sim | Departamento ativo |
| Área impactada | Select | Sim | Departamento ativo |
| Problema | Texto longo | Sim | Bloco obrigatório |
| Indicadores de sucesso | Texto longo | Sim | Bloco obrigatório |
| Como resolver sem IA | Texto longo | Sim | Bloco obrigatório |
| Como resolver com IA | Texto longo | Sim | Bloco obrigatório |
| Para quem/personas | Texto longo | Sim | Bloco obrigatório |
| Dados e fontes | Texto longo | Não | Opcional |
| Ferramentas | Texto longo | Não | Opcional |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Sugestão IA | Chama `ai-assist-block` e exibe sugestão editável |
| Enviar ideia | Valida, aplica anti-spam e chama `submit-idea` |
| Aprovar resumo | Marca resumo aprovado e status `aprovada_autor` |
| Editar/comentar resumo | Grava comentário ou ajuste antes da aprovação |

#### Estados da tela

- Estado inicial: formulário vazio com orientações por bloco.
- Estado de carregamento: botões desabilitados e feedback visual.
- Estado vazio: não aplicável.
- Estado de erro: mensagens por campo ou erro geral.
- Estado de sucesso: tela de confirmação.

#### Protótipo / referência visual

**Link:** A definir / Lovable.  
**Observações:** Tema escuro Rennova com acento dourado.

<a id="ef-tela-2-login"></a>
### Tela 2 - Login

#### Objetivo da tela

Autenticar usuários internos.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| E-mail | E-mail | Sim | Formato válido |
| Senha | Senha | Sim | Não vazio |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Entrar | Autentica e redireciona |
| Sair | Encerra sessão em áreas internas |

#### Estados da tela

- Estado inicial: formulário de login.
- Estado de carregamento: botão em loading.
- Estado de erro: credenciais inválidas ou usuário inativo.
- Estado de sucesso: redireciona para Dashboard.

#### Protótipo / referência visual

**Link:** A definir / Lovable.

<a id="ef-tela-3-dashboard"></a>
### Tela 3 - Dashboard

#### Objetivo da tela

Fornecer visão executiva do portfólio.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Projetos ativos | KPI | Sim | Calculado de `projects` |
| Progresso médio | KPI | Sim | Média de `progress_pct` |
| Tarefas abertas | KPI | Sim | Soma de `asana_sync.num_incomplete` |
| Ideias em triagem | KPI | Sim | Count por status |
| Lista de projetos | Lista/cards | Sim | Filtro por status/área |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Filtrar por área/status | Atualiza lista |
| Abrir projeto | Navega para `/projetos/:id` |

#### Estados da tela

- Estado inicial: KPIs e lista carregados.
- Estado de carregamento: skeleton/loading.
- Estado vazio: sem projetos.
- Estado de erro: erro de consulta Supabase.
- Estado de sucesso: dados renderizados.

#### Protótipo / referência visual

**Link:** Protótipo atual Lovable/GitHub.  
**Observações:** Tela já existe com dados mockados.

<a id="ef-tela-4-matriz-impacto-x-esforco"></a>
### Tela 4 - Matriz Impacto × Esforço

#### Objetivo da tela

Priorizar ideias visualmente.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Ideia | Ponto/lista | Sim | Ideias elegíveis |
| Impacto | Número 1–5 | Sim | IA ou final |
| Esforço | Número 1–5 | Sim | IA ou final |
| Status | Badge | Sim | Status controlado |
| Origem/impactada | Texto | Sim | Departamentos |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Clicar em ponto | Abre detalhe da ideia |
| Filtrar | Atualiza matriz/lista, se implementado |

#### Estados da tela

- Estado inicial: matriz com pontos.
- Estado de carregamento: loading.
- Estado vazio: sem ideias elegíveis.
- Estado de erro: erro ao carregar ideias.

#### Protótipo / referência visual

**Link:** Tela Ideias atual contém matriz mockada.  
**Observações:** Ajustar escala para 1–5.

<a id="ef-tela-5-triagem"></a>
### Tela 5 - Triagem

#### Objetivo da tela

Permitir decisão mensal sobre ideias.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Ideia | Texto | Sim | Nome/resumo |
| Resumo IA | Texto | Sim | Se disponível |
| Impacto final | Número/select 1–5 | Sim para decisão | Interno |
| Esforço final | Número/select 1–5 | Sim para decisão | Interno |
| Decisão | Ação | Sim | Vira Projeto, Backlog, Arquivar |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Salvar notas | Atualiza impacto/esforço final |
| Vira Projeto | Chama `asana-create-project` |
| Backlog | Status `backlog` |
| Arquivar | Status `arquivada` |

#### Estados da tela

- Estado inicial: lista do mês.
- Estado vazio: nenhuma ideia elegível.
- Estado de erro: falha ao salvar/conveter.
- Estado de sucesso: decisão registrada.

#### Protótipo / referência visual

**Link:** A definir / Lovable.

<a id="ef-tela-6-detalhe-do-projeto"></a>
### Tela 6 - Detalhe do projeto

#### Objetivo da tela

Concentrar governança executiva do projeto.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Nome | Texto | Sim | Projeto |
| Status | Badge | Sim | Ativo, pausado, encerrado |
| Progresso | Barra | Sim | `progress_pct` |
| Área/owner/datas | Metadados | Sim | Quando disponíveis |
| Resumo IA | Texto | Não | Destaque visual |
| Objetivo/problema/descrição | Texto | Não | Dados do projeto |
| Fases | Stepper | Sim | 5 fases fixas |
| Checklist | Lista | Não | Por fase |
| Métricas | Lista/form | Não | Meta e resultado |
| Asana | Bloco leitura | Não | `asana_sync` |
| Comentários | Timeline/lista | Não | Governança |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Marcar checklist | Atualiza item |
| Concluir fase | Atualiza fase e progresso |
| Registrar resultado | Salva métrica |
| Gerar insight | Chama IA e grava insight |
| Adicionar comentário | Salva governança |
| Encerrar projeto | Status `encerrado` |
| Abrir no Asana | Abre permalink |

#### Estados da tela

- Estado inicial: dados do projeto.
- Estado de carregamento: skeleton/loading.
- Estado vazio: projeto não encontrado.
- Estado de erro: erro de consulta/salvamento.
- Estado de sucesso: feedback após ação.

#### Protótipo / referência visual

**Link:** Protótipo atual Lovable/GitHub.  
**Observações:** Tela já existe com dados mockados.

<a id="ef-tela-7-admin"></a>
### Tela 7 - Admin

#### Objetivo da tela

Gerenciar cadastros básicos e permissões.

#### Campos exibidos

| Campo | Tipo | Obrigatório? | Validação / observação |
|---|---|---:|---|
| Departamentos | Lista/form | Sim | Nome único, ativo/inativo |
| Usuários | Lista/form | Sim | Nome, e-mail, role, ativo |

#### Ações disponíveis

| Ação | Comportamento esperado |
|---|---|
| Criar/editar departamento | Salva cadastro |
| Inativar departamento | Remove de novas seleções |
| Alterar papel de usuário | Atualiza `profiles.role` |
| Ativar/inativar usuário | Atualiza acesso |

#### Estados da tela

- Estado inicial: listas carregadas.
- Estado vazio: sem registros.
- Estado de erro: falha ao salvar.
- Estado de sucesso: toast/feedback.

#### Protótipo / referência visual

**Link:** A definir / Lovable.

---

<a id="ef-9-requisitos-nao-funcionais"></a>
## 9. Requisitos não funcionais

<a id="ef-9-1-seguranca"></a>
### 9.1 Segurança

- [x] O sistema deve exigir autenticação para áreas restritas.
- [x] O sistema deve controlar acesso por perfil/permissão.
- [x] Dados sensíveis não devem ser expostos no frontend, logs ou mensagens de erro.
- [x] Tokens de Asana, IA e Supabase service role devem ficar apenas em secrets.
- [x] RLS deve estar habilitado nas tabelas do Supabase.
- [x] Inputs públicos devem ser validados no backend.
- [x] Formulário público deve ter proteção anti-spam.

<a id="ef-9-2-performance"></a>
### 9.2 Performance

- [x] Principais telas internas devem carregar em até 3 segundos em condições normais.
- [x] Dashboard deve ler dados cacheados do Supabase, sem chamada ao Asana em tempo real.
- [x] Listagens devem suportar pelo menos 500 ideias e 100 projetos sem degradação relevante na primeira versão.
- [x] Operações de IA e Asana devem exibir loading e não travar a UI.

<a id="ef-9-3-usabilidade"></a>
### 9.3 Usabilidade

- [x] Campos obrigatórios devem ser identificados.
- [x] Mensagens de erro devem ser claras para o usuário.
- [x] O sistema deve fornecer feedback visual após ações importantes.
- [x] Conteúdos gerados por IA devem ser identificados.
- [x] Badges, barras de progresso e stepper devem seguir padrão visual Rennova.

<a id="ef-9-4-compatibilidade"></a>
### 9.4 Compatibilidade

- [x] Navegadores suportados: Chrome, Edge e Safari em versões atuais.
- [x] Dispositivos suportados: desktop e notebook; responsividade básica para tablet.
- [x] Resolução mínima recomendada: 1366×768.
- [x] Mobile não é foco da primeira versão, mas não deve quebrar fluxos básicos.

<a id="ef-9-5-logs-e-auditoria-funcional"></a>
### 9.5 Logs e auditoria funcional

- [x] Erros críticos devem ser registrados.
- [x] Ações sensíveis devem ser rastreadas.
- [x] Conversões, alterações de status e falhas de integração devem gerar log.
- [x] Logs não devem conter secrets ou senhas.

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

| ID | Dúvida / pendência | Responsável | Decisão | Status |
|---|---|---|---|---|
| P001 | Definir se o autor poderá retomar aprovação do resumo por link/token após sair da tela | Inovação / Técnico | Recomendado token temporário ou aprovação na mesma sessão | Aberta |
| P002 | Definir se haverá notificação por e-mail ao autor após submissão | Inovação | Fora do MVP salvo decisão contrária | Aberta |
| P003 | Definir lista final de departamentos | Inovação | Usar seed inicial e ajustar em Admin | Aberta |
| P004 | Definir se `/ideias` será mantida separada de `/matriz` e `/triagem` | Produto / Técnico | Manter se agregar valor de backlog/listagem | Aberta |
| P005 | Definir política de edição de projeto após encerramento | Inovação | Recomendado bloquear alterações, exceto comentários administrativos | Aberta |
| P006 | Definir visual final da tela de triagem | Produto / Lovable | Criar no Lovable com base nesta especificação | Aberta |

---

<a id="ef-12-controle-de-mudancas-de-escopo"></a>
## 12. Controle de mudanças de escopo

| Data | Solicitação | Impacto | Aprovado por | Status |
|---|---|---|---|---|
| 2026-07-07 | Criação da especificação inicial | Define escopo funcional base | A definir | Em revisão |

---

<a id="ef-13-aprovacao-funcional"></a>
## 13. Aprovação funcional

| Papel | Nome | Data | Aprovação |
|---|---|---|---|
| Solicitante / Dono do produto | A definir |  |  |
| Desenvolvimento | Phablo Tavares | 2026-07-07 | Em revisão |
