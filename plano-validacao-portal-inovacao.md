Biblioteca
/
plano-validacao-portal-inovacao.md


# Plano de Validação — Portal de Gestão da Inovação Rennova

> Plano enxuto para validar os fluxos críticos do **Rennova Spark Hub** antes do aceite.  
> Baseado na versão 0.7 da especificação funcional e na versão 0.6 do design técnico.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável | Phablo Tavares |
| Documento funcional de referência | `especificacao-funcional-portal-inovacao.md`, versão 0.7 |
| Documento técnico de referência | `design-tecnico-portal-inovacao.md`, versão 0.6 |
| Data | 2026-07-13 |
| Versão | 0.6 |
| Objetivo | Confirmar os fluxos principais, o cálculo reproduzível de Impacto × Esforço, as permissões e a preservação dos dados em falhas. |

---

## 2. Como validar

A validação será manual, complementada por testes unitários das fórmulas de pontuação. Para cada caso, registrar:

- `Aprovado`, `Reprovado` ou `Bloqueado`;
- uma evidência: captura de tela, resposta da API, registro no banco, log ou link do Asana;
- observação apenas quando houver desvio.

A entrega não pode ser aceita com falha crítica em submissão, permissões, cálculo de pontuação, triagem, conversão, template Asana, idempotência ou preservação dos dados.

---

## 3. Pré-requisitos

- usuário `inovacao` e usuário `diretoria`;
- acesso ao Supabase, Storage e logs;
- modelo de pontuação `1.0` semeado conforme as seções 5.3 e 5.4 da especificação;
- acesso ao Asana e ao template `INV | Modelo Base`;
- e-mails válidos dos quatro domínios e um e-mail de domínio não autorizado;
- arquivos de teste abaixo e acima de 50 MB;
- possibilidade de simular falhas da IA, do catálogo de pontuação e do Asana;
- duas ideias de teste com dados suficientes para calcular todas as notas.

### 3.1 Massa de teste para o cálculo

**Impacto:**

| Critério | Nota | Peso |
|---|---:|---:|
| Alinhamento estratégico | 7 | 20% |
| Gravidade da demanda | 6 | 15% |
| Ganho esperado | 8 | 25% |
| Alcance dos beneficiados | 5 | 15% |
| Potencial de escala | 6 | 15% |
| Urgência/redução de risco | 4 | 10% |

Resultado esperado: `6,35`, armazenado como `6,4` e arredondado para a matriz como `6`.

**Esforço:**

| Critério | Nota | Peso |
|---|---:|---:|
| Complexidade técnica | 6 | 25% |
| Integrações/dados externos | 5 | 20% |
| Tempo de implementação | 6 | 20% |
| Mudança operacional | 4 | 15% |
| Dependências | 3 | 10% |
| Custo de 12 meses | 2 | 10% |

Resultado esperado: `4,80`, armazenado como `4,8` e arredondado para a matriz como `5`.

A nota `6` em **Tempo estimado de implementação** deve aparecer com o significado exato **“De 16 a 22 dias úteis”**.

---

## 4. Casos de validação

