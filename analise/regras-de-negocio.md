# Regras de Negócio — Sistema de Gestão de Eventos

**Documento de origem:** [Elicitacao-Gestao-de-Eventos.md](../elicitacao/Elicitacao-Gestao-de-Eventos.md)
**Documentos relacionados:** [requisitos-funcionais.md](requisitos-funcionais.md) · [requisitos-nao-funcionais.md](requisitos-nao-funcionais.md)
**Versão:** 1.0
**Status:** Em análise

## Convenções

- **Identificação:** RN-XX (numeração sequencial), agrupadas por tema.
- **Distinção adotada:** regras de negócio expressam **políticas e restrições da Eventus** (o "o que é permitido/obrigatório e sob quais condições"), independentemente de como o sistema as implementa; os requisitos funcionais expressam **o que o sistema faz** para cumpri-las.
- **Status:** *Definida* (sustentada por declaração explícita da elicitação) ou *Parcial* ⚠️ (o princípio foi declarado, mas parâmetros essenciais estão pendentes — detalhados no campo "Pendência").
- **RFs relacionados:** requisitos funcionais que implementam ou dependem da regra.

---

## 1. Eventos e Vagas

### RN-01 — Limite de vagas
Todo evento e toda atividade possuem um número máximo de vagas, definido pelo organizador no cadastro. O número de inscrições confirmadas nunca pode exceder esse limite.
- **Status:** Definida
- **Fonte:** Organizadores ("Precisamos controlar automaticamente o número de vagas").
- **RFs relacionados:** RF-01, RF-02, RF-04

### RN-02 — Evento lotado gera lista de espera
Quando as vagas de um evento ou atividade se esgotam, novas solicitações de inscrição não são aceitas diretamente; o interessado pode ingressar em lista de espera.
- **Status:** Parcial ⚠️
- **Fonte:** Organizadores ("Quando um evento lotar, seria interessante criar uma lista de espera").
- **Pendência:** critério de ordenação (ordem de chegada?), forma e prazo de convocação quando surge vaga, e se a lista de espera vale para todos os eventos ou é configurável.
- **RFs relacionados:** RF-05, RF-14

### RN-03 — Atividades simultâneas são permitidas na programação
Um evento pode ter atividades (workshops) programadas para o mesmo dia e o mesmo horário, ocorrendo simultaneamente.
- **Status:** Definida
- **Fonte:** Organizadores ("Os workshops que acontecem no mesmo horário devem ocorrer simultaneamente").
- **RFs relacionados:** RF-02

### RN-04 — Inscrição em múltiplas atividades
O participante pode inscrever-se em mais de uma atividade do mesmo evento, inclusive no mesmo dia.
- **Status:** Parcial ⚠️
- **Fonte:** Participantes ("Gostaria de me inscrever em vários workshops que acontecerão no mesmo dia").
- **Pendência:** se é permitida a inscrição em atividades com **horários conflitantes** (a elicitação registra o ponto como não discutido). Há tensão aparente com RN-03: atividades simultâneas existem, mas não se definiu se uma mesma pessoa pode se inscrever em duas delas.
- **RFs relacionados:** RF-10

---

## 2. Inscrições e Cancelamentos

### RN-05 — Cancelamento em autoatendimento
O participante pode cancelar sua própria inscrição diretamente pelo sistema, sem contato com a organização — desde que o evento permita cancelamento (RN-06).
- **Status:** Definida
- **Fonte:** Participantes ("gostaria de cancelar minha inscrição sem precisar entrar em contato com a organização").
- **RFs relacionados:** RF-13

### RN-06 — Permissão de cancelamento é definida por evento
Nem todo evento permite cancelamento de inscrição. A permissão (ou proibição) de cancelamento é uma característica configurada de cada evento.
- **Status:** Parcial ⚠️
- **Fonte:** Organizadores ("Nem todos os eventos permitem o cancelamento da inscrição").
- **Pendência:** prazo-limite para cancelar (até quando antes do evento?) e se o prazo também é configurável por evento.
- **RFs relacionados:** RF-03, RF-13

### RN-07 — Cancelamento libera a vaga
O cancelamento de uma inscrição libera a vaga correspondente, que fica disponível para novos inscritos ou para a convocação da lista de espera (RN-02).
- **Status:** Definida (consequência lógica de RN-01 e RN-02)
- **Fonte:** Derivada — necessária para que o controle de vagas e a lista de espera façam sentido.
- **RFs relacionados:** RF-04, RF-05, RF-13

### RN-08 — Comprovante de inscrição
Toda inscrição efetivada gera um comprovante para o participante, imediatamente após sua efetivação.
- **Status:** Parcial ⚠️
- **Fonte:** Participantes ("Seria interessante receber um comprovante logo após a inscrição").
- **Pendência:** canal de envio e conteúdo do comprovante; definição de quando uma inscrição paga é considerada "efetivada" (ver RN-11).
- **RFs relacionados:** RF-11, RF-22

---

## 3. Pagamentos e Reembolsos

### RN-09 — Gratuidade é definida por evento
Cada evento é gratuito ou pago; a condição é definida no cadastro do evento. Eventos gratuitos não exigem pagamento para a efetivação da inscrição.
- **Status:** Definida
- **Fonte:** Equipe Financeira ("Alguns eventos são gratuitos e outros exigem pagamento").
- **RFs relacionados:** RF-01, RF-09, RF-15

