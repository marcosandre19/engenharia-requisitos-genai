# Ambiguidades, Inconsistências e Pontos a Esclarecer — Sistema de Gestão de Eventos

**Documento de origem:** [Elicitacao-Gestao-de-Eventos.md](../elicitacao/Elicitacao-Gestao-de-Eventos.md)
**Documentos relacionados:** [requisitos-funcionais.md](requisitos-funcionais.md) · [requisitos-nao-funcionais.md](requisitos-nao-funcionais.md) · [regras-de-negocio.md](regras-de-negocio.md)
**Versão:** 1.0
**Status:** Aguardando validação com stakeholders

## Objetivo

Consolidar todos os pontos marcados com ⚠️ nos documentos de análise, organizados para servir de **pauta das próximas reuniões de elicitação**. Cada item traz: a questão, sua origem, os artefatos impactados, perguntas sugeridas aos stakeholders e a criticidade para o andamento do projeto.

**Criticidade:** 🔴 *Bloqueante* (impede fechar o desenho da solução) · 🟡 *Alta* (impacta escopo/esforço) · 🟢 *Moderada* (pode ser definida durante o desenvolvimento).

---

## 1. Lacunas — decisões pendentes dos stakeholders

### Q-01 — Momento da reserva da vaga em inscrições pagas 🔴
A vaga é reservada quando o participante **inicia** o pagamento ou somente após sua **confirmação**?
- **Origem:** Seção 4 da elicitação (lacuna explícita).
- **Impacta:** RF-04, RF-09, RF-16 · RN-01, RN-02, RN-08, RN-10, **RN-11** · RNF-10.
- **Por que é bloqueante:** define o modelo de concorrência do controle de vagas — o núcleo do sistema. Sem isso, não há como especificar inscrição paga, lista de espera nem o painel de vagas.
- **Perguntas sugeridas:**
  - Ao iniciar um pagamento, a vaga fica bloqueada para o participante? Por quanto tempo?
  - Se o pagamento não for confirmado nesse prazo, a vaga volta para o público/lista de espera?
  - Pode haver mais intenções de pagamento em andamento do que vagas restantes?
- **Responsáveis pela resposta:** Equipe Financeira + Organizadores.

### Q-02 — Prazo e condições de cancelamento 🔴
Até quando o participante pode cancelar a inscrição? O prazo é único ou configurável por evento?
- **Origem:** Seção 4 da elicitação; Organizadores ("nem todos os eventos permitem cancelamento").
- **Impacta:** RF-03, RF-13 · RN-05, RN-06, RN-07.
- **Perguntas sugeridas:**
  - O prazo-limite é uma política da Eventus ou de cada evento?
  - O que acontece com pedidos após o prazo — são simplesmente bloqueados ou passam por análise da organização?
  - Em eventos que "não permitem cancelamento", o participante ainda pode desistir (perdendo o valor), liberando ou não a vaga?
- **Responsáveis:** Organizadores.

### Q-03 — Política de reembolso 🔴
Em quais situações há reembolso? Integral ou parcial? Qual a relação com o prazo de cancelamento?
- **Origem:** Seção 4 da elicitação; Equipe Financeira ("em alguns casos há direito ao reembolso, em outros não").
- **Impacta:** RF-13, RF-17 · RN-12 (e sua relação com RN-06).
- **Perguntas sugeridas:**
  - O direito a reembolso depende do evento, do prazo do cancelamento, ou de ambos?
  - Há reembolso parcial (percentual escalonado por antecedência)?
  - Cancelamento permitido implica reembolso garantido, ou são políticas independentes?
  - Quem aprova o reembolso e por qual meio ele é pago?
- **Responsáveis:** Equipe Financeira + Organizadores.

### Q-04 — Funcionamento da lista de espera 🟡
Como a lista de espera opera quando surge uma vaga?
- **Origem:** Seção 4 da elicitação; Organizadores ("seria interessante criar uma lista de espera").
- **Impacta:** RF-05, RF-14 · RN-02, RN-07 · RNF-20.
- **Perguntas sugeridas:**
  - A convocação segue a ordem de entrada na lista? Há prioridades?
  - O convocado tem prazo para confirmar (e pagar, se for o caso)? O que ocorre se não responder?
  - A lista de espera existe em todos os eventos ou é opcional por evento?
  - Há limite de tamanho para a lista?
- **Responsáveis:** Organizadores.
- **Observação:** o verbo "seria interessante" sugere requisito **desejável**, não essencial — confirmar prioridade de escopo.

