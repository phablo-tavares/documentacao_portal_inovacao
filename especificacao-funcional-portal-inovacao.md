# Especificação Funcional — Portal de Gestão da Inovação Rennova

> Fonte funcional para orientar construção, aceite e evolução do **Rennova Spark Hub**.  
> Esta versão consolida as decisões funcionais sobre Canvas público, avaliação de suficiência e complementação por IA, Brainstorm Estratégico com IA, matriz Impacto × Esforço, triagem, conversão de ideias, integração com o Asana, entregas e governança. As métricas de impacto e esforço utilizam critérios ponderados e escalas ancoradas nas notas 2, 4, 6, 8 e 10, com exceção da escala específica de alcance dos beneficiados.

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
    - [RF021 - Configuração inicial do projeto no Asana](#rf021---configuração-inicial-do-projeto-no-asana)
    - [RF022 - Avaliação de suficiência e complementação estratégica](#rf022---avaliação-de-suficiência-e-complementação-estratégica)
  - [5. Regras de negócio](#5-regras-de-negócio)
    - [5.1 Framework SCAMPER](#51-framework-scamper)
    - [5.2 Estrutura obrigatória de cada solução](#52-estrutura-obrigatória-de-cada-solução)
    - [5.3 Métrica de Impacto](#53-métrica-de-impacto)
      - [5.3.1 Critérios, pesos e cálculo](#531-critérios-pesos-e-cálculo)
      - [5.3.2 Escalas ancoradas dos critérios](#532-escalas-ancoradas-dos-critérios)
        - [A. Gravidade ou relevância da demanda — Peso: 20%](#a-gravidade-ou-relevância-da-demanda--peso-20)
        - [B. Ganho esperado de eficiência, receita, economia, qualidade ou compliance — Peso: 30%](#b-ganho-esperado-de-eficiência-receita-economia-qualidade-ou-compliance--peso-30)
        - [C. Quantidade de áreas, usuários ou processos beneficiados — Peso: 20%](#c-quantidade-de-áreas-usuários-ou-processos-beneficiados--peso-20)
        - [D. Potencial de escala ou reutilização em outras áreas — Peso: 20%](#d-potencial-de-escala-ou-reutilização-em-outras-áreas--peso-20)
        - [E. Urgência ou redução de risco relevante — Peso: 10%](#e-urgência-ou-redução-de-risco-relevante--peso-10)
    - [5.4 Métrica de Esforço](#54-métrica-de-esforço)
      - [5.4.1 Critérios, pesos e cálculo](#541-critérios-pesos-e-cálculo)
      - [5.4.2 Escalas ancoradas dos critérios](#542-escalas-ancoradas-dos-critérios)
        - [A. Complexidade técnica — Peso: 30%](#a-complexidade-técnica--peso-30)
        - [B. Necessidade de integrações ou dados externos — Peso: 25%](#b-necessidade-de-integrações-ou-dados-externos--peso-25)
        - [C. Tempo estimado de implementação — Peso: 20%](#c-tempo-estimado-de-implementação--peso-20)
        - [D. Mudança operacional ou processual necessária — Peso: 15%](#d-mudança-operacional-ou-processual-necessária--peso-15)
        - [E. Custo estimado de implantação e manutenção — Peso: 10%](#e-custo-estimado-de-implantação-e-manutenção--peso-10)
    - [5.5 Regra da matriz Impacto × Esforço](#55-regra-da-matriz-impacto--esforço)
    - [5.6 Recomendação da IA](#56-recomendação-da-ia)
  - [6. Fluxos de usuário](#6-fluxos-de-usuário)
    - [6.1 Acesso e submissão pública de ideia](#61-acesso-e-submissão-pública-de-ideia)
    - [6.2 Avaliação de suficiência e complementação](#62-avaliação-de-suficiência-e-complementação)
    - [6.3 Geração do Brainstorm Estratégico IA](#63-geração-do-brainstorm-estratégico-ia)
    - [6.4 Triagem de ideia](#64-triagem-de-ideia)
    - [6.5 Conversão em projeto com Asana](#65-conversão-em-projeto-com-asana)
    - [6.6 Sincronização Asana → Portal](#66-sincronização-asana--portal)
    - [6.7 Gestão de entregas](#67-gestão-de-entregas)
  - [7. Mapa de navegação](#7-mapa-de-navegação)
  - [8. Telas e comportamento visual](#8-telas-e-comportamento-visual)
    - [Tela 1 - Canvas público](#tela-1---canvas-público)
    - [Tela 2 - Login](#tela-2---login)
    - [Tela 3 - Dashboard](#tela-3---dashboard)
    - [Tela 4 - Gestão de ideias](#tela-4---gestão-de-ideias)
    - [Tela 5 - Conversão em projeto](#tela-5---conversão-em-projeto)
    - [Tela 6 - Detalhe do projeto](#tela-6---detalhe-do-projeto)
    - [Tela 7 - Admin](#tela-7---admin)
  - [9. Requisitos não funcionais](#9-requisitos-não-funcionais)
  - [10. Mensagens do sistema](#10-mensagens-do-sistema)
  - [11. Critérios de aceite consolidados](#11-critérios-de-aceite-consolidados)
  - [12. Decisões funcionais consolidadas](#12-decisões-funcionais-consolidadas)
  - [13. Aprovação funcional](#13-aprovação-funcional)

---

<a id="ef-1-identificacao-do-projeto"></a>
## 1. Identificação do projeto

| Campo | Valor |
|---|---|
| Nome do projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável pelo documento | Phablo Tavares |
| Área/Time | Inovação / Desenvolvimento de Agentes e Soluções de IA |
| Data | 2026-07-14 |
| Versão | 0.8 |
| Alteração desta versão | Simplificação das métricas de impacto e esforço; inclusão da avaliação de suficiência do Canvas, complementação estratégica condicional por IA e adequação dos fluxos, regras, telas e critérios de aceite. |

---

<a id="ef-2-visao-geral"></a>
## 2. Visão geral

<a id="ef-2-1-contexto"></a>
### 2.1 Contexto

A área de Inovação da Rennova recebe ideias de diferentes áreas, avalia potencial, prioriza iniciativas e acompanha projetos aprovados. Parte desse processo atualmente fica dispersa entre conversas, documentos, planilhas e ferramentas operacionais. O portal deve centralizar a entrada de ideias, a triagem, a priorização, a conversão em projetos e o acompanhamento executivo.

Já existe um protótipo visual no Lovable/GitHub, com Dashboard, Projetos, Detalhe de Projeto e Ideias usando dados mockados. A entrega alvo deve transformar o protótipo em produto funcional com Supabase, autenticação, banco real, IA e integração com o Asana.

Antes do Brainstorm Estratégico, a IA deve avaliar se as informações do Canvas são suficientes. Quando necessário, o autor responderá uma única rodada de até 10 perguntas estratégicas para complementar o contexto usado no resumo, nas notas de impacto e esforço e no brainstorm.

O cadastro da ideia deve gerar um **Brainstorm Estratégico com IA**, usando SCAMPER como framework de inovação. O brainstorm apoiará a triagem, acompanhará a ideia quando convertida e será registrado na descrição do projeto criado no Asana.

<a id="ef-2-2-objetivo"></a>
### 2.2 Objetivo

Construir um portal interno para centralizar a gestão da inovação na Rennova, permitindo que colaboradores submetam ideias, a IA apoie a estruturação, a complementação e a análise inicial, a Inovação qualifique e priorize iniciativas, a Diretoria acompanhe o portfólio e projetos aprovados sejam integrados ao Asana para execução operacional.

<a id="ef-2-3-publico-alvo-usuarios"></a>
### 2.3 Público-alvo / usuários

| Ator / Perfil | Responsabilidade | Principais ações |
|---|---|---|
| Colaborador / Autor da ideia | Submeter ideia pelo Canvas público | Concluir CAPTCHA, preencher Canvas, solicitar sugestões de IA, responder complementação quando necessária, revisar resumo e aprovar submissão |
| Inovação | Gerir funil e governança da inovação | Triar ideias, consultar complementações, revisar impacto/esforço, consultar brainstorm, converter ideias, gerir projetos, fases, métricas, entregas, comentários e cadastros |
| Diretoria | Acompanhar portfólio em visão executiva | Consultar dashboard, backlog, matriz, triagem e detalhes de ideias/projetos; registrar comentários de governança |
| Administrador funcional | Gerir cadastros básicos | Gerenciar departamentos e perfis de usuários |
| Sistema / Integrações | Executar automações | Validar CAPTCHA, avaliar suficiência, gerar perguntas, resumos, brainstorms e insights; criar projetos no Asana; sincronizar dados e registrar logs |

---

<a id="ef-3-escopo"></a>
## 3. Escopo

<a id="ef-3-1-escopo-incluido"></a>
### 3.1 Escopo incluído

- [x] Base visual inicial com tema escuro, dashboard, projetos, detalhes e ideias usando `mockData`.
- [ ] Canvas público sem login para submissão de ideias.
- [ ] CAPTCHA obrigatório e validado antes da exibição do Canvas.
- [ ] Validação de e-mail por lista de domínios corporativos autorizados.
- [ ] Sugestões de IA por bloco do Canvas considerando o contexto completo da ideia.
- [ ] Avaliação de suficiência das informações do Canvas por IA.
- [ ] Modal condicional com uma rodada de até 10 perguntas estratégicas.
- [ ] Persistência das perguntas e respostas complementares vinculadas à ideia.
- [ ] Resumo consolidado da ideia por IA usando Canvas e complementação.
- [ ] Aprovação ou ajuste do resumo pelo autor.
- [ ] Brainstorm Estratégico com IA baseado em SCAMPER ao cadastrar ideia.
- [ ] Geração de 3 soluções estratégicas por ideia.
- [ ] Recomendação de uma solução pela IA, com justificativa.
- [ ] Métricas de impacto e esforço com critérios ponderados, escalas ancoradas simplificadas e cálculo reproduzível.
- [ ] Matriz Impacto × Esforço para ideias elegíveis.
- [ ] Login com Supabase Auth por e-mail e senha.
- [ ] Controle de acesso por perfis `diretoria` e `inovacao`.
- [ ] Dashboard executivo com indicadores do portfólio e dados cacheados do Asana.
- [ ] Triagem mensal de ideias pela Inovação, consultável pela Diretoria.
- [ ] Histórico de ideias arquivadas com justificativa e auditoria da decisão.
- [ ] Conversão de ideia em projeto no portal e no Asana.
- [ ] Solicitação obrigatória do nome do projeto durante a conversão.
- [ ] Criação do projeto Asana pelo template fixo `INV | Modelo Base`, ID `1213945719343548`.
- [ ] Registro do Brainstorm Estratégico na descrição do projeto Asana.
- [ ] Detalhe do projeto com fases, checklist executivo, métricas, resultados, insights de IA, entregas e comentários de governança.
- [ ] Armazenamento de arquivos de entrega no Supabase Storage, com limite de 50 MB por arquivo.
- [ ] Bloco Asana somente leitura no detalhe do projeto.
- [ ] Sincronização Asana → portal por webhook e cron diário de reconciliação.
- [ ] Administração de departamentos e usuários.
- [ ] Logs de auditoria para ações relevantes.

<a id="ef-3-2-fora-de-escopo"></a>
### 3.2 Fora de escopo

- Substituir o Asana como ferramenta operacional de tarefas.
- Editar tarefas Asana dentro do portal.
- Criar projeto Asana vazio ou com template diferente do `INV | Modelo Base`.
- Criar task exclusiva para armazenar o Brainstorm Estratégico.
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
- Mais de uma rodada de perguntas complementares no Canvas.
- Treinamento de modelo próprio de IA.
- Cálculo financeiro detalhado de ROI por IA.
- Edição de comentários de governança já publicados.
- Edição do conteúdo binário de arquivos de entrega já enviados; um novo envio deverá gerar outro arquivo.
- Versionamento ou processo de homologação de futuras alterações do template Asana, pois o template é considerado fixo para este escopo.

<a id="ef-3-3-premissas"></a>
### 3.3 Premissas

- Lovable continuará sendo a principal ferramenta de evolução do front-end.
- Supabase será usado para Auth, Postgres, RLS, Edge Functions e Storage.
- A sessão seguirá o comportamento padrão do Supabase Auth, incluindo persistência e renovação automática de tokens, sem timeout customizado nesta versão.
- Asana será a fonte operacional de tarefas e sprints.
- Supabase será a fonte de verdade para ideias, complementações, triagem, governança, métricas, usuários, entregas e visão executiva.
- Tokens de Asana e IA ficarão somente em secrets nas Edge Functions.
- Workspace, portfólio e owner padrão do Asana serão parametrizados.
- O template Asana será fixo e identificado pelo ID `1213945719343548`.
- Nome do template Asana: `INV | Modelo Base`.
- Link de referência do template: `https://app.asana.com/0/project-templates/1213945719343548/list`.
- A credencial utilizada pela integração terá acesso ao template, ao workspace e ao portfólio necessários.
- Respostas de IA serão estruturadas em JSON e validadas antes de gravação.
- A IA decidirá se o Canvas possui informações suficientes para prosseguir sem perguntas adicionais.
- O Brainstorm Estratégico usará SCAMPER como base de ideação.
- O Brainstorm Estratégico completo será registrado na descrição do projeto Asana.
- A primeira versão priorizará desktop e responsividade básica para web.

<a id="ef-3-4-restricoes"></a>
### 3.4 Restrições

- Não expor chaves, tokens ou `service_role` no front-end.
- Não chamar Asana nem provedores de IA diretamente pelo browser.
- Evitar edição manual ampla do front-end fora do Lovable.
- Não exibir o Canvas antes da validação do CAPTCHA.
- Proteger o formulário público com CAPTCHA obrigatório, rate limit e honeypot.
- Validar o token CAPTCHA no backend e manter uma sessão de acesso válida durante o preenchimento e a submissão.
- Aceitar submissões apenas dos domínios de e-mail autorizados.
- Não exibir impacto/esforço ao autor da ideia no fluxo público.
- Aplicar permissões no front-end e reforçá-las por RLS/Edge Functions.
- Não depender de chamada ao Asana em tempo real no dashboard.
- Não gravar resposta de IA sem validação mínima de estrutura.
- Não permitir conversão em projeto sem notas finais válidas e nome do projeto informado.
- Não marcar a conversão como concluída se o projeto não for criado pelo template obrigatório.
- Arquivos de entrega devem ter no máximo 50 MB por arquivo.

---

<a id="ef-4-requisitos-funcionais"></a>
## 4. Requisitos funcionais

> Todos os RFs mantêm a estrutura: **Descrição, Ator, Pré-condições, Fluxo principal, Exceções, Critérios de aceite, Regras e Observação**.

<a id="ef-rf001-autenticacao-no-portal-interno"></a>
### RF001 - Autenticação no portal interno

| Item | Especificação |
|---|---|
| Descrição | Permitir login no portal interno por e-mail e senha via Supabase Auth, usando o gerenciamento padrão de sessão da plataforma. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário cadastrado no Supabase Auth; perfil correspondente em `profiles`; usuário ativo. |
| Fluxo principal | 1. Acessar `/login`.<br>2. Informar e-mail e senha.<br>3. Autenticar no Supabase.<br>4. Consultar perfil e permissões.<br>5. Redirecionar para o Dashboard.<br>6. Manter a sessão conforme persistência e renovação automática padrão do Supabase Auth. |
| Exceções | `FA001` credenciais inválidas: exibir mensagem genérica.<br>`FA002` usuário inativo: bloquear acesso e orientar contato com Inovação.<br>`FA003` perfil inexistente: bloquear e registrar erro técnico.<br>`FA004` sessão inválida ou não renovável: encerrar sessão e redirecionar para `/login`. |
| Critérios de aceite | Usuário ativo com credenciais válidas acessa o Dashboard; usuário inativo é bloqueado; usuário não autenticado em rota interna é enviado para `/login`; a sessão válida é renovada pelo comportamento padrão do Supabase. |
| Regras | RN001, RN002, RN003. |
| Observação | SSO e timeout customizado de sessão não fazem parte da primeira versão. |

<a id="ef-rf002-controle-de-acesso-por-perfil"></a>
### RF002 - Controle de acesso por perfil

| Item | Especificação |
|---|---|
| Descrição | Restringir funcionalidades conforme perfil `diretoria` ou `inovacao`. |
| Ator | Sistema. |
| Pré-condições | Usuário autenticado; `profiles.role` definido. |
| Fluxo principal | 1. Usuário acessa rota interna.<br>2. Sistema carrega o perfil.<br>3. UI exibe apenas menus e ações permitidos.<br>4. RLS e Edge Functions reforçam a permissão.<br>5. Diretoria consulta backlog, matriz, triagem, detalhes e projetos.<br>6. Diretoria e Inovação podem registrar comentários de governança.<br>7. Apenas Inovação altera dados de gestão, notas e decisões. |
| Exceções | Diretoria acessando `/admin`: acesso negado.<br>Diretoria tentando alterar notas, decisão, projeto ou cadastro por chamada direta: bloqueio por RLS/Edge Function.<br>Perfil ausente ou desconhecido: bloqueio por segurança. |
| Critérios de aceite | Diretoria consulta dashboard, ideias, matriz, triagem e projetos; pode comentar; não altera notas nem decisões; Inovação acessa ações de gestão e administração. |
| Regras | RN001, RN002, RN003, RN016, RN042. |
| Observação | Ocultar botão no front-end não substitui validação server-side. |

<a id="ef-rf003-submissao-de-ideia-pelo-canvas-publico"></a>
### RF003 - Submissão de ideia pelo Canvas público

| Item | Especificação |
|---|---|
| Descrição | Permitir que colaborador acesse e envie ideia pela rota pública `/canvas`, sem login, após validação prévia do CAPTCHA. |
| Ator | Colaborador. |
| Pré-condições | Rota pública disponível; Edge Functions de CAPTCHA e `submit-idea` configuradas; lista de domínios autorizados disponível. |
| Fluxo principal | 1. Acessar `/canvas`.<br>2. Exibir somente a etapa de verificação CAPTCHA.<br>3. Validar o CAPTCHA no backend.<br>4. Liberar o Canvas após validação válida.<br>5. Preencher identificação, área/departamento em campo aberto e blocos do Canvas.<br>6. Informar e-mail corporativo.<br>7. Solicitar a continuidade do envio.<br>8. Executar a avaliação de suficiência do RF022.<br>9. Gerar e apresentar o resumo conforme RF005.<br>10. Autor aprova ou complementa o resumo.<br>11. Edge Function valida campos obrigatórios, domínio do e-mail, sessão CAPTCHA, honeypot e rate limit.<br>12. Sistema grava `ideas.status = enviada`, o resumo e a complementação existente.<br>13. Sistema inicia a geração do Brainstorm Estratégico IA quando a avaliação de suficiência estiver concluída.<br>14. Exibir confirmação de envio. |
| Exceções | CAPTCHA ausente, inválido ou expirado antes do acesso: não exibir o Canvas.<br>Sessão CAPTCHA expirada durante o preenchimento: solicitar nova validação sem descartar os dados locais.<br>Campos obrigatórios vazios: bloquear e destacar campos.<br>E-mail com domínio não autorizado: bloquear.<br>Serviço CAPTCHA indisponível: informar indisponibilidade e não liberar o Canvas.<br>Rate limit ou honeypot acionado: bloquear com mensagem genérica.<br>Falha de gravação: exibir erro e permitir nova tentativa.<br>Falha técnica na avaliação de suficiência: permitir a submissão, salvar a ideia e manter o brainstorm pendente para recuperação controlada.<br>Falha de IA após a gravação: manter a ideia salva e registrar pendência ou erro de IA.<br>Usuário tenta sair antes do envio: exibir aviso de perda dos dados preenchidos. |
| Critérios de aceite | Colaborador sem login acessa a etapa de CAPTCHA; o Canvas só é exibido após validação válida; Canvas incompleto é bloqueado; somente domínios autorizados são aceitos; submissão válida cria registro em `ideas` com status `enviada`; falha de IA não elimina a ideia; saída antes do envio apresenta aviso. |
| Regras | RN004, RN005, RN006, RN007, RN008, RN009, RN011, RN018, RN019, RN030, RN032, RN034, RN045, RN046, RN048, RN049. |
| Observação | Escrita pública no banco ocorrerá somente via Edge Function com `service_role`. A validação do CAPTCHA deverá ocorrer no backend. |

<a id="ef-rf004-sugestao-de-ia-por-bloco-do-canvas"></a>
### RF004 - Sugestão de IA por bloco do Canvas

| Item | Especificação |
|---|---|
| Descrição | Permitir que o autor solicite sugestão de IA para cada bloco do Canvas, considerando o conteúdo já preenchido e o objetivo geral da ideia. |
| Ator | Colaborador. |
| Pré-condições | CAPTCHA validado; `/canvas` liberado; `ai-assist-block` configurada; provider de IA configurado por secret. |
| Fluxo principal | 1. Clicar em “Sugestão IA” em um bloco.<br>2. Enviar o bloco, os demais campos preenchidos e o objetivo geral para a Edge Function.<br>3. IA retorna sugestão contextualizada e objetiva.<br>4. Sistema exibe sugestão para aceitar, editar ou ignorar. |
| Exceções | IA indisponível: manter edição manual.<br>Resposta inválida: ignorar resposta, registrar erro e exibir mensagem genérica.<br>Conteúdo insuficiente: IA pode retornar pergunta orientadora ou sugestão limitada. |
| Critérios de aceite | Sugestão considera o contexto completo disponível; retorna texto editável; falha de IA não impede preenchimento manual. |
| Regras | RN007, RN008, RN009, RN030, RN032, RN045. |
| Observação | Enviar ao provider somente o contexto necessário para a funcionalidade. |

<a id="ef-rf005-resumo-de-ia-e-aprovacao-pelo-autor"></a>
### RF005 - Resumo de IA e aprovação pelo autor

| Item | Especificação |
|---|---|
| Descrição | Gerar resumo consolidado da ideia e permitir aprovação ou complemento pelo autor antes da conclusão da submissão. |
| Ator | Autor da ideia. |
| Pré-condições | Canvas preenchido; avaliação de suficiência concluída ou complementação encerrada; `ai-summarize-idea` configurada. |
| Fluxo principal | 1. Enviar os blocos do Canvas e as respostas complementares existentes para a Edge Function.<br>2. IA retorna JSON com resumo e classificação inicial.<br>3. Exibir o resumo ao autor, sem notas de impacto e esforço.<br>4. Autor aprova ou complementa.<br>5. Incorporar o ajuste ao resumo.<br>6. Após a submissão válida, gravar a ideia, o resumo e a aprovação do autor.<br>7. Seguir para geração do brainstorm e triagem. |
| Exceções | IA falha: permitir submissão com resumo pendente para Inovação.<br>JSON inválido: não gravar campos controlados e registrar erro.<br>Autor complementa: incorporar o ajuste antes da submissão.<br>Autor abandona a página: dados não enviados não são persistidos; o navegador deve alertar sobre a perda. |
| Critérios de aceite | Resumo considera Canvas e respostas complementares existentes; resumo válido é exibido ao autor; aprovação ou complemento é registrado na submissão; impacto e esforço nunca aparecem ao autor; dados não enviados não são persistidos. |
| Regras | RN004, RN007, RN008, RN009, RN011, RN030, RN032, RN046, RN047, RN048. |
| Observação | Não haverá retomada posterior de Canvas não enviado nesta versão. |

<a id="ef-rf006-dashboard-executivo"></a>
### RF006 - Dashboard executivo

| Item | Especificação |
|---|---|
| Descrição | Exibir visão executiva do portfólio de inovação. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; dados de `projects`, `ideas` e `asana_sync` disponíveis. |
| Fluxo principal | 1. Acessar `/` ou `/dashboard`.<br>2. Exibir KPIs: projetos ativos, progresso médio, tarefas abertas e ideias em triagem.<br>3. Exibir lista de projetos com área, status, progresso e última atualização.<br>4. Permitir filtros por área e status.<br>5. Permitir acesso aos detalhes. |
| Exceções | Sem projetos: exibir estado vazio.<br>Sem dados Asana: indicar indisponível ou pendente.<br>Erro de carregamento: exibir erro e opção de tentar novamente. |
| Critérios de aceite | KPIs são calculados com dados do Supabase e cache do Asana; filtros funcionam; indisponibilidade do Asana não quebra a tela nem gera chamada ao vivo. |
| Regras | RN001, RN011, RN012, RN030. |
| Observação | A tela existente com dados mockados deverá ser conectada a consultas reais. |

<a id="ef-rf007-matriz-impacto-x-esforco"></a>
### RF007 - Matriz Impacto × Esforço

| Item | Especificação |
|---|---|
| Descrição | Exibir ideias elegíveis em matriz de priorização Impacto × Esforço, usando resultados finais entre 2 e 10, dentro da área de ideias. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; ideias elegíveis com notas válidas dos critérios de impacto e esforço ou com brainstorm gerado. |
| Fluxo principal | 1. Acessar `/ideias?aba=matriz`.<br>2. Buscar ideias elegíveis em `aprovada_autor`, `em_triagem` ou `backlog`.<br>3. Quando não houver avaliação final da triagem, usar as notas ponderadas da solução recomendada pela IA.<br>4. Diferenciar a avaliação inicial da IA e a avaliação final da triagem.<br>5. Calcular impacto e esforço pelas fórmulas das seções 5.3 e 5.4.<br>6. Arredondar os resultados para classificação na matriz.<br>7. Plotar esforço no eixo X e impacto no eixo Y.<br>8. Classificar o quadrante pela regra objetiva.<br>9. Permitir acesso ao detalhe da ideia e às notas de cada critério. |
| Exceções | Ideia sem avaliação completa: não plotar e listar como pendente.<br>Nota de critério ausente ou diferente das notas permitidas: não calcular a nota final e bloquear o salvamento da avaliação.<br>Sem elegíveis: exibir estado vazio.<br>Diretoria: leitura sem ações de decisão. |
| Critérios de aceite | Ideias elegíveis aparecem nos quadrantes calculados a partir das notas ponderadas; critérios, pesos e resultados ficam visíveis; ideias convertidas ou arquivadas não aparecem na matriz ativa; Diretoria não altera avaliações; Inovação pode revisar notas e o sistema recalcula os resultados finais. |
| Regras | RN010, RN013, RN014, RN015, RN016, RN017, RN026, RN027. |
| Observação | Não haverá rota independente `/matriz`. |

<a id="ef-rf008-triagem-mensal-de-ideias"></a>
### RF008 - Triagem mensal de ideias

| Item | Especificação |
|---|---|
| Descrição | Permitir que a Inovação realize a triagem, revise as notas dos critérios de impacto e esforço e registre a decisão; permitir que a Diretoria consulte os dados da triagem. |
| Ator | Inovação para gestão; Diretoria em leitura. |
| Pré-condições | Usuário autenticado; ideias em `aprovada_autor`, `em_triagem` ou estado elegível. |
| Fluxo principal | 1. Acessar `/ideias?aba=triagem`.<br>2. Listar ideias elegíveis do período.<br>3. Revisar Canvas, respostas complementares, resumo IA, brainstorm e solução recomendada.<br>4. Revisar ou informar obrigatoriamente as notas permitidas para cada critério de impacto e esforço, usando as escalas das seções 5.3 e 5.4.<br>5. Sistema calcula automaticamente `impacto_final` e `esforco_final` pelas fórmulas ponderadas.<br>6. Exibir notas dos critérios, pesos, resultado decimal e resultado arredondado usado na matriz.<br>7. Decidir: Vira Projeto, Backlog ou Arquivar/Rejeitar.<br>8. Para arquivar/rejeitar, informar justificativa obrigatória em texto livre.<br>9. Registrar data, usuário responsável e participantes da decisão, quando informados.<br>10. Atualizar status, registrar sessão em `triage_sessions` e log em `activity_log`.<br>11. Disponibilizar ideias arquivadas em `/ideias?aba=arquivadas`. |
| Exceções | Nota de critério ausente ou diferente das notas permitidas: bloquear o cálculo e o salvamento da avaliação.<br>“Vira Projeto” sem cálculo final completo: bloquear.<br>“Vira Projeto” sem brainstorm gerado: permitir somente com confirmação explícita da Inovação.<br>Arquivamento sem justificativa: bloquear.<br>Falha ao converter no Asana: manter ideia e projeto em estado seguro e exibir erro.<br>Usuário sem permissão de decisão: bloquear alterações. |
| Critérios de aceite | Todas as notas dos critérios são válidas e justificadas; resultados finais são calculados automaticamente; Backlog permanece na matriz; arquivamento registra justificativa, autor e data; ideias arquivadas ficam disponíveis no histórico; Vira Projeto somente prossegue quando a avaliação estiver completa. |
| Regras | RN001, RN010, RN015, RN016, RN017, RN018, RN026, RN027, RN028, RN030, RN032, RN043. |
| Observação | A triagem será uma aba da área de ideias, sem rota independente. |

<a id="ef-rf009-conversao-de-ideia-em-projeto"></a>
### RF009 - Conversão de ideia em projeto

| Item | Especificação |
|---|---|
| Descrição | Converter uma ideia aprovada em projeto no portal e instanciar o projeto correspondente no Asana a partir do template obrigatório. |
| Ator | Inovação. |
| Pré-condições | Ideia com decisão “Vira Projeto”; `impacto_final` e `esforco_final` válidos; usuário `inovacao`; secrets Asana configurados; integração com acesso ao template `INV | Modelo Base`; portfólio disponível. |
| Fluxo principal | 1. Acionar “Vira Projeto”.<br>2. Abrir campo de texto obrigatório solicitando o nome do projeto.<br>3. Usuário informa e confirma o nome.<br>4. Sistema normaliza o nome e define o título final como `INV | {nome informado}`.<br>5. Validar permissão, notas finais, nome e idempotência.<br>6. Buscar dados completos da ideia, incluindo resumo e brainstorm.<br>7. Criar ou preparar projeto no Supabase.<br>8. Copiar o brainstorm para o projeto interno.<br>9. Chamar `asana-create-project` ou função equivalente.<br>10. Instanciar o template Asana de ID `1213945719343548` e aguardar a conclusão do job.<br>11. Aplicar o nome final ao projeto.<br>12. Preservar seções, sprints, tarefas padrão e campos personalizados do template.<br>13. Preencher a descrição do projeto Asana com o Brainstorm Estratégico completo.<br>14. Configurar owner, portfólio, webhook e metadados.<br>15. Gravar `asana_project_gid`, `asana_permalink` e o vínculo da ideia.<br>16. Registrar log e marcar a ideia como `virou_projeto`. |
| Exceções | Nome vazio: bloquear.<br>Nome já contém `INV |`: normalizar para evitar prefixo duplicado.<br>Ideia já convertida: retornar conflito sem criar outro projeto.<br>Notas finais ausentes: bloquear.<br>Brainstorm ausente: permitir somente com confirmação explícita da Inovação.<br>Template não encontrado, sem acesso ou inválido: não concluir a conversão.<br>Job Asana falha ou expira: registrar falha e permitir recuperação.<br>Falha ao preencher descrição: registrar pendência e não indicar integração completa.<br>Falha ao adicionar ao portfólio, configurar owner ou webhook: registrar pendência de sincronização.<br>Falha parcial após criar projeto no Asana: registrar o identificador para recuperação e impedir duplicidade.<br>Token inválido: exibir erro controlado e registrar log técnico. |
| Critérios de aceite | Campo de nome é obrigatório; projeto interno e projeto Asana são criados; o título segue `INV | {nome informado}`; o Asana utiliza o template de ID `1213945719343548`; a estrutura do template é preservada; o brainstorm é copiado internamente e gravado na descrição do Asana; nenhuma task exclusiva de brainstorm é criada; tentativa duplicada é impedida; falha Asana não gera sucesso falso nem perda do projeto interno. |
| Regras | RN016, RN017, RN018, RN019, RN028, RN029, RN030, RN031, RN032, RN036, RN037, RN038, RN039, RN040, RN044. |
| Observação | Idempotência e tratamento de falhas parciais são obrigatórios. O template é fixo para este escopo. |

<a id="ef-rf010-detalhe-e-governanca-do-projeto"></a>
### RF010 - Detalhe e governança do projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir e permitir gestão das informações executivas, entregas e governança do projeto aprovado. |
| Ator | Inovação; Diretoria em leitura, com permissão para comentários. |
| Pré-condições | Usuário autenticado; projeto existente. |
| Fluxo principal | 1. Acessar `/projetos/:id`.<br>2. Exibir título, status, progresso, área, owner e datas.<br>3. Exibir resumo IA, objetivo, problema e descrição.<br>4. Exibir brainstorm herdado da ideia.<br>5. Exibir fases, checklist, métricas, dados Asana e comentários.<br>6. Exibir seção “Entregas”.<br>7. Inovação adiciona links ou envia arquivos.<br>8. Arquivos são armazenados no Supabase Storage e registrados no banco.<br>9. Diretoria e Inovação consultam e baixam as entregas.<br>10. Permitir edição de dados de gestão somente para Inovação. |
| Exceções | Projeto inexistente: exibir “Projeto não encontrado”.<br>Usuário sem permissão: ocultar ou bloquear ações editáveis.<br>Dados Asana ausentes: exibir bloco vazio ou indisponível.<br>Brainstorm ausente: exibir estado “não disponível”.<br>Arquivo maior que 50 MB: bloquear upload.<br>Falha de upload: não criar registro inconsistente e permitir nova tentativa.<br>Link inválido: bloquear salvamento. |
| Critérios de aceite | Detalhe exibe seções executivas; Diretoria não edita dados de gestão; Inovação gere fases, checklist, métricas e entregas; links e arquivos ficam acessíveis; cada arquivo tem no máximo 50 MB; brainstorm herdado é rastreável. |
| Regras | RN001, RN011, RN012, RN020, RN021, RN022, RN025, RN028, RN041, RN042. |
| Observação | Qualquer formato de arquivo será aceito nesta versão, respeitando o limite por arquivo. |

<a id="ef-rf011-gestao-de-fases-e-checklist-executivo"></a>
### RF011 - Gestão de fases e checklist executivo

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação acompanhe cinco fases fixas e checklist executivo por fase. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao`; projeto existente; fases semeadas em `project_phases`. |
| Fluxo principal | 1. Acessar detalhe do projeto.<br>2. Exibir stepper de cinco fases.<br>3. Marcar checklist da fase atual.<br>4. Marcar fase como concluída.<br>5. Atualizar status da fase.<br>6. Trigger ou rotina recalcula `progress_pct`. |
| Exceções | Fase anterior pendente: impedir avanço.<br>Projeto encerrado: bloquear alteração de fases e checklist.<br>Falha ao salvar: exibir erro e manter estado anterior. |
| Critérios de aceite | Fase concluída recalcula progresso; cinco fases concluídas resultam em 100%; projeto encerrado bloqueia alteração. |
| Regras | RN020, RN021, RN022. |
| Observação | Checklist do portal é executivo e não substitui tarefas do Asana. |

<a id="ef-rf012-metricas-resultados-e-insight-de-ia"></a>
### RF012 - Métricas, resultados e insight de IA

| Item | Especificação |
|---|---|
| Descrição | Permitir registrar métricas executivas, metas e resultados no Supabase e gerar insight de IA comparando meta e realizado. |
| Ator | Inovação. |
| Pré-condições | Projeto existente; métricas cadastradas ou derivadas da ideia; `ai-generate-insight` configurada. |
| Fluxo principal | 1. Acessar métricas no detalhe.<br>2. Exibir indicador, meta, unidade e resultado.<br>3. Preencher resultado.<br>4. Salvar no Supabase.<br>5. Acionar “Gerar insight”.<br>6. Chamar Edge Function.<br>7. Gravar `insight_ia` no Supabase. |
| Exceções | Resultado vazio: bloquear insight.<br>IA indisponível: manter resultado salvo e informar falha.<br>Resposta inválida: não gravar insight e registrar erro. |
| Critérios de aceite | Métrica, meta, resultado e insight ficam persistidos no Supabase; falha da IA não perde o resultado. |
| Regras | RN007, RN008, RN009, RN023, RN030, RN032. |
| Observação | Métricas executivas não devem ser confundidas com dados operacionais de tarefas sincronizados do Asana. |

<a id="ef-rf013-bloco-asana-no-projeto"></a>
### RF013 - Bloco Asana no projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir dados operacionais sincronizados do Asana no detalhe do projeto em modo somente leitura. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Projeto com `asana_project_gid`; dados em `asana_sync` ou estado vazio. |
| Fluxo principal | 1. Acessar detalhe.<br>2. Consultar `asana_sync`.<br>3. Exibir total de tarefas, abertas e concluídas.<br>4. Exibir distribuição por status.<br>5. Exibir, quando disponíveis, nome da tarefa, status, responsável, data de início e data de conclusão.<br>6. Exibir data e hora da última sincronização.<br>7. Exibir “Abrir no Asana”. |
| Exceções | Projeto sem Asana: indicar não integrado.<br>Cache vazio: exibir “Aguardando sincronização”.<br>Permalink ausente: ocultar botão ou marcar indisponível.<br>Campo não informado no Asana: exibir valor vazio sem quebrar a lista. |
| Critérios de aceite | Dados vêm de `asana_sync`; detalhes das tarefas são exibidos quando disponíveis; botão abre o projeto no Asana; nenhuma edição de tarefa é possível no portal. |
| Regras | RN011, RN012, RN024, RN029. |
| Observação | O portal não consultará o Asana ao vivo durante a renderização. |

<a id="ef-rf014-comentarios-de-governanca"></a>
### RF014 - Comentários de governança

| Item | Especificação |
|---|---|
| Descrição | Permitir que Diretoria e Inovação registrem comentários de governança no projeto. |
| Ator | Diretoria e Inovação. |
| Pré-condições | Usuário autenticado; projeto existente. |
| Fluxo principal | 1. Acessar detalhe.<br>2. Exibir comentários existentes.<br>3. Adicionar comentário.<br>4. Salvar com autor, perfil, data e hora.<br>5. Permitir exclusão conforme permissão.<br>6. Registrar log da criação e exclusão. |
| Exceções | Comentário vazio: bloquear.<br>Tentativa de editar comentário publicado: bloquear.<br>Usuário tentando excluir comentário de outro autor sem perfil `inovacao`: bloquear.<br>Falha ao salvar ou excluir: exibir erro e manter estado consistente. |
| Critérios de aceite | Comentário válido aparece no histórico; Diretoria e Inovação podem comentar; comentários não podem ser editados; o autor pode excluir o próprio comentário; Inovação pode excluir qualquer comentário por necessidade de governança. |
| Regras | RN001, RN025, RN030, RN032, RN042. |
| Observação | Comentários operacionais de tarefas permanecem no Asana. |

<a id="ef-rf015-administracao-de-departamentos-e-usuarios"></a>
### RF015 - Administração de departamentos e usuários

| Item | Especificação |
|---|---|
| Descrição | Permitir que Inovação gerencie departamentos internos e perfis de usuários. |
| Ator | Inovação. |
| Pré-condições | Usuário `inovacao` autenticado. |
| Fluxo principal | 1. Acessar `/admin`.<br>2. Exibir departamentos e usuários.<br>3. Criar, editar ou inativar departamento.<br>4. Alterar nome, papel ou status de usuário.<br>5. Salvar e registrar log. |
| Exceções | Departamento duplicado: bloquear.<br>Departamento em uso: preferir inativação.<br>Tentativa de autoelevação de papel: bloquear.<br>Usuário sem permissão: bloquear. |
| Critérios de aceite | Departamento único é criado; departamento em uso pode ser inativado sem quebrar histórico; Diretoria recebe acesso negado em `/admin`; cadastro de departamentos não controla o campo aberto de área/departamento do Canvas público. |
| Regras | RN001, RN002, RN003, RN030, RN032. |
| Observação | Os departamentos permanecem úteis para usuários, projetos, filtros e dados internos. |

<a id="ef-rf016-sincronizacao-asana-portal"></a>
### RF016 - Sincronização Asana → Portal

| Item | Especificação |
|---|---|
| Descrição | Manter dados operacionais do Asana sincronizados em `asana_sync`, usando webhook como mecanismo principal e cron diário para reconciliação. |
| Ator | Sistema. |
| Pré-condições | Projeto com `asana_project_gid`; `asana-webhook` e `asana-sync` configuradas; token Asana válido. |
| Fluxo principal | 1. Criar webhook na conversão do projeto.<br>2. Receber e responder o handshake do Asana.<br>3. Receber eventos de alteração.<br>4. Consultar ou processar os dados necessários e atualizar `asana_sync`.<br>5. Executar cron diário de reconciliação.<br>6. Dashboard e detalhe leem somente `asana_sync`. |
| Exceções | Evento de webhook perdido: cron diário reconcilia.<br>Handshake inválido: não criar webhook e registrar erro.<br>Token inválido: registrar erro.<br>Rate limit: aplicar retry e backoff.<br>Falha temporária: manter último cache válido e registrar status da sincronização. |
| Critérios de aceite | Alterações do Asana atualizam o cache prioritariamente pelo webhook; cron diário corrige divergências; front-end não chama API Asana diretamente. |
| Regras | RN011, RN012, RN029, RN030, RN032. |
| Observação | Validação de assinatura ou segredo pertence ao design técnico e é obrigatória para a segurança da integração. |

<a id="ef-rf017-auditoria-de-acoes-relevantes"></a>
### RF017 - Auditoria de ações relevantes

| Item | Especificação |
|---|---|
| Descrição | Registrar ações relevantes em `activity_log`. |
| Ator | Sistema. |
| Pré-condições | Tabela `activity_log` disponível. |
| Fluxo principal | 1. Usuário ou sistema executa ação relevante.<br>2. Sistema identifica entidade, ação, ator e detalhes não sensíveis.<br>3. Sistema grava log.<br>4. Inovação consulta logs quando necessário. |
| Exceções | Falha ao gravar log não crítico: não bloquear fluxo principal, mas registrar erro técnico quando possível.<br>Dados sensíveis: remover ou mascarar antes de gravar. |
| Critérios de aceite | Avaliação de suficiência, complementação, conversão, mudanças de status, arquivamento, comentários, entregas e exclusões relevantes geram log; logs não contêm tokens, senhas ou chaves. |
| Regras | RN030, RN032, RN043, RN046, RN049. |
| Observação | Log funcional não substitui monitoramento técnico das Edge Functions. |

<a id="ef-rf018-brainstorm-estrategico-com-ia"></a>
### RF018 - Brainstorm Estratégico com IA

| Item | Especificação |
|---|---|
| Descrição | Gerar automaticamente um Brainstorm Estratégico com IA após o cadastro de uma nova ideia. |
| Ator | Sistema / IA. |
| Pré-condições | Ideia cadastrada; avaliação de suficiência concluída; Canvas e respostas complementares disponíveis; provider de IA configurado; Edge Function de brainstorm disponível. |
| Fluxo principal | 1. Sistema reúne Canvas, respostas complementares e resumo disponível.<br>2. Sistema aciona a Edge Function de IA.<br>3. IA usa SCAMPER como base.<br>4. IA gera exatamente 3 soluções estratégicas.<br>5. Para cada solução, a IA atribui uma nota permitida a cada critério de impacto e esforço, conforme as escalas das seções 5.3 e 5.4, e registra a justificativa correspondente.<br>6. Quando as informações permanecerem incompletas após a complementação, a IA pode realizar inferências coerentes para atribuir as notas.<br>7. Sistema valida as notas e calcula automaticamente o impacto e o esforço finais de cada solução pelas fórmulas ponderadas.<br>8. Cada solução recebe análise de viabilidade, riscos e mitigações.<br>9. IA recomenda uma solução.<br>10. Sistema valida a resposta estruturada.<br>11. Sistema salva o brainstorm vinculado à ideia. |
| Exceções | Primeira tentativa falha: realizar uma segunda tentativa automática.<br>Segunda tentativa falha: marcar brainstorm como `erro`, manter a ideia salva e disponibilizar retentativa manual no detalhe da ideia.<br>Resposta inválida, critério ausente ou nota diferente das permitidas: tratar como tentativa com falha e não persistir conteúdo inválido.<br>Timeout: tratar como tentativa com falha.<br>Avaliação de suficiência com erro técnico: manter brainstorm pendente até retentativa controlada. |
| Critérios de aceite | São realizadas no máximo duas tentativas automáticas por geração; brainstorm válido contém exatamente 3 soluções; cada solução possui todos os critérios de impacto e esforço com notas permitidas e justificativas; resultados finais são calculados pelas fórmulas ponderadas; uma solução é recomendada; após duas falhas, a ideia permanece disponível com ação manual de retentativa. |
| Regras | RN007, RN008, RN009, RN018, RN019, RN020, RN021, RN022, RN023, RN024, RN025, RN035, RN046, RN047, RN048, RN049. |
| Observação | As duas tentativas correspondem à tentativa inicial e a uma retentativa automática. Retentativas manuais posteriores não exigem versionamento completo. |

<a id="ef-rf019-exibicao-do-brainstorm-no-detalhe-da-ideia"></a>
### RF019 - Exibição do brainstorm no detalhe da ideia

| Item | Especificação |
|---|---|
| Descrição | Exibir o contexto complementar, o Brainstorm Estratégico e seus status no detalhe da ideia. |
| Ator | Inovação e Diretoria em leitura; retentativas disponíveis somente para Inovação. |
| Pré-condições | Ideia existente; usuário autenticado; avaliação de suficiência e brainstorm em qualquer estado. |
| Fluxo principal | 1. Usuário abre o detalhe da ideia.<br>2. Sistema exibe o resultado da avaliação de suficiência.<br>3. Quando existentes, exibe perguntas estratégicas e respostas do autor.<br>4. Sistema exibe status do brainstorm.<br>5. Se gerado, exibe as 3 soluções.<br>6. Destaca a solução recomendada.<br>7. Exibe impacto, esforço, viabilidade, riscos e mitigações.<br>8. Se houver erro técnico na avaliação de suficiência, exibe ação de retentativa para Inovação.<br>9. Se houver erro após as duas tentativas automáticas do brainstorm, exibe “Tentar novamente” para Inovação. |
| Exceções | Avaliação ou brainstorm pendente: indicar processamento pendente.<br>Avaliação ou brainstorm com erro: exibir mensagem amigável e ação manual para Inovação.<br>Retentativa manual falha: manter status de erro e permitir novo acionamento posterior.<br>Usuário sem permissão: bloquear ações de retentativa e decisão. |
| Critérios de aceite | Usuário visualiza Canvas, perguntas e respostas complementares existentes, soluções, notas, riscos, mitigações e recomendação; Inovação pode acionar retentativas após falhas. |
| Regras | RN001, RN002, RN018, RN019, RN026, RN027, RN035, RN047, RN049. |
| Observação | O detalhe deve preservar separadamente o conteúdo original do Canvas, as respostas do autor e o conteúdo gerado pela IA. |

<a id="ef-rf020-copia-do-brainstorm-para-projeto-convertido"></a>
### RF020 - Cópia do brainstorm para projeto convertido

| Item | Especificação |
|---|---|
| Descrição | Ao converter uma ideia em projeto, copiar o Brainstorm Estratégico para o registro interno do projeto. |
| Ator | Inovação / Sistema. |
| Pré-condições | Ideia aprovada; projeto interno em criação; brainstorm gerado ou conversão sem brainstorm explicitamente confirmada. |
| Fluxo principal | 1. Usuário aciona a conversão.<br>2. Sistema busca o brainstorm vinculado à ideia.<br>3. Sistema cria o projeto interno.<br>4. Sistema copia o brainstorm para o projeto.<br>5. Sistema mantém referência à ideia original. |
| Exceções | Brainstorm ausente: exigir confirmação explícita da Inovação.<br>Erro na criação do projeto: não alterar a ideia para `virou_projeto`.<br>Erro ao copiar brainstorm: registrar falha e não confirmar conversão completa. |
| Critérios de aceite | Projeto criado contém referência à ideia original e ao brainstorm usado na decisão. |
| Regras | RN018, RN019, RN028, RN030, RN032. |
| Observação | O brainstorm copiado representa o estado usado na decisão de conversão. |

<a id="ef-rf021-configuracao-inicial-do-projeto-no-asana"></a>
### RF021 - Configuração inicial do projeto no Asana

| Item | Especificação |
|---|---|
| Descrição | Configurar no Asana o projeto originado de uma ideia, utilizando obrigatoriamente o template `INV | Modelo Base` e registrando o Brainstorm Estratégico na descrição do projeto. |
| Ator | Sistema / Asana API. |
| Pré-condições | Projeto interno criado; ideia aprovada; nome informado; integração Asana configurada; acesso ao template de ID `1213945719343548`; brainstorm disponível ou ausência confirmada pela Inovação. |
| Fluxo principal | 1. Localizar o template pelo ID `1213945719343548`.<br>2. Instanciar um projeto a partir do template.<br>3. Aguardar a conclusão do processo de criação.<br>4. Aplicar o nome `INV | {nome informado}`.<br>5. Preservar seções, sprints, tarefas padrão, campos personalizados e demais estruturas do template.<br>6. Inserir o Brainstorm Estratégico completo na descrição do projeto.<br>7. Configurar owner, portfólio, webhook e metadados.<br>8. Gravar identificadores, permalink e status da integração.<br>9. Não criar task específica de brainstorm. |
| Exceções | Template indisponível, removido ou sem permissão: bloquear conclusão e registrar erro.<br>Falha parcial após criação: registrar projeto para recuperação e não duplicar.<br>Brainstorm ausente: continuar somente com confirmação explícita da Inovação.<br>Falha ao atualizar descrição: registrar pendência e permitir retentativa.<br>Conteúdo extenso: aplicar formatação controlada, preservando as três soluções, recomendação, notas, riscos e mitigações. |
| Critérios de aceite | Projeto é criado a partir do template correto; estrutura do modelo é preservada; nome segue o padrão; descrição contém o brainstorm; vínculo com a ideia é registrado; nenhuma task exclusiva de brainstorm é criada. |
| Regras | RN028, RN029, RN030, RN031, RN032, RN036, RN037, RN038, RN039, RN040, RN044. |
| Observação | O template é fixo e não haverá mecanismo de versionamento ou homologação de alterações futuras neste escopo. |

<a id="ef-rf022-avaliacao-de-suficiencia-e-complementacao-estrategica"></a>
### RF022 - Avaliação de suficiência e complementação estratégica

| Item | Especificação |
|---|---|
| Descrição | Avaliar por IA se o Canvas possui informações suficientes e, somente quando necessário, solicitar uma rodada de perguntas estratégicas antes do resumo e do brainstorm. |
| Ator | Colaborador / Sistema / IA. |
| Pré-condições | CAPTCHA validado; Canvas com campos obrigatórios preenchidos; Edge Function de avaliação configurada. |
| Fluxo principal | 1. Autor solicita continuar com a submissão.<br>2. Sistema envia o conteúdo completo do Canvas para a IA.<br>3. IA decide se as informações são suficientes.<br>4. Se suficientes, registrar o resultado e seguir diretamente para o resumo.<br>5. Se insuficientes, IA gera de 1 a 10 perguntas estratégicas.<br>6. Sistema valida quantidade e estrutura das perguntas.<br>7. Abrir modal com uma única rodada de perguntas.<br>8. Autor responde integral ou parcialmente e conclui a complementação.<br>9. Persistir perguntas e respostas vinculadas à ideia durante a submissão.<br>10. Incorporar as respostas ao contexto utilizado no resumo, nas notas e no brainstorm.<br>11. Prosseguir sem abrir nova rodada de perguntas. |
| Exceções | Resposta da IA inválida, sem decisão ou com mais de 10 perguntas: tratar como falha técnica.<br>Falha técnica ou timeout: permitir que o autor conclua a submissão; salvar a ideia com avaliação em erro e manter o brainstorm pendente até retentativa pela Inovação.<br>Informações ainda incompletas após a rodada: não bloquear o envio e permitir que a IA realize inferências no brainstorm e nas notas.<br>Falha ao salvar perguntas ou respostas: não concluir a submissão até recuperar a persistência ou descartar a complementação de forma controlada. |
| Critérios de aceite | Canvas suficiente não abre modal; Canvas considerado insuficiente abre somente uma rodada com até 10 perguntas; perguntas são contextuais, objetivas, não repetem informações já fornecidas e não apresentam notas ao autor; respostas são persistidas e utilizadas nas etapas seguintes; informações remanescentes incompletas não bloqueiam o envio; falha técnica não causa perda da ideia. |
| Regras | RN007, RN008, RN009, RN011, RN030, RN032, RN045, RN046, RN047, RN048, RN049. |
| Observação | A decisão de suficiência pertence ao modelo de IA. Não haverá segunda rodada de complementação no MVP. |

---

<a id="ef-5-regras-de-negocio"></a>
## 5. Regras de negócio

| ID | Regra | Aplicável em | Critério / observação |
|---|---|---|---|
| RN001 | O portal terá perfis `diretoria` e `inovacao`. | RF001, RF002, RF006–RF017, RF019 | Diretoria consulta e comenta; Inovação executa gestão e decisões. |
| RN002 | Permissões devem ser reforçadas por RLS e/ou Edge Functions. | RF002, RF008, RF010, RF014, RF015, RF019 | Ocultar ação na UI não basta. |
| RN003 | Usuário com `profiles.ativo = false` não acessa áreas internas. | RF001, RF002 | O bloqueio ocorre ao carregar o perfil, mesmo que o Auth ainda reconheça a conta. |
| RN004 | Campos obrigatórios do Canvas: nome, e-mail, área/departamento em texto livre, Problema, Indicadores, Como resolver sem IA, Como resolver com IA e Para quem/personas. Dados/fontes e Ferramentas são opcionais. | RF003, RF005, RF022 | Envio deve ser bloqueado se qualquer obrigatório estiver ausente. |
| RN005 | Ideias devem seguir status controlados: `rascunho`, `enviada`, `resumo_gerado`, `aprovada_autor`, `em_triagem`, `virou_projeto`, `backlog`, `arquivada`. | RF003, RF005, RF007, RF008, RF009 | Transições inválidas devem ser bloqueadas. |
| RN006 | O front público não pode inserir diretamente em `ideas`; toda submissão passa por `submit-idea`. | RF003 | Insert anônimo direto deve ser bloqueado por RLS. |
| RN007 | O CAPTCHA deve ser validado no backend antes da exibição do Canvas. A sessão validada, o honeypot e o rate limit protegem a submissão. | RF003, RF004, RF005, RF022 | CAPTCHA ausente, inválido ou expirado impede o acesso ao Canvas. |
| RN008 | IA é apoio, não autoridade final. | RF004, RF005, RF012, RF018, RF022 | Conteúdo de IA pode ser revisado pela Inovação. |
| RN009 | Edge Functions de IA devem solicitar e validar JSON estruturado antes de gravar campos controlados. | RF004, RF005, RF012, RF018, RF022 | Resposta inválida não deve persistir campos críticos. |
| RN010 | Cada critério de impacto e esforço recebe uma das notas `2`, `4`, `6`, `8` ou `10`, conforme sua escala ancorada. O critério de alcance dos beneficiados utiliza `4`, `6`, `8` ou `10`. | RF005, RF007, RF008, RF009, RF018 | Valores diferentes devem ser bloqueados; o resultado decimal é preservado e o arredondado é usado na matriz. |
| RN011 | Impacto e esforço não devem aparecer no fluxo público do autor. | RF003, RF005, RF022 | Notas são internas. |
| RN012 | Dashboard e detalhe usam cache de `asana_sync`, não chamada Asana ao vivo. | RF006, RF013, RF016 | Evita lentidão, rate limit e dependência externa. |
| RN013 | A matriz usa esforço no eixo X e impacto no eixo Y. | RF007 | Maior esforço à direita; maior impacto acima. |
| RN014 | Ideias sem avaliação final da triagem podem usar os resultados ponderados calculados a partir das notas dos critérios da solução recomendada pela IA, indicando a origem. | RF007, RF008 | Quando houver avaliação final da triagem, ela prevalece. |
| RN015 | Ideias arquivadas, rejeitadas ou convertidas não aparecem na matriz ativa. | RF007, RF008 | Devem permanecer disponíveis em histórico ou filtros. |
| RN016 | Somente Inovação registra ou revisa as notas dos critérios e a decisão de triagem. | RF002, RF007, RF008, RF009 | Diretoria consulta critérios, pesos e resultados, e pode comentar, mas não decide. |
| RN017 | “Vira Projeto” exige avaliação completa dos critérios, `impacto_final`, `esforco_final` e nome do projeto válidos. | RF008, RF009 | Ausência de qualquer item bloqueia a conversão. |
| RN018 | O Brainstorm Estratégico deve ser gerado após o cadastro da ideia e a conclusão da avaliação de suficiência. | RF003, RF018, RF022 | A geração pode ser assíncrona, com status controlado. |
| RN019 | A ideia deve permanecer salva mesmo se a geração do brainstorm falhar. | RF003, RF018, RF020 | Falha de IA não pode causar perda da submissão. |
| RN020 | Uma resposta válida de brainstorm contém exatamente 3 soluções. | RF018 | Quantidade diferente invalida a resposta controlada. |
| RN021 | Cada solução indica uma abordagem SCAMPER aplicada. | RF018 | Sempre que possível, usar abordagens diferentes. |
| RN022 | Cada solução contém todos os critérios de impacto e esforço com notas permitidas, justificativa para cada nota e resultados finais calculados. | RF018 | As notas seguem as escalas das seções 5.3 e 5.4. |
| RN023 | A solução recomendada deve ser uma das 3 soluções geradas. | RF018 | `recommendedSolutionId` deve existir em `solutions`. |
| RN024 | A justificativa da recomendação considera impacto, esforço, viabilidade e riscos. | RF018 | Não escolher somente pela ambição. |
| RN025 | O Brainstorm Estratégico usa SCAMPER como framework principal. | RF018, RF019 | SCAMPER não substitui julgamento da Inovação. |
| RN026 | Os resultados ponderados da solução recomendada alimentam a classificação inicial da matriz. | RF007, RF018, RF019 | Inovação pode revisar as notas na triagem; o sistema recalcula os resultados finais. |
| RN027 | A matriz classifica quadrantes por regra objetiva usando os resultados finais arredondados. | RF007, RF008 | Ver seção 5.5. |
| RN028 | Ao converter ideia em projeto, o brainstorm deve ser copiado para o projeto interno. | RF009, RF010, RF020 | Preserva rastreabilidade da decisão. |
| RN029 | O Asana é ferramenta operacional; o portal mantém governança e dados principais. | RF009, RF013, RF016, RF021 | Falhas do Asana não apagam dados internos. |
| RN030 | Ações relevantes geram log funcional sem dados sensíveis. | RF003–RF022 | Logs apoiam auditoria e troubleshooting. |
| RN031 | O Brainstorm Estratégico deve ser registrado na descrição do projeto Asana criado pelo template obrigatório. | RF009, RF021 | Não criar task exclusiva de brainstorm. |
| RN032 | Falhas de IA ou Asana devem ser tratadas sem perda de dados principais. | RF003, RF009, RF018, RF021, RF022 | Registrar erro e permitir recuperação. |
| RN033 | Comentários operacionais de tarefas permanecem no Asana; comentários de governança ficam no portal. | RF014 | Evita duplicidade de ferramentas. |
| RN034 | O Canvas aceita somente e-mails terminados exatamente em `@nutriex.com.br`, `@nutriex.com`, `@innovapharma.com` ou `@rennova.com`, sem diferenciação entre maiúsculas e minúsculas. | RF003 | Remover espaços antes da validação e rejeitar qualquer outro domínio. |
| RN035 | Cada geração automática de brainstorm possui no máximo duas tentativas: tentativa inicial e uma retentativa automática. Após ambas falharem, Inovação pode tentar novamente no detalhe da ideia. | RF018, RF019 | Retentativas manuais não exigem versionamento completo. |
| RN036 | Todo projeto Asana originado pelo portal deve ser criado a partir do template `INV | Modelo Base`. | RF009, RF021 | Projeto vazio ou outro template devem ser bloqueados. |
| RN037 | A integração deve identificar o template pelo ID `1213945719343548`. | RF009, RF021 | O nome é referência funcional; o ID é a referência técnica. |
| RN038 | Seções, sprints, tarefas padrão, campos personalizados e configurações existentes no template devem ser preservados. | RF009, RF021 | Não recriar manualmente a estrutura. |
| RN039 | A conversão não pode ser marcada como concluída se o projeto Asana não for instanciado pelo template obrigatório ou se houver falha crítica sem recuperação registrada. | RF009, RF021 | Evita sucesso falso. |
| RN040 | O nome final do projeto será `INV | {nome informado no momento da conversão}`. | RF009, RF021 | Remover espaços excedentes e evitar prefixo duplicado. |
| RN041 | Entregas podem ser links ou arquivos em qualquer formato, armazenados no Supabase Storage, com limite de 50 MB por arquivo. | RF010 | Metadados e vínculo com o projeto ficam no banco. |
| RN042 | Comentários publicados não podem ser editados. O autor pode excluir o próprio comentário e Inovação pode excluir qualquer comentário por governança. | RF002, RF010, RF014 | Criação e exclusão devem ser auditadas. |
| RN043 | Arquivar ou rejeitar uma ideia exige justificativa em texto livre, data, responsável e registro dos participantes informados. | RF008, RF017 | Dados devem permanecer no histórico. |
| RN044 | O template Asana é considerado fixo para o escopo e não terá mecanismo de versionamento ou tratamento de alterações futuras. | RF009, RF021 | A integração continuará apontando para o mesmo ID. |
| RN045 | O Canvas somente pode ser exibido após validação válida do CAPTCHA. | RF003, RF004, RF022 | A verificação ocorre antes do preenchimento. |
| RN046 | Após o preenchimento, a IA decide se o Canvas possui informações suficientes para seguir ao resumo e ao brainstorm. | RF003, RF005, RF017, RF018, RF022 | Se considerar suficiente, nenhum modal é aberto. |
| RN047 | Quando necessário, a IA gera uma única rodada de até 10 perguntas objetivas, contextuais e não repetitivas; perguntas e respostas são persistidas e usadas nas etapas seguintes. | RF005, RF018, RF019, RF022 | As perguntas não devem exibir nem solicitar notas ao autor. |
| RN048 | Informações ainda incompletas após a rodada de complementação não bloqueiam a submissão; a IA pode inferir as notas e o brainstorm a partir do contexto disponível. | RF003, RF005, RF018, RF022 | Não haverá nova rodada de perguntas. |
| RN049 | Falha técnica na avaliação de suficiência não bloqueia nem apaga a submissão; o brainstorm permanece pendente até retentativa controlada pela Inovação. | RF003, RF017, RF018, RF019, RF022 | A falha deve ser registrada e recuperável. |

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

Regra: cada uma das 3 soluções deve indicar a abordagem SCAMPER aplicada.

### 5.2 Estrutura obrigatória de cada solução

Cada solução deve conter:

- abordagem SCAMPER aplicada;
- descrição da solução;
- racional estratégico;
- como resolve a demanda;
- notas dos critérios de impacto, respectivas justificativas e impacto final calculado;
- notas dos critérios de esforço, respectivas justificativas e esforço final calculado;
- análise de viabilidade;
- riscos principais;
- mitigações sugeridas.

### 5.3 Métrica de Impacto

A Métrica de Impacto representa o benefício potencial da ideia para a Rennova.

A nota final é calculada a partir dos critérios definidos nesta seção. Cada critério recebe uma das seguintes notas:

```text
2, 4, 6, 8 ou 10
```

Não são permitidas notas intermediárias.

O critério **Quantidade de áreas, usuários ou processos beneficiados** utiliza somente as notas `4`, `6`, `8` e `10`, conforme sua escala específica.

#### 5.3.1 Critérios, pesos e cálculo

| Critério | Peso |
|---|---:|
| Gravidade ou relevância da demanda | 20% |
| Ganho esperado de eficiência, receita, economia, qualidade ou compliance | 30% |
| Quantidade de áreas, usuários ou processos beneficiados | 20% |
| Potencial de escala ou reutilização em outras áreas | 20% |
| Urgência ou redução de risco relevante | 10% |

A nota final de Impacto deve ser calculada pela seguinte fórmula:

```text
Impacto =
(Gravidade da demanda × 0,20)
+ (Ganho esperado × 0,30)
+ (Alcance dos beneficiados × 0,20)
+ (Potencial de escala × 0,20)
+ (Urgência ou redução de risco × 0,10)
```

O resultado deve ser armazenado com uma casa decimal para garantir rastreabilidade.

Para classificação na matriz Impacto × Esforço, o resultado deve ser arredondado para o número inteiro mais próximo. Resultados terminados em `0,5` devem ser arredondados para cima.

A interpretação da nota final é:

| Nota final | Interpretação |
|---:|---|
| 2 a 3 | Impacto baixo |
| 4 a 6 | Impacto moderado |
| 7 a 8 | Impacto alto |
| 9 a 10 | Impacto estratégico ou crítico |

Quando a situação avaliada estiver entre duas descrições, deve ser utilizada a menor nota, salvo quando houver evidência suficiente para justificar a maior.

#### 5.3.2 Escalas ancoradas dos critérios

##### A. Gravidade ou relevância da demanda — Peso: 20%

Avalia o nível de prejuízo, limitação ou consequência causada pelo problema atual.

| Nota | Significado exato |
|---:|---|
| 2 | A demanda representa uma conveniência ou um problema pouco frequente, com impacto mínimo e sem prejuízo relevante. |
| 4 | O problema é recorrente, mas localizado, causando pequenos atrasos, retrabalho ou dificuldades operacionais em uma equipe. |
| 6 | O problema afeta de forma frequente a produtividade, a qualidade ou a execução de um processo de uma área ou departamento. |
| 8 | O problema afeta múltiplas equipes ou um processo importante, causando perdas relevantes, falhas frequentes, reclamações ou exposição significativa a risco. |
| 10 | O problema compromete processo crítico, resultado financeiro, cliente, qualidade, continuidade operacional ou obrigação legal, regulatória ou reputacional. |

##### B. Ganho esperado de eficiência, receita, economia, qualidade ou compliance — Peso: 30%

Avalia a intensidade do principal benefício mensurável esperado.

Deve ser utilizada a dimensão principal do benefício da ideia, como:

- redução de tempo;
- redução de custo;
- aumento de receita;
- redução de erros;
- aumento de produtividade;
- melhoria de qualidade;
- melhoria de compliance.

| Nota | Significado exato |
|---:|---|
| 2 | O ganho ainda não foi demonstrado ou representa melhoria inferior a 5% no indicador principal. |
| 4 | Ganho estimado entre 5% e 15% no indicador principal. |
| 6 | Ganho estimado entre 16% e 30% no indicador principal. |
| 8 | Ganho estimado entre 31% e 50% no indicador principal. |
| 10 | Ganho estimado superior a 50% ou eliminação de falha crítica de qualidade, segurança ou compliance. |

A justificativa deve registrar o indicador utilizado, seu valor atual e o ganho estimado.

Exemplo:

```text
Indicador: tempo médio de execução
Valor atual: 10 horas
Valor esperado: 7 horas
Ganho esperado: 30%
Nota: 6
```

##### C. Quantidade de áreas, usuários ou processos beneficiados — Peso: 20%

Avalia o alcance direto da solução dentro da estrutura organizacional.

| Nota | Significado exato |
|---:|---|
| 4 | Beneficia somente a própria equipe. |
| 6 | Beneficia de duas a três equipes. |
| 8 | Beneficia todo o departamento. |
| 10 | Beneficia departamentos pertencentes a outras gerências ou diretorias. |

Devem ser consideradas somente as equipes e os departamentos diretamente afetados ou beneficiados pela solução.

##### D. Potencial de escala ou reutilização em outras áreas — Peso: 20%

Avalia a possibilidade de reutilizar a solução além da demanda original.

| Nota | Significado exato |
|---:|---|
| 2 | Solução de uso único ou extremamente específica, sem possibilidade prática de reutilização. |
| 4 | Pode ser reutilizada somente dentro da própria equipe, exigindo adaptações relevantes ou reconstrução parcial. |
| 6 | Pode ser reutilizada em outros processos da mesma área ou em uma ou duas outras áreas, com adaptações moderadas. |
| 8 | Pode ser utilizada por múltiplas áreas com pequenas adaptações ou se tornar um componente, serviço ou processo padrão. |
| 10 | Pode ser aplicada amplamente como padrão corporativo, plataforma, produto ou capacidade estratégica reutilizável. |

##### E. Urgência ou redução de risco relevante — Peso: 10%

Avalia o prazo necessário para tratar a demanda ou o risco reduzido pela solução.

| Nota | Significado exato |
|---:|---|
| 2 | Não existe prazo relevante ou a demanda pode aguardar mais de 12 meses sem consequência significativa. |
| 4 | A demanda deve ser tratada entre 3 e 12 meses. |
| 6 | A demanda deve ser tratada entre 1 e 3 meses ou reduz risco operacional moderado. |
| 8 | A demanda deve ser tratada em até 30 dias ou está associada a auditoria, compromisso formal ou risco elevado. |
| 10 | Existe prazo obrigatório iminente, incidente ativo, risco de paralisação, segurança, perda relevante ou descumprimento legal ou regulatório. |

### 5.4 Métrica de Esforço

A Métrica de Esforço representa a quantidade de trabalho, complexidade e recursos necessários para implementar e manter a ideia.

Uma nota maior representa maior esforço de implementação.

A nota final é calculada a partir dos critérios definidos nesta seção. Cada critério recebe uma das seguintes notas:

```text
2, 4, 6, 8 ou 10
```

Não são permitidas notas intermediárias.

As notas não devem ser atribuídas por percepção livre. O avaliador deve identificar a descrição que melhor representa a situação da ideia e utilizar a nota correspondente.

#### 5.4.1 Critérios, pesos e cálculo

| Critério | Peso |
|---|---:|
| Complexidade técnica | 30% |
| Necessidade de integrações ou dados externos | 25% |
| Tempo estimado de implementação | 20% |
| Mudança operacional ou processual necessária | 15% |
| Custo estimado de implantação e manutenção | 10% |

A nota final de Esforço deve ser calculada pela seguinte fórmula:

```text
Esforço =
(Complexidade técnica × 0,30)
+ (Integrações ou dados externos × 0,25)
+ (Tempo estimado × 0,20)
+ (Mudança operacional × 0,15)
+ (Custo × 0,10)
```

O resultado deve ser armazenado com uma casa decimal para garantir rastreabilidade.

Para classificação na matriz Impacto × Esforço, o resultado deve ser arredondado para o número inteiro mais próximo. Resultados terminados em `0,5` devem ser arredondados para cima.

A interpretação da nota final é:

| Nota final | Interpretação |
|---:|---|
| 2 a 3 | Esforço baixo |
| 4 a 6 | Esforço moderado |
| 7 a 8 | Esforço alto |
| 9 a 10 | Esforço muito alto ou crítico |

Quando a situação avaliada estiver entre duas descrições, deve ser utilizada a maior nota, evitando a subestimação do esforço necessário.

#### 5.4.2 Escalas ancoradas dos critérios

##### A. Complexidade técnica — Peso: 30%

Avalia a dificuldade técnica da implementação considerando arquitetura, componentes, banco de dados, segurança e nível de conhecimento necessário.

| Nota | Significado exato |
|---:|---|
| 2 | Configuração simples ou pequena alteração localizada em um componente conhecido. |
| 4 | Desenvolvimento simples em um único componente ou alteração em múltiplos componentes do mesmo sistema, sem mudança relevante de arquitetura. |
| 6 | Nova funcionalidade com regras de negócio, persistência, alterações de banco de dados e testes relevantes. |
| 8 | Implementação envolvendo nova arquitetura parcial, nova tecnologia, múltiplos sistemas, migração de dados, segurança ou alta criticidade técnica. |
| 10 | Arquitetura crítica, grande incerteza técnica, necessidade de prova de conceito, viabilidade não comprovada ou redesenho estrutural da plataforma. |

##### B. Necessidade de integrações ou dados externos — Peso: 25%

Avalia a quantidade e a dificuldade das integrações ou dependências de dados externos.

| Nota | Significado exato |
|---:|---|
| 2 | Nenhuma integração é necessária ou será utilizada uma integração existente sem alterações. |
| 4 | Exige pequena alteração em integração existente ou uma nova integração simples e bem documentada. |
| 6 | Exige integração com autenticação, validação e tratamento de erros, duas novas integrações ou uma integração de média complexidade. |
| 8 | Exige três ou mais integrações, comunicação bidirecional ou assíncrona, dados sensíveis, alto volume ou dependência relevante de fornecedor. |
| 10 | Exige integração crítica com sistemas legados, instáveis ou pouco documentados, ou múltiplos sistemas externos sem ambiente de testes ou garantia de disponibilidade. |

##### C. Tempo estimado de implementação — Peso: 20%

Avalia o esforço total necessário para concluir a entrega.

O tempo deve incluir:

- levantamento e detalhamento;
- desenvolvimento;
- testes;
- correções;
- homologação;
- documentação;
- implantação.

A estimativa representa esforço de trabalho, e não tempo corrido aguardando outras áreas.

| Nota | Significado exato |
|---:|---|
| 2 | Até 3 dias úteis. |
| 4 | De 4 a 10 dias úteis. |
| 6 | De 11 a 22 dias úteis. |
| 8 | De 23 a 45 dias úteis. |
| 10 | Mais de 45 dias úteis. |

Exemplo:

```text
Tempo estimado: 18 dias úteis
Nota: 6
```

##### D. Mudança operacional ou processual necessária — Peso: 15%

Avalia o nível de alteração causado na rotina, no processo ou na forma de trabalho dos usuários.

| Nota | Significado exato |
|---:|---|
| 2 | Nenhuma mudança operacional relevante ou apenas alteração visual ou de configuração praticamente imperceptível ao usuário. |
| 4 | Pequena alteração em uma atividade ou em uma etapa de processo executada por uma equipe. |
| 6 | Mudança relevante em um processo de uma área, exigindo comunicação, orientação ou treinamento simples. |
| 8 | Mudança envolvendo múltiplas áreas, atualização de procedimentos, treinamento formal, transição e acompanhamento de adoção. |
| 10 | Transformação de processo crítico, mudança no modelo operacional ou transformação corporativa de grande alcance. |

##### E. Custo estimado de implantação e manutenção — Peso: 10%

Avalia o custo adicional necessário para implantar a solução e mantê-la durante os primeiros 12 meses.

Devem ser considerados:

- licenças;
- serviços de terceiros;
- infraestrutura;
- consumo de APIs;
- desenvolvimento contratado;
- suporte;
- manutenção;
- custos recorrentes.

Não deve ser considerado o custo do time interno quando ele já fizer parte da estrutura normal da área.

| Nota | Significado exato |
|---:|---|
| 2 | Sem custo adicional ou custo de até R$ 1.000. |
| 4 | De R$ 1.001 a R$ 10.000. |
| 6 | De R$ 10.001 a R$ 50.000. |
| 8 | De R$ 50.001 a R$ 250.000. |
| 10 | Acima de R$ 250.000. |

Quando o custo ainda não puder ser confirmado, deve ser utilizada a melhor estimativa disponível, registrando que o valor depende de orçamento ou validação.

### 5.5 Regra da matriz Impacto × Esforço

A matriz deve utilizar os resultados finais arredondados, calculados conforme as fórmulas das seções 5.3 e 5.4.

| Quadrante | Critério | Interpretação |
|---|---|---|
| Oportunidade Imediata | Impacto >= 7 e Esforço <= 4 | Alta prioridade. Considerar execução rápida. |
| Grande Projeto | Impacto >= 7 e Esforço >= 5 | Alta relevância, mas exige planejamento, sponsor e recursos. |
| Ganho Tático / Astuto | Impacto entre 4 e 6 e Esforço <= 4 | Pode avançar se houver capacidade ou ganho operacional claro. |
| Retorno Limitado | Impacto entre 4 e 6 e Esforço >= 5 | Baixa prioridade, salvo justificativa forte. |
| Baixa Atratividade | Impacto <= 3 | Normalmente não priorizar, salvo obrigação regulatória, compliance ou decisão estratégica. |

### 5.6 Recomendação da IA

A IA deve recomendar a solução com melhor equilíbrio entre:

- impacto;
- esforço;
- viabilidade;
- riscos controláveis;
- aderência à demanda original;
- possibilidade de execução no contexto da Rennova.

Quando o contexto permanecer incompleto após a rodada de complementação, a IA pode utilizar inferências coerentes para concluir a análise.

---

<a id="ef-6-fluxos-de-usuario"></a>
## 6. Fluxos de usuário

### 6.1 Acesso e submissão pública de ideia

```text
Colaborador acessa /canvas
  -> sistema exibe a verificação CAPTCHA
  -> colaborador conclui o CAPTCHA
  -> backend valida e libera o Canvas
  -> colaborador preenche identificação, e-mail, área/departamento e blocos
  -> solicita sugestões pontuais de IA, se necessário
  -> solicita continuar com a submissão
  -> sistema executa a avaliação de suficiência
  -> sistema gera o resumo com o contexto disponível
  -> colaborador revisa e aprova o resumo
  -> sistema valida domínio, sessão CAPTCHA e proteções anti-spam
  -> sistema salva a ideia e os dados complementares
  -> sistema inicia o Brainstorm Estratégico quando elegível
  -> sistema confirma a submissão
```

### 6.2 Avaliação de suficiência e complementação

```text
Canvas preenchido
  -> IA decide se as informações são suficientes
  -> se suficientes, segue diretamente para o resumo
  -> se insuficientes, IA gera até 10 perguntas estratégicas
  -> sistema abre um único modal de complementação
  -> colaborador responde integral ou parcialmente
  -> sistema incorpora as respostas ao contexto
  -> sistema segue para o resumo sem nova rodada
  -> se ocorrer falha técnica, permite o envio e mantém o brainstorm pendente
```

### 6.3 Geração do Brainstorm Estratégico IA

```text
Ideia salva e avaliação de suficiência concluída
  -> sistema realiza a primeira tentativa
  -> IA usa Canvas, complementação e resumo disponível
  -> IA usa SCAMPER e retorna 3 soluções estruturadas
  -> IA atribui notas permitidas aos critérios de impacto e esforço
  -> sistema valida o JSON e calcula os resultados ponderados
  -> se válido, salva o brainstorm e define classificação inicial
  -> se falhar, realiza uma segunda tentativa automática
  -> se a segunda tentativa falhar, marca erro
  -> detalhe da ideia disponibiliza retentativa manual para Inovação
```

### 6.4 Triagem de ideia

```text
Inovação acessa /ideias?aba=triagem
  -> abre detalhe da ideia
  -> consulta Canvas, complementação, resumo IA, brainstorm, solução recomendada e matriz
  -> revisa as notas dos critérios de impacto e esforço
  -> sistema recalcula impacto_final e esforco_final
  -> decide Backlog, Arquivar/Rejeitar ou Vira Projeto
  -> arquivamento exige justificativa e auditoria
  -> Diretoria pode consultar os dados, sem registrar decisão
```

### 6.5 Conversão em projeto com Asana

```text
Inovação aciona Vira Projeto
  -> sistema abre campo obrigatório para nome do projeto
  -> usuário informa o nome
  -> sistema valida permissão, notas finais, nome e idempotência
  -> sistema cria projeto interno
  -> sistema copia o Brainstorm Estratégico para o projeto interno
  -> sistema instancia o template Asana 1213945719343548
  -> sistema aguarda a criação pelo template INV | Modelo Base
  -> sistema aplica o nome INV | {nome informado}
  -> sistema preenche a descrição do projeto com o brainstorm
  -> sistema configura owner, portfólio e webhook
  -> sistema registra vínculo e logs
  -> ideia passa para status virou_projeto
```

### 6.6 Sincronização Asana → Portal

```text
Asana envia webhook ao ocorrer alteração
  -> Edge Function processa o evento
  -> atualiza cache em asana_sync
  -> cron diário executa reconciliação
  -> dashboard e bloco Asana leem os dados cacheados
```

### 6.7 Gestão de entregas

```text
Inovação acessa o detalhe do projeto
  -> adiciona link ou seleciona arquivo
  -> sistema valida link ou limite de 50 MB
  -> arquivo é enviado ao Supabase Storage
  -> metadados são registrados no banco
  -> Diretoria e Inovação acessam a entrega
```

---

<a id="ef-7-mapa-de-navegacao"></a>
## 7. Mapa de navegação

| Rota | Acesso | Objetivo |
|---|---|---|
| `/canvas` | Público | Validação CAPTCHA e submissão de ideias por colaboradores |
| `/login` | Público | Login no portal interno |
| `/` ou `/dashboard` | Diretoria / Inovação | Visão executiva do portfólio |
| `/ideias?aba=backlog` | Diretoria / Inovação | Backlog de ideias |
| `/ideias?aba=matriz` | Diretoria / Inovação | Matriz Impacto × Esforço |
| `/ideias?aba=triagem` | Diretoria / Inovação | Triagem; leitura para Diretoria e gestão para Inovação |
| `/ideias?aba=arquivadas` | Diretoria / Inovação | Histórico de ideias arquivadas ou rejeitadas |
| `/ideias/:id` | Diretoria / Inovação | Detalhe da ideia, complementação, resumo IA e brainstorm |
| `/projetos` | Diretoria / Inovação | Lista de projetos de inovação |
| `/projetos/:id` | Diretoria / Inovação | Detalhe, governança, entregas, fases, métricas e Asana |
| `/admin` | Inovação / Admin | Departamentos e usuários |

As rotas independentes `/matriz` e `/triagem` não fazem parte da navegação final.

---

<a id="ef-8-telas-e-comportamento-visual"></a>
## 8. Telas e comportamento visual

### Tela 1 - Canvas público

- Deve ser simples, sem login e responsivo.
- Ao acessar `/canvas`, deve exibir inicialmente somente a verificação CAPTCHA.
- O Canvas deve ser exibido apenas após validação válida do CAPTCHA.
- Deve conter nome, e-mail, área/departamento em texto livre e blocos da ideia.
- Deve validar os quatro domínios corporativos autorizados.
- Pode oferecer sugestões de IA por bloco.
- Ao continuar, deve exibir estado de análise enquanto a IA avalia a suficiência.
- Quando necessário, deve abrir modal com uma única rodada de até 10 perguntas estratégicas.
- O modal deve permitir respostas em texto livre e conclusão com respostas parciais.
- Se o Canvas for considerado suficiente, o modal não deve ser aberto.
- Deve permitir revisão do resumo IA após a avaliação ou complementação.
- Não deve mostrar notas de impacto/esforço ao autor.
- Deve alertar sobre perda dos dados quando o usuário tentar sair antes do envio.
- Após envio, deve exibir confirmação clara.

### Tela 2 - Login

- Deve permitir autenticação por e-mail e senha.
- Deve tratar credenciais inválidas sem expor detalhes técnicos.
- Deve redirecionar usuário autenticado conforme o perfil.
- Deve usar o comportamento padrão de sessão do Supabase Auth.

### Tela 3 - Dashboard

- Deve mostrar indicadores consolidados de ideias, projetos, status, fases, riscos e evolução.
- Deve consumir dados do Supabase e cache do Asana.
- Não deve executar chamadas diretas ao Asana em tempo real.

### Tela 4 - Gestão de ideias

A rota `/ideias` deve organizar o conteúdo em abas:

- Backlog;
- Matriz Impacto × Esforço;
- Triagem;
- Arquivadas.

A listagem deve apresentar, conforme aplicável:

- nome ou resumo da ideia;
- status;
- origem;
- área impactada;
- data;
- impacto;
- esforço;
- quadrante;
- status da avaliação de suficiência;
- status do brainstorm.

O detalhe da ideia deve exibir:

- descrição original;
- Canvas e respostas principais;
- resultado da avaliação de suficiência;
- perguntas estratégicas e respostas complementares, quando existentes;
- resumo IA;
- classificação IA;
- status do brainstorm;
- Brainstorm Estratégico com 3 soluções;
- solução recomendada destacada;
- notas de cada critério de impacto e esforço, pesos e resultados finais calculados;
- análise de viabilidade;
- riscos e mitigações;
- ação de retentativa da avaliação ou do brainstorm para Inovação, quando aplicável;
- ações de backlog, arquivar/rejeitar e converter conforme permissão.

A aba Triagem deve:

- apoiar a decisão da Inovação;
- permitir consulta das respostas complementares;
- permitir revisão das notas dos critérios de impacto e esforço;
- recalcular automaticamente os resultados finais ponderados;
- registrar decisão, responsável, participantes e data;
- permitir consulta integral pela Diretoria.

A aba Arquivadas deve mostrar:

- justificativa;
- data da decisão;
- usuário responsável;
- participantes informados;
- acesso ao detalhe em leitura.

### Tela 5 - Conversão em projeto

Ao acionar “Vira Projeto”, deve ser exibido diálogo ou etapa de confirmação com:

- campo de texto obrigatório “Nome do projeto”;
- prévia do nome final `INV | {nome informado}`;
- notas finais de impacto e esforço;
- aviso de uso obrigatório do template `INV | Modelo Base`;
- confirmação explícita para conversão sem brainstorm, quando aplicável;
- botão de confirmar e botão de cancelar.

### Tela 6 - Detalhe do projeto

- Deve mostrar objetivo, problema, descrição, fase, checklist, próximos passos, histórico, métricas e comentários.
- Deve exibir o brainstorm herdado da ideia.
- Deve conter seção “Entregas” para links e arquivos.
- Deve permitir upload de arquivos de qualquer formato, até 50 MB por arquivo, somente para Inovação.
- Deve permitir consulta e download das entregas por Diretoria e Inovação.
- Deve conter bloco Asana somente leitura com dados operacionais sincronizados.
- Deve exibir link “Abrir no Asana”.
- Deve indicar status e data da última sincronização.

### Tela 7 - Admin

- Deve permitir manutenção de departamentos e usuários conforme permissão.
- Deve impedir autoelevação indevida de perfil.
- O cadastro de departamentos não deve limitar o campo aberto do Canvas público.

---

<a id="ef-9-requisitos-nao-funcionais"></a>
## 9. Requisitos não funcionais

| Código | Requisito |
|---|---|
| RNF001 | A interface deve manter a identidade visual do protótipo Lovable. |
| RNF002 | A primeira versão deve priorizar desktop e responsividade web básica. |
| RNF003 | Chaves de IA, Asana e Supabase `service_role` não podem estar no front-end. |
| RNF004 | Operações sensíveis devem passar por Edge Functions. |
| RNF005 | RLS deve proteger dados internos e o acesso ao Supabase Storage. |
| RNF006 | Respostas de IA devem ser validadas antes da persistência. |
| RNF007 | Falhas de IA e Asana devem ser tratadas sem perda dos dados principais. |
| RNF008 | Logs não devem armazenar tokens, senhas, chaves, prompts sensíveis completos ou dados desnecessários. |
| RNF009 | Dashboard deve usar dados cacheados para evitar chamadas externas em tempo real. |
| RNF010 | O sistema deve permitir retentativa controlada em falhas de integração. |
| RNF011 | O token CAPTCHA deve ser validado no backend antes da exibição do Canvas e não pode ser considerado válido apenas pelo estado do front-end. |
| RNF012 | Validação de domínios de e-mail deve ser feita no backend, sem diferenciação de maiúsculas e minúsculas. |
| RNF013 | Upload deve ser interrompido antes da persistência quando o arquivo exceder 50 MB. |
| RNF014 | Arquivos armazenados não devem ser executados pelo portal; devem ser disponibilizados como conteúdo de entrega. |
| RNF015 | A sessão seguirá os padrões de persistência, expiração e renovação do Supabase Auth. |
| RNF016 | A criação do projeto Asana deve ser idempotente e impedir duplicidade em retentativas. |
| RNF017 | O identificador do template Asana deve ser configurado em ambiente seguro e validado pela Edge Function. |
| RNF018 | O webhook será o mecanismo principal de atualização do Asana e o cron diário será o mecanismo de reconciliação. |
| RNF019 | A avaliação de suficiência, as perguntas e as respostas devem usar JSON estruturado e validação de esquema. |
| RNF020 | Falha técnica na avaliação de suficiência deve permitir a submissão e manter o brainstorm recuperável, sem perda dos dados da ideia. |

---

<a id="ef-10-mensagens-do-sistema"></a>
## 10. Mensagens do sistema

| Situação | Mensagem sugerida |
|---|---|
| CAPTCHA necessário | Confirme a verificação de segurança para acessar o Canvas. |
| CAPTCHA inválido ou expirado | A verificação de segurança expirou ou não é válida. Realize a validação novamente. |
| CAPTCHA indisponível | A verificação de segurança está temporariamente indisponível. Tente novamente mais tarde. |
| Analisando informações | Estamos analisando as informações da ideia. |
| Complementação necessária | Precisamos de algumas informações adicionais para compreender melhor a ideia. |
| Falha na avaliação de suficiência | Não foi possível concluir a análise complementar. A ideia ainda poderá ser enviada. |
| Complementação salva | Informações adicionais registradas com sucesso. |
| Ideia enviada | Ideia enviada com sucesso. A área de Inovação fará a análise. |
| Falha ao enviar ideia | Ocorreu um erro na plataforma e não foi possível enviar a ideia. Tente novamente. Caso o problema persista por mais de 24 horas, entre em contato com o time de Inovação pelo Teams. |
| E-mail não autorizado | Utilize um e-mail corporativo autorizado para enviar a ideia. |
| Saída com dados não enviados | Os dados preenchidos ainda não foram enviados e serão perdidos se você sair desta página. |
| IA indisponível | A ideia foi salva, mas a análise por IA não pôde ser gerada no momento. |
| Brainstorm aguardando avaliação | A ideia foi salva e o brainstorm será gerado após a recuperação da análise complementar. |
| Brainstorm gerado | Brainstorm Estratégico gerado com sucesso. |
| Brainstorm em segunda tentativa | A primeira geração não foi concluída. Uma nova tentativa está sendo realizada. |
| Brainstorm com erro | Não foi possível gerar o brainstorm após duas tentativas. Use “Tentar novamente” na visualização da ideia. |
| Arquivamento sem justificativa | Informe o motivo do arquivamento para concluir a decisão. |
| Notas finais ausentes | Informe as notas finais de impacto e esforço antes de transformar a ideia em projeto. |
| Nome do projeto ausente | Informe o nome do projeto para continuar. |
| Conversão concluída | Projeto criado com sucesso a partir do modelo padrão e integrado ao Asana. |
| Template Asana indisponível | Não foi possível acessar o modelo `INV | Modelo Base`. O projeto não foi concluído. |
| Falha ao criar pelo template | Não foi possível criar o projeto a partir do modelo oficial do Asana. Tente novamente ou acione o suporte responsável. |
| Falha na descrição Asana | O projeto foi criado no Asana, mas o Brainstorm Estratégico ainda não foi registrado na descrição. |
| Falha parcial no Asana | Projeto criado no portal, mas houve falha parcial na integração com o Asana. A recuperação poderá ser tentada novamente. |
| Arquivo acima do limite | O arquivo excede o limite de 50 MB. Selecione outro arquivo. |
| Upload concluído | Entrega adicionada com sucesso. |
| Comentário não editável | Comentários publicados não podem ser editados. Exclua o comentário e publique um novo, se necessário. |
| Acesso negado | Você não tem permissão para executar esta ação. |

---

<a id="ef-11-criterios-de-aceite-consolidados"></a>
## 11. Critérios de aceite consolidados

| Código | Critério |
|---|---|
| CA001 | Colaborador sem login acessa `/canvas`, mas o Canvas somente é exibido após CAPTCHA validado no backend. |
| CA002 | São aceitos somente `@nutriex.com.br`, `@nutriex.com`, `@innovapharma.com` e `@rennova.com`. |
| CA003 | Tentativa de sair antes da submissão apresenta aviso e dados não enviados não são persistidos. |
| CA004 | Sistema gera resumo IA com o Canvas e a complementação existente ou permite salvar a ideia mesmo em caso de falha da IA. |
| CA005 | Sistema gera Brainstorm Estratégico com exatamente 3 soluções baseadas em SCAMPER. |
| CA006 | Cada solução apresenta descrição, racional, resolução da demanda, impacto, esforço, viabilidade, riscos e mitigações. |
| CA007 | Uma solução é recomendada pela IA com justificativa. |
| CA008 | Cada critério de impacto e esforço utiliza somente as notas permitidas em sua escala; os resultados finais são calculados pelas fórmulas ponderadas. |
| CA009 | Em caso de falha, o sistema realiza no máximo duas tentativas automáticas de brainstorm e depois disponibiliza retentativa manual para Inovação. |
| CA010 | Matriz classifica a ideia no quadrante correto e está disponível como aba de `/ideias`. |
| CA011 | Inovação pode revisar as notas dos critérios na triagem; o sistema recalcula impacto e esforço finais; Diretoria consulta critérios, pesos e resultados sem editar. |
| CA012 | “Vira Projeto” é bloqueado sem `impacto_final` e `esforco_final` válidos. |
| CA013 | Arquivar ou rejeitar exige justificativa e registra responsável, data e participantes informados. |
| CA014 | Ideias arquivadas permanecem acessíveis na aba de histórico. |
| CA015 | Conversão solicita obrigatoriamente o nome do projeto. |
| CA016 | Conversão cria projeto interno e preserva vínculo com a ideia original. |
| CA017 | Nome final do projeto segue `INV | {nome informado}`. |
| CA018 | Projeto Asana é criado obrigatoriamente pelo template `INV | Modelo Base`, ID `1213945719343548`. |
| CA019 | Estrutura de seções, sprints, tarefas padrão e campos do template é preservada. |
| CA020 | Brainstorm é copiado para o projeto interno e registrado na descrição do projeto Asana. |
| CA021 | Nenhuma task exclusiva chamada `Brainstorm Estratégico IA` é criada. |
| CA022 | Falha no Asana não causa perda do projeto interno nem criação duplicada em retentativa. |
| CA023 | Detalhe do projeto permite à Inovação adicionar links e arquivos de qualquer formato, limitados a 50 MB por arquivo, usando Supabase Storage. |
| CA024 | Diretoria e Inovação conseguem consultar e baixar entregas autorizadas. |
| CA025 | Diretoria e Inovação podem criar comentários de governança; comentários não podem ser editados. |
| CA026 | Autor pode excluir o próprio comentário e Inovação pode excluir qualquer comentário com registro de auditoria. |
| CA027 | Bloco Asana apresenta dados cacheados, incluindo status, responsável e datas das tarefas quando disponíveis. |
| CA028 | Sessão autenticada segue o comportamento padrão do Supabase Auth. |
| CA029 | Ações relevantes geram log funcional sem dados sensíveis. |
| CA030 | RF001–RF022 mantêm a estrutura padrão de especificação funcional. |
| CA031 | A IA decide se o Canvas possui informações suficientes; quando suficiente, nenhum modal de perguntas é aberto. |
| CA032 | Quando a IA considerar o Canvas insuficiente, o sistema abre uma única rodada com no máximo 10 perguntas estratégicas. |
| CA033 | As perguntas são contextuais, objetivas, não repetem informações já preenchidas e não exibem notas de impacto ou esforço ao autor. |
| CA034 | Perguntas e respostas complementares são persistidas, exibidas no detalhe interno e utilizadas no resumo, nas notas e no brainstorm. |
| CA035 | Respostas parciais ou informações ainda incompletas após a rodada não bloqueiam a submissão nem geram uma segunda rodada. |
| CA036 | A IA pode inferir notas e soluções com base no contexto disponível após a complementação. |
| CA037 | Falha técnica na avaliação de suficiência não causa perda nem bloqueio da ideia; o brainstorm permanece pendente até retentativa controlada. |

---

<a id="ef-12-decisoes-funcionais-consolidadas"></a>
## 12. Decisões funcionais consolidadas

| Código | Decisão | Definição final |
|---|---|---|
| PD001 | Permitir conversão sem brainstorm gerado? | Sim, somente com confirmação explícita da Inovação. |
| PD002 | Permitir regerar brainstorm? | Sim. Serão realizadas duas tentativas automáticas; após falha, Inovação poderá tentar novamente no detalhe da ideia. Não haverá versionamento completo no MVP. |
| PD003 | Usar notas das 3 soluções ou somente da recomendada? | Salvar as notas dos critérios e os resultados ponderados das 3 soluções; usar os resultados da solução recomendada para a matriz inicial. |
| PD004 | Onde registrar o brainstorm no Asana? | Na descrição do projeto. |
| PD005 | Criar task inicial para o brainstorm? | Não. Nenhuma task exclusiva será criada. |
| PD006 | Como as notas finais de impacto e esforço serão calculadas? | A IA ou a Inovação atribui somente as notas permitidas nas escalas das seções 5.3 e 5.4; o sistema aplica as fórmulas ponderadas e calcula os resultados finais. |
| PD007 | Onde ficam matriz e triagem? | Em abas dentro de `/ideias`. |
| PD008 | Quais domínios podem submeter ideias? | `@nutriex.com.br`, `@nutriex.com`, `@innovapharma.com` e `@rennova.com`. |
| PD009 | Como funcionará a sessão? | Será mantido o padrão do Supabase Auth, sem timeout customizado. |
| PD010 | Notas finais são obrigatórias para conversão? | Sim. Impacto final e esforço final válidos são obrigatórios. |
| PD011 | Onde armazenar arquivos de entrega? | Supabase Storage. Qualquer formato, até 50 MB por arquivo. |
| PD012 | Comentários podem ser editados? | Não. Somente exclusão conforme permissão. |
| PD013 | Como será definido o nome do projeto? | No RF009, o usuário informa o nome em campo obrigatório; o nome final será `INV | {nome informado}`. |
| PD014 | Qual template Asana utilizar? | `INV | Modelo Base`, identificado pelo ID `1213945719343548`. |
| PD015 | O sistema pode criar projeto vazio se o template falhar? | Não. A conversão permanece incompleta e deve permitir recuperação controlada. |
| PD016 | O template terá versionamento ou tratamento de mudanças futuras? | Não. O template é considerado fixo e não haverá alterações futuras neste escopo. |
| PD017 | Como o campo de departamento funcionará no Canvas? | Será campo aberto de texto e não dependerá do cadastro interno de departamentos. |
| PD018 | Diretoria pode acessar a triagem? | Sim, em leitura, sem alterar notas ou decisões. |
| PD019 | Diretoria pode comentar? | Sim. Diretoria e Inovação podem criar comentários de governança. |
| PD020 | Como arquivamentos serão registrados? | Justificativa obrigatória, data, responsável e participantes informados. |
| PD021 | Quando o CAPTCHA será solicitado? | Antes da exibição do Canvas. O usuário só acessará o formulário após validação válida no backend. |
| PD022 | Quem decide se o Canvas possui informações suficientes? | O modelo de IA, com base no conteúdo preenchido. |
| PD023 | Como funcionará a complementação estratégica? | Haverá somente uma rodada, com até 10 perguntas geradas pela IA e exibidas em modal apenas quando necessárias. |
| PD024 | Informações incompletas após a complementação bloqueiam o envio? | Não. A submissão prossegue e a IA pode inferir as notas e o brainstorm com o contexto disponível. |
| PD025 | Onde as perguntas e respostas serão disponibilizadas? | Serão persistidas com a ideia e exibidas no detalhe interno para Inovação e Diretoria. |
| PD026 | O que acontece se a avaliação de suficiência falhar tecnicamente? | A ideia pode ser enviada e salva; o brainstorm permanece pendente até retentativa controlada pela Inovação. |

---

<a id="ef-13-aprovacao-funcional"></a>
## 13. Aprovação funcional

| Papel | Nome | Status | Data |
|---|---|---|---|
| Responsável funcional | A definir | Pendente | - |
| Responsável técnico | Phablo Tavares | Pendente | - |
| Gerência solicitante | A definir | Pendente | - |