### RN-10 — Confirmação de pagamento condiciona a inscrição
Em eventos pagos, determinadas inscrições só são liberadas (efetivadas) após a confirmação do pagamento pela Equipe Financeira.
- **Status:** Parcial ⚠️
- **Fonte:** Equipe Financeira ("Precisamos confirmar os pagamentos antes de liberar determinadas inscrições").
- **Pendência:** o que caracteriza as "determinadas inscrições" (todas as pagas? apenas alguns eventos?); se a confirmação é manual ou automática (integração com meio de pagamento).
- **RFs relacionados:** RF-15, RF-16

### RN-11 — Momento da reserva da vaga em inscrições pagas
⚠️ **Regra pendente de definição.** Não está definido se a vaga é reservada quando o participante **inicia** o pagamento ou somente após sua **confirmação**. A escolha impacta diretamente RN-01 (vagas), RN-02 (lista de espera) e RN-08 (efetivação/comprovante).
- **Status:** Parcial ⚠️ (lacuna explícita da elicitação, Seção 4)
- **Pendência:** definição do momento da reserva; se houver reserva temporária, prazo de expiração do pagamento não confirmado.
- **RFs relacionados:** RF-04, RF-09, RF-16

### RN-12 — Direito a reembolso é condicional
O reembolso de inscrições pagas não é universal: em alguns casos o participante tem direito, em outros não.
- **Status:** Parcial ⚠️
- **Fonte:** Equipe Financeira ("Em alguns casos o participante tem direito ao reembolso, em outros não").
- **Pendência:** as situações que dão direito a reembolso (política do evento? prazo do cancelamento? percentual?); relação com RN-06 (cancelamento permitido ≠ reembolso garantido — a distinção precisa ser confirmada).
- **RFs relacionados:** RF-13, RF-17

---

## 4. Certificados e Presença

### RN-13 — Certificado é emitido após o evento
O certificado de participação só pode ser emitido após a realização do evento (ou da atividade correspondente).
- **Status:** Definida
- **Fonte:** Participantes ("Quero conseguir emitir meu certificado depois do evento").
- **RFs relacionados:** RF-18

### RN-14 — Condição de emissão do certificado
⚠️ **Regra pendente de definição.** Não foi definido se o certificado é emitido automaticamente para todo inscrito ou se depende da confirmação de presença. A decisão determina a necessidade do registro de presença (RF-19).
- **Status:** Parcial ⚠️ (lacuna explícita da elicitação, Seção 4)
- **Pendência:** critério de elegibilidade (inscrição? presença? percentual mínimo de presença em eventos de múltiplos dias?).
- **RFs relacionados:** RF-18, RF-19

---

## 5. Acesso à Informação

### RN-15 — Palestrante acessa apenas suas atividades
O palestrante pode consultar a lista de participantes **apenas das atividades sob sua responsabilidade**, não de outras atividades ou eventos.
- **Status:** Parcial ⚠️
- **Fonte:** Palestrantes ("consultar a lista de participantes inscritos em **minhas** atividades").
- **Pendência:** quais dados dos participantes são visíveis (nome apenas? contato?) — restrição reforçada pela LGPD (ver RNF-06).
- **RFs relacionados:** RF-20, RF-21

### RN-16 — Visibilidade das informações por perfil
Cada perfil acessa somente as informações pertinentes ao seu interesse: participantes veem os próprios dados e inscrições; organizadores, os dados de seus eventos; a Equipe Financeira, os dados de pagamento; palestrantes, o previsto em RN-15.
- **Status:** Definida (derivada da tabela de stakeholders)
- **Fonte:** Seção 2 da elicitação (interesses distintos por stakeholder).
- **RFs relacionados:** RF-23; RNF-01

---

## Matriz regra × requisito funcional

| Regra | RFs que a implementam/dependem | Status |
| --- | --- | --- |
| RN-01 Limite de vagas | RF-01, RF-02, RF-04 | Definida |
| RN-02 Lista de espera | RF-05, RF-14 | Parcial ⚠️ |
| RN-03 Atividades simultâneas | RF-02 | Definida |
| RN-04 Múltiplas atividades | RF-10 | Parcial ⚠️ |
| RN-05 Cancelamento em autoatendimento | RF-13 | Definida |
| RN-06 Cancelamento por evento | RF-03, RF-13 | Parcial ⚠️ |
| RN-07 Cancelamento libera vaga | RF-04, RF-05, RF-13 | Definida |
| RN-08 Comprovante de inscrição | RF-11, RF-22 | Parcial ⚠️ |
| RN-09 Gratuidade por evento | RF-01, RF-09, RF-15 | Definida |
| RN-10 Pagamento condiciona inscrição | RF-15, RF-16 | Parcial ⚠️ |
| RN-11 Momento da reserva da vaga | RF-04, RF-09, RF-16 | Parcial ⚠️ |
| RN-12 Reembolso condicional | RF-13, RF-17 | Parcial ⚠️ |
| RN-13 Certificado após o evento | RF-18 | Definida |
| RN-14 Condição de emissão do certificado | RF-18, RF-19 | Parcial ⚠️ |
| RN-15 Palestrante só vê suas atividades | RF-20, RF-21 | Parcial ⚠️ |
| RN-16 Visibilidade por perfil | RF-23 | Definida |

**Resumo:** 16 regras identificadas — 7 definidas e 9 parciais. As pendências das regras parciais serão consolidadas, com as demais lacunas, no documento de ambiguidades e pontos em aberto.
