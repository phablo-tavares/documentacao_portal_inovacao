# Plano de Sprints — Rennova Spark Hub

## 1. Identificação

| Item | Definição |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Objetivo do documento | Organizar a construção do sistema em cinco incrementos funcionais, explicando a motivação, a cobertura e o resultado esperado de cada sprint. |
| Especificação de referência | `especificacao-funcional-portal-inovacao.md`, versão 0.8 |
| Design técnico de referência | `design-tecnico-portal-inovacao.md`, versão 0.7 |
| Plano de validação de referência | `plano-validacao-portal-inovacao.md`, versão 0.7 |
| Data da referência documental | 14/07/2026 |

---

## 2. Premissas

- O escopo funcional e técnico definido nos documentos de referência está aprovado e será tratado como fonte oficial para a construção.
- O desenvolvimento será organizado em cinco sprints sequenciais e, ao final da Sprint 5, o sistema deverá estar completo, testado, validado e funcionando em produção.
- Cada sprint deve produzir um incremento integrado e utilizável, ainda que algumas funcionalidades sejam concluídas apenas em sprints posteriores.
- Cada sprint terá dois checkpoints obrigatórios de code review: um intermediário e outro ao final da sprint.
- Pendências críticas encontradas em code review devem ser corrigidas antes do aceite da sprint. Pendências não críticas podem ser registradas e priorizadas, desde que não comprometam o incremento nem criem risco relevante para as sprints seguintes.
- Testes, segurança, auditoria e tratamento de erros serão construídos junto com as funcionalidades. A Sprint 5 fará a consolidação e a validação final, mas não será o primeiro momento em que o sistema será testado.
- O pipeline de integração contínua começará na Sprint 1 e evoluirá durante o projeto. Na Sprint 5 serão acrescentados os controles e a automação necessários ao deploy em produção.
- O protótipo existente em React/Vite e Lovable será aproveitado como base visual, substituindo progressivamente os dados mockados por dados reais.
- O Lovable continuará sendo a principal ferramenta de evolução do front-end.
- O Supabase será utilizado para autenticação, banco de dados, RLS, Edge Functions, Storage e gerenciamento de secrets, além de ser a fonte de verdade dos dados de governança.
- O Asana permanecerá como ferramenta operacional para tarefas e sprints. O portal não substituirá o Asana nem permitirá editar suas tarefas.
- O acesso ao Asana, aos provedores de IA e ao provedor de CAPTCHA ocorrerá somente pelo backend seguro. Tokens e chaves privadas não poderão ser expostos no front-end.
- O projeto Asana criado pelo portal deverá utilizar exclusivamente o template `INV | Modelo Base`, identificado pelo ID `1213945719343548`.
- O sistema atenderá inicialmente aos perfis `diretoria` e `inovacao`, com permissões reforçadas no backend por RLS e Edge Functions.
- A primeira versão priorizará o uso em desktop, com responsividade básica para web.
- A validação funcional seguirá os 18 casos definidos no plano de validação, com evidências registradas para os resultados aprovados, reprovados ou bloqueados.
- Uma sprint somente será considerada aceita quando suas entregas estiverem integradas, o pipeline estiver aprovado, os dois checkpoints de code review tiverem sido concluídos e os critérios de aceite correspondentes tiverem sido atendidos.

---

## 3. Visão geral

O plano segue uma estratégia incremental orientada pelas dependências do produto. Primeiro é criada a fundação técnica e de segurança. Em seguida, é entregue a entrada pública de ideias. Depois, as ideias recebem análise de IA, pontuação e triagem. A quarta sprint transforma ideias aprovadas em projetos governados e integrados ao Asana. Por fim, a quinta sprint consolida a visão executiva, a qualidade, o CI/CD e a publicação em produção.

| Sprint | Foco | Incremento esperado |
|---|---|---|
| Sprint 1 | Fundação técnica, segurança e ambientes | Aplicação integrada ao Supabase, publicada em homologação, com autenticação, perfis, autorização e CI inicial. |
| Sprint 2 | Canvas público e submissão de ideias | Colaborador consegue estruturar, complementar e enviar uma ideia com apoio da IA. |
| Sprint 3 | Brainstorm, pontuação, matriz e triagem | Ideias enviadas passam a ser analisáveis, comparáveis e priorizáveis pela Inovação. |
| Sprint 4 | Conversão, Asana e governança de projetos | Ideias aprovadas viram projetos executáveis e acompanháveis pelo portal. |
| Sprint 5 | Dashboard, validação, CI/CD e produção | Produto completo, validado, observável e disponibilizado em produção. |

