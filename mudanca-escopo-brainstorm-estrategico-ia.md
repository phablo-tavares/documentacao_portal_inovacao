# Mudança de Escopo — Brainstorm Estratégico com IA

> Complemento da documentação funcional e técnica do **Rennova Spark Hub — Portal de Gestão da Inovação**.  
> Esta mudança adiciona a geração de brainstorm estratégico com IA no fluxo de cadastro e conversão de ideias em projetos.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | Rennova Spark Hub — Portal de Gestão da Inovação |
| Tipo | Mudança de escopo funcional e técnica |
| Solicitante | Gerência |
| Responsável pela documentação | Phablo Tavares |
| Data | 2026-07-08 |
| Status | Proposto para implementação |

---

## 2. Contexto da mudança

A gerência solicitou que, ao cadastrar uma ideia no **Backlog de Ideias de Inovação**, o sistema gere automaticamente um **Brainstorm Estratégico com IA**.

O objetivo é apoiar a análise inicial da ideia, apresentando alternativas de solução mais estruturadas antes da conversão em projeto.

A funcionalidade deve permitir que a IA:

1. Analise a demanda cadastrada.
2. Gere 3 possíveis soluções estratégicas.
3. Use um framework de inovação como base do raciocínio.
4. Atribua notas claras de impacto e esforço.
5. Classifique a ideia/soluções na matriz Impacto × Esforço.
6. Recomende uma das soluções.
7. Leve o brainstorm para o Asana quando a ideia for convertida em projeto.

---

## 3. Escopo adicionado

O sistema deverá:

1. Gerar automaticamente um brainstorm estratégico ao cadastrar uma nova ideia.
2. Usar o framework **SCAMPER** como base de ideação.
3. Gerar exatamente 3 possíveis soluções estratégicas para a demanda.
4. Para cada solução, registrar:
   - abordagem SCAMPER aplicada;
   - descrição da solução;
   - racional estratégico;
   - como resolve a demanda;
   - impacto estimado;
   - esforço estimado;
   - análise de viabilidade;
   - riscos principais;
   - mitigações sugeridas.
5. Eleger uma das 3 soluções como recomendada.
6. Justificar a recomendação da IA.
7. Persistir o brainstorm vinculado à ideia.
8. Copiar o brainstorm para o projeto quando a ideia for convertida.
9. Criar uma task inicial no Asana com o conteúdo completo do brainstorm.

---

## 4. Fora de escopo nesta mudança

Não fazem parte desta mudança:

1. Edição colaborativa avançada do brainstorm.
2. Versionamento completo de múltiplas gerações de IA.
3. Comparação histórica entre brainstorms gerados.
4. Aprovação formal de cada solução individual.
5. Treinamento de modelo próprio de IA.
6. Cálculo financeiro detalhado de ROI.
7. Substituição da triagem mensal de ideias.
8. Substituição da decisão humana da área de Inovação.

---

## 5. Framework de inovação adotado

### 5.1 Framework principal

O framework recomendado para a geração do brainstorm é o **SCAMPER**.

O SCAMPER deve ser usado pela IA como base para propor alternativas de inovação a partir da demanda cadastrada.

As abordagens possíveis são:

| Letra | Abordagem | Uso no contexto do portal |
|---|---|---|
| S | Substituir | Trocar processo, ferramenta, etapa, tecnologia ou abordagem atual por outra mais eficiente. |
| C | Combinar | Unir processos, sistemas, áreas, dados ou soluções já existentes para criar uma solução melhor. |
| A | Adaptar | Adaptar uma prática, tecnologia ou solução de outro contexto para a demanda apresentada. |
| M | Modificar | Melhorar, ampliar, simplificar ou redesenhar algo existente. |
| P | Propor outro uso | Reaproveitar ativos, dados, sistemas ou processos existentes para uma nova finalidade. |
| E | Eliminar | Remover etapas, retrabalhos, controles manuais ou complexidades desnecessárias. |
| R | Reorganizar | Reordenar fluxos, responsabilidades, etapas, integrações ou jornadas. |

### 5.2 Regra de uso do SCAMPER

A IA não precisa usar todas as abordagens do SCAMPER em toda ideia.

Regra obrigatória:

