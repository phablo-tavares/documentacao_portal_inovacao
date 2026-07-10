# Especificação Funcional — Portal de Gestão da Inovação Rennova

> Fonte funcional para orientar construção, aceite e evolução do **Rennova Spark Hub**.  
> Esta versão preserva o padrão completo dos requisitos funcionais e incorpora o **Brainstorm Estratégico com IA baseado em SCAMPER**, a matriz Impacto × Esforço em escala 1–10 e a criação de task inicial no Asana.

---

<a id="sumario"></a>
## Sumário

- [Especificação Funcional — Portal de Gestão da Inovação Rennova](#especificação-funcional--portal-de-gestão-da-inovação-rennova)
  - [Sumário](#sumário)
  - [1. Identificação do projeto](#1-identificação-do-projeto)
  - [2. Visão geral](#2-visão-geral)
    - [2.1 Contexto](#21-contexto)
    - [2.2 Objetivo](#22-objetivo)
    - [2.3 Público-alvo / usuários](#23-público-alvo--usuários)
  - [3. Escopo](#3-escopo)
    - [3.1 Escopo incluído](#31-escopo-incluído)
    - [3.2 Fora de escopo](#32-fora-de-escopo)
    - [3.3 Premissas](#33-premissas)
    - [3.4 Restrições](#34-restrições)
  - [4. Requisitos funcionais](#4-requisitos-funcionais)
    - [RF001 - Autenticação no portal interno](#rf001---autenticação-no-portal-interno)
    - [RF002 - Controle de acesso por perfil](#rf002---controle-de-acesso-por-perfil)
    - [RF003 - Submissão de ideia pelo Canvas público](#rf003---submissão-de-ideia-pelo-canvas-público)
    - [RF004 - Sugestão de IA por bloco do Canvas](#rf004---sugestão-de-ia-por-bloco-do-canvas)
    - [RF005 - Resumo de IA e aprovação pelo autor](#rf005---resumo-de-ia-e-aprovação-pelo-autor)
    - [RF006 - Dashboard executivo](#rf006---dashboard-executivo)
    - [RF007 - Matriz Impacto × Esforço](#rf007---matriz-impacto--esforço)
    - [RF008 - Triagem mensal de ideias](#rf008---triagem-mensal-de-ideias)
    - [RF009 - Conversão de ideia em projeto](#rf009---conversão-de-ideia-em-projeto)
    - [RF010 - Detalhe e governança do projeto](#rf010---detalhe-e-governança-do-projeto)
    - [RF011 - Gestão de fases e checklist executivo](#rf011---gestão-de-fases-e-checklist-executivo)
    - [RF012 - Métricas, resultados e insight de IA](#rf012---métricas-resultados-e-insight-de-ia)
    - [RF013 - Bloco Asana no projeto](#rf013---bloco-asana-no-projeto)
    - [RF014 - Comentários de governança](#rf014---comentários-de-governança)
    - [RF015 - Administração de departamentos e usuários](#rf015---administração-de-departamentos-e-usuários)
    - [RF016 - Sincronização Asana → Portal](#rf016---sincronização-asana--portal)
    - [RF017 - Auditoria de ações relevantes](#rf017---auditoria-de-ações-relevantes)
    - [RF018 - Brainstorm Estratégico com IA](#rf018---brainstorm-estratégico-com-ia)
    - [RF019 - Exibição do brainstorm no detalhe da ideia](#rf019---exibição-do-brainstorm-no-detalhe-da-ideia)
    - [RF020 - Cópia do brainstorm para projeto convertido](#rf020---cópia-do-brainstorm-para-projeto-convertido)
    - [RF021 - Task inicial no Asana com brainstorm](#rf021---task-inicial-no-asana-com-brainstorm)
  - [5. Regras de negócio](#5-regras-de-negócio)
    - [5.1 Framework SCAMPER](#51-framework-scamper)
    - [5.2 Estrutura obrigatória de cada solução](#52-estrutura-obrigatória-de-cada-solução)
    - [5.3 Métrica de Impacto](#53-métrica-de-impacto)
    - [5.4 Métrica de Esforço](#54-métrica-de-esforço)
    - [5.5 Regra da matriz Impacto × Esforço](#55-regra-da-matriz-impacto--esforço)
    - [5.6 Recomendação da IA](#56-recomendação-da-ia)
  - [6. Fluxos de usuário](#6-fluxos-de-usuário)
    - [6.1 Submissão pública de ideia](#61-submissão-pública-de-ideia)
    - [6.2 Geração do Brainstorm Estratégico IA](#62-geração-do-brainstorm-estratégico-ia)
    - [6.3 Triagem de ideia](#63-triagem-de-ideia)
    - [6.4 Conversão em projeto com Asana](#64-conversão-em-projeto-com-asana)
    - [6.5 Sincronização Asana → Portal](#65-sincronização-asana--portal)
  - [7. Mapa de navegação](#7-mapa-de-navegação)
  - [8. Telas e comportamento visual](#8-telas-e-comportamento-visual)
    - [Tela 1 - Canvas público](#tela-1---canvas-público)
    - [Tela 2 - Login](#tela-2---login)
    - [Tela 3 - Dashboard](#tela-3---dashboard)
    - [Tela 4 - Backlog, detalhe da ideia e matriz Impacto × Esforço](#tela-4---backlog-detalhe-da-ideia-e-matriz-impacto--esforço)
    - [Tela 5 - Triagem](#tela-5---triagem)
    - [Tela 6 - Detalhe do projeto](#tela-6---detalhe-do-projeto)
    - [Tela 7 - Admin](#tela-7---admin)
  - [9. Requisitos não funcionais](#9-requisitos-não-funcionais)
  - [10. Mensagens do sistema](#10-mensagens-do-sistema)
  - [11. Critérios de aceite consolidados](#11-critérios-de-aceite-consolidados)
  - [12. Pendências e decisões funcionais](#12-pendências-e-decisões-funcionais)
  - [13. Aprovação funcional](#13-aprovação-funcional)

---

<a id="ef-1-identificacao-do-projeto"></a>
## 1. Identificação do projeto

| Campo | Valor |
|---|---|
| Nome do projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável pelo documento | Phablo Tavares |
| Área/Time | Inovação / Desenvolvimento de Agentes e Soluções de IA |
| Data | 2026-07-08 |
| Versão | 0.5 |
| Alteração desta versão | Restauração do padrão completo dos RFs e incorporação controlada do Brainstorm Estratégico IA |

---

<a id="ef-2-visao-geral"></a>
## 2. Visão geral

<a id="ef-2-1-contexto"></a>
### 2.1 Contexto

A área de Inovação da Rennova recebe ideias de diferentes áreas, avalia potencial, prioriza iniciativas e acompanha projetos aprovados. Parte desse processo hoje fica dispersa entre conversas, documentos, planilhas e ferramentas operacionais. O portal deve centralizar entrada de ideias, triagem, priorização, conversão em projetos e acompanhamento executivo.

Já existe um protótipo visual no Lovable/GitHub, com Dashboard, Projetos, Detalhe de Projeto e Ideias usando dados mockados. A entrega alvo deve transformar o protótipo em produto funcional com Supabase, autenticação, banco real, IA e integração com Asana.

A nova demanda da gerência adiciona a geração de um **Brainstorm Estratégico com IA** no cadastro da ideia, usando SCAMPER como framework de inovação. Esse brainstorm deve apoiar a triagem e acompanhar a ideia quando ela for convertida em projeto.

<a id="ef-2-2-objetivo"></a>
### 2.2 Objetivo

Construir um portal interno para centralizar a gestão da inovação na Rennova, permitindo que colaboradores submetam ideias, a IA apoie a estruturação e análise inicial, a Inovação qualifique e priorize iniciativas, a Diretoria acompanhe o portfólio e projetos aprovados sejam integrados ao Asana para execução operacional.

<a id="ef-2-3-publico-alvo-usuarios"></a>
### 2.3 Público-alvo / usuários

| Ator / Perfil | Responsabilidade | Principais ações |
|---|---|---|
| Colaborador / Autor da ideia | Submeter ideia pelo Canvas público | Preencher Canvas, solicitar sugestões de IA, revisar resumo e aprovar submissão |
| Inovação | Gerir funil e governança da inovação | Triar ideias, revisar impacto/esforço, consultar brainstorm, converter ideias, gerir projetos, fases, métricas, comentários e cadastros |
| Diretoria | Acompanhar portfólio em visão executiva | Consultar dashboard, matriz e detalhes de ideias/projetos sem editar dados |
| Administrador funcional | Gerir cadastros básicos | Gerenciar departamentos e perfis de usuários |
| Sistema / Integrações | Executar automações | Gerar sugestões/resumos/brainstorms/insights, criar projetos no Asana, criar task inicial, sincronizar dados e registrar logs |

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
- [ ] Brainstorm Estratégico com IA baseado em SCAMPER ao cadastrar ideia.
- [ ] Geração de 3 soluções estratégicas por ideia.
- [ ] Recomendação de uma solução pela IA, com justificativa.
- [ ] Métricas claras de impacto e esforço em escala 1–10.
- [ ] Matriz Impacto × Esforço para ideias elegíveis.
- [ ] Login com Supabase Auth por e-mail e senha.
- [ ] Controle de acesso por perfis `diretoria` e `inovacao`.
- [ ] Dashboard executivo com indicadores do portfólio e dados cacheados do Asana.
- [ ] Triagem mensal de ideias pela Inovação.
- [ ] Conversão de ideia em projeto no portal e no Asana.
- [ ] Criação de task inicial no Asana com o Brainstorm Estratégico IA.
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
- Edição colaborativa avançada do brainstorm.
- Versionamento completo de múltiplas gerações de brainstorm.
- Treinamento de modelo próprio de IA.
- Cálculo financeiro detalhado de ROI por IA.

<a id="ef-3-3-premissas"></a>
### 3.3 Premissas

- Lovable continuará sendo a principal ferramenta de evolução do front-end.
- Supabase será usado para Auth, Postgres, RLS e Edge Functions.
- Asana será a fonte operacional de tarefas e sprints.
- Supabase será a fonte de verdade para ideias, triagem, governança, métricas, usuários e visão executiva.
> Quais métricas que estariam dentro do Supabase? Não seria dentro do Asana? Registrando naquela parte de atualização do projeto?
> 
> RESPOSTA: O Supabase será a fonte de verdade para métricas executivas e de impacto/resultado, como indicadores definidos na ideia, metas, resultados alcançados e insights de IA. O Asana continuará sendo a fonte operacional para tarefas, responsáveis, prazos, status das atividades e andamento da execução. O portal apenas sincroniza esses dados operacionais do Asana para exibição em leitura.
- Tokens de Asana e IA ficarão somente em secrets nas Edge Functions.
- Workspace, template, portfólio e owner padrão do Asana já foram identificados ou serão parametrizados.
- Respostas de IA serão estruturadas em JSON e validadas antes de gravação.
- O Brainstorm Estratégico deve usar SCAMPER como base de ideação.
- A task inicial do Asana será o local operacional para registrar o brainstorm completo do projeto convertido.
> Na verdade, não seria melhor a questão de criar um projeto, seguindo o padrão "INV | XXXXX". O brainstorm entra como descrição do Projeto.
> 
> RESPOSTA: Preferi colocar como task por 2 motivos: 1 - A partir do brainstorm podem ser derivadas novas tarefas, subtarefas, etc. 2 - O brainstorm não é impositivo, portanto outra solução diferente pode ser sefinida para o projeto. Sendo assim avaliei que colocar como task já finalizada faz mais sentido, mas se necessário pode mudar
- A primeira versão priorizará desktop e responsividade básica para web.

<a id="ef-3-4-restricoes"></a>
### 3.4 Restrições

- Não expor chaves, tokens ou `service_role` no front-end.
- Não chamar Asana nem provedores de IA diretamente pelo browser.
- Evitar edição manual ampla do front-end fora do Lovable.
- Proteger o formulário público contra spam.
> Isso é uma restrição ou uma premissa?
> 
> RESPOSTA: vou mover para premissa
- Não exibir impacto/esforço ao autor da ideia no fluxo público.
- Aplicar permissões no front-end e reforçar por RLS/Edge Functions.
- Não depender de chamada ao Asana em tempo real no dashboard.
> Isso significa que as informações do Asana vão pro Supabase? Serão atualizados a cada X horas/dias?
> 
> RESPOSTA: Sim. Informações como status das tarefas, responsáveis, datas de início e conclusão do Asana serão sincronizadas para o Supabase. O dashboard não consultará o Asana em tempo real para evitar rate limit e dependência direta da API do Asana para carregamento da tela. A sincronização Asana -> Supabase ocorrerá via webhook quando houver alteração dos dados no asana. 
- Não gravar resposta de IA sem validação mínima de estrutura.

---

<a id="ef-4-requisitos-funcionais"></a>
## 4. Requisitos funcionais

> Todos os RFs devem manter a estrutura padrão: **Descrição, Ator, Pré-condições, Fluxo principal, Exceções, Critérios de aceite, Regras e Observação**.

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

> `FA004`Qual seria o critério para a sessão expirar? Dias?
>
> RESPOSTA: A expiração da sessão será definida pelo Supabase Auth. O usuário permanece logado enquanto a sessão for renovada automaticamente, desde que continue ativo em profiles. Se for inativado, o acesso é bloqueado imediatamente. A duração exata será definida antes da produção.

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
| Regras | RN001, RN002, RN003. |
| Observação | Ocultar botão no front-end não substitui validação server-side. |
> Acredito que não há problema da diretoria acessar a parte de triagem.
>
> RESPOSTA: Certo, vou ajustar

<a id="ef-rf003-submissao-de-ideia-pelo-canvas-publico"></a>
### RF003 - Submissão de ideia pelo Canvas público

| Item | Especificação |
|---|---|
| Descrição | Permitir que colaborador envie ideia pela rota pública `/canvas`, sem login. |
| Ator | Colaborador. |
| Pré-condições | Rota pública disponível; departamentos ativos disponíveis; Edge Function `submit-idea` configurada. |
| Fluxo principal | 1. Acessar `/canvas`.<br>2. Preencher dados do solicitante, departamentos e blocos do Canvas.<br>3. Enviar ideia.<br>4. Sistema valida dados obrigatórios e anti-spam.<br>5. Sistema grava `ideas.status = enviada`.<br>6. Sistema inicia/chama geração de resumo por IA.<br>7. Sistema inicia/chama geração do Brainstorm Estratégico IA. |
| Exceções | Campos obrigatórios vazios: bloquear e destacar campos.<br>E-mail inválido: bloquear.<br>Rate limit/honeypot: bloquear com mensagem genérica.<br>Falha de gravação: exibir erro e permitir nova tentativa.<br>Departamentos indisponíveis: exibir alternativa ou indisponibilidade temporária.<br>Falha de IA: salvar ideia e registrar pendência/erro de IA. |
| Critérios de aceite | Colaborador sem login acessa `/canvas`; Canvas incompleto é bloqueado; submissão válida cria registro em `ideas` com status `enviada`; falha de IA não impede a ideia de ser salva. |
| Regras | RN004, RN005, RN006, RN007, RN008, RN009, RN030, RN032. |
| Observação | Escrita pública no banco deve ocorrer somente via Edge Function com `service_role`. |
> Você vai criar uma regra de poder entrar a ideia apenas com o e-mail final @innovapharma? Se sim, deixa uma liberação para @nutriex, também.
>
> RESPOSTA: Sim vai ser criado essa regra, vou ajustar o documento. 
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
| Regras | RN007, RN008, RN009, RN030, RN032. |
| Observação | Enviar ao provider somente o contexto necessário. |
> Criar uma IA com contexto que saiba sugerir o bloco de acordo com o objetivo total do Canvas. Não seja apenas uma melhoria de escrita.
>
> RESPOSTA: Perfeito, a ideia é justamente essa

<a id="ef-rf005-resumo-de-ia-e-aprovacao-pelo-autor"></a>
### RF005 - Resumo de IA e aprovação pelo autor

| Item | Especificação |
|---|---|
| Descrição | Gerar resumo consolidado da ideia e permitir aprovação/complemento pelo autor antes da triagem. |
| Ator | Autor da ideia. |
| Pré-condições | Ideia com status `enviada`; `ai-summarize-idea` configurada. |
| Fluxo principal | 1. Enviar blocos da ideia para Edge Function.<br>2. IA retorna JSON com resumo e classificação inicial.<br>3. Sistema grava `resumo_ia` e campos de apoio definidos.<br>4. Exibir resumo ao autor, sem notas de impacto/esforço.<br>5. Autor aprova ou complementa.<br>6. Gravar aprovação/comentário e seguir para triagem. |
| Exceções | IA falha: permitir submissão com resumo pendente para Inovação.<br>JSON inválido: não gravar campos controlados e registrar erro.<br>Autor edita/comenta: gravar ajuste e seguir para aprovação.<br>Autor abandona tela: manter estado definido ou aplicar fluxo de expiração posterior. |
| Critérios de aceite | Resumo válido é exibido antes da triagem; aprovação do autor é registrada; impacto/esforço nunca aparecem ao autor. |
| Regras | RN005, RN007, RN008, RN009, RN010, RN030, RN032. |
| Observação | Retomada após abandono ainda depende de definição funcional. |
> Criar um aviso caso a pessoa abandone a página antes de enviar a ideia. 
>
> RESPOSTA: Certo. Vai ter um aviso que as informações serão perdidas e se a pessoa sair perde tudo que foi preenchido. Como não é área logada, seria mais difícil manter o estado então. 

<a id="ef-rf006-dashboard-executivo"></a>
### RF006 - Dashboard executivo

| Item | Especificação |
|---|---|
| Descrição | Exibir visão executiva do portfólio de inovação. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; dados de `projects`, `ideas` e `asana_sync` disponíveis. |
| Fluxo principal | 1. Acessar `/` ou `/dashboard`.<br>2. Exibir KPIs: projetos ativos, progresso médio, tarefas abertas e ideias em triagem.<br>3. Exibir lista de projetos com área, status, progresso e última atualização.<br>4. Permitir filtro por área/status e acesso ao detalhe. |
| Exceções | Sem projetos: estado vazio.<br>Sem dados Asana: indicar indisponível/pendente conforme regra.<br>Erro de carregamento: exibir erro e opção de tentar novamente. |
| Critérios de aceite | KPIs calculados com dados do Supabase; filtros funcionam; indisponibilidade do Asana não quebra a tela nem gera chamada Asana ao vivo. |
| Regras | RN001, RN011, RN012, RN030. |
| Observação | Tela já existe em protótipo com dados mockados; substituir por consultas reais. |

<a id="ef-rf007-matriz-impacto-x-esforco"></a>
### RF007 - Matriz Impacto × Esforço

| Item | Especificação |
|---|---|
| Descrição | Exibir ideias elegíveis em matriz de priorização impacto×esforço, usando escala 1–10. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; ideias elegíveis com pontuações de impacto/esforço ou brainstorm gerado. |
| Fluxo principal | 1. Acessar `/matriz` ou área equivalente dentro de `/ideias`.<br>2. Buscar ideias elegíveis em `aprovada_autor`, `em_triagem` ou `backlog`.<br>3. Usar pontuação da solução recomendada quando a origem for IA.<br>4. Diferenciar pontuação IA e pontuação final de triagem, quando houver.<br>5. Plotar esforço no eixo X e impacto no eixo Y.<br>6. Classificar quadrante pela regra objetiva.<br>7. Permitir clique para detalhe. |
| Exceções | Ideia sem pontuação: não plotar ou listar como pendente de triagem.<br>Sem elegíveis: estado vazio.<br>Diretoria: leitura sem ações de decisão.<br>Notas fora de 1–10: bloquear salvamento. |
| Critérios de aceite | Ideias elegíveis aparecem nos quadrantes corretos; ideias convertidas/arquivadas não aparecem; diretoria não altera decisão; Inovação pode revisar pontuação final. |
| Regras | RN010, RN013, RN014, RN015, RN016, RN017, RN026, RN027. |
| Observação | A versão final deve usar escala 1–10. O protótipo/mock deve ser ajustado se estiver em outra escala. |

<a id="ef-rf008-triagem-mensal-de-ideias"></a>
### RF008 - Triagem mensal de ideias

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação realize triagem mensal, ajuste notas e registre decisão. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; ideias em `aprovada_autor`, `em_triagem` ou estado elegível. |
| Fluxo principal | 1. Acessar `/triagem` ou backlog interno.<br>2. Listar ideias elegíveis do período.<br>3. Revisar Canvas, descrição, resumo IA, brainstorm e solução recomendada.<br>4. Ajustar `impacto_final` e `esforco_final`, se necessário.<br>5. Decidir: Vira Projeto, Backlog ou Arquivar/Rejeitar.<br>6. Atualizar status, registrar sessão em `triage_sessions` e log em `activity_log`. |
| Exceções | Notas fora de 1–10: bloquear.<br>“Vira Projeto” sem notas finais: bloquear ou exigir confirmação.<br>“Vira Projeto” sem brainstorm gerado: permitir apenas com confirmação explícita da Inovação.<br>Falha ao converter no Asana: manter ideia/projeto em estado seguro e exibir erro.<br>Usuário sem permissão: bloquear. |
| Critérios de aceite | Notas válidas são salvas; Backlog permanece na matriz; Arquivar/Rejeitar sai da matriz ativa; Vira Projeto converte com sucesso quando elegível. |
| Regras | RN001, RN010, RN015, RN016, RN017, RN018, RN026, RN027, RN028, RN030, RN032. |
| Observação | Triagem pode ser simples na primeira versão, sem aprovação multinível. |

> O que seria essas notas finais? POr exemplo "Vira projeto" sem notas finais tem um bloqueio? <br> Pensar em uma visualização do que foi "Arquivado". Abrir campo de justificativa do motivo do Arquivamento - Campo em aberto para escrita - Registro da data e envolvidos na decisão.
>
> RESPOSTA: As “notas finais” são as pontuações de impacto e esforço confirmadas pela Inovação após a análise da ideia, elas podem manter ou substituir as notas sugeridas pela IA e são usadas na matriz de priorização.<br>O bloqueio de “Vira Projeto” sem notas finais foi pensado para evitar a conversão de uma ideia sem avaliação mínima registrada. Podemos manter ou remover essa regra. <br> Sobre arquivar ideias, faz sentido. vou ajustar os requisitos.

<a id="ef-rf009-conversao-de-ideia-em-projeto"></a>
### RF009 - Conversão de ideia em projeto

| Item | Especificação |
|---|---|
| Descrição | Converter uma ideia aprovada em projeto no portal e instanciar projeto correspondente no Asana. |
| Ator | Inovação. |
| Pré-condições | Ideia com decisão “Vira Projeto”; notas finais válidas; secrets Asana configurados; template e portfólio disponíveis; usuário com permissão `inovacao`. |
| Fluxo principal | 1. Confirmar “Vira Projeto”.<br>2. Validar idempotência para impedir dupla conversão.<br>3. Buscar dados completos da ideia, incluindo resumo IA e brainstorm estratégico.<br>4. Criar/preparar projeto no Supabase.<br>5. Copiar o brainstorm estratégico para o projeto interno.<br>6. Chamar `asana-create-project` ou função equivalente.<br>7. Instanciar template no Asana e aguardar job, quando aplicável.<br>8. Adicionar ao portfólio, quando aplicável.<br>9. Atualizar descrição, owner e metadados no Asana.<br>10. Criar task inicial `Brainstorm Estratégico IA` no Asana.<br>11. Gravar `asana_project_gid`, `asana_permalink` e vínculo da ideia.<br>12. Registrar log e marcar ideia como `virou_projeto`. |
| Exceções | Ideia já convertida: retornar conflito.<br>Brainstorm ausente: permitir apenas com confirmação explícita da Inovação.<br>Job Asana falha: registrar e não confirmar sucesso total.<br>Falha ao adicionar ao portfólio: registrar pendência de sync.<br>Falha parcial após criar Asana: registrar estado de recuperação manual.<br>Falha ao criar task inicial: manter projeto e registrar pendência.<br>Token inválido: erro controlado e log técnico. |
| Critérios de aceite | Ideia não convertida gera projeto no portal e no Asana; tentativa duplicada é impedida; brainstorm é copiado para o projeto; task inicial é criada no Asana; falha Asana não gera sucesso falso nem perda do projeto interno. |
| Regras | RN016, RN017, RN018, RN019, RN028, RN029, RN030, RN031, RN032. |
| Observação | Idempotência e tratamento de falhas parciais são obrigatórios. |

<a id="ef-rf010-detalhe-e-governanca-do-projeto"></a>
### RF010 - Detalhe e governança do projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir e permitir gestão das informações executivas do projeto aprovado. |
| Ator | Inovação; Diretoria em leitura. |
| Pré-condições | Usuário autenticado; projeto existente. |
| Fluxo principal | 1. Acessar `/projetos/:id`.<br>2. Exibir título, status, progresso, área, owner e datas.<br>3. Exibir resumo IA, objetivo, problema e descrição.<br>4. Exibir brainstorm estratégico herdado da ideia, quando houver.<br>5. Exibir fases, checklist, métricas, Asana e comentários.<br>6. Permitir edição apenas para `inovacao`. |
| Exceções | Projeto inexistente: “Projeto não encontrado”.<br>Usuário sem permissão: ocultar/bloquear ações editáveis.<br>Dados Asana ausentes: bloco vazio/indisponível.<br>Brainstorm ausente: exibir estado “não disponível” sem quebrar a tela. |
| Critérios de aceite | Detalhe exibe seções executivas; diretoria não edita; Inovação gere fases, checklist, métricas e comentários; brainstorm herdado é rastreável. |
| Regras | RN001, RN011, RN012, RN020, RN021, RN022, RN025, RN028. |
| Observação | Tela já existe em protótipo com dados mockados e deve ser preservada visualmente quando possível. |

> O que acha de ter um espaço para link no Projeto que iremos colocar o produto que estamos criando? Assim a Diretoria tem fácil acesso para demonstrar/acessar.
>
> RESPOSTA: Acho que faz sentido uma seção "entregas" que pode ter links e arquivos, etc. 

<a id="ef-rf011-gestao-de-fases-e-checklist-executivo"></a>
### RF011 - Gestão de fases e checklist executivo

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação acompanhe cinco fases fixas e checklist executivo por fase. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; projeto existente; fases semeadas em `project_phases`. |
| Fluxo principal | 1. Acessar detalhe do projeto.<br>2. Exibir stepper de cinco fases.<br>3. Marcar checklist da fase atual.<br>4. Marcar fase como concluída.<br>5. Atualizar status da fase.<br>6. Trigger ou rotina recalcula `progress_pct`. |
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
| Regras | RN007, RN008, RN009, RN023, RN030, RN032. |
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
| Regras | RN011, RN012, RN024, RN029. |
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
| Regras | RN001, RN025, RN030, RN032. |
| Observação | Comentários operacionais de tarefas permanecem no Asana. |

> Acho que pode ser válido o usuário Diretor também poder comentar. Por exemplo, ele está apresentando para o Geraldo ou Léo, pegou um feedback lá na hora, ele já escreve nesse campo.
>
> RESPOSTA: Ok, vou ajustar os requisitos. 

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
| Regras | RN001, RN002, RN003, RN030, RN032. |
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
| Regras | RN011, RN012, RN029, RN030, RN032. |
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
| Regras | RN030, RN032. |
| Observação | Log funcional não substitui monitoramento técnico das Edge Functions. |

<a id="ef-rf018-brainstorm-estrategico-com-ia"></a>
### RF018 - Brainstorm Estratégico com IA

| Item | Especificação |
|---|---|
| Descrição | Gerar automaticamente um Brainstorm Estratégico com IA ao cadastrar uma nova ideia no backlog. |
| Ator | Sistema / IA. |
| Pré-condições | Ideia cadastrada com dados mínimos suficientes para análise; provider de IA configurado; Edge Function de brainstorm disponível. |
| Fluxo principal | 1. Sistema salva a ideia.<br>2. Sistema aciona Edge Function de IA.<br>3. IA usa SCAMPER como base de ideação.<br>4. IA gera exatamente 3 soluções estratégicas.<br>5. Cada solução recebe impacto, esforço, viabilidade, riscos e mitigações.<br>6. IA recomenda uma solução.<br>7. Sistema valida resposta estruturada.<br>8. Sistema salva o brainstorm vinculado à ideia. |
| Exceções | Falha da IA: marcar brainstorm como erro e manter ideia salva.<br>Resposta inválida: não gravar brainstorm inválido e registrar erro.<br>Timeout: marcar erro controlado e permitir retentativa.<br>Dados insuficientes: registrar status pendente ou gerar análise limitada conforme regra. |
| Critérios de aceite | Brainstorm contém exatamente 3 soluções; cada solução possui campos obrigatórios; uma solução é recomendada; há notas e justificativas de impacto/esforço; falha de IA não perde a ideia. |
| Regras | RN007, RN008, RN009, RN018, RN019, RN020, RN021, RN022, RN023, RN024, RN025. |
| Observação | A IA apoia a decisão; a Inovação mantém autoridade para revisar notas e decidir priorização. |

<a id="ef-rf019-exibicao-do-brainstorm-no-detalhe-da-ideia"></a>
### RF019 - Exibição do brainstorm no detalhe da ideia

| Item | Especificação |
|---|---|
| Descrição | Exibir o Brainstorm Estratégico no detalhe da ideia. |
| Ator | Inovação; Diretoria em leitura, se a tela for disponibilizada para consulta. |
| Pré-condições | Ideia existente no backlog; usuário autenticado; brainstorm gerado, pendente ou com erro. |
| Fluxo principal | 1. Usuário abre detalhe da ideia.<br>2. Sistema exibe status do brainstorm.<br>3. Se gerado, exibe as 3 soluções.<br>4. Sistema destaca a solução recomendada.<br>5. Sistema exibe impacto, esforço, viabilidade, riscos e mitigações.<br>6. Usuário usa as informações para triagem ou conversão. |
| Exceções | Brainstorm pendente: indicar geração em andamento ou aguardando.<br>Brainstorm com erro: exibir mensagem amigável e opção de nova tentativa, se permitido.<br>Usuário sem permissão: bloquear ações de decisão. |
| Critérios de aceite | Usuário visualiza soluções, notas, riscos, mitigações e recomendação antes de converter a ideia em projeto. |
| Regras | RN001, RN002, RN018, RN019, RN026, RN027. |
| Observação | O detalhe da ideia deve preservar a descrição original e o resumo IA, sem substituir conteúdo do autor. |

<a id="ef-rf020-copia-do-brainstorm-para-projeto-convertido"></a>
### RF020 - Cópia do brainstorm para projeto convertido

| Item | Especificação |
|---|---|
| Descrição | Ao converter uma ideia em projeto, copiar o Brainstorm Estratégico para o registro do projeto. |
| Ator | Inovação / Sistema. |
| Pré-condições | Ideia aprovada para conversão; projeto interno em criação; brainstorm gerado ou conversão sem brainstorm explicitamente confirmada. |
| Fluxo principal | 1. Usuário aciona conversão em projeto.<br>2. Sistema busca brainstorm vinculado à ideia.<br>3. Sistema cria projeto interno.<br>4. Sistema copia o brainstorm da ideia para o projeto.<br>5. Sistema mantém rastreabilidade com a ideia original. |
| Exceções | Brainstorm ausente: exigir confirmação explícita da Inovação ou bloquear conforme regra definida.<br>Erro na criação do projeto: não alterar status da ideia para convertida/virou projeto.<br>Erro ao copiar brainstorm: registrar falha e não confirmar conversão completa. |
| Critérios de aceite | Projeto criado contém referência à ideia original e ao brainstorm estratégico usado na decisão. |
| Regras | RN018, RN019, RN028, RN030, RN032. |
| Observação | O brainstorm copiado representa o estado usado na decisão de conversão. Versionamento completo fica fora do escopo inicial. |

<a id="ef-rf021-task-inicial-no-asana-com-brainstorm"></a>
### RF021 - Task inicial no Asana com brainstorm

| Item | Especificação |
|---|---|
| Descrição | Criar uma task inicial no projeto do Asana contendo o Brainstorm Estratégico completo. |
| Ator | Sistema / Asana API. |
| Pré-condições | Projeto interno criado; projeto Asana criado ou identificado; brainstorm disponível no projeto interno. |
| Fluxo principal | 1. Sistema cria/identifica projeto no Asana.<br>2. Sistema monta conteúdo do brainstorm em Markdown/texto estruturado.<br>3. Sistema cria task inicial chamada `Brainstorm Estratégico IA`.<br>4. Sistema preenche a descrição da task com o brainstorm completo.<br>5. Sistema registra identificador/status da criação da task, quando aplicável. |
| Exceções | Falha na API do Asana: registrar pendência e permitir retentativa.<br>Projeto Asana não criado: não criar task e manter erro de sincronização.<br>Brainstorm ausente: criar task apenas se houver conteúdo aprovado ou sinalizar pendência.<br>Conteúdo muito extenso: aplicar formatação/resumo controlado sem omitir a solução recomendada. |
| Critérios de aceite | O projeto no Asana contém uma task inicial com as 3 soluções, recomendação da IA, notas de impacto/esforço, riscos e mitigações. |
| Regras | RN028, RN029, RN030, RN031, RN032. |
| Observação | O portal cria o conteúdo inicial; edições operacionais posteriores podem ocorrer diretamente no Asana. |

> Acredito que faça mais sentido entrar na Descrição do Projeto do que como uma Task, não acha?
>> Outro ponto: Importante que o Projeto entre com o nosso mockup de estrutura do Asana - Sprints.
>
> RESPOSTA: Sobre a estrutura base do asana que usamos, sim faz sentido vou ajustar os requisitos. 

---

<a id="ef-5-regras-de-negocio"></a>
## 5. Regras de negócio

| ID | Regra | Aplicável em | Critério / observação |
|---|---|---|---|
| RN001 | O portal terá perfis `diretoria` e `inovacao`. | RF001, RF002, RF006–RF017, RF019 | Diretoria tem leitura; Inovação executa gestão. Novos perfis exigem mudança de escopo. |
| RN002 | Permissões devem ser reforçadas por RLS e/ou Edge Functions. | RF002, RF008, RF010, RF015, RF019 | Ocultar ação na UI não basta; chamadas diretas indevidas devem ser bloqueadas. |
| RN003 | Usuário com `profiles.ativo = false` não acessa áreas internas. | RF001, RF002 | Bloqueio pode ocorrer após autenticação, ao carregar perfil. |
| RN004 | Campos obrigatórios do Canvas: nome, e-mail, departamentos, Problema, Indicadores, Como resolver sem IA, Como resolver com IA e Para quem/personas. Dados/fontes e Ferramentas são opcionais. | RF003 | Envio deve ser bloqueado se qualquer obrigatório estiver ausente. |
| RN005 | Ideias devem seguir status controlados: `rascunho`, `enviada`, `resumo_gerado`, `aprovada_autor`, `em_triagem`, `virou_projeto`, `backlog`, `arquivada`. | RF003, RF005, RF007, RF008, RF009 | Transições inválidas devem ser bloqueadas na aplicação. |
| RN006 | O front público não deve inserir diretamente em `ideas`; toda submissão passa por `submit-idea`. | RF003 | Insert anônimo direto deve ser bloqueado por RLS. |
| RN007 | Submissões públicas devem ter proteção anti-spam. | RF003 | Usar honeypot, rate limit e/ou captcha leve; mensagens ao usuário devem ser genéricas. |
| RN008 | IA é apoio, não autoridade final. | RF004, RF005, RF012, RF018 | Sugestões, resumo, notas, brainstorm e insights podem ser revisados pela Inovação. |
| RN009 | Edge Functions de IA devem solicitar e validar JSON estruturado antes de gravar campos controlados. | RF004, RF005, RF012, RF018 | Resposta não JSON não deve gravar campos críticos indevidamente. |
| RN010 | Impacto e esforço usam escala inteira de 1 a 10. | RF005, RF007, RF008, RF009, RF018 | Valores fora da escala devem ser bloqueados; mocks em outra escala devem ser ajustados. |
| RN011 | Impacto e esforço não devem aparecer no fluxo público do autor da ideia. | RF003, RF005 | Notas são apoio interno para Inovação/Diretoria. |
| RN012 | Dashboard e detalhe devem usar cache de `asana_sync`, não chamada Asana ao vivo. | RF006, RF013, RF016 | Evita lentidão, rate limit e indisponibilidade por dependência externa. |
| RN013 | A matriz usa esforço no eixo X e impacto no eixo Y. | RF007 | Quanto maior o esforço, mais à direita; quanto maior o impacto, mais acima. |
| RN014 | Ideias sem pontuação final podem usar pontuação sugerida pela IA, mas devem indicar origem da nota. | RF007, RF008 | Quando houver nota final da triagem, ela prevalece. |
| RN015 | Ideias arquivadas, rejeitadas ou já convertidas não aparecem como oportunidades ativas na matriz. | RF007, RF008 | Podem aparecer apenas em filtros/histórico. |
| RN016 | Somente Inovação pode registrar decisão de triagem. | RF008, RF009 | Diretoria consulta, mas não decide pelo sistema. |
| RN017 | Decisão “Vira Projeto” exige impacto/esforço válidos e dados mínimos do projeto. | RF008, RF009 | Pode exigir sponsor, owner e área conforme definição final. |
| RN018 | O Brainstorm Estratégico deve ser gerado após o cadastro da ideia. | RF003, RF018 | Geração pode ser síncrona ou assíncrona, desde que status seja controlado. |
| RN019 | A ideia deve ser salva mesmo se a geração do brainstorm falhar. | RF003, RF018, RF020 | Falha de IA não pode causar perda da submissão. |
| RN020 | Uma resposta válida de brainstorm deve conter exatamente 3 soluções. | RF018 | Menos ou mais soluções tornam a resposta inválida para persistência controlada. |
| RN021 | Cada solução deve indicar uma abordagem SCAMPER aplicada. | RF018 | Sempre que possível, as 3 soluções devem usar abordagens diferentes. |
| RN022 | Cada solução deve conter nota de impacto e esforço de 1 a 10. | RF018 | Cada nota deve ter justificativa objetiva. |
| RN023 | A solução recomendada deve ser uma das 3 soluções geradas. | RF018 | `recommendedSolutionId` deve existir em `solutions`. |
| RN024 | A justificativa da recomendação deve considerar impacto, esforço, viabilidade e riscos. | RF018 | Não escolher apenas a solução mais ambiciosa. |
| RN025 | O Brainstorm Estratégico deve usar SCAMPER como framework principal. | RF018, RF019 | SCAMPER orienta geração, mas não substitui julgamento da Inovação. |
| RN026 | As notas da solução recomendada alimentam a classificação inicial da matriz. | RF007, RF018, RF019 | A Inovação pode revisar notas na triagem. |
| RN027 | A matriz deve classificar quadrantes por regra objetiva 1–10. | RF007, RF008 | Ver seção 5.5. |
| RN028 | Ao converter ideia em projeto, o brainstorm deve ser copiado para o projeto interno. | RF009, RF010, RF020 | Preserva rastreabilidade da decisão. |
| RN029 | O Asana é ferramenta operacional; o portal mantém a governança. | RF009, RF013, RF016, RF021 | Falhas de Asana não devem apagar dados internos. |
| RN030 | Ações relevantes devem gerar log funcional sem dados sensíveis. | RF003–RF021 | Logs devem apoiar auditoria e troubleshooting. |
| RN031 | Ao criar o projeto no Asana, o sistema deve criar task inicial `Brainstorm Estratégico IA`. | RF009, RF021 | A task recebe o conteúdo completo do brainstorm. |
| RN032 | Falhas de IA ou Asana devem ser tratadas sem perda de dados principais. | RF003, RF009, RF018, RF021 | Registrar erro e permitir retentativa quando aplicável. |
| RN033 | Comentários operacionais de tasks permanecem no Asana; comentários de governança ficam no portal. | RF014 | Evita duplicidade de ferramentas. |
| RN034 | Departamentos inativos não aparecem no Canvas público. | RF003, RF015 | Histórico deve ser preservado. |
| RN035 | Regeração de brainstorm pode existir no MVP, mas sem versionamento completo obrigatório. | RF018, RF019 | Se implementada, deve preservar rastreabilidade mínima. |

> Não entendi o 034 - Departamentos inativos não aparecem no Canvas Publico. Você pensou em listar no 004? Acho que pode ser um campo aberto mesmo.
>
> RESPOSTA: pode ser aberto sim, vou ajustar os requisitos
### 5.1 Framework SCAMPER

O Brainstorm Estratégico deve usar o SCAMPER como framework principal.

| Letra | Abordagem | Uso no portal |
|---|---|---|
| S | Substituir | Trocar processo, ferramenta, etapa, tecnologia ou abordagem atual por outra mais eficiente. |
| C | Combinar | Unir processos, sistemas, áreas, dados ou soluções existentes. |
| A | Adaptar | Adaptar prática, tecnologia ou solução de outro contexto para a demanda apresentada. |
| M | Modificar | Melhorar, ampliar, simplificar ou redesenhar algo existente. |
| P | Propor outro uso | Reaproveitar ativos, dados, sistemas ou processos para nova finalidade. |
| E | Eliminar | Remover etapas, retrabalhos, controles manuais ou complexidades desnecessárias. |
| R | Reorganizar | Reordenar fluxos, responsabilidades, etapas, integrações ou jornadas. |

Regra: cada uma das 3 soluções deve indicar a abordagem SCAMPER aplicada. Sempre que possível, as soluções devem usar abordagens diferentes.

### 5.2 Estrutura obrigatória de cada solução

Cada solução deve conter:

- abordagem SCAMPER aplicada;
- descrição da solução;
- racional estratégico;
- como resolve a demanda;
- impacto estimado e justificativa;
- esforço estimado e justificativa;
- análise de viabilidade;
- riscos principais;
- mitigações sugeridas.

### 5.3 Métrica de Impacto

| Nota | Interpretação |
|---|---|
| 1 a 3 | Baixo impacto |
| 4 a 6 | Impacto moderado |
| 7 a 8 | Alto impacto |
| 9 a 10 | Impacto estratégico/crítico |

Critérios e pesos:

| Critério | Peso |
|---|---:|
| Alinhamento estratégico com objetivos da Rennova | 20% |
| Gravidade ou relevância da demanda | 15% |
| Ganho esperado de eficiência, receita, economia, qualidade ou compliance | 25% |
| Quantidade de áreas, usuários ou processos beneficiados | 15% |
| Potencial de escala/reutilização em outras áreas | 15% |
| Urgência ou redução de risco relevante | 10% |

### 5.4 Métrica de Esforço

| Nota | Interpretação |
|---|---|
| 1 a 3 | Baixo esforço |
| 4 a 6 | Esforço moderado |
| 7 a 8 | Alto esforço |
| 9 a 10 | Esforço muito alto/crítico |

Critérios e pesos:

| Critério | Peso |
|---|---:|
| Complexidade técnica | 25% |
| Necessidade de integrações ou dados externos | 20% |
| Tempo estimado de implementação | 20% |
| Mudança operacional/processual necessária | 15% |
| Dependência de outras áreas, fornecedores ou aprovações | 10% |
| Custo estimado de implantação/manutenção | 10% |

### 5.5 Regra da matriz Impacto × Esforço

| Quadrante | Critério | Interpretação |
|---|---|---|
| Oportunidade Imediata | Impacto >= 7 e Esforço <= 4 | Alta prioridade. Deve ser considerada para execução rápida. |
| Grande Projeto | Impacto >= 7 e Esforço >= 5 | Alta relevância, mas exige planejamento, sponsor e recursos. |
| Ganho Tático / Astuto | Impacto entre 4 e 6 e Esforço <= 4 | Pode ser executado se houver capacidade disponível ou ganho operacional claro. |
| Retorno Limitado | Impacto <= 6 e Esforço >= 5 | Baixa prioridade. Só deve avançar com justificativa forte. |
| Baixa Atratividade | Impacto <= 3 | Normalmente não priorizar, salvo obrigação regulatória, compliance ou decisão estratégica. |

### 5.6 Recomendação da IA

A IA deve recomendar a solução com melhor equilíbrio entre:

- impacto;
- esforço;
- viabilidade;
- riscos controláveis;
- aderência à demanda original;
- possibilidade de execução no contexto da Rennova.

---

<a id="ef-6-fluxos-de-usuario"></a>
## 6. Fluxos de usuário

### 6.1 Submissão pública de ideia

```text
Colaborador acessa /canvas
  -> preenche dados e blocos do Canvas
  -> solicita sugestões pontuais de IA, se necessário
  -> revisa resumo gerado por IA
  -> aprova envio
  -> sistema salva ideia
  -> sistema inicia geração do Brainstorm Estratégico IA
```

### 6.2 Geração do Brainstorm Estratégico IA

```text
Ideia salva
  -> Edge Function monta prompt com dados da ideia
  -> IA usa SCAMPER como base
  -> IA retorna 3 soluções estruturadas
  -> sistema valida JSON
  -> sistema salva brainstorm na ideia
  -> sistema define impacto, esforço e quadrante inicial pela solução recomendada
```

### 6.3 Triagem de ideia

```text
Inovação acessa backlog/triagem
  -> abre detalhe da ideia
  -> consulta Canvas, resumo IA, brainstorm, solução recomendada e matriz
  -> revisa impacto/esforço, se necessário
  -> decide Backlog, Arquivar/Rejeitar ou Vira Projeto
```

### 6.4 Conversão em projeto com Asana

```text
Inovação aciona Vira Projeto
  -> sistema valida permissão, idempotência e dados mínimos
  -> sistema cria projeto interno
  -> sistema copia Brainstorm Estratégico da ideia para o projeto
  -> sistema cria projeto no Asana
  -> sistema cria task inicial Brainstorm Estratégico IA
  -> sistema registra vínculo e logs
  -> ideia passa para status virou_projeto
```

### 6.5 Sincronização Asana → Portal

```text
Asana envia webhook ou cron executa reconciliação
  -> Edge Function consulta/recebe evento do Asana
  -> atualiza cache em asana_sync
  -> dashboard e bloco Asana leem dados cacheados
```

---

<a id="ef-7-mapa-de-navegacao"></a>
## 7. Mapa de navegação

| Rota | Acesso | Objetivo |
|---|---|---|
| `/canvas` | Público | Submissão de ideias por colaboradores |
| `/login` | Público | Login no portal interno |
| `/` ou `/dashboard` | Diretoria / Inovação | Visão executiva do portfólio |
| `/ideias` | Diretoria / Inovação | Backlog, matriz e triagem de ideias |
| `/ideias/:id` | Diretoria / Inovação | Detalhe da ideia, resumo IA e brainstorm |
| `/matriz` | Diretoria / Inovação | Matriz Impacto × Esforço, caso separada de `/ideias` |
| `/triagem` | Inovação | Triagem mensal, caso separada de `/ideias` |
| `/projetos` | Diretoria / Inovação | Lista de projetos de inovação |
| `/projetos/:id` | Diretoria / Inovação | Detalhe, governança, fases, métricas e Asana |
| `/admin` | Inovação / Admin | Departamentos e usuários |

> Minha visão é que matriz e triagem devem estar dentro de /ideias. Sendo abas ali dentro.
>
> RESPOSTA: concordo, vou ajustar os requisitos
---

<a id="ef-8-telas-e-comportamento-visual"></a>
## 8. Telas e comportamento visual

### Tela 1 - Canvas público

- Deve ser simples, sem login e responsivo.
- Deve conter campos de identificação do autor, departamentos e blocos da ideia.
- Pode oferecer sugestões de IA por bloco.
- Deve permitir revisão do resumo IA quando aplicável.
- Não deve mostrar notas de impacto/esforço ao autor.
- Após envio, deve exibir confirmação clara.

### Tela 2 - Login

- Deve permitir autenticação por e-mail e senha.
- Deve tratar credenciais inválidas sem expor detalhes técnicos.
- Deve redirecionar usuário autenticado conforme perfil.

### Tela 3 - Dashboard

- Deve mostrar indicadores consolidados de ideias, projetos, status, fases, riscos e evolução.
- Deve consumir dados do Supabase e cache do Asana, não chamadas diretas ao Asana em tempo real.

### Tela 4 - Backlog, detalhe da ideia e matriz Impacto × Esforço

- Deve listar ideias com status, origem, área impactada, data, impacto, esforço e quadrante.
- Deve permitir abrir detalhe da ideia.
- O detalhe da ideia deve exibir:
  - descrição original;
  - Canvas/respostas principais;
  - resumo IA;
  - classificação IA;
  - status do brainstorm;
  - Brainstorm Estratégico com 3 soluções;
  - solução recomendada destacada;
  - notas de impacto/esforço;
  - análise de viabilidade;
  - riscos e mitigações;
  - ações de enviar ao comitê, aprovar, rejeitar, backlog, arquivar e converter em projeto conforme fluxo definido.
- A matriz deve seguir escala 1–10 e regra de quadrante documentada.

### Tela 5 - Triagem

- Deve apoiar decisão da Inovação com Canvas, resumo, brainstorm, matriz e dados da ideia.
- Deve permitir revisão de impacto, esforço e quadrante.
- Deve registrar decisão, responsável e data.

### Tela 6 - Detalhe do projeto

- Deve mostrar objetivo, problema, descrição, fase, checklist, próximos passos, histórico, métricas e comentários.
- Deve exibir o brainstorm herdado da ideia ou referência ao conteúdo que originou o projeto.
- Deve conter bloco Asana somente leitura com status operacional sincronizado.

### Tela 7 - Admin

- Deve permitir manutenção de departamentos e usuários conforme permissão.
- Deve impedir autoelevação indevida de perfil.

---

<a id="ef-9-requisitos-nao-funcionais"></a>
## 9. Requisitos não funcionais

| Código | Requisito |
|---|---|
| RNF001 | Interface deve manter identidade visual do protótipo Lovable. |
| RNF002 | Primeira versão deve priorizar desktop e responsividade web básica. |
| RNF003 | Chaves de IA, Asana e Supabase service role não podem estar no front-end. |
| RNF004 | Operações sensíveis devem passar por Edge Functions. |
| RNF005 | RLS deve proteger dados internos. |
| RNF006 | Respostas de IA devem ser validadas antes de persistência. |
| RNF007 | Falhas de IA e Asana devem ser tratadas sem perda de dados principais. |
| RNF008 | Logs não devem armazenar tokens, prompts sensíveis completos ou dados desnecessários. |
| RNF009 | Dashboard deve usar dados cacheados para evitar dependência de chamadas externas em tempo real. |
| RNF010 | O sistema deve permitir retentativa controlada em falhas de integração. |

---

<a id="ef-10-mensagens-do-sistema"></a>
## 10. Mensagens do sistema

| Situação | Mensagem sugerida |
|---|---|
| Ideia enviada | Ideia enviada com sucesso. A área de Inovação fará a análise. |
| Falha ao enviar ideia | Não foi possível enviar a ideia agora. Tente novamente. |
| IA indisponível | A ideia foi salva, mas a análise por IA não pôde ser gerada no momento. |
| Brainstorm gerado | Brainstorm Estratégico gerado com sucesso. |
| Brainstorm com erro | Não foi possível gerar o brainstorm. Tente novamente ou prossiga mediante validação da Inovação. |
| Conversão concluída | Projeto criado com sucesso e integrado ao Asana. |
| Falha parcial no Asana | Projeto criado no portal, mas houve falha ao sincronizar com o Asana. A sincronização poderá ser tentada novamente. |
| Acesso negado | Você não tem permissão para executar esta ação. |

> "Não foi possível enviar a ideia agora. Tente novamente." Deixar claro que é um erro nosso, da plataforma. Além de sugerir que se o erro persistir por mais de  24h, procurar o time de Inovação no Teams. 
>
> RESPOSTA: Ok, vou ajustar os requisitos

> O Brainstorme com erro vai ter um botão para forçar uma nova tentativa da IA? 
>
> RESPOSTA: pensei em tentar novamente depois de x segundos, mas vou entender a melhor maneira de fazer isso
---

<a id="ef-11-criterios-de-aceite-consolidados"></a>
## 11. Critérios de aceite consolidados

| Código | Critério |
|---|---|
| CA001 | Colaborador consegue submeter ideia válida pelo Canvas público. |
| CA002 | Sistema gera resumo IA da ideia ou salva a ideia mesmo em caso de falha de IA. |
| CA003 | Sistema gera Brainstorm Estratégico com exatamente 3 soluções baseadas em SCAMPER. |
| CA004 | Cada solução apresenta descrição, racional, resolução da demanda, impacto, esforço, viabilidade, riscos e mitigações. |
| CA005 | Uma solução é recomendada pela IA com justificativa. |
| CA006 | Impacto e esforço usam escala 1–10 e justificativa objetiva. |
| CA007 | Matriz classifica a ideia no quadrante correto. |
| CA008 | Inovação pode revisar impacto/esforço na triagem. |
| CA009 | Inovação consegue aprovar, rejeitar, manter em análise, backlog, arquivar ou converter ideia conforme estados definidos. |
| CA010 | Conversão cria projeto interno e preserva vínculo com a ideia original. |
| CA011 | Brainstorm é copiado para o projeto convertido. |
| CA012 | Asana recebe projeto e task inicial `Brainstorm Estratégico IA`. |
| CA013 | Falha no Asana não causa perda do projeto interno. |
| CA014 | Diretoria acessa informações em leitura sem ações de edição. |
| CA015 | Ações relevantes geram log funcional. |
| CA016 | RF001–RF021 mantêm estrutura padrão de especificação funcional. |

> Entender realmente a necessidade de task inicial.
---

<a id="ef-12-pendencias-e-decisoes-funcionais"></a>
## 12. Pendências e decisões funcionais

| Código | Decisão | Status / Recomendação |
|---|---|---|
| PD001 | Permitir conversão sem brainstorm gerado? | Permitir apenas com confirmação explícita da Inovação. |
| PD002 | Permitir regerar brainstorm? | Sim, mas sem versionamento completo na primeira versão. |
| PD003 | Usar notas das 3 soluções ou só da recomendada? | Salvar notas das 3 soluções; usar a recomendada para matriz inicial. |
| PD004 | Onde registrar brainstorm no Asana? | Criar task inicial `Brainstorm Estratégico IA`. |
| PD005 | A task do Asana pode ser editada manualmente? | Sim, pelo Asana; o portal cria o conteúdo inicial. |
| PD006 | Fórmula exata de cálculo ponderado será automática ou assistida pela IA? | IA deve justificar as notas com base nos pesos; cálculo determinístico pode ser implementado posteriormente. |
| PD007 | `/triagem` e `/matriz` serão rotas próprias ou visões dentro de `/ideias`? | Pode ser definido na implementação, preservando os comportamentos funcionais. |

---

<a id="ef-13-aprovacao-funcional"></a>
## 13. Aprovação funcional

| Papel | Nome | Status | Data |
|---|---|---|---|
| Responsável funcional | A definir | Pendente | - |
| Responsável técnico | Phablo Tavares | Pendente | - |
| Gerência solicitante | A definir | Pendente | - |