| ID | Fluxo | Execução mínima | Resultado esperado | Cobre |
|---|---|---|---|---|
| CV001 | Login, sessão e perfis | Entrar como Diretoria e Inovação; atualizar a página; tentar ações restritas. | Sessão segue o padrão do Supabase; Diretoria consulta e comenta, mas não altera critérios, decisões ou cadastros; Inovação executa gestão; backend também bloqueia ações indevidas. | RF001, RF002 |
| CV002 | Canvas, domínios e CAPTCHA | Enviar com campo vazio, domínio inválido, sem CAPTCHA e com cada domínio autorizado. Tentar sair antes do envio. | Somente `@nutriex.com.br`, `@nutriex.com`, `@innovapharma.com` e `@rennova.com` são aceitos; CAPTCHA válido é obrigatório; ideia válida é criada; saída antes do envio apresenta aviso. | RF003, RF005 |
| CV003 | Sugestão e resumo por IA | Solicitar sugestão por bloco; editar ou ignorar; gerar resumo; simular falha da IA. | Sugestão considera o contexto e é editável; resumo não exibe Impacto/Esforço; falha da IA não impede preenchimento nem elimina ideia já enviada. | RF004, RF005 |
| CV004 | Brainstorm, critérios e retentativa | Gerar brainstorm; inspecionar as três soluções; simular falha na primeira tentativa e nas duas; usar “Tentar novamente”. | Exatamente 3 soluções SCAMPER; cada solução contém os 12 critérios, notas inteiras, justificativas, âncoras oficiais e resultados recalculados pelo backend; somente uma retentativa automática; após duas falhas a ideia permanece salva e Inovação pode tentar manualmente. | RF018, RF019 |
| CV005 | Cálculo de Impacto | Informar a massa de Impacto da seção 3.1; tentar omitir, duplicar ou usar nota fora de 1–10; comparar pesos e âncoras exibidos. | Backend aceita somente os seis critérios válidos, usa os pesos `20/15/25/15/15/10`, calcula `6,4`, arredonda para `6` e exibe o significado oficial de cada nota. Resultado final enviado pelo cliente ou IA é ignorado. | RF007, RF008, RF018; 5.3 |
| CV006 | Cálculo de Esforço | Informar a massa de Esforço da seção 3.1; conferir especialmente Tempo = 6; tentar valor decimal ou critério ausente. | Backend usa os pesos `25/20/20/15/10/10`, calcula `4,8`, arredonda para `5`; Tempo = 6 significa `16 a 22 dias úteis`; notas não inteiras, critérios ausentes ou justificativas vazias são bloqueados. | RF007, RF008, RF018; 5.4 |
| CV007 | Recalculo, matriz e triagem | Salvar a massa completa; alterar Alinhamento estratégico de 7 para 8; acessar como Diretoria e Inovação. | Impacto muda de `6,4/6` para `6,6/7`; Esforço permanece `4,8/5`; quadrante muda de `Retorno Limitado` para `Grande Projeto`; Diretoria somente consulta; Inovação revisa critérios e o sistema recalcula automaticamente. | RF007, RF008; 5.5 |
| CV008 | Conversão e template Asana | Tentar converter sem avaliação completa e sem nome; informar `Portal de Teste`; converter; repetir a conversão. | Conversão é bloqueada sem avaliação; nome final `INV | Portal de Teste`; projeto interno vinculado à ideia; Asana usa template `1213945719343548`; estrutura é preservada; brainstorm fica na descrição; nenhuma task exclusiva é criada; repetição não duplica projeto. | RF009, RF020, RF021 |
| CV009 | Falha parcial Asana | Simular template inacessível e falha após criação do projeto; executar recuperação. | Não há sucesso falso; projeto interno é preservado; GID existente é salvo; estado parcial é registrado; recuperação reutiliza o projeto existente. | RF009, RF017, RF021 |
| CV010 | Entregas | Adicionar link; enviar arquivo menor que 50 MB; tentar maior que 50 MB; consultar como Diretoria; excluir como Inovação. | Link e arquivo são registrados; arquivo fica no Supabase Storage; limite é aplicado; Diretoria consulta; somente Inovação cria ou exclui; exclusão é auditada. | RF010 |
| CV011 | Comentários | Criar como Diretoria e Inovação; tentar editar; excluir comentário próprio; tentar excluir comentário alheio como Diretoria; excluir como Inovação. | Ambos podem comentar; edição é bloqueada; autor exclui o próprio; Diretoria não exclui comentário alheio; Inovação exclui qualquer comentário; ações geram log. | RF014, RF017 |
| CV012 | Sincronização Asana | Alterar tarefas; conferir webhook; simular perda do evento; executar ou aguardar cron. | `asana_sync` contém totais, status, responsáveis e datas; front-end usa cache; cron diário corrige divergências. | RF006, RF013, RF016 |
| CV013 | Fases, métricas e insight | Concluir fases; conferir progresso; registrar meta/resultado; gerar insight; simular falha da IA. | Progresso é recalculado; métricas permanecem no Supabase; falha da IA não remove meta nem resultado. | RF011, RF012 |
| CV014 | Segurança e auditoria | Inspecionar bundle e requisições; tentar escrita direta e manipular resultados finais; executar ações críticas; consultar logs. | Nenhum secret está no front-end; RLS bloqueia operações indevidas; valores finais manipulados são ignorados; logs registram versão do modelo, alterações dos critérios e ações críticas sem expor credenciais. | RF002, RF003, RF007, RF008, RF015, RF017, RNFs |

---

## 5. Checklist de aceite

| Item | Status |
|---|---|
| Login, sessão e permissões funcionam no front-end e backend | Pendente |
| Canvas valida campos, domínios e CAPTCHA | Pendente |
| Sugestão, resumo e brainstorm funcionam | Pendente |
| Brainstorm respeita duas tentativas e retentativa manual | Pendente |
| As três soluções possuem os 12 critérios e justificativas | Pendente |
| Catálogo exibe pesos e significados exatos das notas | Pendente |
| Fórmula de Impacto retorna `6,4` para a massa definida | Pendente |
| Fórmula de Esforço retorna `4,8` para a massa definida | Pendente |
| Arredondamento da matriz usa metade para cima | Pendente |
| Alterar um critério recalcula resultados e quadrante | Pendente |
| Matriz, triagem e histórico de arquivadas funcionam | Pendente |
| Conversão exige avaliação final completa e nome | Pendente |
| Projeto usa o template Asana `1213945719343548` | Pendente |
| Brainstorm está na descrição e não em task exclusiva | Pendente |
| Conversão não cria duplicidade e recupera falha parcial | Pendente |
| Entregas usam Storage e respeitam 50 MB | Pendente |
| Comentários não podem ser editados e respeitam exclusão | Pendente |
| Webhook e cron atualizam o cache do Asana | Pendente |
| Fases, métricas e insights funcionam | Pendente |
| Logs e controles de segurança foram verificados | Pendente |

---

## 6. Falhas que bloqueiam o aceite

- submissão aceita sem CAPTCHA válido ou com domínio não autorizado;
- exposição de tokens, secrets ou `service_role`;
- Diretoria conseguindo alterar critérios, decisão ou cadastro restrito;
- peso, âncora ou critério divergente da especificação funcional 0.7;
- nota final calculada pelo cliente ou pela IA sendo aceita sem recálculo do backend;
- critério ausente, duplicado, fora da escala ou sem justificativa sendo persistido;
- fórmula ou arredondamento produzindo resultado diferente da massa de teste;
- matriz usando valor decimal no lugar do valor inteiro arredondado;
- conversão sem avaliação final completa ou sem nome;
- criação de projeto fora do template obrigatório;
- projeto duplicado após retentativa;
- perda da ideia ou do projeto interno por falha de IA ou Asana;
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