> Cada uma das 3 soluções deve indicar explicitamente qual abordagem SCAMPER foi aplicada. Sempre que possível, as 3 soluções devem explorar abordagens diferentes para evitar respostas repetitivas.

Exemplo:

| Solução | Abordagem SCAMPER |
|---|---|
| Solução 1 | Adaptar |
| Solução 2 | Combinar |
| Solução 3 | Reorganizar |

---

## 6. Estrutura obrigatória de cada solução

Cada solução gerada pela IA deve seguir a estrutura abaixo.

```md
### Solução [n] — [Nome da solução]

**Abordagem SCAMPER aplicada:**  
[Substituir / Combinar / Adaptar / Modificar / Propor outro uso / Eliminar / Reorganizar]

**Descrição da solução:**  
[Explicação objetiva da solução proposta]

**Racional estratégico:**  
[Por que essa solução faz sentido para a demanda e para a Rennova]

**Como resolve a demanda:**  
[Explicação prática de como a solução endereça o problema ou oportunidade]

**Impacto estimado:**  
Nota: [1 a 10]  
Justificativa: [...]

**Esforço estimado:**  
Nota: [1 a 10]  
Justificativa: [...]

**Análise de viabilidade:**  
[Análise técnica, operacional, financeira e de prazo]

**Riscos principais:**  
- [Risco 1]
- [Risco 2]
- [Risco 3]

**Mitigações sugeridas:**  
- [Mitigação 1]
- [Mitigação 2]
```

---

## 7. Métrica de Impacto

A nota de **Impacto** deve ir de **1 a 10**.

| Nota | Interpretação |
|---|---|
| 1 a 3 | Baixo impacto |
| 4 a 6 | Impacto moderado |
| 7 a 8 | Alto impacto |
| 9 a 10 | Impacto estratégico/crítico |

### 7.1 Critérios de composição da nota de impacto

| Critério | Peso |
|---|---:|
| Alinhamento estratégico com objetivos da Rennova | 20% |
| Gravidade ou relevância da demanda | 15% |
| Ganho esperado de eficiência, receita, economia, qualidade ou compliance | 25% |
| Quantidade de áreas, usuários ou processos beneficiados | 15% |
| Potencial de escala/reutilização em outras áreas | 15% |
| Urgência ou redução de risco relevante | 10% |

### 7.2 Regra de justificativa

A IA deve justificar a nota de impacto em linguagem objetiva.

Exemplo:

```md
Impacto estimado: 8/10

Justificativa: A solução tem forte alinhamento estratégico, reduz retrabalho operacional e pode ser reutilizada por mais de uma área. O impacto não recebeu nota máxima porque depende de adesão dos usuários e integração com sistemas internos.
```

---

## 8. Métrica de Esforço

A nota de **Esforço** deve ir de **1 a 10**.

Quanto maior a nota, maior o esforço necessário.

| Nota | Interpretação |
|---|---|
| 1 a 3 | Baixo esforço |
| 4 a 6 | Esforço moderado |
| 7 a 8 | Alto esforço |
| 9 a 10 | Esforço muito alto/crítico |

### 8.1 Critérios de composição da nota de esforço

| Critério | Peso |
|---|---:|
| Complexidade técnica | 25% |
| Necessidade de integrações ou dados externos | 20% |
| Tempo estimado de implementação | 20% |
| Mudança operacional/processual necessária | 15% |
| Dependência de outras áreas, fornecedores ou aprovações | 10% |
| Custo estimado de implantação/manutenção | 10% |

### 8.2 Regra de justificativa

A IA deve justificar a nota de esforço em linguagem objetiva.

Exemplo:

```md
Esforço estimado: 6/10

Justificativa: A solução exige integração com sistema interno e validação com área usuária, mas não demanda construção de infraestrutura complexa nem alto investimento inicial.
```

---

## 9. Regra da matriz Impacto × Esforço

A classificação na matriz deve seguir a regra abaixo.

| Quadrante | Critério | Interpretação |
|---|---|---|
| Oportunidade Imediata | Impacto >= 7 e Esforço <= 4 | Alta prioridade. Deve ser considerada para execução rápida. |
| Grande Projeto | Impacto >= 7 e Esforço >= 5 | Alta relevância, mas exige planejamento, sponsor e recursos. |
| Ganho Tático / Astuto | Impacto entre 4 e 6 e Esforço <= 4 | Pode ser executado se houver capacidade disponível ou ganho operacional claro. |
| Retorno Limitado | Impacto <= 6 e Esforço >= 5 | Baixa prioridade. Só deve avançar com justificativa forte. |
| Baixa Atratividade | Impacto <= 3 | Normalmente não priorizar, salvo obrigação regulatória, compliance ou decisão estratégica. |

