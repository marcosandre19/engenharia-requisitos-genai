# Requisitos Funcionais — Sistema de Gestão de Eventos

**Documento de origem:** [Elicitacao-Gestao-de-Eventos.md](../elicitacao/Elicitacao-Gestao-de-Eventos.md)
**Versão:** 1.0
**Status:** Em análise

## Convenções

- **Identificação:** RF-XX (numeração sequencial).
- **Prioridade:** classificação preliminar segundo o valor percebido nas entrevistas — *Essencial*, *Importante* ou *Desejável* — sujeita a validação com os stakeholders.
- **Origem:** stakeholder cuja declaração na elicitação motivou o requisito.
- Requisitos marcados com ⚠️ dependem de esclarecimentos registrados no documento de elicitação (Seção 4 — Observações) e detalhados no documento de ambiguidades.

---

## 1. Gestão de Eventos (Organizadores)

### RF-01 — Cadastrar evento
O sistema deve permitir que o organizador cadastre eventos (congressos, workshops e eventos corporativos), informando, no mínimo: nome, descrição, tipo, data(s), horário(s), local, número de vagas, gratuidade ou valor da inscrição, política de cancelamento e programação de atividades.
- **Origem:** Organizadores ("Criar eventos"); Equipe Financeira ("Alguns eventos são gratuitos e outros exigem pagamento").
- **Prioridade:** Essencial

### RF-02 — Gerenciar atividades do evento
O sistema deve permitir que o organizador cadastre atividades (ex.: workshops, palestras) vinculadas a um evento, com data, horário, local, palestrante(s) e número de vagas próprio, admitindo atividades simultâneas (mesmo horário).
- **Origem:** Organizadores ("Os workshops que acontecem no mesmo horário devem ocorrer simultaneamente"); Participantes ("me inscrever em vários workshops que acontecerão no mesmo dia").
- **Prioridade:** Essencial

### RF-03 — Configurar política de cancelamento por evento
O sistema deve permitir que o organizador configure, por evento, se o cancelamento de inscrição é permitido ou não. ⚠️ *O prazo-limite de cancelamento ainda não foi definido.*
- **Origem:** Organizadores ("Nem todos os eventos permitem o cancelamento da inscrição").
- **Prioridade:** Essencial

### RF-04 — Controlar vagas automaticamente
O sistema deve controlar automaticamente o número de vagas de eventos e atividades, decrementando a disponibilidade a cada inscrição efetivada e impedindo novas inscrições quando as vagas se esgotarem. ⚠️ *O momento exato da reserva da vaga (ao iniciar ou ao confirmar o pagamento) ainda não foi definido.*
- **Origem:** Organizadores ("Precisamos controlar automaticamente o número de vagas").
- **Prioridade:** Essencial

### RF-05 — Gerenciar lista de espera
O sistema deve permitir a formação de lista de espera quando as vagas de um evento ou atividade se esgotarem. ⚠️ *O funcionamento da lista de espera (ordem, convocação, prazos) ainda não foi definido.*
- **Origem:** Organizadores ("Quando um evento lotar, seria interessante criar uma lista de espera").
- **Prioridade:** Importante

### RF-06 — Acompanhar inscrições em tempo real
O sistema deve disponibilizar ao organizador um painel de acompanhamento com a quantidade de inscritos por evento e por atividade, atualizado em tempo real, incluindo vagas ocupadas, vagas disponíveis e lista de espera.
- **Origem:** Organizadores ("Gostaríamos de acompanhar a quantidade de inscritos em tempo real").
- **Prioridade:** Essencial

### RF-07 — Gerenciar participantes
O sistema deve permitir que o organizador consulte e gerencie os participantes inscritos em seus eventos (ex.: visualizar dados da inscrição, situação do pagamento, presença).
- **Origem:** Organizadores ("gerenciar participantes").
- **Prioridade:** Essencial

---