As sprints não representam camadas isoladas de front-end ou backend. Cada uma deve entregar fluxos verticais, combinando interface, regras de negócio, persistência, segurança, integrações, testes e tratamento de falhas necessários ao incremento.

---

## 4. Sprint 1 — Fundação técnica, segurança e ambientes

### 4.1 Objetivo

Estabelecer a base técnica, operacional e de segurança sobre a qual todo o produto será construído. A sprint deve transformar o protótipo visual em uma aplicação preparada para trabalhar com dados reais, ambientes controlados, autenticação e autorização.

A motivação desta sprint é reduzir riscos estruturais desde o início. Banco, migrations, perfis, RLS, organização do código, ambientes e integração contínua são dependências diretas de praticamente todos os fluxos posteriores. Sem essa base, as próximas sprints tenderiam a produzir funcionalidades isoladas, difíceis de integrar e inseguras.

### 4.2 Requisitos, regras de negócio e fluxos cobertos

**Requisitos funcionais:**

- RF001 — Autenticação no portal interno.
- RF002 — Controle de acesso por perfil.
- RF015 — Administração de departamentos e usuários.
- RF017 — Auditoria de ações relevantes, parcialmente, por meio da estrutura inicial de logs e rastreabilidade.
- Base técnica necessária para todos os demais requisitos.

**Regras de negócio:**

- RN001 — Perfis `diretoria` e `inovacao`, com responsabilidades distintas.
- RN002 — Permissões reforçadas por RLS e/ou Edge Functions.
- RN003 — Bloqueio de usuários internos inativos.
- RN030 — Registro de ações relevantes sem dados sensíveis, parcialmente.
- RN032 — Tratamento de falhas sem perda de dados principais, como princípio transversal da arquitetura.

**Fluxos de usuário cobertos:**

- Acesso ao portal interno por e-mail e senha.
- Renovação e encerramento da sessão conforme o comportamento padrão do Supabase Auth.
- Redirecionamento de usuário não autenticado para o login.
- Carregamento do perfil e liberação das funcionalidades conforme a permissão.
- Bloqueio de acesso de usuário inativo, sem perfil ou sem autorização.
- Administração básica de departamentos e perfis por usuário de Inovação.

### 4.3 Entregas

- Base React/Vite organizada e preparada para evolução pelo Lovable.
- Ambientes de desenvolvimento e homologação configurados.
- Supabase integrado à aplicação.
- Estrutura inicial do banco criada por migrations versionadas.
- Dados e configurações iniciais necessários aos ambientes.
- Autenticação interna com Supabase Auth.
- Perfis `diretoria` e `inovacao` implementados.
- Rotas protegidas, RLS e validações server-side de autorização.
- Administração básica de departamentos e usuários.
- Estrutura inicial de auditoria e logs técnicos.
- Camada de acesso a dados reais e redução progressiva da dependência de `mockData`.
- Pipeline inicial de CI com verificações de qualidade, testes e build.
- Aplicação publicada e acessível no ambiente de homologação.
- Dois checkpoints de code review concluídos.

### 4.4 Critérios de aceite

- Usuário ativo e com credenciais válidas consegue entrar no portal e acessar o Dashboard.
- Usuário não autenticado não consegue acessar rotas internas.
- Usuário inativo, sem perfil ou com perfil desconhecido é bloqueado com segurança.
- Diretoria e Inovação visualizam somente menus e ações compatíveis com suas permissões.
- Uma tentativa de executar uma ação proibida por chamada direta é bloqueada pelo backend, independentemente da interface.
- Somente Inovação consegue realizar as operações administrativas previstas.
- Migrations podem ser aplicadas de forma reproduzível em um ambiente limpo.
- Tokens e chaves privadas não estão presentes no código ou no bundle do front-end.
- O pipeline executa as verificações definidas e bloqueia a integração de código com falha.
- A aplicação gera build válido e está operacional em homologação.
- Não existem pendências críticas abertas nos checkpoints de code review.