### 9.1 Observação sobre a ideia e as soluções

A IA pode atribuir impacto e esforço para cada solução individual.

Para a ideia no backlog, o sistema deve usar preferencialmente as notas da **solução recomendada** como referência inicial de impacto, esforço e quadrante.

A área de Inovação poderá revisar manualmente as notas durante a triagem.

---

## 10. Regra para recomendação da IA

A IA não deve escolher necessariamente a solução mais inovadora ou mais ambiciosa.

A solução recomendada deve ser aquela com melhor equilíbrio entre:

1. impacto;
2. esforço;
3. viabilidade;
4. riscos controláveis;
5. aderência à demanda original;
6. possibilidade de execução no contexto da Rennova.

Formato obrigatório da recomendação:

```md
## Solução recomendada pela IA

**Solução escolhida:** [Nome da solução]

**Justificativa:**  
[A solução foi recomendada porque apresenta melhor relação entre impacto, esforço e viabilidade...]
```

---

## 11. Requisitos funcionais adicionados

### RF018 - Gerar brainstorm estratégico com IA

| Item | Especificação |
|---|---|
| Descrição | Gerar automaticamente um brainstorm estratégico com IA ao cadastrar uma nova ideia no backlog. |
| Ator | Sistema / IA. |
| Pré-condições | Ideia cadastrada com dados mínimos suficientes para análise. |
| Fluxo principal | 1. Usuário cadastra ideia.<br>2. Sistema salva a ideia.<br>3. Sistema aciona Edge Function de IA.<br>4. IA gera 3 soluções baseadas em SCAMPER.<br>5. Sistema valida a resposta estruturada.<br>6. Sistema salva o brainstorm vinculado à ideia. |
| Exceções | Falha da IA; resposta inválida; timeout; dados insuficientes. |
| Critérios de aceite | Brainstorm contém 3 soluções, cada solução possui os campos obrigatórios, uma solução é recomendada e há justificativa para impacto/esforço. |

### RF019 - Exibir brainstorm no detalhe da ideia

| Item | Especificação |
|---|---|
| Descrição | Exibir o brainstorm estratégico no detalhe da ideia. |
| Ator | Inovação. |
| Pré-condições | Ideia existente no backlog. |
| Fluxo principal | 1. Usuário abre detalhe da ideia.<br>2. Sistema exibe status do brainstorm.<br>3. Se gerado, exibe as 3 soluções e destaca a recomendada. |
| Exceções | Brainstorm pendente ou com erro. |
| Critérios de aceite | O usuário visualiza as soluções, notas, riscos, mitigações e recomendação antes de converter a ideia em projeto. |

### RF020 - Copiar brainstorm para projeto convertido

| Item | Especificação |
|---|---|
| Descrição | Ao converter uma ideia em projeto, copiar o brainstorm estratégico para o registro do projeto. |
| Ator | Inovação / Sistema. |
| Pré-condições | Ideia aprovada para conversão. |
| Fluxo principal | 1. Usuário aciona conversão em projeto.<br>2. Sistema cria projeto interno.<br>3. Sistema copia o brainstorm da ideia para o projeto.<br>4. Sistema mantém rastreabilidade com a ideia original. |
| Exceções | Brainstorm ausente; erro na criação do projeto. |
| Critérios de aceite | Projeto criado contém referência à ideia original e ao brainstorm estratégico usado na decisão. |

### RF021 - Criar task inicial no Asana com brainstorm

| Item | Especificação |
|---|---|
| Descrição | Criar uma task inicial no projeto do Asana contendo o brainstorm estratégico completo. |
| Ator | Sistema / Asana API. |
| Pré-condições | Projeto interno criado; projeto Asana criado ou identificado. |
| Fluxo principal | 1. Sistema cria/identifica projeto no Asana.<br>2. Sistema cria task inicial chamada `Brainstorm Estratégico IA`.<br>3. Sistema preenche a descrição da task com o brainstorm completo. |
| Exceções | Falha na API do Asana; projeto Asana não criado; brainstorm ausente. |
| Critérios de aceite | O projeto no Asana contém uma task inicial com as 3 soluções, a recomendação da IA e as notas de impacto/esforço. |