### Q-05 — Condição de emissão do certificado 🟡
O certificado é automático para todo inscrito ou depende de presença confirmada?
- **Origem:** Seção 4 da elicitação.
- **Impacta:** RF-18, **RF-19 (existe apenas se presença for exigida)** · RN-13, RN-14.
- **Perguntas sugeridas:**
  - Quem define a condição — a Eventus ou cada evento?
  - Se depender de presença: como a presença será registrada (credenciamento, QR code, lista manual)? Há percentual mínimo em eventos de vários dias?
  - O certificado é por evento, por atividade, ou ambos? Que informações deve conter?
- **Responsáveis:** Organizadores.

### Q-06 — Comprovantes e notificações 🟡
Por quais canais e em quais momentos o sistema se comunica com o participante?
- **Origem:** Seção 4 da elicitação.
- **Impacta:** RF-11, RF-22 · RN-08 · RNF-20.
- **Perguntas sugeridas:**
  - Canal de envio: e-mail, área do participante no sistema, ambos, outros (WhatsApp/SMS)?
  - Quais eventos disparam notificação (inscrição, pagamento, convocação de lista, cancelamento, certificado disponível, lembrete de evento)?
  - Que dados o comprovante de inscrição deve conter?
- **Responsáveis:** Organizadores + Participantes (validação).

### Q-07 — Conflito de horários na inscrição 🟡
O sistema deve impedir, alertar ou permitir inscrição em atividades com horários conflitantes?
- **Origem:** Seção 4 da elicitação (ponto "não discutido").
- **Impacta:** RF-10 · RN-03, RN-04.
- **Perguntas sugeridas:**
  - Uma pessoa pode se inscrever em duas atividades simultâneas (ex.: para garantir opção)?
  - Se for impedido: conflito é sobreposição total, parcial, ou inclui intervalo mínimo de deslocamento entre salas?
- **Responsáveis:** Organizadores.

### Q-08 — Dados de participantes visíveis aos palestrantes 🟡
Quais informações dos inscritos o palestrante pode ver?
- **Origem:** Seção 4 da elicitação.
- **Impacta:** RF-21 · RN-15 · RNF-05, RNF-06 (LGPD).
- **Perguntas sugeridas:**
  - Nome apenas? Instituição/empresa? Contato (e-mail)?
  - Há necessidade real de contato direto palestrante → participante, ou basta a contagem e os nomes?
  - A área jurídica/DPO da Eventus precisa validar essa exposição de dados?
- **Responsáveis:** Palestrantes + Organizadores + área jurídica.

### Q-09 — Requisitos não funcionais não elicitados 🟡
Segurança, desempenho, disponibilidade, acessibilidade e privacidade **não foram levantados** com os stakeholders.
- **Origem:** Seção 4 da elicitação (lacuna declarada).
- **Impacta:** todo o documento de RNFs — os 20 requisitos propostos são hipóteses de trabalho.
- **Perguntas sugeridas:**
  - Validar as metas propostas: resposta ≤ 3s (RNF-08), painel com defasagem ≤ 30s (RNF-09), disponibilidade 99,5% (RNF-12), RPO/RTO de backup (RNF-13).
  - Volumetria (necessária para RNF-11): quantos eventos simultâneos, inscritos por evento, pico de acessos na abertura de inscrições?
  - Há política de privacidade/DPO na Eventus? Requisitos de acessibilidade obrigatórios para o público atendido?
- **Responsáveis:** Equipe de TI + Organizadores + área jurídica.

### Q-10 — Escopo do pagamento 🟢
O pagamento é processado dentro do sistema (integração com gateway) ou apenas registrado/confirmado manualmente pela Equipe Financeira?
- **Origem:** Derivada — a fala "precisamos confirmar os pagamentos" sugere processo manual, mas não foi explicitado.
- **Impacta:** RF-15, RF-16 · RN-10 · esforço/arquitetura da solução.
- **Perguntas sugeridas:**
  - Quais meios de pagamento serão aceitos (Pix, cartão, boleto)?
  - "Confirmar pagamento" é conciliação manual ou haverá confirmação automática via gateway?
  - Quais são as "determinadas inscrições" que exigem confirmação prévia — todas as pagas ou um subconjunto?
- **Responsáveis:** Equipe Financeira + Equipe de TI.

---

## 2. Ambiguidades — termos vagos nas declarações