## 2. Inscrições (Participantes)

### RF-08 — Consultar catálogo de eventos
O sistema deve exibir aos participantes todos os eventos disponíveis em um único local, com suas informações e programação de atividades.
- **Origem:** Participantes ("visualizar todos os eventos disponíveis em um único lugar").
- **Prioridade:** Essencial

### RF-09 — Realizar inscrição em evento
O sistema deve permitir que o participante se inscreva em eventos com vagas disponíveis. Para eventos pagos, a inscrição deve seguir o fluxo de pagamento (ver RF-15 e RF-16).
- **Origem:** Participantes ("Inscrever-se em eventos").
- **Prioridade:** Essencial

### RF-10 — Realizar inscrição em múltiplas atividades
O sistema deve permitir que o participante se inscreva em mais de uma atividade de um mesmo evento, inclusive em atividades que ocorrem no mesmo dia. ⚠️ *O tratamento de inscrições em atividades com horários conflitantes ainda não foi definido.*
- **Origem:** Participantes ("me inscrever em vários workshops que acontecerão no mesmo dia").
- **Prioridade:** Essencial

### RF-11 — Emitir comprovante de inscrição
O sistema deve gerar e enviar ao participante um comprovante imediatamente após a efetivação da inscrição. ⚠️ *O canal de envio (e-mail, sistema, outro) ainda não foi definido.*
- **Origem:** Participantes ("receber um comprovante logo após a inscrição").
- **Prioridade:** Essencial

### RF-12 — Acompanhar inscrições
O sistema deve permitir que o participante consulte suas inscrições e a situação de cada uma (ex.: confirmada, aguardando pagamento, em lista de espera, cancelada).
- **Origem:** Participantes ("acompanhar inscrições").
- **Prioridade:** Essencial

### RF-13 — Cancelar inscrição (autoatendimento)
O sistema deve permitir que o participante cancele sua própria inscrição, sem necessidade de contato com a organização, respeitando a política de cancelamento do evento (RF-03). Ao cancelar, a vaga deve ser liberada (e a lista de espera acionada, conforme RF-05). ⚠️ *Prazo-limite de cancelamento e regras de reembolso ainda não foram definidos.*
- **Origem:** Participantes ("cancelar minha inscrição sem precisar entrar em contato com a organização"); Organizadores ("Nem todos os eventos permitem o cancelamento").
- **Prioridade:** Essencial

### RF-14 — Entrar em lista de espera
O sistema deve permitir que o participante entre na lista de espera de um evento ou atividade lotada e ser notificado quando surgir vaga. ⚠️ *Regras de convocação ainda não definidas.*
- **Origem:** Organizadores ("lista de espera") — benefício direto ao participante.
- **Prioridade:** Importante

---

## 3. Pagamentos (Equipe Financeira)

### RF-15 — Registrar pagamento de inscrição
O sistema deve registrar o pagamento das inscrições em eventos pagos, vinculando cada pagamento à respectiva inscrição.
- **Origem:** Equipe Financeira ("Alguns eventos são gratuitos e outros exigem pagamento").
- **Prioridade:** Essencial

### RF-16 — Confirmar pagamento para liberação da inscrição
O sistema deve permitir que a Equipe Financeira confirme os pagamentos, e deve condicionar a efetivação de determinadas inscrições à confirmação do pagamento. ⚠️ *O momento da reserva da vaga em relação ao pagamento ainda não foi definido.*
- **Origem:** Equipe Financeira ("Precisamos confirmar os pagamentos antes de liberar determinadas inscrições").
- **Prioridade:** Essencial

### RF-17 — Processar reembolso
O sistema deve permitir o registro e o controle de reembolsos de inscrições canceladas, conforme a política do evento. ⚠️ *As situações que dão direito a reembolso ainda não foram definidas.*
- **Origem:** Equipe Financeira ("Em alguns casos o participante tem direito ao reembolso, em outros não").
- **Prioridade:** Essencial

