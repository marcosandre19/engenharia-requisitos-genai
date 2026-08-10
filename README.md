# Engenharia de Requisitos com GenAI — Sistema de Gestão de Eventos

Atividade de análise e especificação de requisitos apoiada por IA generativa, a partir do [documento de elicitação](elicitacao/Elicitacao-Gestao-de-Eventos.md) do Sistema de Gestão de Eventos da empresa fictícia Eventus.

## Estrutura do repositório

| Pasta | Conteúdo |
| --- | --- |
| `elicitacao/` | Documento de elicitação original (entrevistas com stakeholders) |
| `analise/` | [Requisitos funcionais](analise/requisitos-funcionais.md) · [Requisitos não funcionais](analise/requisitos-nao-funcionais.md) · [Regras de negócio](analise/regras-de-negocio.md) · [Dúvidas e lacunas](analise/duvidas-e-lacunas.md) |
| `especificacao/` | [Diagrama de estados](especificacao/diagrama-estados-inscricao.md) · [Tabelas de decisão](especificacao/tabelas-de-decisao.md) · [Glossário](especificacao/glossario.md) · [Modelo conceitual](especificacao/modelo-conceitual.md) · [Casos de uso](especificacao/casos-de-uso.md) · [Wireframes](especificacao/wireframes.md) · [Critérios de aceitação](especificacao/criterios-de-aceitacao.md) |

**Ordem de leitura sugerida:** elicitação → análise (RFs → RNFs → regras → dúvidas) → especificação (glossário → modelo conceitual → diagrama de estados → tabelas de decisão → casos de uso → wireframes → critérios de aceitação).

## Ferramenta de GenAI utilizada

**Claude Code** (Anthropic)

## Como a IA apoiou as etapas da atividade

1. **Análise:** derivação de 24 requisitos funcionais, 20 não funcionais e 16 regras de negócio, cada item rastreado à fala do stakeholder que o originou e com prioridade preliminar. A IA distinguiu explicitamente o que foi *declarado* nas entrevistas do que foi *derivado* ou *proposto* por boa prática (ex.: LGPD, autenticação).
2. **Identificação de problemas:** consolidação de 10 questões em aberto (3 bloqueantes), 7 ambiguidades e 4 tensões entre declarações de stakeholders diferentes, organizadas como pauta de reuniões com perguntas prontas e responsáveis pela resposta.
3. **Recomendação de artefatos:** a IA sugeriu quais artefatos de especificação usar, com justificativa e ordem de produção.
5. **Especificação:** geração dos sete artefatos, mantendo consistência cruzada (mesmos IDs, estados, termos e premissas em todos) e sinalizando em cada um os pontos que dependem das questões pendentes.
6. **Descoberta de lacunas novas:** o próprio ato de especificar revelou pendências que a elicitação não registrou — ex.: cancelamento do evento *pelo organizador* (diagrama de estados) e pagamento confirmado *após* a expiração da reserva (caso de uso UC-10/E1) — incorporadas à pauta de esclarecimentos.

## Sugestões aceitas

- O conjunto de artefatos recomendado pela IA e sua ordem de produção: diagrama de estados → tabelas de decisão → glossário + modelo conceitual → casos de uso → wireframes → Gherkin.
- A postura metodológica de **não inventar decisões que pertencem aos stakeholders**: itens indefinidos foram marcados (⚠️ Q-XX) e transformados em pauta de reunião, em vez de preenchidos arbitrariamente.
- As decisões de modelagem propostas com justificativa, como: inscrição por evento com detalhamento por atividade; lista de espera como estado da inscrição (não entidade); políticas de cancelamento/reembolso como atributos do evento.
- Os requisitos derivados não declarados nas entrevistas (autenticação/perfis, histórico, conformidade LGPD, integridade sob concorrência), aceitos por serem necessários ou obrigatórios.

## Sugestões descartadas ou modificadas

- **BPMN completo — descartado:** a própria IA ponderou e a avaliação confirmou que casos de uso + máquina de estados cobrem os processos com menos cerimônia; BPMN só se justificaria se a confirmação de pagamento se revelar um processo manual com múltiplas alçadas (a reavaliar após a resposta de Q-10).
- **User stories como artefato principal — descartadas:** o formato "como X quero Y" perderia justamente o que este domínio mais exige — regras condicionais e ciclo de vida com estados. Ficaram admitidas apenas como eventual unidade de planejamento ágil, ancoradas nos demais artefatos.
- **Metas quantitativas dos RNFs — aceitas com ressalva (modificadas em status):** os valores propostos pela IA (resposta ≤ 3s, disponibilidade 99,5%, painel ≤ 30s, RPO/RTO) **não foram aceitos como definitivos** — foram mantidos como hipóteses de trabalho explicitamente marcadas para validação, já que a elicitação declara que RNFs não foram levantados com os stakeholders.
- **Premissas de comportamento pendente — aceitas como provisórias:** onde havia lacuna (reserva de vaga com expiração, convocação da lista por ordem de chegada, alerta sem bloqueio em conflito de horário), as premissas da IA foram mantidas nos artefatos, porém sempre acompanhadas da alternativa e da questão que as decide — nenhuma foi incorporada como definição final.

## Por que estes artefatos foram os mais adequados

A escolha decorre de três características do projeto:

1. **O núcleo do domínio é um ciclo de vida com estados** — a inscrição transita por solicitação, pagamento, confirmação, lista de espera, cancelamento, reembolso e certificado. O **diagrama de estados** representa isso melhor que qualquer texto, e as três questões bloqueantes do projeto são, no fundo, perguntas sobre transições desse diagrama.
2. **As políticas são condicionais e variam por evento** — cancelamento, reembolso e certificado dependem de combinações de condições que texto corrido esconde. As **tabelas de decisão** expõem todas as combinações, inclusive as não tratadas nas entrevistas, e derivaram diretamente os **critérios de aceitação em Gherkin** (29 cenários, com rastreabilidade tabela → cenário).
3. **Os stakeholders são majoritariamente não técnicos e há muitas pendências** — o **glossário** ataca as ambiguidades de vocabulário ("cancelar" ≠ "reembolsar", "workshop" ≠ "atividade"); os **casos de uso** comunicam os fluxos por ator em linguagem natural; e os **wireframes** de baixa fidelidade funcionam como "perguntas desenhadas" para as reuniões de validação — stakeholders reagem a telas, não a listas de requisitos. O **modelo conceitual** resolve cedo as perguntas estruturais (inscrição é no evento ou na atividade?) das quais os demais artefatos dependem.