| # | Termo/Declaração ambígua | Fonte | Interpretações possíveis | Tratamento proposto |
| --- | --- | --- | --- | --- |
| A-01 | "**tempo real**" (acompanhar inscritos) | Organizadores | (a) atualização instantânea via push; (b) atualização ao recarregar; (c) defasagem de segundos/minutos | RNF-09 propõe ≤ 30s — validar (Q-09) |
| A-02 | "**determinadas inscrições**" (liberar após pagamento) | Equipe Financeira | (a) todas as inscrições pagas; (b) apenas eventos específicos; (c) apenas certos tipos de participante | Q-10 |
| A-03 | "**seria interessante**" (lista de espera; comprovante) | Organizadores; Participantes | desejo opcional × requisito obrigatório — afeta priorização do escopo | Q-04 e Q-06 confirmam prioridade |
| A-04 | "**depois do evento**" (emitir certificado) | Participantes | imediatamente após? após confirmação de presença? há prazo-limite para emissão? | Q-05 |
| A-05 | "**vários workshops no mesmo dia**" | Participantes | inclui workshops no mesmo **horário** ou apenas em horários distintos do mesmo dia? | Q-07 |
| A-06 | "**evento lotar**" | Organizadores | lotação considera apenas inscrições confirmadas ou também pagamentos em andamento? | Depende de Q-01 |
| A-07 | "**gerenciar participantes**" | Organizadores (tabela de stakeholders) | escopo indefinido: editar dados? cancelar inscrição de terceiros? transferir vagas? comunicar-se em massa? | Detalhar em reunião com Organizadores |

---

## 3. Inconsistências e tensões entre declarações

### T-01 — Cancelamento livre × cancelamento restrito
**Participantes:** "gostaria de cancelar minha inscrição sem precisar entrar em contato com a organização" × **Organizadores:** "nem todos os eventos permitem o cancelamento da inscrição".
- **Análise:** não é contradição direta — o autoatendimento (RN-05) pode coexistir com a restrição por evento (RN-06) —, mas a **expectativa do participante ficará frustrada** em eventos sem cancelamento. É preciso alinhar as duas partes e deixar a política visível **antes** da inscrição.
- **Encaminhamento:** Q-02; exigir que a política de cancelamento seja exibida na página do evento (candidato a novo RF).

### T-02 — Cancelamento permitido × reembolso não garantido
**Participantes** esperam cancelar livremente; **Equipe Financeira** afirma que nem sempre há reembolso.
- **Análise:** cancelar a inscrição e reaver o valor são direitos distintos que as entrevistas misturam. Se o participante puder cancelar sem reembolso, isso deve estar explícito no ato do cancelamento.
- **Encaminhamento:** Q-02 + Q-03 devem ser respondidas em conjunto, preferencialmente na mesma reunião com os dois grupos.

### T-03 — Workshops simultâneos × inscrição múltipla no mesmo dia
**Organizadores** programam atividades simultâneas (RN-03); **Participantes** querem se inscrever em vários workshops do mesmo dia (RN-04).
- **Análise:** as duas declarações são compatíveis até o ponto em que os workshops desejados **coincidem no horário** — exatamente o caso que a elicitação registra como não discutido.
- **Encaminhamento:** Q-07.

### T-04 — Comprovante "logo após a inscrição" × inscrição condicionada ao pagamento
**Participantes** esperam comprovante imediato (RN-08); **Equipe Financeira** condiciona a efetivação à confirmação do pagamento (RN-10).
- **Análise:** em eventos pagos, "logo após a inscrição" é ambíguo — após o pedido ou após a confirmação? Possível solução: dois documentos (recibo do pedido + comprovante da inscrição efetivada), a validar.
- **Encaminhamento:** Q-01 + Q-06.

---

## 4. Priorização para a próxima rodada de elicitação

| Prioridade | Questões | Reunião sugerida |
| --- | --- | --- |
| 🔴 Bloqueantes | Q-01, Q-02, Q-03 (+ tensões T-01, T-02, T-04) | Organizadores + Equipe Financeira, em conjunto |
| 🟡 Altas | Q-04, Q-05, Q-06, Q-07 (+ T-03) | Organizadores (com validação de Participantes) |
| 🟡 Altas | Q-08, Q-09 | Palestrantes, Equipe de TI e área jurídica |
| 🟢 Moderadas | Q-10 | Equipe Financeira + Equipe de TI |

**Recomendação:** resolver Q-01–Q-03 antes de iniciar a especificação detalhada dos fluxos de inscrição e pagamento, pois qualquer decisão nesses pontos reestrutura RN-11 e os RFs centrais (RF-04, RF-09, RF-13, RF-16, RF-17).
