# Especificação Funcional — Portal de Gestão da Inovação Rennova

> Fonte funcional para orientar construção, aceite e evolução do **Rennova Spark Hub**.  
> Versão consolidada com a funcionalidade de **Brainstorm Estratégico com IA baseado em SCAMPER**, incluindo matriz Impacto × Esforço 1–10 e envio do brainstorm para task inicial no Asana.

---

<a id="sumario"></a>
## Sumário

- [1. Identificação do projeto](#ef-1-identificacao-do-projeto)
- [2. Visão geral](#ef-2-visao-geral)
- [3. Escopo](#ef-3-escopo)
- [4. Requisitos funcionais](#ef-4-requisitos-funcionais)
- [5. Regras de negócio](#ef-5-regras-de-negocio)
- [6. Fluxos de usuário](#ef-6-fluxos-de-usuario)
- [7. Mapa de navegação](#ef-7-mapa-de-navegacao)
- [8. Telas e comportamento visual](#ef-8-telas-e-comportamento-visual)
- [9. Requisitos não funcionais](#ef-9-requisitos-nao-funcionais)
- [10. Mensagens do sistema](#ef-10-mensagens-do-sistema)
- [11. Critérios de aceite consolidados](#ef-11-criterios-de-aceite-consolidados)
- [12. Pendências e decisões funcionais](#ef-12-pendencias-e-decisoes-funcionais)
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
| Versão | 0.4 |
| Alteração desta versão | Inclusão do Brainstorm Estratégico com IA, SCAMPER, notas 1–10 de impacto/esforço e task inicial no Asana |

---

<a id="ef-2-visao-geral"></a>
## 2. Visão geral

### 2.1 Contexto

A área de Inovação da Rennova recebe ideias de diferentes áreas, avalia potencial, prioriza iniciativas e acompanha projetos aprovados. Parte desse processo hoje fica dispersa entre conversas, documentos, planilhas e ferramentas operacionais.

O portal deve centralizar entrada de ideias, apoio por IA, triagem, priorização, conversão em projetos, governança e acompanhamento executivo.

Já existe um protótipo visual no Lovable/GitHub com Dashboard, Projetos, Detalhe de Projeto e Ideias usando dados mockados. A entrega alvo deve transformar o protótipo em produto funcional com Supabase, autenticação, banco real, IA e integração com Asana.

### 2.2 Objetivo

Construir um portal interno para centralizar a gestão da inovação na Rennova, permitindo que:

- colaboradores submetam ideias;
- a IA apoie a estruturação e análise inicial das ideias;
- a área de Inovação qualifique, priorize e converta ideias em projetos;
- a Diretoria acompanhe o portfólio em visão executiva;
- projetos aprovados sejam integrados ao Asana para execução operacional.

### 2.3 Público-alvo / usuários

| Ator / Perfil | Responsabilidade | Principais ações |
|---|---|---|
| Colaborador / Autor da ideia | Submeter ideia pelo Canvas público | Preencher Canvas, solicitar sugestões de IA, revisar resumo e aprovar submissão |
| Inovação | Gerir funil e governança da inovação | Triar ideias, revisar impacto/esforço, consultar brainstorm, converter ideias, gerir projetos e cadastros |
| Diretoria | Acompanhar portfólio em visão executiva | Consultar dashboard, matriz, detalhes de ideias/projetos e evolução do portfólio |
| Administrador funcional | Gerir cadastros básicos | Gerenciar departamentos e perfis de usuários |
| Sistema / Integrações | Executar automações | Gerar IA, criar projetos no Asana, criar task inicial, sincronizar dados e registrar logs |

---

<a id="ef-3-escopo"></a>
## 3. Escopo

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
- [ ] Sincronização Asana → Portal por webhook e cron de reconciliação.
- [ ] Administração de departamentos e usuários.
- [ ] Logs de auditoria para ações relevantes.

### 3.2 Fora de escopo

- Substituir o Asana como ferramenta operacional de tarefas.
- Editar tarefas do Asana dentro do portal.
- SSO corporativo na primeira versão.
- Aplicativo mobile nativo.
- Gestão financeira detalhada de orçamento, custos ou CAPEX/OPEX.
- Workflow completo de aprovação multinível fora da triagem de Inovação.
- BI avançado fora dos indicadores previstos no dashboard.
- Migração automática de dados históricos não estruturados.
- Integrações com ERP, CRM, e-mail ou sistemas internos além do Asana.
- Acompanhamento da evolução da ideia pelo autor após aprovação, salvo definição em nova fase.
- Edição colaborativa avançada ou versionamento completo de múltiplos brainstorms.
- Treinamento de modelo próprio de IA.
- Cálculo financeiro detalhado de ROI por IA.

### 3.3 Premissas

- Lovable continuará sendo a principal ferramenta de evolução do front-end.
- Supabase será usado para Auth, Postgres, RLS e Edge Functions.
- Asana será a fonte operacional de tarefas e sprints.
- Supabase será a fonte de verdade para ideias, triagem, governança, métricas, usuários e visão executiva.
- Tokens de Asana e IA ficarão somente em secrets nas Edge Functions.
- Respostas de IA serão estruturadas em JSON e validadas antes de gravação.
- O Brainstorm Estratégico deve usar SCAMPER como base de ideação.
- A task inicial do Asana será o local operacional para registrar o brainstorm completo do projeto convertido.
- A primeira versão priorizará desktop e responsividade básica para web.

### 3.4 Restrições

- Não expor chaves, tokens ou `service_role` no front-end.
- Não chamar Asana nem provedores de IA diretamente pelo browser.
- Evitar edição manual ampla do front-end fora do Lovable.
- Proteger o formulário público contra spam.
- Não exibir impacto/esforço ao autor da ideia no Canvas público.
- Aplicar permissões no front-end e reforçar por RLS/Edge Functions.
- Não depender de chamada ao Asana em tempo real no dashboard.
- Não gravar resposta de IA sem validação mínima de estrutura.

---

<a id="ef-4-requisitos-funcionais"></a>
## 4. Requisitos funcionais

> Cada RF consolida comportamento, exceções e aceite. As regras detalhadas estão na seção [5. Regras de negócio](#ef-5-regras-de-negocio).

### RF001 - Autenticação no portal interno

| Item | Especificação |
|---|---|
| Descrição | Permitir login no portal interno por e-mail e senha via Supabase Auth. |
| Ator | Diretoria e Inovação. |
| Critérios de aceite | Usuário ativo com credenciais válidas acessa Dashboard; usuário inativo é bloqueado; usuário não autenticado em rota interna é enviado para `/login`. |
| Regras | RN001, RN002, RN003. |

### RF002 - Controle de acesso por perfil

| Item | Especificação |
|---|---|
| Descrição | Restringir funcionalidades conforme perfil `diretoria` ou `inovacao`. |
| Ator | Sistema. |
| Critérios de aceite | Diretoria consulta dados em leitura; Inovação acessa triagem, admin e ações de gestão; permissões são reforçadas por RLS/Edge Functions. |
| Regras | RN001, RN002, RN003, RN027. |

### RF003 - Submissão de ideia pelo Canvas público

| Item | Especificação |
|---|---|
| Descrição | Permitir que colaborador envie ideia pela rota pública `/canvas`, sem login. |
| Ator | Colaborador. |
| Fluxo principal | 1. Acessar `/canvas`.<br>2. Preencher dados do solicitante, departamentos e blocos do Canvas.<br>3. Enviar ideia.<br>4. Sistema valida dados e anti-spam.<br>5. Sistema grava a ideia.<br>6. Sistema inicia a geração de resumo e brainstorm por IA. |
| Exceções | Campos obrigatórios vazios; e-mail inválido; rate limit; falha de gravação. |
| Critérios de aceite | Ideia válida é gravada; autor recebe confirmação; ideia fica disponível para Inovação. |
| Regras | RN004, RN005, RN006, RN018. |

### RF004 - Sugestão de IA por bloco do Canvas

| Item | Especificação |
|---|---|
| Descrição | Permitir que o colaborador solicite ajuda da IA para melhorar o preenchimento de blocos do Canvas. |
| Ator | Colaborador / Sistema IA. |
| Critérios de aceite | IA retorna sugestão útil sem substituir automaticamente o texto do usuário; usuário decide aceitar, ajustar ou descartar. |
| Regras | RN007, RN008. |

### RF005 - Resumo de IA e aprovação pelo autor

| Item | Especificação |
|---|---|
| Descrição | Gerar resumo consolidado da ideia por IA e permitir que o autor revise antes da submissão final. |
| Ator | Colaborador / Sistema IA. |
| Critérios de aceite | Resumo é apresentado ao autor; autor pode aprovar ou ajustar; ideia final mantém texto aprovado. |
| Regras | RN007, RN008, RN009. |

### RF006 - Dashboard executivo

| Item | Especificação |
|---|---|
| Descrição | Exibir visão executiva do portfólio de inovação. |
| Ator | Diretoria e Inovação. |
| Critérios de aceite | Dashboard exibe indicadores de ideias, projetos, status, fases, riscos e dados cacheados do Asana. |
| Regras | RN010, RN011. |

### RF007 - Matriz Impacto × Esforço

| Item | Especificação |
|---|---|
| Descrição | Exibir e classificar ideias e soluções usando notas de impacto e esforço em escala 1–10. |
| Ator | Diretoria e Inovação. |
| Fluxo principal | 1. Sistema obtém impacto/esforço da solução recomendada pela IA.<br>2. Sistema classifica a ideia em quadrante.<br>3. Inovação pode revisar notas durante triagem.<br>4. Matriz exibe posição atualizada. |
| Critérios de aceite | Ideias elegíveis aparecem na matriz; quadrante segue regra documentada; notas podem ser revisadas pela Inovação. |
| Regras | RN012, RN013, RN014, RN015, RN025, RN026. |

### RF008 - Triagem mensal de ideias

| Item | Especificação |
|---|---|
| Descrição | Permitir que a área de Inovação analise, priorize, aprove, rejeite ou mantenha ideias em análise. |
| Ator | Inovação. |
| Critérios de aceite | Inovação visualiza ideia, resumo, brainstorm, matriz e dados de origem antes de decidir. |
| Regras | RN016, RN017, RN026. |

### RF009 - Conversão de ideia em projeto

| Item | Especificação |
|---|---|
| Descrição | Converter uma ideia aprovada em projeto interno e projeto operacional no Asana. |
| Ator | Inovação / Sistema. |
| Fluxo principal | 1. Inovação aciona conversão.<br>2. Sistema valida dados mínimos.<br>3. Sistema cria projeto interno.<br>4. Sistema copia brainstorm estratégico para o projeto.<br>5. Sistema cria projeto no Asana.<br>6. Sistema cria task inicial `Brainstorm Estratégico IA` no Asana. |
| Exceções | Falha ao criar projeto interno; falha no Asana; brainstorm ausente; permissão insuficiente. |
| Critérios de aceite | Projeto interno é criado; ideia muda para convertida; Asana recebe projeto e task inicial; vínculo com ideia original é preservado. |
| Regras | RN021, RN022, RN027, RN028. |

### RF010 - Detalhe e governança do projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir dados completos do projeto, incluindo objetivo, problema, descrição, fase, checklist, histórico, métricas, comentários e brainstorm herdado da ideia. |
| Ator | Diretoria e Inovação. |
| Critérios de aceite | Detalhe do projeto mostra informações de governança e mantém rastreabilidade com a ideia original. |
| Regras | RN023, RN024, RN027. |

### RF011 - Gestão de fases e checklist executivo

| Item | Especificação |
|---|---|
| Descrição | Gerenciar fases do projeto e checklist executivo. |
| Ator | Inovação. |
| Critérios de aceite | Fases seguem fluxo definido; checklist pode ser atualizado por Inovação; Diretoria visualiza em leitura. |
| Regras | RN023, RN027. |

### RF012 - Métricas, resultados e insight de IA

| Item | Especificação |
|---|---|
| Descrição | Registrar métricas e resultados do projeto e permitir geração de insight executivo por IA. |
| Ator | Inovação / Sistema IA. |
| Critérios de aceite | Métricas são salvas; insight IA é gerado por Edge Function; respostas inválidas não são persistidas. |
| Regras | RN007, RN008, RN024. |

### RF013 - Bloco Asana no projeto

| Item | Especificação |
|---|---|
| Descrição | Exibir no portal dados sincronizados do projeto Asana em modo somente leitura. |
| Ator | Diretoria e Inovação. |
| Critérios de aceite | Bloco Asana mostra status operacional cacheado; portal não edita tasks do Asana. |
| Regras | RN010, RN011, RN029. |

### RF014 - Comentários de governança

| Item | Especificação |
|---|---|
| Descrição | Permitir comentários internos de governança no projeto. |
| Ator | Inovação. |
| Critérios de aceite | Comentários são salvos com autor e data; Diretoria pode consultar. |
| Regras | RN030. |

### RF015 - Administração de departamentos e usuários

| Item | Especificação |
|---|---|
| Descrição | Permitir manutenção de departamentos e perfis de usuários. |
| Ator | Administrador funcional / Inovação. |
| Critérios de aceite | Cadastro respeita permissões; departamentos inativos não aparecem no Canvas público. |
| Regras | RN001, RN002, RN031. |

### RF016 - Sincronização Asana → Portal

| Item | Especificação |
|---|---|
| Descrição | Sincronizar dados operacionais do Asana para cache no portal por webhook e cron de reconciliação. |
| Ator | Sistema. |
| Critérios de aceite | Eventos do Asana atualizam cache; cron corrige divergências; falhas são registradas. |
| Regras | RN010, RN011, RN029. |

### RF017 - Auditoria de ações relevantes

| Item | Especificação |
|---|---|
| Descrição | Registrar ações críticas em log funcional. |
| Ator | Sistema. |
| Critérios de aceite | Submissão, IA, triagem, conversão, Asana, alteração de fase e erros relevantes geram log. |
| Regras | RN032. |

### RF018 - Gerar Brainstorm Estratégico com IA

| Item | Especificação |
|---|---|
| Descrição | Gerar automaticamente um Brainstorm Estratégico com IA ao cadastrar uma nova ideia no backlog. |
| Ator | Sistema / IA. |
| Pré-condições | Ideia cadastrada com dados mínimos suficientes para análise. |
| Fluxo principal | 1. Sistema salva a ideia.<br>2. Sistema aciona Edge Function de IA.<br>3. IA usa SCAMPER como base de ideação.<br>4. IA gera 3 soluções estratégicas.<br>5. Sistema valida resposta estruturada.<br>6. Sistema salva o brainstorm vinculado à ideia. |
| Exceções | Falha da IA; resposta inválida; timeout; dados insuficientes. |
| Critérios de aceite | Brainstorm contém exatamente 3 soluções, cada solução possui campos obrigatórios, uma solução é recomendada e há notas/justificativas de impacto e esforço. |
| Regras | RN018, RN019, RN020, RN021, RN022, RN023, RN024. |

### RF019 - Exibir brainstorm no detalhe da ideia

| Item | Especificação |
|---|---|
| Descrição | Exibir o Brainstorm Estratégico no detalhe da ideia. |
| Ator | Inovação. |
| Pré-condições | Ideia existente no backlog. |
| Fluxo principal | 1. Usuário abre detalhe da ideia.<br>2. Sistema exibe status do brainstorm.<br>3. Se gerado, exibe as 3 soluções e destaca a recomendada.<br>4. Usuário pode usar as informações para triagem ou conversão. |
| Exceções | Brainstorm pendente ou com erro; possibilidade de nova tentativa conforme regra definida. |
| Critérios de aceite | Usuário visualiza soluções, notas, riscos, mitigações e recomendação antes de converter a ideia em projeto. |
| Regras | RN018, RN019, RN026. |

### RF020 - Copiar brainstorm para projeto convertido

| Item | Especificação |
|---|---|
| Descrição | Ao converter uma ideia em projeto, copiar o Brainstorm Estratégico para o registro do projeto. |
| Ator | Inovação / Sistema. |
| Pré-condições | Ideia aprovada para conversão. |
| Fluxo principal | 1. Usuário aciona conversão em projeto.<br>2. Sistema cria projeto interno.<br>3. Sistema copia o brainstorm da ideia para o projeto.<br>4. Sistema mantém rastreabilidade com a ideia original. |
| Exceções | Brainstorm ausente; erro na criação do projeto. |
| Critérios de aceite | Projeto criado contém referência à ideia original e ao brainstorm estratégico usado na decisão. |
| Regras | RN027. |

### RF021 - Criar task inicial no Asana com brainstorm

| Item | Especificação |
|---|---|
| Descrição | Criar uma task inicial no projeto do Asana contendo o Brainstorm Estratégico completo. |
| Ator | Sistema / Asana API. |
| Pré-condições | Projeto interno criado; projeto Asana criado ou identificado. |
| Fluxo principal | 1. Sistema cria/identifica projeto no Asana.<br>2. Sistema cria task inicial chamada `Brainstorm Estratégico IA`.<br>3. Sistema preenche a descrição da task com o brainstorm completo. |
| Exceções | Falha na API do Asana; projeto Asana não criado; brainstorm ausente. |
| Critérios de aceite | O projeto no Asana contém uma task inicial com as 3 soluções, recomendação da IA, notas de impacto/esforço, riscos e mitigações. |
| Regras | RN028, RN029. |

---

<a id="ef-5-regras-de-negocio"></a>
## 5. Regras de negócio

| Código | Regra |
|---|---|
| RN001 | Todo acesso ao portal interno exige autenticação. |
| RN002 | Perfis de acesso aceitos na primeira versão: `diretoria` e `inovacao`. |
| RN003 | Permissões devem ser aplicadas no front-end e reforçadas por RLS/Edge Functions. |
| RN004 | O Canvas público não exige login. |
| RN005 | Ideias submetidas pelo Canvas devem ter autor, e-mail, área de origem, área impactada e campos mínimos do Canvas. |
| RN006 | Submissão pública deve ter validação anti-spam e rate limit. |
| RN007 | Chamadas de IA devem ocorrer somente via Edge Functions. |
| RN008 | Respostas de IA devem ser estruturadas e validadas antes de gravação. |
| RN009 | O autor pode aprovar ou ajustar o resumo da ideia antes da submissão final. |
| RN010 | O Supabase é a fonte de verdade de governança. |
| RN011 | O Asana é ferramenta operacional; o portal consome cache sincronizado para visão executiva. |
| RN012 | Impacto deve usar escala 1–10. |
| RN013 | Esforço deve usar escala 1–10, onde nota maior significa maior esforço. |
| RN014 | A matriz Impacto × Esforço deve usar regras objetivas de quadrante. |
| RN015 | A Inovação pode revisar manualmente impacto, esforço e quadrante durante triagem. |
| RN016 | Ideias podem assumir estados como enviada, em análise, aprovada, rejeitada e convertida. |
| RN017 | Apenas Inovação pode aprovar, rejeitar ou converter ideias. |
| RN018 | O Brainstorm Estratégico deve ser gerado após o cadastro da ideia. |
| RN019 | A ideia deve ser salva mesmo se a geração do brainstorm falhar. |
| RN020 | Uma resposta válida da IA deve conter exatamente 3 soluções. |
| RN021 | Cada solução deve indicar uma abordagem SCAMPER aplicada. |
| RN022 | Cada solução deve conter nota de impacto e esforço de 1 a 10. |
| RN023 | A solução recomendada deve ser uma das 3 soluções geradas. |
| RN024 | A justificativa da recomendação deve considerar impacto, esforço, viabilidade e riscos. |
| RN025 | As notas da solução recomendada devem alimentar a classificação inicial da matriz Impacto × Esforço da ideia. |
| RN026 | A área de Inovação pode revisar manualmente impacto, esforço e quadrante na triagem. |
| RN027 | Ao converter a ideia em projeto, o brainstorm deve ser copiado para o projeto interno. |
| RN028 | Ao criar o projeto no Asana, o sistema deve criar uma task inicial com o conteúdo completo do brainstorm. |
| RN029 | Falhas de integração com Asana não devem causar perda do projeto interno. |
| RN030 | Comentários de governança devem guardar autor, data e vínculo com o projeto. |
| RN031 | Departamentos inativos não devem aparecer no Canvas público. |
| RN032 | Ações relevantes devem gerar log funcional sem dados sensíveis. |

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
Inovação acessa backlog
  -> abre detalhe da ideia
  -> consulta resumo IA, brainstorm, solução recomendada e matriz
  -> revisa impacto/esforço, se necessário
  -> aprova, rejeita, mantém em análise ou converte em projeto
```

### 6.4 Conversão em projeto com Asana

```text
Inovação aciona Converter em Projeto
  -> sistema valida permissão e dados mínimos
  -> sistema cria projeto interno
  -> sistema copia Brainstorm Estratégico da ideia para o projeto
  -> sistema cria projeto no Asana
  -> sistema cria task inicial Brainstorm Estratégico IA
  -> sistema registra vínculo e logs
  -> ideia passa para status convertida
```

### 6.5 Sincronização Asana → Portal

```text
Asana envia webhook ou cron executa reconciliação
  -> Edge Function consulta Asana
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
| `/projetos` | Diretoria / Inovação | Lista de projetos de inovação |
| `/projetos/:id` | Diretoria / Inovação | Detalhe, governança, fases, métricas e Asana |
| `/admin` | Inovação / Admin | Departamentos e usuários |

---

<a id="ef-8-telas-e-comportamento-visual"></a>
## 8. Telas e comportamento visual

### Tela 1 - Canvas público

- Deve ser simples, sem login e responsivo.
- Deve conter campos de identificação do autor e blocos da ideia.
- Pode oferecer sugestões de IA por bloco.
- Não deve mostrar notas de impacto/esforço ao autor.
- Após envio, deve exibir confirmação clara.

### Tela 2 - Login

- Deve permitir autenticação por e-mail e senha.
- Deve tratar credenciais inválidas sem expor detalhes técnicos.

### Tela 3 - Dashboard

- Deve mostrar indicadores consolidados de ideias, projetos, status, fases, riscos e evolução.
- Deve consumir dados do Supabase e cache do Asana, não chamadas diretas ao Asana em tempo real.

### Tela 4 - Backlog, detalhe da ideia e matriz Impacto × Esforço

- Deve listar ideias com status, origem, área impactada, data, impacto, esforço e quadrante.
- Deve permitir abrir detalhe da ideia.
- O detalhe da ideia deve exibir:
  - descrição original;
  - resumo IA;
  - classificação IA;
  - status do brainstorm;
  - Brainstorm Estratégico com 3 soluções;
  - solução recomendada destacada;
  - notas de impacto/esforço;
  - análise de viabilidade;
  - riscos e mitigações;
  - ações de enviar ao comitê, aprovar, rejeitar e converter em projeto.
- A matriz deve seguir escala 1–10 e regra de quadrante documentada.

### Tela 5 - Triagem

- Deve apoiar decisão da Inovação com resumo, brainstorm, matriz e dados da ideia.
- Deve permitir revisão de impacto, esforço e quadrante.
- Deve registrar decisão e responsável.

### Tela 6 - Detalhe do projeto

- Deve mostrar objetivo, problema, descrição, fase, checklist, próximos passos, histórico, métricas e comentários.
- Deve exibir o brainstorm herdado da ideia ou, no mínimo, link/referência ao conteúdo que originou o projeto.
- Deve conter bloco Asana somente leitura com status operacional sincronizado.

### Tela 7 - Admin

- Deve permitir manutenção de departamentos e usuários conforme permissão.

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
| CA009 | Inovação consegue aprovar, rejeitar, manter em análise ou converter ideia. |
| CA010 | Conversão cria projeto interno e preserva vínculo com a ideia original. |
| CA011 | Brainstorm é copiado para o projeto convertido. |
| CA012 | Asana recebe projeto e task inicial `Brainstorm Estratégico IA`. |
| CA013 | Falha no Asana não causa perda do projeto interno. |
| CA014 | Diretoria acessa informações em leitura sem ações de edição. |
| CA015 | Ações relevantes geram log funcional. |

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

---

<a id="ef-13-aprovacao-funcional"></a>
## 13. Aprovação funcional

| Papel | Nome | Status | Data |
|---|---|---|---|
| Responsável funcional | A definir | Pendente | - |
| Responsável técnico | Phablo Tavares | Pendente | - |
| Gerência solicitante | A definir | Pendente | - |