---

## 5. Sprint 2 — Canvas público e submissão de ideias

### 5.1 Objetivo

Entregar o fluxo público completo de entrada de ideias, permitindo que um colaborador, sem login, valide o CAPTCHA, preencha o Canvas, receba apoio da IA, complemente informações quando necessário, revise o resumo e conclua a submissão.

A motivação desta sprint é colocar em funcionamento a principal porta de entrada do processo de inovação. Ao final, o portal já deverá ser capaz de capturar ideias com contexto suficiente e persistir seus dados com segurança, ainda que a análise estratégica, a matriz e a triagem sejam concluídas na sprint seguinte.

### 5.2 Requisitos, regras de negócio e fluxos cobertos

**Requisitos funcionais:**

- RF003 — Submissão de ideia pelo Canvas público.
- RF004 — Sugestão de IA por bloco do Canvas.
- RF005 — Resumo de IA e aprovação pelo autor.
- RF022 — Avaliação de suficiência e complementação estratégica.
- RF017 — Auditoria das ações e falhas relevantes do fluxo público, parcialmente.
- RF018 — Preparação do estado necessário para iniciar o brainstorm após a submissão, parcialmente.

**Regras de negócio:**

- RN004 a RN009 — Campos obrigatórios, estados, submissão segura, CAPTCHA e respostas estruturadas da IA.
- RN011 — Impacto e esforço não aparecem ao autor.
- RN018 e RN019 — Preparação do brainstorm e preservação da ideia em caso de falha, parcialmente.
- RN030 e RN032 — Auditoria e preservação dos dados diante de falhas.
- RN034 — Aceite exclusivo dos domínios corporativos autorizados.
- RN045 a RN049 — CAPTCHA antes do Canvas, avaliação de suficiência, complementação única, respostas parciais e recuperação de falhas.

**Fluxos de usuário cobertos:**

- Fluxo 6.1 — Acesso e submissão pública de ideia.
- Fluxo 6.2 — Avaliação de suficiência e complementação.
- Acesso ao Canvas somente após CAPTCHA válido.
- Solicitação de sugestões de IA por bloco.
- Avaliação do Canvas como suficiente ou insuficiente.
- Exibição de uma única rodada de até 10 perguntas quando necessária.
- Aceite de respostas completas, parciais ou vazias.
- Geração, edição e aprovação do resumo pelo autor.
- Persistência transacional da ideia, da avaliação e da complementação.
- Renovação da sessão CAPTCHA sem perda dos dados locais.

### 5.3 Entregas

- Etapa pública de CAPTCHA anterior à exibição do Canvas.
- Sessão pública própria, temporária e validada pelo backend.
- Proteções de honeypot, rate limit e validação de domínios.
- Canvas público com campos e validações definidos na especificação.
- Preservação local do preenchimento e aviso de saída antes da submissão.
- Sugestões contextuais de IA por bloco.
- Avaliação de suficiência do Canvas por IA.
- Modal condicional de complementação estratégica.
- Persistência de perguntas e respostas vinculadas à ideia.
- Resumo consolidado, editável e aprovável pelo autor.
- Submissão segura e transacional da ideia por Edge Function.
- Estados e mecanismos de recuperação para falhas do CAPTCHA, da IA ou da gravação.
- Testes automatizados e evidências dos casos CV002 a CV006.
- Dois checkpoints de code review concluídos.

### 5.4 Critérios de aceite

- Antes da validação do CAPTCHA, somente a etapa de verificação é exibida.
- APIs públicas rejeitam sessão ausente, inválida, expirada ou consumida indevidamente.
- A expiração durante o preenchimento solicita novo CAPTCHA sem apagar os dados locais.
- Campos obrigatórios ausentes impedem a submissão.
- Somente e-mails terminados exatamente nos quatro domínios autorizados são aceitos.
- Sugestões de IA são contextuais, editáveis e opcionais.
- Canvas considerado suficiente segue diretamente para o resumo, sem abrir modal.
- Canvas considerado insuficiente abre somente uma rodada com no máximo 10 perguntas.
- Respostas parciais ou informações ainda incompletas não bloqueiam indevidamente o envio.
- O resumo utiliza Canvas e complementação disponível, pode ser ajustado e não mostra notas de Impacto ou Esforço.
- Ideia, avaliação, perguntas, respostas e resumo são persistidos de forma consistente.
- Falha técnica na avaliação de suficiência não apaga nem impede a submissão da ideia.
- Os casos de validação CV002 a CV006 estão aprovados e com evidências.
- Não existem pendências críticas abertas nos checkpoints de code review.

