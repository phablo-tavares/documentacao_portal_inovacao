# Plano de Validação — Portal de Gestão da Inovação Rennova

> Plano objetivo para validar os principais fluxos do **Rennova Spark Hub** antes de aceite funcional/técnico.  
> Versão atualizada com validação do **Brainstorm Estratégico com IA baseado em SCAMPER**, matriz Impacto × Esforço 1–10 e criação de task inicial no Asana.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável | Phablo Tavares |
| Data | 2026-07-08 |
| Versão | 0.4 |
| Objetivo | Validar os fluxos essenciais de submissão, IA, triagem, conversão em projeto, Asana e governança |

---

## 2. Estratégia de validação

A validação deve ser objetiva e orientada aos fluxos críticos do produto.

Não é necessário executar uma bateria extensa de testes nesta fase. O foco é confirmar que:

1. o usuário consegue submeter uma ideia;
2. a IA gera os artefatos esperados;
3. a Inovação consegue analisar e converter ideias;
4. o projeto é criado corretamente;
5. o Asana recebe os dados necessários;
6. falhas previsíveis não causam perda de dados.

---

## 3. Escopo da validação

| Área | Validar |
|---|---|
| Canvas público | Submissão de ideia sem login |
| IA | Sugestões, resumo e Brainstorm Estratégico SCAMPER |
| Backlog de ideias | Listagem, detalhe, status e matriz |
| Matriz Impacto × Esforço | Notas 1–10 e quadrante correto |
| Triagem | Aprovar, rejeitar, manter em análise e converter |
| Projeto interno | Criação com vínculo à ideia e brainstorm copiado |
| Asana | Criação de projeto e task inicial `Brainstorm Estratégico IA` |
| Segurança | Permissões e ausência de tokens no front-end |
| Falhas | IA indisponível, JSON inválido e falha parcial no Asana |

---

## 4. Casos de validação

### CV001 - Submissão de ideia pelo Canvas público

**Objetivo:** confirmar que uma ideia pode ser enviada sem login.

**Passos:**

1. Acessar `/canvas` sem autenticação.
2. Preencher dados do autor, área de origem, área impactada e campos do Canvas.
3. Enviar a ideia.

**Resultado esperado:**

- Ideia é salva no banco.
- Usuário recebe mensagem de sucesso.
- Ideia aparece no backlog interno.
- Nenhum dado técnico sensível é exibido ao usuário.

---

### CV002 - Sugestão de IA por bloco do Canvas

**Objetivo:** confirmar que a IA auxilia o preenchimento sem substituir automaticamente o usuário.

**Passos:**

1. Preencher parcialmente um bloco do Canvas.
2. Solicitar sugestão de IA.
3. Avaliar resposta retornada.

**Resultado esperado:**

- Sugestão é retornada em linguagem clara.
- Usuário pode aceitar, editar ou ignorar.
- Falha de IA mostra mensagem amigável.

---

### CV003 - Resumo consolidado da ideia por IA

**Objetivo:** confirmar que a IA gera um resumo útil da ideia.

**Passos:**

1. Submeter ideia com dados completos.
2. Acionar geração de resumo, se não for automática.
3. Abrir detalhe da ideia.

**Resultado esperado:**

- Resumo IA é salvo e exibido.
- O texto não substitui a descrição original.
- Falha de IA não impede a ideia de ser salva.

---

### CV004 - Brainstorm Estratégico IA com SCAMPER

**Objetivo:** confirmar que o brainstorm estratégico é gerado no formato correto.

**Passos:**

1. Cadastrar uma ideia com dados suficientes.
2. Aguardar ou acionar geração do brainstorm.
3. Abrir o detalhe da ideia.

**Resultado esperado:**

- Brainstorm possui framework `SCAMPER`.
- São geradas exatamente 3 soluções.
- Cada solução informa a abordagem SCAMPER aplicada.
- Cada solução contém:
  - descrição;
  - racional estratégico;
  - como resolve a demanda;
  - impacto estimado;
  - esforço estimado;
  - análise de viabilidade;
  - riscos;
  - mitigações.
