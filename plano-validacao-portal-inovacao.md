# Plano de Validação — Portal de Gestão da Inovação Rennova

> Plano enxuto para validar os fluxos críticos do **Rennova Spark Hub** antes do aceite.  
> Baseado na versão 0.8 da especificação funcional e na versão 0.7 do design técnico.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável | Phablo Tavares |
| Documento funcional de referência | `especificacao-funcional-portal-inovacao.md`, versão 0.8 |
| Documento técnico de referência | `design-tecnico-portal-inovacao.md`, versão 0.7 |
| Data | 2026-07-14 |
| Versão | 0.7 |
| Objetivo | Confirmar o acesso protegido ao Canvas, a complementação por IA, a pontuação reproduzível, as permissões e a preservação dos dados em falhas. |

---

## 2. Como validar

A validação será manual, complementada por testes unitários do motor de pontuação. Para cada caso, registrar:

- `Aprovado`, `Reprovado` ou `Bloqueado`;
- uma evidência: captura de tela, resposta da API, registro no banco, log ou link do Asana;
- observação apenas quando houver desvio.

A entrega não pode ser aceita com falha crítica no CAPTCHA, submissão, complementação, permissões, pontuação, triagem, conversão, template Asana, idempotência ou preservação dos dados.

---

## 3. Pré-requisitos

- usuário `inovacao` e usuário `diretoria`;
- acesso ao Supabase, Storage e logs;
- modelo de pontuação `2.0` semeado conforme as seções 5.3 e 5.4;
- acesso ao Asana e ao template `INV | Modelo Base`;
- e-mails válidos dos quatro domínios e um domínio não autorizado;
- arquivos de teste abaixo e acima de 50 MB;
- possibilidade de simular falhas da IA, CAPTCHA, catálogo e Asana;
- um Canvas claramente suficiente;
- um Canvas que exija complementação;
- um Canvas que permaneça incompleto após respostas parciais.

### 3.1 Massa de teste para o cálculo

**Impacto:**

| Critério | Nota | Peso |
|---|---:|---:|
| Gravidade da demanda | 6 | 20% |
| Ganho esperado | 8 | 30% |
| Alcance dos beneficiados | 6 | 20% |
| Potencial de escala | 8 | 20% |
| Urgência/redução de risco | 4 | 10% |

Resultado esperado: `6,8`, arredondado para a matriz como `7`.

**Esforço:**

| Critério | Nota | Peso |
|---|---:|---:|
| Complexidade técnica | 6 | 30% |
| Integrações/dados externos | 4 | 25% |
| Tempo de implementação | 6 | 20% |
| Mudança operacional | 4 | 15% |
| Custo de 12 meses | 2 | 10% |

Resultado esperado: `4,8`, arredondado para a matriz como `5`.

A nota `6` em **Tempo estimado de implementação** deve aparecer com o significado exato **“De 11 a 22 dias úteis”**.

---

## 4. Casos de validação