---

## 6. Sprint 3 — Brainstorm, pontuação, matriz e triagem

### 6.1 Objetivo

Transformar as ideias submetidas em itens estruturados, comparáveis e priorizáveis. A sprint deverá gerar o Brainstorm Estratégico, calcular Impacto e Esforço de forma reproduzível, apresentar as ideias na matriz e permitir que a Inovação registre a avaliação e a decisão de triagem.

A motivação desta sprint é entregar o núcleo de decisão do produto. O portal deixa de ser apenas um canal de coleta e passa a apoiar efetivamente a qualificação, a comparação e a seleção das iniciativas de inovação.

### 6.2 Requisitos, regras de negócio e fluxos cobertos

**Requisitos funcionais:**

- RF007 — Matriz Impacto × Esforço.
- RF008 — Triagem mensal de ideias.
- RF018 — Brainstorm Estratégico com IA.
- RF019 — Exibição do brainstorm no detalhe da ideia.
- RF017 — Auditoria das avaliações, decisões e retentativas, parcialmente.
- RF003 e RF022 — Continuidade do processamento iniciado na submissão, parcialmente.

**Regras de negócio:**

- RN007 a RN010 — Uso controlado da IA, JSON validado e notas permitidas.
- RN013 a RN17 — Eixos da matriz, origem das avaliações, elegibilidade, permissão de triagem e pré-condições para conversão.
- RN018 a RN027 — Geração, estrutura, recomendação, pontuação e classificação do brainstorm.
- RN030 e RN032 — Auditoria e tratamento de falhas.
- RN035 — Duas tentativas automáticas e retentativa manual controlada.
- RN043 — Justificativa e rastreabilidade para arquivamento ou rejeição.
- RN046 a RN049 — Uso da avaliação e da complementação, inclusive recuperação de falha de suficiência.

**Fluxos de usuário cobertos:**

- Fluxo 6.3 — Geração do Brainstorm Estratégico IA.
- Fluxo 6.4 — Triagem de ideia.
- Consulta interna ao Canvas, complementação, resumo e brainstorm.
- Geração de três soluções estratégicas baseadas em SCAMPER.
- Pontuação inicial de cada solução e recomendação de uma delas.
- Posicionamento da ideia na matriz Impacto × Esforço.
- Revisão das notas e justificativas pela Inovação.
- Recálculo dos resultados e do quadrante pelo backend.
- Decisão entre backlog, arquivamento/rejeição ou preparação para virar projeto.
- Consulta da triagem pela Diretoria sem permissão de alteração.

### 6.3 Entregas

- Catálogo versionado de pontuação `2.0`, com critérios, pesos, notas e âncoras oficiais.
- Motor autoritativo de cálculo de Impacto e Esforço no backend.
- Testes unitários das fórmulas, notas permitidas e arredondamento `ROUND_HALF_UP`.
- Geração estruturada de Brainstorm Estratégico usando SCAMPER.
- Validação das três soluções, critérios, justificativas, riscos e recomendação.
- Estados, retentativas automáticas e retentativa manual de IA.
- Detalhe interno da ideia com Canvas, complementação, resumo, brainstorm e pontuações.
- Matriz Impacto × Esforço com diferenciação entre avaliação inicial da IA e avaliação final da triagem.
- Fluxo de triagem com revisão de critérios e decisão registrada.
- Histórico de ideias arquivadas ou rejeitadas.
- Auditoria das alterações de notas, decisões e falhas.
- Testes automatizados e evidências dos casos CV007 a CV011.
- Dois checkpoints de code review concluídos.

### 6.4 Critérios de aceite

