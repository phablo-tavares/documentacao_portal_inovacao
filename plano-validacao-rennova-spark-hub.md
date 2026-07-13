# Plano de Validação — Portal de Gestão da Inovação Rennova

> Plano enxuto para validar os fluxos críticos do **Rennova Spark Hub** antes do aceite.  
> Baseado na versão 0.6 da especificação funcional.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Responsável | Phablo Tavares |
| Documento de referência | `especificacao-funcional-portal-inovacao.md`, versão 0.6 |
| Data | 2026-07-13 |
| Versão | 0.5 |
| Objetivo | Confirmar os fluxos principais, as permissões e a preservação dos dados em falhas. |

---

## 2. Como validar

A validação será manual e concentrada nos fluxos de maior risco. Para cada caso, registrar:

- `Aprovado`, `Reprovado` ou `Bloqueado`;
- uma evidência: captura de tela, registro no banco, log ou link do Asana;
- observação apenas quando houver desvio.

A entrega não pode ser aceita com falha crítica em submissão, permissões, triagem, conversão, template Asana, idempotência ou preservação dos dados.

---

## 3. Pré-requisitos

- usuário `inovacao` e usuário `diretoria`;
- acesso ao Supabase, Storage e logs;
- acesso ao Asana e ao template `INV | Modelo Base`;
- e-mails válidos dos quatro domínios e um e-mail de domínio não autorizado;
- arquivos de teste abaixo e acima de 50 MB;
- possibilidade de simular falhas da IA e do Asana.

---

## 4. Casos de validação

| ID | Fluxo | Execução mínima | Resultado esperado | Cobre |
|---|---|---|---|---|
| CV001 | Login, sessão e perfis | Entrar como Diretoria e Inovação; atualizar a página; tentar ações restritas. | Sessão segue o padrão do Supabase; Diretoria consulta e comenta, mas não altera notas, decisões ou cadastros; Inovação executa gestão; backend também bloqueia ações indevidas. | RF001, RF002 |
| CV002 | Canvas, domínios e CAPTCHA | Enviar com campo vazio, domínio inválido, sem CAPTCHA e com cada domínio autorizado. Tentar sair antes do envio. | Somente `@nutriex.com.br`, `@nutriex.com`, `@innovapharma.com` e `@rennova.com` são aceitos; CAPTCHA válido é obrigatório; ideia válida é criada; saída antes do envio apresenta aviso. | RF003, RF005 |
| CV003 | Sugestão e resumo por IA | Solicitar sugestão por bloco; editar ou ignorar; gerar resumo; simular falha da IA. | Sugestão considera o contexto e é editável; resumo não exibe impacto/esforço; falha da IA não impede preenchimento nem elimina ideia já enviada. | RF004, RF005 |
| CV004 | Brainstorm e retentativa | Gerar brainstorm; simular falha na primeira tentativa; simular falha nas duas; usar “Tentar novamente”. | Exatamente 3 soluções SCAMPER com notas, justificativas, viabilidade, riscos e mitigações; somente uma retentativa automática; após duas falhas a ideia permanece salva e Inovação pode tentar manualmente. | RF018, RF019 |
| CV005 | Matriz e triagem | Conferir quadrantes; acessar triagem como Diretoria e Inovação; tentar converter sem notas; arquivar sem e com justificativa. | Matriz usa escala 1–10; Diretoria não edita; notas finais são obrigatórias; arquivamento exige justificativa, responsável e data; ideia arquivada aparece no histórico. | RF007, RF008 |
| CV006 | Conversão e template Asana | Acionar “Vira Projeto”; tentar sem nome; informar `Portal de Teste`; converter; repetir a conversão. | Nome final `INV | Portal de Teste`; projeto interno vinculado à ideia; Asana usa template `1213945719343548`; estrutura é preservada; brainstorm fica na descrição; nenhuma task exclusiva é criada; repetição não duplica projeto. | RF009, RF020, RF021 |
| CV007 | Falha parcial Asana | Simular template inacessível e falha após criação do projeto; executar recuperação. | Não há sucesso falso; projeto interno é preservado; GID existente é salvo; estado parcial é registrado; recuperação reutiliza o projeto existente. | RF009, RF017, RF021 |
| CV008 | Entregas | Adicionar link; enviar arquivo menor que 50 MB; tentar maior que 50 MB; consultar como Diretoria; excluir como Inovação. | Link e arquivo são registrados; arquivo fica no Supabase Storage; limite é aplicado; Diretoria consulta; somente Inovação cria ou exclui; exclusão é auditada. | RF010 |
| CV009 | Comentários | Criar como Diretoria e Inovação; tentar editar; excluir comentário próprio; tentar excluir comentário alheio como Diretoria; excluir como Inovação. | Ambos podem comentar; edição é bloqueada; autor exclui o próprio; Diretoria não exclui comentário alheio; Inovação exclui qualquer comentário; ações geram log. | RF014, RF017 |
| CV010 | Sincronização Asana | Alterar tarefas; conferir webhook; simular perda do evento; executar ou aguardar cron. | `asana_sync` contém totais, status, responsáveis e datas; front-end usa cache; cron diário corrige divergências. | RF006, RF013, RF016 |
| CV011 | Fases, métricas e insight | Concluir fases; conferir progresso; registrar meta/resultado; gerar insight; simular falha da IA. | Progresso é recalculado; métricas permanecem no Supabase; falha da IA não remove meta nem resultado. | RF011, RF012 |
| CV012 | Segurança e auditoria | Inspecionar bundle e requisições; tentar escrita direta; executar ações críticas; consultar logs. | Nenhum secret está no front-end; RLS bloqueia operações indevidas; ações aparecem em `activity_log`; logs não expõem credenciais ou dados sensíveis. | RF002, RF003, RF015, RF017, RNFs |

---

## 5. Checklist de aceite

| Item | Status |
|---|---|
| Login, sessão e permissões funcionam no front-end e backend | Pendente |
| Canvas valida campos, domínios e CAPTCHA | Pendente |
| Sugestão, resumo e brainstorm funcionam | Pendente |
| Brainstorm respeita duas tentativas e retentativa manual | Pendente |
| Matriz, triagem e histórico de arquivadas funcionam | Pendente |
| Conversão exige notas finais e nome | Pendente |
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
- Diretoria conseguindo alterar decisão, nota ou cadastro restrito;
- conversão sem notas finais ou sem nome;
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