| ID | Fluxo | Execução mínima | Resultado esperado | Cobre |
|---|---|---|---|---|
| CV001 | Login, sessão e perfis | Entrar como Diretoria e Inovação; atualizar a página; tentar ações restritas. | Sessão segue o Supabase; Diretoria consulta e comenta sem alterar decisões; Inovação executa gestão; backend bloqueia ações indevidas. | RF001, RF002 |
| CV002 | CAPTCHA antes do Canvas | Acessar `/canvas`; tentar visualizar ou chamar APIs sem CAPTCHA; validar CAPTCHA; expirar a sessão durante o preenchimento. | Antes da validação somente o CAPTCHA é exibido; APIs públicas rejeitam sessão ausente; após validação o Canvas é liberado; expiração solicita novo CAPTCHA sem perder dados locais. | RF003, RF022 |
| CV003 | Canvas, domínios, sugestão e resumo | Testar campo vazio, domínio inválido e quatro domínios válidos; solicitar sugestão; gerar e editar resumo. | Campos obrigatórios e domínio são validados; sugestão é editável; resumo considera o contexto disponível e não exibe notas. | RF003, RF004, RF005 |
| CV004 | Canvas suficiente | Preencher uma ideia completa e solicitar continuidade. | IA registra contexto suficiente; nenhum modal é aberto; fluxo segue para o resumo. | RF022 |
| CV005 | Complementação única | Preencher Canvas insuficiente; conferir perguntas; responder parcialmente; tentar provocar nova rodada; concluir envio. | Abre somente um modal com 1 a 10 perguntas contextuais; respostas parciais são aceitas; não há segunda rodada; perguntas e respostas são persistidas. | RF005, RF019, RF022 |
| CV006 | Falha da avaliação de suficiência | Simular timeout ou JSON inválido; enviar a ideia; acessar o detalhe como Inovação; executar retentativa. | Ideia é salva; brainstorm fica aguardando avaliação; não há perda de dados; retentativa interna conclui a avaliação e inicia o brainstorm sem novo modal público. | RF003, RF018, RF019, RF022 |
| CV007 | Brainstorm e retentativas | Gerar brainstorm; inspecionar soluções; simular falha na primeira e nas duas tentativas; usar “Tentar novamente”. | Exatamente 3 soluções SCAMPER; cada solução contém 5 critérios de Impacto e 5 de Esforço; somente uma retentativa automática; após duas falhas a ideia permanece salva. | RF018, RF019 |
| CV008 | Cálculo de Impacto | Usar a massa da seção 3.1; omitir, duplicar ou usar nota não permitida; testar nota `2` em alcance. | Backend usa pesos `20/30/20/20/10`, calcula `6,8` e matriz `7`; exige cinco critérios; rejeita nota fora de `2/4/6/8/10` e rejeita `2` em alcance. | RF007, RF008, RF018; 5.3 |
| CV009 | Cálculo de Esforço | Usar a massa da seção 3.1; tentar nota decimal, ímpar ou critério ausente. | Backend usa pesos `30/25/20/15/10`, calcula `4,8` e matriz `5`; Tempo = 6 significa `11 a 22 dias úteis`; valores inválidos são bloqueados. | RF007, RF008, RF018; 5.4 |
| CV010 | Recalculo, matriz e triagem | Salvar a massa; alterar Ganho esperado de 8 para 6; acessar como Diretoria e Inovação. | Impacto muda de `6,8/7` para `6,2/6`; quadrante muda de `Grande Projeto` para `Retorno Limitado`; Diretoria consulta; Inovação revisa e o backend recalcula. | RF007, RF008; 5.5 |
| CV011 | Detalhe interno da ideia | Abrir ideia com complementação como Diretoria e Inovação. | Canvas, decisão de suficiência, perguntas, respostas, resumo, brainstorm e pontuações são exibidos em leitura; prompts e dados técnicos não são expostos. | RF019, RF022 |
| CV012 | Conversão e template Asana | Tentar converter sem avaliação final e sem nome; informar `Portal de Teste`; converter; repetir. | Conversão é bloqueada quando inválida; nome final `INV | Portal de Teste`; template correto é usado; brainstorm fica na descrição; repetição não duplica projeto. | RF009, RF020, RF021 |
| CV013 | Falha parcial Asana | Simular template inacessível e falha após criação; executar recuperação. | Não há sucesso falso; projeto interno e GID são preservados; recuperação reutiliza o projeto existente. | RF009, RF017, RF021 |
| CV014 | Entregas | Adicionar link; enviar arquivo menor e maior que 50 MB; consultar como Diretoria; excluir como Inovação. | Link e arquivo válidos são registrados; limite é aplicado; Diretoria consulta; somente Inovação cria ou exclui; exclusão é auditada. | RF010 |
| CV015 | Comentários | Criar como Diretoria e Inovação; tentar editar e excluir conforme diferentes permissões. | Comentários não são editáveis; autor exclui o próprio; Inovação exclui qualquer; ações geram log. | RF014, RF017 |
| CV016 | Sincronização Asana | Alterar tarefas; conferir webhook; simular perda do evento; executar cron. | `asana_sync` é atualizado; front-end usa cache; cron corrige divergências. | RF006, RF013, RF016 |
| CV017 | Fases, métricas e insight | Concluir fases; registrar meta/resultado; gerar insight; simular falha da IA. | Progresso é recalculado; métricas permanecem salvas; falha da IA não remove dados. | RF011, RF012 |
| CV018 | Segurança e auditoria | Inspecionar bundle e requisições; tentar escrita direta, reutilizar sessão, criar segunda rodada e manipular resultados. | Nenhum secret está no front-end; RLS bloqueia escrita; sessão expirada ou consumida é rejeitada; segunda rodada é impedida; resultados externos são ignorados; logs não expõem tokens ou respostas completas. | RF002, RF003, RF007, RF008, RF017, RF022, RNFs |