- Cada brainstorm válido contém exatamente três soluções e indica uma abordagem SCAMPER para cada uma.
- Cada solução contém os cinco critérios de Impacto e os cinco de Esforço, com notas permitidas e justificativas.
- O backend ignora resultados finais enviados pelo cliente ou pela IA e realiza o cálculo autoritativo.
- A massa de Impacto definida no plano de validação produz `6,8` e posição `7` na matriz.
- A massa de Esforço definida no plano de validação produz `4,8` e posição `5` na matriz.
- A nota `2` é rejeitada para o critério de alcance dos beneficiados.
- Falha na geração não apaga a ideia e respeita o limite de tentativas automáticas.
- O detalhe interno apresenta o contexto complementar sem expor prompts ou dados técnicos indevidos.
- A matriz utiliza Esforço no eixo X, Impacto no eixo Y e o valor inteiro arredondado para classificação.
- Somente Inovação consegue alterar critérios e registrar decisão; Diretoria possui acesso de consulta.
- Alterar uma nota recalcula os resultados e o quadrante de forma reproduzível.
- Arquivamento ou rejeição exige justificativa e gera histórico e auditoria.
- Os casos de validação CV007 a CV011 estão aprovados e com evidências.
- Não existem pendências críticas abertas nos checkpoints de code review.

---

## 7. Sprint 4 — Conversão, Asana e governança de projetos

### 7.1 Objetivo

Permitir que uma ideia aprovada seja transformada em projeto interno e operacional, preservando sua rastreabilidade, criando a estrutura correspondente no Asana e disponibilizando os recursos necessários para acompanhamento executivo e governança.

A motivação desta sprint é completar a passagem entre seleção e execução. A integração deve evitar projetos duplicados, preservar dados em falhas externas e manter uma separação clara: o Asana controla o trabalho operacional, enquanto o portal mantém a visão executiva, as decisões e as evidências do projeto.

### 7.2 Requisitos, regras de negócio e fluxos cobertos

**Requisitos funcionais:**

- RF009 — Conversão de ideia em projeto.
- RF010 — Detalhe e governança do projeto.
- RF011 — Gestão de fases e checklist executivo.
- RF012 — Métricas, resultados e insight de IA.
- RF013 — Bloco Asana no projeto.
- RF014 — Comentários de governança.
- RF016 — Sincronização Asana → Portal.
- RF020 — Cópia do brainstorm para o projeto convertido.
- RF021 — Configuração inicial do projeto no Asana.
- RF017 — Auditoria das operações de projeto e integração, parcialmente.

**Regras de negócio:**

- RN011 e RN012 — Separação do fluxo público e uso do cache do Asana.
- RN016 e RN017 — Permissão e pré-condições para conversão.
- RN020 a RN025 — Estrutura e recomendação preservadas no brainstorm.
- RN028 a RN033 — Cópia do brainstorm, papéis do portal e Asana, auditoria, falhas e comentários.
- RN036 a RN040 — Template obrigatório, identificação, estrutura preservada, conclusão segura e nome do projeto.
- RN041 e RN042 — Entregas e comentários de governança.
- RN044 — Template Asana fixo no escopo desta versão.

**Fluxos de usuário cobertos:**

- Fluxo 6.5 — Conversão em projeto com Asana.
- Fluxo 6.6 — Sincronização Asana → Portal.
- Fluxo 6.7 — Gestão de entregas.
- Conversão de uma ideia aprovada mediante nome e avaliação final válidos.
- Criação de projeto interno e instanciação do template no Asana.
- Recuperação de falhas parciais sem duplicação.
- Consulta dos dados operacionais sincronizados do Asana.
- Acompanhamento de fases e checklist executivo.
- Registro de metas, resultados e insights de IA.
- Inclusão e exclusão controlada de entregas e comentários.

### 7.3 Entregas

- Modelo interno de projetos e vínculo único com a ideia de origem.
- Conversão idempotente de ideia em projeto.
- Instanciação do template obrigatório no Asana.
- Nomeação do projeto no padrão `INV | {nome informado}`.
- Cópia do brainstorm para o projeto interno e para a descrição do projeto Asana.
- Controle do estado da integração e recuperação de falhas parciais.
- Webhook do Asana e cron diário de reconciliação.
- Cache operacional `asana_sync` utilizado pelo portal.
- Detalhe do projeto com visão executiva e bloco Asana somente leitura.
- Fases fixas e checklist executivo.
- Métricas, metas, resultados e insights de IA.
- Entregas por link e arquivos no Supabase Storage.
- Comentários imutáveis de governança.
- Auditoria das ações e operações de integração.
- Testes automatizados e evidências dos casos CV012 a CV017.
- Dois checkpoints de code review concluídos.