- Uma solução é marcada como recomendada.
- A recomendação possui justificativa objetiva.

---

### CV005 - Métrica de Impacto 1–10

**Objetivo:** confirmar que a nota de impacto segue a regra definida.

**Passos:**

1. Abrir uma ideia com brainstorm gerado.
2. Conferir impacto das 3 soluções.
3. Conferir justificativa da nota.

**Resultado esperado:**

- Cada solução possui nota entre 1 e 10.
- A nota é acompanhada de justificativa.
- A justificativa considera critérios como alinhamento estratégico, ganho esperado, escala, urgência e relevância.

---

### CV006 - Métrica de Esforço 1–10

**Objetivo:** confirmar que a nota de esforço segue a regra definida.

**Passos:**

1. Abrir uma ideia com brainstorm gerado.
2. Conferir esforço das 3 soluções.
3. Conferir justificativa da nota.

**Resultado esperado:**

- Cada solução possui nota entre 1 e 10.
- Quanto maior a nota, maior o esforço.
- A justificativa considera critérios como complexidade técnica, integrações, prazo, dependências e custo.

---

### CV007 - Classificação na matriz Impacto × Esforço

**Objetivo:** confirmar que a matriz usa impacto/esforço corretamente.

**Passos:**

1. Abrir backlog ou matriz de ideias.
2. Selecionar ideia com brainstorm gerado.
3. Comparar impacto/esforço da solução recomendada com o quadrante exibido.

**Resultado esperado:**

- A ideia usa, inicialmente, as notas da solução recomendada.
- Quadrante segue a regra:
  - impacto >= 7 e esforço <= 4: Oportunidade Imediata;
  - impacto >= 7 e esforço >= 5: Grande Projeto;
  - impacto entre 4 e 6 e esforço <= 4: Ganho Tático / Astuto;
  - impacto <= 6 e esforço >= 5: Retorno Limitado;
  - impacto <= 3: Baixa Atratividade.
- Inovação consegue revisar manualmente impacto/esforço, se permitido.

---

### CV008 - Falha na geração do brainstorm

**Objetivo:** confirmar que falha de IA não causa perda da ideia.

**Passos:**

1. Simular indisponibilidade da IA ou retorno inválido.
2. Cadastrar uma ideia.
3. Abrir detalhe da ideia.

**Resultado esperado:**

- Ideia é salva.
- `brainstorm_status` fica como `erro` ou equivalente.
- Sistema exibe mensagem amigável.
- Sistema permite nova tentativa ou conversão mediante confirmação explícita da Inovação.

---

### CV009 - Triagem de ideia

**Objetivo:** confirmar que a Inovação consegue analisar a ideia com apoio da IA.

**Passos:**

1. Acessar backlog interno.
2. Abrir detalhe de uma ideia.
3. Avaliar descrição, resumo IA, brainstorm, solução recomendada, impacto/esforço e quadrante.
4. Executar uma decisão de triagem.

**Resultado esperado:**

- Dados necessários à decisão aparecem na tela.
- Ação de triagem é registrada.
- Usuário sem permissão não consegue executar ações de triagem.

---

### CV010 - Conversão de ideia em projeto

**Objetivo:** confirmar que uma ideia aprovada vira projeto interno.

**Passos:**

1. Selecionar ideia aprovada ou elegível.
2. Acionar `Converter em Projeto`.
3. Confirmar conversão.

**Resultado esperado:**

- Projeto interno é criado.
- Ideia muda para status `convertida`.
- Projeto mantém `origin_idea_id` ou vínculo equivalente.
- Brainstorm Estratégico é copiado para o projeto.

---

### CV011 - Criação de projeto no Asana

**Objetivo:** confirmar integração operacional com Asana.

**Passos:**