---

## 5. Checklist de aceite

| Item | Status |
|---|---|
| CAPTCHA é exibido antes do Canvas e validado no backend | Pendente |
| Sessão do Canvas é temporária, restrita e renovável sem perda local | Pendente |
| Canvas valida campos e domínios autorizados | Pendente |
| Canvas suficiente não abre modal | Pendente |
| Canvas insuficiente abre uma única rodada com até 10 perguntas | Pendente |
| Respostas parciais não bloqueiam o envio | Pendente |
| Perguntas e respostas aparecem no detalhe interno | Pendente |
| Falha de suficiência preserva a ideia e permite recuperação | Pendente |
| Resumo usa Canvas e complementação disponível | Pendente |
| Brainstorm respeita 3 soluções e duas tentativas automáticas | Pendente |
| Cada solução possui 5 critérios de Impacto e 5 de Esforço | Pendente |
| Catálogo exibe pesos, notas permitidas e âncoras oficiais | Pendente |
| Fórmula de Impacto retorna `6,8` para a massa definida | Pendente |
| Fórmula de Esforço retorna `4,8` para a massa definida | Pendente |
| Alcance rejeita a nota `2` | Pendente |
| Arredondamento usa metade para cima | Pendente |
| Alterar um critério recalcula resultado e quadrante | Pendente |
| Matriz, triagem e histórico funcionam | Pendente |
| Conversão exige avaliação final e nome | Pendente |
| Projeto usa o template Asana `1213945719343548` | Pendente |
| Brainstorm está na descrição e não em task exclusiva | Pendente |
| Conversão é idempotente e recupera falha parcial | Pendente |
| Entregas usam Storage e respeitam 50 MB | Pendente |
| Comentários respeitam imutabilidade e exclusão | Pendente |
| Webhook e cron atualizam o cache do Asana | Pendente |
| Fases, métricas e insights funcionam | Pendente |
| Logs e controles de segurança foram verificados | Pendente |

---

## 6. Falhas que bloqueiam o aceite

- Canvas exibido sem CAPTCHA válido;
- API pública aceitando sessão ausente, expirada ou inválida;
- exposição de tokens, secrets ou `service_role`;
- domínio não autorizado aceito;
- mais de uma rodada pública de complementação ou mais de 10 perguntas;
- respostas parciais bloqueando indevidamente a submissão;
- perguntas e respostas não persistidas com a ideia;
- falha de suficiência causando perda da ideia;
- brainstorm iniciado automaticamente enquanto a avaliação está em erro;
- Diretoria alterando critérios, decisão ou cadastro restrito;
- peso, critério, nota permitida ou âncora divergente da especificação 0.8;
- resultado calculado pelo cliente ou IA aceito sem recálculo do backend;
- critério ausente, duplicado ou sem justificativa persistido;
- nota fora da escala aceita, incluindo nota `2` em alcance;
- fórmula ou arredondamento diferente da massa de teste;
- conversão sem avaliação final completa ou sem nome;
- criação de projeto fora do template obrigatório;
- projeto duplicado após retentativa;
- perda da ideia ou projeto interno por falha de IA ou Asana;
- arquivo acima de 50 MB aceito;
- edição de comentário publicado.

---

## 7. Registro da execução

| Caso | Resultado | Evidência | Observação |
|---|---|---|---|
| CV001 | Pendente | - | - |
| CV002 | Pendente | - | - |
| CV003 | Pendente | - | - |
| CV004 | Pendente | - | - |
| CV005 | Pendente | - | - |
| CV006 | Pendente | - | - |
| CV007 | Pendente | - | - |
| CV008 | Pendente | - | - |
| CV009 | Pendente | - | - |
| CV010 | Pendente | - | - |
| CV011 | Pendente | - | - |
| CV012 | Pendente | - | - |
| CV013 | Pendente | - | - |
| CV014 | Pendente | - | - |
| CV015 | Pendente | - | - |
| CV016 | Pendente | - | - |
| CV017 | Pendente | - | - |
| CV018 | Pendente | - | - |