### 7.4 Critérios de aceite

- Conversão sem avaliação final completa ou sem nome válido é bloqueada.
- Uma ideia pode originar somente um projeto interno.
- O projeto Asana é criado pelo template `1213945719343548`, preservando sua estrutura.
- O nome final segue o padrão `INV | {nome}` sem prefixo duplicado.
- O brainstorm é copiado para o projeto interno e para a descrição no Asana, sem criação de task exclusiva.
- Repetir a conversão não cria projetos duplicados.
- Falha parcial preserva o projeto interno, os identificadores já obtidos e permite recuperação segura.
- O portal não indica sucesso quando houver falha crítica do Asana ainda não recuperada.
- Webhook atualiza o cache e o cron diário corrige eventos perdidos ou divergências.
- O front-end utiliza `asana_sync` e não consulta a API do Asana durante a renderização.
- Fases, checklist, métricas, resultados e insights funcionam e preservam os dados diante de falha da IA.
- Arquivos com até 50 MB são aceitos e arquivos acima do limite são rejeitados.
- Comentários publicados não podem ser editados e respeitam as regras de exclusão.
- Operações críticas geram registros de auditoria sem expor credenciais.
- Os casos de validação CV012 a CV017 estão aprovados e com evidências.
- Não existem pendências críticas abertas nos checkpoints de code review.

---

## 8. Sprint 5 — Dashboard, qualidade final, CI/CD e produção

### 8.1 Objetivo

Consolidar o produto completo, disponibilizar a visão executiva do portfólio, eliminar lacunas de integração, validar integralmente os requisitos e colocar o sistema em produção com pipeline de CI/CD, observabilidade e estratégia de recuperação.

A motivação desta sprint é transformar os incrementos construídos em um produto pronto para uso real. O foco não deve ser concentrar funcionalidades essenciais deixadas para o final, mas integrar, endurecer, validar e publicar o sistema com confiança operacional.

### 8.2 Requisitos, regras de negócio e fluxos cobertos

**Requisitos funcionais:**

- RF006 — Dashboard executivo.
- RF017 — Auditoria de ações relevantes, concluído de forma transversal.
- Consolidação e regressão de RF001 a RF022.
- Todos os requisitos não funcionais e critérios de aceite consolidados da especificação.

**Regras de negócio:**

- RN001 — Visões compatíveis com os perfis internos.
- RN011 e RN012 — Separação de informações públicas e uso do cache Asana.
- RN029 — Separação de responsabilidades entre portal e Asana.
- RN030 — Auditoria funcional sem dados sensíveis.
- RN032 — Tratamento de falhas sem perda de dados principais.
- Regressão de RN001 a RN049 nos fluxos em que cada regra se aplica.

**Fluxos de usuário cobertos:**

- Consulta do Dashboard executivo, indicadores e portfólio.
- Navegação completa entre ideias, matriz, triagem, projetos e detalhes.
- Regressão ponta a ponta dos fluxos 6.1 a 6.7.
- Operação completa desde a submissão pública até o acompanhamento do projeto convertido.
- Publicação controlada em produção e validação pós-deploy.

### 8.3 Entregas

- Dashboard conectado aos dados reais de ideias, projetos e `asana_sync`.
- KPIs, filtros, estados vazios, erros e navegação para os detalhes.
- Ajustes finais de responsividade, usabilidade e acessibilidade.
- Tratamento consolidado de erros e mensagens do sistema.
- Logs, observabilidade e mecanismos de troubleshooting.
- Revisão final de segurança, RLS, secrets, APIs públicas e uploads.
- Cobertura automatizada dos fluxos críticos e regressão integrada.
- Ambientes e configurações de produção.
- Pipeline de CI/CD com gates de qualidade, migrations, deploy, smoke test e estratégia de rollback.
- Execução integral dos casos CV001 a CV018.
- Registro das evidências e correção dos desvios encontrados.
- Documentação operacional mínima para publicação, rollback e diagnóstico.
- Release aprovado, sistema implantado em produção e smoke test concluído.
- Dois checkpoints de code review concluídos, incluindo a aprovação final do release.