1. Converter ideia em projeto.
2. Abrir Asana.
3. Localizar projeto criado.

**Resultado esperado:**

- Projeto Asana é criado no workspace/time correto.
- Portal armazena `asana_project_gid` ou identificador equivalente.
- Falha no Asana não apaga o projeto interno.

---

### CV012 - Criação da task inicial no Asana com brainstorm

**Objetivo:** confirmar que o brainstorm é enviado para o Asana em task inicial.

**Passos:**

1. Converter uma ideia com brainstorm gerado.
2. Abrir projeto correspondente no Asana.
3. Localizar task `Brainstorm Estratégico IA`.
4. Conferir descrição da task.

**Resultado esperado:**

- Existe task inicial chamada `Brainstorm Estratégico IA`.
- A task contém:
  - ideia de origem;
  - framework SCAMPER;
  - solução recomendada;
  - justificativa da recomendação;
  - 3 soluções completas;
  - notas de impacto e esforço;
  - riscos e mitigações.

---

### CV013 - Sincronização Asana → Portal

**Objetivo:** confirmar que o portal recebe dados operacionais do Asana.

**Passos:**

1. Alterar informação operacional no Asana.
2. Acionar webhook ou aguardar cron de reconciliação.
3. Abrir detalhe do projeto no portal.

**Resultado esperado:**

- Cache `asana_sync` ou equivalente é atualizado.
- Bloco Asana no portal reflete a alteração.
- Falhas são registradas para diagnóstico.

---

### CV014 - Permissões internas

**Objetivo:** confirmar que perfis respeitam escopo de acesso.

**Passos:**

1. Acessar com perfil Diretoria.
2. Tentar editar/triagem/conversão.
3. Acessar com perfil Inovação.
4. Executar ações permitidas.

**Resultado esperado:**

- Diretoria acessa dados em leitura.
- Diretoria não executa ações de gestão.
- Inovação executa triagem, conversão e administração conforme permissão.
- Bloqueio ocorre também no backend/RLS, não apenas na interface.

---

### CV015 - Logs de auditoria

**Objetivo:** confirmar registro de ações relevantes.

**Passos:**

1. Submeter ideia.
2. Gerar brainstorm.
3. Converter em projeto.
4. Criar projeto/task no Asana.
5. Consultar logs.

**Resultado esperado:**

- Ações relevantes aparecem em `activity_log` ou mecanismo equivalente.
- Logs não expõem tokens, secrets ou dados sensíveis desnecessários.

---

## 5. Checklist mínimo de aceite

| Item | Status |
|---|---|
| Canvas público salva ideia válida | Pendente |
| Sugestão IA por bloco funciona | Pendente |
| Resumo IA é salvo/exibido | Pendente |
| Brainstorm SCAMPER gera 3 soluções | Pendente |
| Solução recomendada é exibida | Pendente |
| Impacto/esforço 1–10 são exibidos | Pendente |
| Matriz classifica quadrante corretamente | Pendente |
| Falha de IA não perde ideia | Pendente |
| Inovação consegue triar ideia | Pendente |
| Conversão cria projeto interno | Pendente |
| Projeto herda brainstorm | Pendente |
| Asana cria projeto | Pendente |
| Asana cria task inicial com brainstorm | Pendente |
| Bloco Asana lê cache sincronizado | Pendente |
| Permissões funcionam por perfil | Pendente |
| Logs funcionais são gerados | Pendente |

---

## 6. Critério final de aceite

A entrega pode ser considerada validada quando:

1. uma ideia realista for cadastrada pelo Canvas;
2. a IA gerar resumo e Brainstorm Estratégico SCAMPER;
3. a matriz classificar a ideia corretamente;
4. a Inovação conseguir converter a ideia em projeto;
5. o projeto interno preservar o brainstorm;
6. o Asana receber projeto e task inicial com o brainstorm;
7. falhas de IA/Asana forem tratadas sem perda de dados;
8. permissões e logs estiverem funcionando conforme esperado.