---

## 12. Regras de negócio adicionadas

| Código | Regra |
|---|---|
| RN018 | O brainstorm estratégico deve ser gerado após o cadastro da ideia. |
| RN019 | A ideia deve ser salva mesmo se a geração do brainstorm falhar. |
| RN020 | Uma resposta válida da IA deve conter exatamente 3 soluções. |
| RN021 | Cada solução deve indicar uma abordagem SCAMPER aplicada. |
| RN022 | Cada solução deve conter nota de impacto e esforço de 1 a 10. |
| RN023 | A solução recomendada deve ser uma das 3 soluções geradas. |
| RN024 | A justificativa da solução recomendada deve considerar impacto, esforço, viabilidade e riscos. |
| RN025 | As notas da solução recomendada devem alimentar a classificação inicial da matriz Impacto × Esforço da ideia. |
| RN026 | A área de Inovação pode revisar manualmente impacto, esforço e quadrante na triagem. |
| RN027 | Ao converter a ideia em projeto, o brainstorm deve ser copiado para o projeto interno. |
| RN028 | Ao criar o projeto no Asana, o sistema deve criar uma task inicial com o conteúdo completo do brainstorm. |

---

## 13. Fluxo funcional atualizado

```text
Usuário cadastra ideia
  -> Sistema salva ideia no backlog
  -> Sistema aciona IA para gerar Brainstorm Estratégico
  -> IA usa SCAMPER como framework de geração
  -> IA retorna 3 soluções estruturadas
  -> Sistema valida estrutura da resposta
  -> Sistema calcula/registra impacto, esforço e quadrante
  -> Sistema salva brainstorm vinculado à ideia
  -> Usuário visualiza brainstorm no detalhe da ideia
  -> Usuário aprova/converte ideia em projeto
  -> Sistema cria projeto interno
  -> Sistema cria projeto no Asana
  -> Sistema cria task inicial no Asana com o Brainstorm Estratégico
```

---

## 14. Impactos no modelo de dados

### 14.1 Estrutura conceitual sugerida

```ts
interface StrategicBrainstorm {
  status: "pendente" | "gerando" | "gerado" | "erro";
  framework: "SCAMPER";
  generatedAt?: string;
  recommendedSolutionId?: string;
  recommendationReason?: string;
  solutions: BrainstormSolution[];
  errorMessage?: string;
}

interface BrainstormSolution {
  id: string;
  title: string;
  scamperApproach:
    | "substituir"
    | "combinar"
    | "adaptar"
    | "modificar"
    | "propor_outro_uso"
    | "eliminar"
    | "reorganizar";
  description: string;
  strategicRationale: string;
  demandResolution: string;
  impactScore: number;
  impactJustification: string;
  effortScore: number;
  effortJustification: string;
  viabilityAnalysis: string;
  risks: string[];
  mitigations: string[];
}
```

### 14.2 Alteração sugerida em `ideas`

Adicionar campos ou estrutura equivalente:

| Campo | Tipo sugerido | Observação |
|---|---|---|
| `strategic_brainstorm` | `jsonb` | Brainstorm completo gerado pela IA. |
| `brainstorm_status` | enum/text | `pendente`, `gerando`, `gerado`, `erro`. |
| `brainstorm_generated_at` | timestamp | Data/hora da geração. |
| `recommended_solution_id` | text | ID da solução recomendada. |

### 14.3 Alteração sugerida em `projects`

Adicionar campos ou estrutura equivalente:

| Campo | Tipo sugerido | Observação |
|---|---|---|
| `origin_idea_id` | uuid | Rastreabilidade da ideia original. |
| `strategic_brainstorm` | `jsonb` | Cópia do brainstorm no momento da conversão. |
| `recommended_solution_id` | text | Solução recomendada herdada da ideia. |

---

## 15. Impactos nas Edge Functions / APIs

### 15.1 Nova função sugerida

```text
POST /functions/v1/ai-generate-strategic-brainstorm
```

Responsabilidade:

