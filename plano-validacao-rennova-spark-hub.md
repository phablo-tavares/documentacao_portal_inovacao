# Plano de Validação — Portal de Gestão da Inovação Rennova

> Checklist de validação para confirmar que o Rennova Spark Hub atende ao escopo funcional e técnico definido.

---

<a id="sumario"></a>
## Sumário

- [1. Informações do projeto](#pv-1-informacoes-do-projeto)
- [2. Objetivo da validação](#pv-2-objetivo-da-validacao)
- [3. Escopo da validação](#pv-3-escopo-da-validacao)
  - [3.1 O que será validado](#pv-3-1-o-que-sera-validado)
  - [3.2 O que não será validado](#pv-3-2-o-que-nao-sera-validado)
- [4. Critérios gerais de aceite](#pv-4-criterios-gerais-de-aceite)
- [5. Checklist de validação funcional](#pv-5-checklist-de-validacao-funcional)
- [6. Checklist técnico mínimo](#pv-6-checklist-tecnico-minimo)
- [7. Validação de segurança e permissões](#pv-7-validacao-de-seguranca-e-permissoes)
- [8. Validação de integração Asana](#pv-8-validacao-de-integracao-asana)
- [9. Validação de IA](#pv-9-validacao-de-ia)
- [10. Pendências encontradas](#pv-10-pendencias-encontradas)
  - [Classificação sugerida](#pv-classificacao-sugerida)
- [11. Critérios de bloqueio para produção](#pv-11-criterios-de-bloqueio-para-producao)
- [12. Decisão final](#pv-12-decisao-final)
  - [Observações finais](#pv-observacoes-finais)
- [13. Aprovação](#pv-13-aprovacao)
- [Histórico de alterações](#pv-historico-de-alteracoes)
---

<a id="pv-1-informacoes-do-projeto"></a>
## 1. Informações do projeto

| Campo | Preenchimento |
|---|---|
| Nome do projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável pela validação | A definir — Inovação / Gerência |
| Responsável pelo desenvolvimento | Phablo Tavares |
| Data prevista de validação | A definir |
| Versão validada | A definir — commit/tag/build do Lovable/Supabase |

---

<a id="pv-2-objetivo-da-validacao"></a>
## 2. Objetivo da validação

Validar se o portal implementa os fluxos principais de gestão da inovação conforme a especificação funcional e o design técnico: submissão de ideias, apoio de IA, triagem, matriz impacto×esforço, governança de projetos, integração com Asana, sincronização, permissões e segurança mínima para uso interno.

---

<a id="pv-3-escopo-da-validacao"></a>
## 3. Escopo da validação

<a id="pv-3-1-o-que-sera-validado"></a>
### 3.1 O que será validado

- Canvas público de submissão de ideias.
- Sugestão de IA por bloco.
- Geração e aprovação de resumo de IA.
- Login e sessão no portal interno.
- Controle de acesso por perfis `diretoria` e `inovacao`.
- Dashboard executivo.
- Matriz Impacto × Esforço.
- Triagem mensal de ideias.
- Conversão de ideia em projeto.
- Criação de projeto no Asana a partir de template.
- Sincronização Asana → portal por webhook e/ou cron.
- Detalhe do projeto: fases, checklist, métricas, insight de IA, bloco Asana e comentários.
- Administração de departamentos e usuários.
- Logs de auditoria.
- Segurança básica: RLS, secrets e ausência de tokens no front-end.
- Build/deploy nos ambientes definidos.

<a id="pv-3-2-o-que-nao-sera-validado"></a>
### 3.2 O que não será validado

- Funcionalidades fora do escopo fechado.
- Testes de carga avançados.
- Compatibilidade com navegadores antigos.
- Aplicativo mobile nativo.
- Edição de tarefas Asana pelo portal.
- SSO corporativo.
- Integrações com ERP, CRM, e-mail ou outros sistemas.
- BI avançado fora do dashboard previsto.
- Migração de dados históricos não estruturados.

---

<a id="pv-4-criterios-gerais-de-aceite"></a>
## 4. Critérios gerais de aceite

A entrega será considerada aprovada quando:

- [ ] Todas as funcionalidades previstas no escopo forem validadas ou formalmente postergadas.
- [ ] Os fluxos principais puderem ser executados sem erro bloqueante.
- [ ] As regras de negócio principais forem respeitadas.
- [ ] As permissões e restrições de acesso funcionarem conforme definido.
- [ ] Os dados forem salvos, exibidos e atualizados corretamente no Supabase.
- [ ] A integração com Asana criar projeto e atualizar `asana_sync` corretamente.
- [ ] Chamadas de IA tiverem fallback seguro em caso de falha.
- [ ] As mensagens de erro ou validação forem compreensíveis para o usuário.
- [ ] Dados sensíveis não estiverem expostos no front-end, logs ou repositório.
- [ ] Não houver pendências críticas abertas.

---

<a id="pv-5-checklist-de-validacao-funcional"></a>
## 5. Checklist de validação funcional

| ID | Item a validar | Resultado esperado | Status | Observações |
|---|---|---|---|---|
| VF001 | Acessar `/canvas` sem login | Formulário público carrega corretamente | Pendente |  |
| VF002 | Carregar departamentos no Canvas | Apenas departamentos ativos aparecem nas listas | Pendente |  |
| VF003 | Enviar Canvas com campos obrigatórios vazios | Sistema bloqueia envio e informa campos pendentes | Pendente |  |
| VF004 | Enviar Canvas com e-mail inválido | Sistema bloqueia envio | Pendente |  |
| VF005 | Enviar Canvas válido | Ideia é criada em `ideas` com status `enviada` | Pendente |  |
| VF006 | Acionar proteção anti-spam | Submissões abusivas são bloqueadas | Pendente | Testar rate limit/honeypot |
| VF007 | Solicitar sugestão IA para bloco do Canvas | Sistema retorna sugestão editável | Pendente |  |
| VF008 | Falha simulada da IA no Canvas | Usuário consegue seguir preenchendo manualmente | Pendente |  |
| VF009 | Gerar resumo de IA da ideia | `resumo_ia`, `impacto_ia` e `esforco_ia` são processados sem exibir notas ao autor | Pendente |  |
| VF010 | Autor aprovar resumo | Ideia passa para `aprovada_autor` | Pendente |  |
| VF011 | Autor complementar resumo | Comentário/ajuste é salvo corretamente | Pendente |  |
| VF012 | Login com usuário válido `diretoria` | Usuário acessa portal interno | Pendente |  |
| VF013 | Login com usuário válido `inovacao` | Usuário acessa portal interno | Pendente |  |
| VF014 | Login com senha inválida | Sistema exibe mensagem de erro e não autentica | Pendente |  |
| VF015 | Usuário inativo tenta acessar | Acesso é bloqueado | Pendente |  |
| VF016 | Diretoria acessa Dashboard | Dashboard carrega em modo leitura | Pendente |  |
| VF017 | Diretoria tenta acessar `/triagem` | Acesso é negado | Pendente |  |
| VF018 | Diretoria tenta acessar `/admin` | Acesso é negado | Pendente |  |
| VF019 | Diretoria tenta editar projeto por UI | Ação não está disponível | Pendente |  |
| VF020 | Diretoria tenta alterar dados por chamada direta | RLS/Edge Function bloqueia | Pendente | Teste técnico |
| VF021 | Dashboard exibe KPIs | Projetos ativos, progresso, tarefas abertas e ideias em triagem batem com base | Pendente |  |
| VF022 | Dashboard filtra por área/status | Lista muda conforme filtros | Pendente |  |
| VF023 | Dashboard sem dados de Asana | Tela permanece funcional e indica ausência/sync pendente | Pendente |  |
| VF024 | Matriz exibe ideias elegíveis | Ideias `aprovada_autor`, `em_triagem` e `backlog` aparecem | Pendente |  |
| VF025 | Matriz oculta ideias convertidas/arquivadas | Ideias `virou_projeto` e `arquivada` não aparecem | Pendente |  |
| VF026 | Matriz usa escala 1–5 | Pontos respeitam escala e quadrantes definidos | Pendente |  |
| VF027 | Clicar em ponto da matriz | Detalhe da ideia é exibido | Pendente |  |
| VF028 | Inovação acessa `/triagem` | Tela carrega ideias elegíveis | Pendente |  |
| VF029 | Salvar impacto/esforço final válido | Notas são salvas em `impacto_final` e `esforco_final` | Pendente |  |
| VF030 | Salvar nota fora da escala | Sistema bloqueia valores fora de 1–5 | Pendente |  |
| VF031 | Decidir Backlog | Ideia muda para `backlog` e permanece na matriz | Pendente |  |
| VF032 | Decidir Arquivar | Ideia muda para `arquivada` e sai da matriz | Pendente |  |
| VF033 | Decidir Vira Projeto sem notas finais | Sistema bloqueia conversão | Pendente |  |
| VF034 | Converter ideia em projeto | Projeto é criado no Supabase e ideia muda para `virou_projeto` | Pendente |  |
| VF035 | Repetir conversão da mesma ideia | Sistema impede duplicidade | Pendente | Testar duplo clique/retry |
| VF036 | Criar projeto no Asana por template | Projeto Asana é criado com nome `INV | ...` | Pendente |  |
| VF037 | Projeto Asana entra no portfólio Inovação | Projeto aparece no portfólio correto | Pendente |  |
| VF038 | Descrição do Asana é preenchida | `html_notes` contém resumo IA e blocos do Canvas | Pendente |  |
| VF039 | Link Asana salvo | `asana_project_gid` e `asana_permalink` são gravados | Pendente |  |
| VF040 | Webhook Asana handshake | Função responde com `X-Hook-Secret` corretamente | Pendente | Teste técnico |
| VF041 | Evento Asana recebido | `asana_sync` é atualizado ou marcado para sync | Pendente |  |
| VF042 | Cron `asana-sync` executado | Contagens e distribuição são atualizadas | Pendente |  |
| VF043 | Detalhe do projeto carrega | Exibe cabeçalho, resumo IA, objetivo, problema e descrição | Pendente |  |
| VF044 | Stepper de fases carrega | Cinco fases aparecem na ordem correta | Pendente |  |
| VF045 | Concluir fase | Status da fase muda e `progress_pct` recalcula | Pendente |  |
| VF046 | Checklist da fase | Itens podem ser marcados/desmarcados pela Inovação | Pendente |  |
| VF047 | Diretoria visualiza fases/checklist | Dados aparecem em leitura, sem edição | Pendente |  |
| VF048 | Registrar métrica/resultado | Resultado é salvo corretamente | Pendente |  |
| VF049 | Gerar insight de IA | `insight_ia` é salvo na métrica | Pendente |  |
| VF050 | Gerar insight sem resultado | Sistema bloqueia ação | Pendente |  |
| VF051 | Bloco Asana no detalhe | Exibe total, abertas, concluídas e distribuição de status | Pendente |  |
| VF052 | Abrir no Asana | Botão abre permalink do projeto | Pendente |  |
| VF053 | Adicionar comentário de governança | Comentário é salvo com autor e data | Pendente |  |
| VF054 | Diretoria tenta comentar | Ação é bloqueada | Pendente |  |
| VF055 | Encerrar projeto | Projeto muda para `encerrado` e grava fase/data | Pendente |  |
| VF056 | Editar projeto encerrado | Alterações restritas são bloqueadas | Pendente | Conforme decisão final |
| VF057 | Admin cria departamento | Departamento novo aparece para uso | Pendente |  |
| VF058 | Admin tenta criar departamento duplicado | Sistema bloqueia duplicidade | Pendente |  |
| VF059 | Admin inativa departamento | Departamento não aparece em novos cadastros | Pendente |  |
| VF060 | Admin altera role de usuário | Permissão muda conforme novo perfil | Pendente |  |
| VF061 | Usuário tenta autoelevar role | Operação é bloqueada | Pendente | Teste crítico de segurança |
| VF062 | Logs de conversão | `activity_log` registra ação `convert` | Pendente |  |
| VF063 | Logs de alteração de status | `activity_log` registra status relevante | Pendente |  |
| VF064 | Mensagens do sistema | Mensagens são claras e sem detalhes técnicos sensíveis | Pendente |  |

**Status permitidos:** `Pendente`, `Aprovado`, `Reprovado`, `Ajuste necessário`.

---

<a id="pv-6-checklist-tecnico-minimo"></a>
## 6. Checklist técnico mínimo

| Item | Critério | Status | Observações |
|---|---|---|---|
| Ambiente | Sistema executa no ambiente previsto | Pendente | Lovable/Supabase definidos |
| Build frontend | Aplicação compila sem erros bloqueantes | Pendente |  |
| Rotas | Rotas públicas e internas funcionam conforme mapa de navegação | Pendente |  |
| Configuração | Variáveis, credenciais e integrações estão configuradas corretamente | Pendente | Sem registrar valores reais |
| Banco de dados | Tabelas, campos, enums, triggers e relacionamentos necessários estão disponíveis | Pendente | Aplicar schema/migrations |
| RLS | Policies impedem acesso indevido | Pendente | Testar diretoria vs inovação vs público |
| Auth | Supabase Auth funciona para usuários internos | Pendente |  |
| Edge Functions | Funções principais respondem conforme contrato | Pendente |  |
| APIs/integrações | Asana e IA respondem com tratamento de erro | Pendente |  |
| Cron | `asana-sync` pode ser agendado/executado | Pendente |  |
| Webhook | `asana-webhook` recebe handshake e eventos | Pendente |  |
| Logs | Erros relevantes são registrados para troubleshooting | Pendente |  |
| Segurança básica | Dados sensíveis não estão expostos no frontend, logs ou repositório | Pendente |  |
| Idempotência | Conversão não gera duplicidade | Pendente |  |
| Performance | Dashboard carrega sem chamada direta ao Asana | Pendente |  |
| Build/deploy | Aplicação pode ser publicada conforme definido | Pendente |  |
| Rollback | Existe procedimento de retorno para versão anterior | Pendente |  |

---

<a id="pv-7-validacao-de-seguranca-e-permissoes"></a>
## 7. Validação de segurança e permissões

| ID | Item a validar | Resultado esperado | Status | Observações |
|---|---|---|---|---|
| VS001 | Token Asana no front-end | Nenhum token aparece em código client-side | Pendente |  |
| VS002 | Chave de IA no front-end | Nenhuma chave aparece em código client-side | Pendente |  |
| VS003 | Service role no front-end | Service role não está exposta | Pendente |  |
| VS004 | RLS em `ideas` | Público não consegue ler/inserir diretamente | Pendente |  |
| VS005 | RLS em `projects` | Somente autenticados leem; edição só Inovação | Pendente |  |
| VS006 | RLS em `profiles` | Usuário não consegue alterar próprio role/ativo indevidamente | Pendente | Requer ajuste se policy permitir |
| VS007 | Endpoint público `submit-idea` | Valida entrada e anti-spam | Pendente |  |
| VS008 | Webhook Asana | Valida segredo/assinatura antes de processar evento | Pendente |  |
| VS009 | Logs | Logs não contêm senhas, tokens ou chaves | Pendente |  |
| VS010 | Mensagens de erro | Não exibem stack trace ou detalhes sensíveis | Pendente |  |

---

<a id="pv-8-validacao-de-integracao-asana"></a>
## 8. Validação de integração Asana

| ID | Cenário | Resultado esperado | Status | Observações |
|---|---|---|---|---|
| VA001 | Secrets Asana configurados | Edge Functions conseguem autenticar | Pendente |  |
| VA002 | Instanciar template | API retorna job e job conclui com projeto criado | Pendente |  |
| VA003 | Adicionar ao portfólio | Projeto aparece no portfólio Inovação | Pendente |  |
| VA004 | Atualizar owner/descrição | Projeto Asana recebe owner e `html_notes` | Pendente |  |
| VA005 | Gravar retorno no Supabase | Projeto tem `asana_project_gid` e `asana_permalink` | Pendente |  |
| VA006 | Criar webhook por projeto | Webhook é criado e registrado | Pendente | Requer tabela/estratégia definida |
| VA007 | Handshake webhook | Header `X-Hook-Secret` é devolvido corretamente | Pendente |  |
| VA008 | Evento de tarefa/status | `asana_sync` reflete mudança após webhook ou cron | Pendente |  |
| VA009 | Cron diário | Atualiza contagens, distribuição e último status update | Pendente |  |
| VA010 | Falha Asana simulada | Sistema registra erro e não confirma sucesso falso | Pendente |  |
| VA011 | Rate limit/retry | Função trata erro temporário sem quebrar dados | Pendente | Se viável no teste |
| VA012 | Sem chamada Asana no front | Network do browser não mostra chamadas à API Asana | Pendente | Teste pelo DevTools |

---

<a id="pv-9-validacao-de-ia"></a>
## 9. Validação de IA

| ID | Cenário | Resultado esperado | Status | Observações |
|---|---|---|---|---|
| VI001 | Provider configurado | Edge Functions de IA executam com sucesso | Pendente |  |
| VI002 | Sugestão por bloco | Retorna texto útil e editável | Pendente |  |
| VI003 | Resumo estruturado | Retorna resumo, impacto, esforço e justificativa válidos | Pendente |  |
| VI004 | Validação de escala | Impacto/esforço fora de 1–5 são rejeitados | Pendente | Simular resposta inválida |
| VI005 | Resposta não JSON | Sistema não grava campos controlados indevidamente | Pendente |  |
| VI006 | Falha do provider | UI exibe fallback e permite continuidade | Pendente |  |
| VI007 | Insight de métrica | Insight compara meta e resultado de forma objetiva | Pendente |  |
| VI008 | Privacidade | Payload enviado à IA não inclui dados desnecessários | Pendente | Revisão técnica |

---

<a id="pv-10-pendencias-encontradas"></a>
## 10. Pendências encontradas

| ID | Descrição | Severidade | Responsável | Status |
|---|---|---|---|---|
| P001 | A definir durante validação | Crítica / Média / Baixa | A definir | Aberta |

<a id="pv-classificacao-sugerida"></a>
### Classificação sugerida

- **Crítica:** impede o uso do sistema ou bloqueia fluxo principal.
- **Média:** afeta funcionalidade importante, mas existe contorno temporário.
- **Baixa:** ajuste visual, melhoria pequena ou detalhe que não impede o uso.

---

<a id="pv-11-criterios-de-bloqueio-para-producao"></a>
## 11. Critérios de bloqueio para produção

A entrega não deve ir para produção se qualquer item abaixo estiver reprovado:

- Login e permissões por perfil.
- RLS impedindo acesso indevido.
- Ausência de tokens/secrets no front-end e repositório.
- Submissão pública validada com proteção anti-spam mínima.
- Conversão de ideia sem duplicidade.
- Integração Asana sem confirmação falsa em caso de falha.
- Dashboard sem chamada direta ao Asana pelo browser.
- Fluxos principais de Canvas, triagem e detalhe de projeto funcionando.
- Logs mínimos de erro/conversão/status.

---

<a id="pv-12-decisao-final"></a>
## 12. Decisão final

| Decisão | Marcar |
|---|---|
| Aprovado sem ressalvas | [ ] |
| Aprovado com pendências não críticas | [ ] |
| Reprovado, exige correções antes da entrega | [ ] |

<a id="pv-observacoes-finais"></a>
### Observações finais

Preencher ao final da validação com resumo das pendências, decisão de aceite e próximos passos.

---

<a id="pv-13-aprovacao"></a>
## 13. Aprovação

| Papel | Nome | Data | Aprovação |
|---|---|---|---|
| Validador / Solicitante | A definir |  |  |
| Responsável técnico | Phablo Tavares |  |  |
| Gerência / Dono do produto | A definir |  |  |

---

<a id="pv-historico-de-alteracoes"></a>
## Histórico de alterações

| Data | Versão | Alteração | Responsável |
|---|---|---|---|
| 2026-07-07 | 0.1 | Criação do plano de validação | Phablo Tavares |