### 8.4 Critérios de aceite

- Dashboard apresenta KPIs calculados com dados reais do Supabase e do cache Asana.
- Filtros, navegação, estados vazios e indisponibilidade de integrações não quebram a interface.
- Todos os requisitos funcionais RF001 a RF022 estão implementados ou comprovadamente atendidos.
- Todas as regras de negócio aplicáveis estão respeitadas no front-end e no backend.
- Todos os casos de validação CV001 a CV018 estão aprovados, com evidências registradas.
- Não existem falhas críticas de submissão, complementação, permissões, pontuação, triagem, conversão, template Asana, idempotência, entregas ou preservação de dados.
- Nenhum token, secret ou `service_role` está exposto no front-end, nos logs ou em respostas indevidas.
- RLS e Edge Functions bloqueiam operações não autorizadas.
- Logs permitem diagnosticar falhas relevantes sem armazenar credenciais, tokens ou respostas completas sensíveis.
- O pipeline bloqueia releases com falha de qualidade, testes ou build.
- Migrations e deploy são executados na ordem segura definida pelo design técnico.
- Existe procedimento de rollback aplicável ao release.
- A aplicação está acessível e funcional em produção.
- O smoke test pós-deploy confirma login, Canvas, consulta interna e integrações críticas.
- Não existem pendências críticas abertas no code review final nem no aceite funcional.
- Qualquer correção de código realizada após a aprovação final reabre as verificações e o code review correspondentes antes de ser considerada concluída.

---

## 9. Checkpoints de code review

Cada sprint terá dois gates formais de revisão:

### 9.1 Checkpoint intermediário

Ocorre quando a primeira parte do incremento já permite avaliar as principais decisões técnicas. Deve verificar:

- aderência à especificação funcional e ao design técnico;
- estrutura, legibilidade e manutenibilidade do código;
- modelagem, migrations e contratos de API;
- autorização, segurança e proteção de secrets;
- tratamento de erros e preservação dos dados;
- qualidade e suficiência dos testes produzidos até o momento;
- riscos de integração para a segunda metade da sprint.

### 9.2 Checkpoint final

Ocorre com o incremento completo e integrado. Deve verificar:

- correção das observações do checkpoint intermediário;
- atendimento aos critérios de aceite da sprint;
- execução aprovada do pipeline;
- cobertura dos testes e evidências de validação correspondentes;
- ausência de regressões conhecidas e falhas críticas;
- atualização de migrations, configurações e documentação relevante;
- segurança para integrar o incremento e iniciar a próxima sprint.

Na Sprint 5, o checkpoint final também funciona como gate de aprovação do release de produção.

---

## 10. Rastreabilidade resumida

| Sprint | Requisitos principais | Fluxos principais | Casos de validação predominantes |
|---|---|---|---|
| Sprint 1 | RF001, RF002, RF015 e RF017 parcial | Login, sessão, perfis e administração | CV001 e parte do CV018 |
| Sprint 2 | RF003, RF004, RF005 e RF022 | Fluxos 6.1 e 6.2 | CV002 a CV006 |
| Sprint 3 | RF007, RF008, RF018 e RF019 | Fluxos 6.3 e 6.4 | CV007 a CV011 |
| Sprint 4 | RF009 a RF014, RF016, RF020 e RF021 | Fluxos 6.5, 6.6 e 6.7 | CV012 a CV017 |
| Sprint 5 | RF006, RF017 e regressão de RF001 a RF022 | Jornada completa e operação em produção | CV001 a CV018 |

---

## 11. Condição de conclusão do plano

O plano será considerado concluído quando:

- as cinco sprints tiverem sido aceitas;
- todos os requisitos funcionais, regras de negócio e fluxos previstos estiverem cobertos;
- os 18 casos do plano de validação estiverem aprovados;
- os checkpoints de code review estiverem concluídos sem pendências críticas;
- o pipeline de CI/CD estiver operacional;
- o sistema estiver publicado em produção;
- os smoke tests pós-deploy estiverem aprovados;
- houver evidência de que os dados principais são preservados diante das falhas previstas;
- a equipe responsável tiver condições de operar, diagnosticar e recuperar o sistema.