1. Receber dados da ideia.
2. Montar prompt seguro para a IA.
3. Exigir resposta estruturada em JSON.
4. Validar quantidade de soluções e campos obrigatórios.
5. Retornar o brainstorm para persistência.

### 15.2 Ajuste em função existente de conversão

A função responsável por converter ideia em projeto deve passar a:

1. Ler o brainstorm vinculado à ideia.
2. Criar o projeto interno com cópia do brainstorm.
3. Criar projeto no Asana.
4. Criar task inicial no Asana com o brainstorm completo.
5. Registrar log funcional em caso de sucesso ou falha.

---

## 16. Contrato JSON esperado da IA

A resposta da IA deve ser validada antes da gravação.

```json
{
  "framework": "SCAMPER",
  "solutions": [
    {
      "id": "solution_1",
      "title": "string",
      "scamperApproach": "adaptar",
      "description": "string",
      "strategicRationale": "string",
      "demandResolution": "string",
      "impactScore": 8,
      "impactJustification": "string",
      "effortScore": 5,
      "effortJustification": "string",
      "viabilityAnalysis": "string",
      "risks": ["string"],
      "mitigations": ["string"]
    }
  ],
  "recommendedSolutionId": "solution_1",
  "recommendationReason": "string"
}
```

Validações mínimas:

1. `framework` deve ser `SCAMPER`.
2. `solutions` deve conter exatamente 3 itens.
3. Cada solução deve ter `impactScore` entre 1 e 10.
4. Cada solução deve ter `effortScore` entre 1 e 10.
5. `recommendedSolutionId` deve existir dentro de `solutions`.
6. Campos textuais obrigatórios não podem estar vazios.

---

## 17. Conteúdo da task inicial no Asana

Na conversão da ideia em projeto, o sistema deve criar uma task inicial no Asana chamada:

```text
Brainstorm Estratégico IA
```

Descrição sugerida da task:

```md
# Brainstorm Estratégico IA

Ideia de origem: [Título da ideia]  
Área de origem: [Área]  
Área impactada: [Área]  
Data da geração: [Data]

## Framework utilizado

SCAMPER

## Solução recomendada

**[Nome da solução]**

**Justificativa da recomendação:**  
[...]

---

## Solução 1 — [Nome]

**Abordagem SCAMPER aplicada:**  
[...]

**Descrição:**  
[...]

**Racional estratégico:**  
[...]

**Como resolve a demanda:**  
[...]

**Impacto estimado:**  
Nota: [1-10]  
Justificativa: [...]

**Esforço estimado:**  
Nota: [1-10]  
Justificativa: [...]

**Análise de viabilidade:**  
[...]

**Riscos:**  
- [...]

**Mitigações:**  
- [...]

---

## Solução 2 — [Nome]
[...]

---

## Solução 3 — [Nome]
[...]
```

---

## 18. Tratamento de falhas

| Situação | Comportamento esperado |
|---|---|
| Falha na IA durante cadastro | Ideia deve ser salva; brainstorm fica com status `erro`; usuário vê mensagem amigável. |
| Timeout da IA | Ideia deve ser salva; sistema pode permitir nova tentativa. |
| JSON inválido retornado pela IA | Não gravar brainstorm inválido; registrar erro técnico; permitir nova tentativa. |
| Falha ao criar task no Asana | Projeto não deve ser perdido; registrar erro; permitir retentativa da sincronização Asana. |
| Brainstorm ausente na conversão | Permitir conversão apenas se a regra funcional aprovar; caso contrário, exigir geração antes da conversão. |

Recomendação funcional:

> Para preservar a qualidade da conversão, a ideia só deve ser convertida em projeto se o brainstorm estiver gerado ou se um usuário de Inovação confirmar explicitamente a conversão sem brainstorm.

---

## 19. Impactos nas telas

### 19.1 Detalhe da ideia

Adicionar seção:

```text
Brainstorm Estratégico IA
```

A seção deve exibir:

1. status da geração;
2. framework utilizado;
3. 3 soluções geradas;
4. destaque visual da solução recomendada;
5. notas de impacto e esforço;
6. riscos e mitigações;
7. justificativa da recomendação.

### 19.2 Backlog de ideias

A lista de ideias pode exibir indicador resumido:

| Campo | Exemplo |
|---|---|
| Brainstorm | Gerado / Pendente / Erro |
| Solução recomendada | Automação via integração X |
| Impacto | 8 |
| Esforço | 5 |
| Quadrante | Grande Projeto |

### 19.3 Conversão em projeto

Antes de confirmar a conversão, o sistema deve indicar:

1. se o brainstorm será copiado para o projeto;
2. se será criada uma task inicial no Asana;
3. qual solução está recomendada pela IA.

---

## 20. Critérios de aceite da mudança

### CA001 - Cadastro com brainstorm gerado

Dado que uma ideia foi cadastrada com dados suficientes, quando o cadastro for concluído, então o sistema deve gerar um brainstorm estratégico com 3 soluções baseadas em SCAMPER.

### CA002 - Estrutura completa das soluções

Dado que o brainstorm foi gerado, quando o usuário visualizar o detalhe da ideia, então cada solução deve apresentar descrição, racional, resolução da demanda, impacto, esforço, viabilidade, riscos e mitigações.

### CA003 - Recomendação da IA

Dado que existem 3 soluções geradas, então a IA deve marcar uma solução como recomendada e justificar a escolha.

### CA004 - Matriz Impacto × Esforço

Dado que a solução recomendada possui notas de impacto e esforço, então o sistema deve classificar a ideia no quadrante correspondente da matriz.

### CA005 - Falha na IA

Dado que a IA falhou, quando o usuário consultar a ideia, então a ideia deve continuar salva e o sistema deve indicar falha amigável na geração do brainstorm.

### CA006 - Conversão em projeto

Dado que uma ideia com brainstorm foi convertida em projeto, então o projeto interno deve conter cópia do brainstorm estratégico.

### CA007 - Criação de task no Asana

Dado que o projeto foi criado no Asana, então deve existir uma task inicial chamada `Brainstorm Estratégico IA` com o conteúdo completo do brainstorm.

---

## 21. Plano de validação objetivo

| Cenário | Validação |
|---|---|
| Cadastro de ideia | Confirmar que a ideia é salva e o brainstorm é gerado. |
| Estrutura do brainstorm | Confirmar 3 soluções, SCAMPER, notas, riscos e recomendação. |
| Falha de IA | Confirmar que a ideia não é perdida e que há mensagem amigável. |
| Matriz Impacto × Esforço | Confirmar que impacto/esforço geram o quadrante correto. |
| Conversão em projeto | Confirmar cópia do brainstorm no projeto interno. |
| Integração Asana | Confirmar criação da task inicial com o brainstorm completo. |

---

## 22. Pendências de decisão

| Código | Decisão pendente | Recomendação |
|---|---|---|
| PD001 | Permitir conversão sem brainstorm gerado? | Permitir apenas com confirmação explícita da Inovação. |
| PD002 | Permitir regerar brainstorm? | Sim, mas sem versionamento completo na primeira versão. |
| PD003 | A IA deve salvar notas individuais por solução ou só da recomendada? | Salvar notas das 3 soluções e usar a recomendada para a matriz inicial. |
| PD004 | A task do Asana deve ser editável manualmente? | Sim, pelo Asana; portal apenas cria o conteúdo inicial. |

---

## 23. Recomendação de implementação

Implementar em etapas:

1. Modelar e persistir `strategic_brainstorm` em ideias.
2. Criar Edge Function de geração do brainstorm com IA.
3. Validar contrato JSON da IA.
4. Exibir brainstorm no detalhe da ideia.
5. Ajustar matriz Impacto × Esforço com as métricas 1 a 10.
6. Copiar brainstorm na conversão em projeto.
7. Criar task inicial no Asana.
8. Validar fluxo completo com pelo menos uma ideia realista.

---

## 24. Resumo executivo

A mudança adiciona uma camada estratégica ao processo de ideação.

O portal deixa de apenas registrar ideias e passa a apoiar a tomada de decisão com:

1. geração estruturada de alternativas;
2. uso de framework de inovação;
3. critérios claros de impacto e esforço;
4. recomendação justificada da IA;
5. rastreabilidade do raciocínio até o projeto no Asana.

A combinação recomendada é:

```text
SCAMPER = gera alternativas melhores
Impacto × Esforço = compara e prioriza
Task inicial no Asana = garante rastreabilidade na execução
```