---

## 4. Certificados

### RF-18 — Emitir certificado de participação
O sistema deve permitir que o participante emita seu certificado após o evento. ⚠️ *Não foi definido se a emissão será automática ou condicionada à confirmação de presença.*
- **Origem:** Participantes ("Quero conseguir emitir meu certificado depois do evento").
- **Prioridade:** Essencial

### RF-19 — Registrar presença
O sistema deve permitir o registro de presença dos participantes nos eventos/atividades, como possível condição para a emissão de certificados (dependente da definição do RF-18). ⚠️ *Requisito condicional — só se confirma se a emissão de certificados depender de presença.*
- **Origem:** Derivado da observação sobre certificados (Seção 4 da elicitação).
- **Prioridade:** Importante (condicional)

---

## 5. Palestrantes

### RF-20 — Consultar programação
O sistema deve permitir que o palestrante consulte a programação dos eventos e de suas atividades.
- **Origem:** Palestrantes ("Consultar a programação").
- **Prioridade:** Importante

### RF-21 — Consultar participantes de suas atividades
O sistema deve permitir que o palestrante consulte a lista de participantes inscritos em suas atividades. ⚠️ *O conjunto de informações dos participantes visível ao palestrante ainda não foi definido (implicações de privacidade).*
- **Origem:** Palestrantes ("consultar a lista de participantes inscritos em minhas atividades").
- **Prioridade:** Importante

---

## 6. Notificações

### RF-22 — Enviar notificações aos participantes
O sistema deve enviar notificações aos participantes sobre eventos relevantes do ciclo de inscrição (ex.: comprovante de inscrição, confirmação de pagamento, convocação da lista de espera, cancelamento, disponibilidade do certificado). ⚠️ *Canais e conteúdo das notificações ainda não foram definidos.*
- **Origem:** Participantes ("receber um comprovante"); Seção 4 da elicitação ("como serão enviados comprovantes de inscrição e demais notificações").
- **Prioridade:** Essencial

---

## 7. Requisitos derivados (implícitos)

Requisitos não declarados explicitamente nas entrevistas, mas necessários para viabilizar os demais. Devem ser validados com os stakeholders.

### RF-23 — Gerenciar contas e perfis de acesso
O sistema deve permitir o cadastro e a autenticação de usuários com perfis distintos (participante, organizador, equipe financeira, palestrante), restringindo as funcionalidades de acordo com o perfil.
- **Justificativa:** os cinco stakeholders identificados possuem interesses e permissões distintas.
- **Prioridade:** Essencial

### RF-24 — Manter histórico de inscrições e transações
O sistema deve manter o histórico de inscrições, cancelamentos, pagamentos e reembolsos, para fins de controle pela organização e pela equipe financeira.
- **Justificativa:** suporte ao controle citado por Organizadores e Equipe Financeira; substitui o controle hoje feito em planilhas.
- **Prioridade:** Importante

---

## Matriz de rastreabilidade (resumo)

| Stakeholder | Requisitos |
| --- | --- |
| Participantes | RF-08, RF-09, RF-10, RF-11, RF-12, RF-13, RF-14, RF-18, RF-22 |
| Organizadores | RF-01, RF-02, RF-03, RF-04, RF-05, RF-06, RF-07, RF-19 |
| Equipe Financeira | RF-15, RF-16, RF-17, RF-24 |
| Palestrantes | RF-20, RF-21 |
| Equipe de TI | (viabiliza todos — sem requisito funcional próprio) |
| Derivados | RF-23, RF-24 |

**Pendências:** os itens marcados com ⚠️ (RF-03, RF-04, RF-05, RF-10, RF-11, RF-13, RF-14, RF-16, RF-17, RF-18, RF-19, RF-21, RF-22) dependem de esclarecimentos junto aos stakeholders e serão consolidados no documento de ambiguidades e pontos em aberto.
