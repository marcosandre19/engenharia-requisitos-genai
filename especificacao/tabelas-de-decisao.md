# Tabelas de Decisão — Sistema de Gestão de Eventos

**Documentos relacionados:** [regras-de-negocio.md](../analise/regras-de-negocio.md) · [duvidas-e-lacunas.md](../analise/duvidas-e-lacunas.md) · [diagrama-estados-inscricao.md](diagrama-estados-inscricao.md)
**Versão:** 1.0
**Status:** Proposta para validação com stakeholders

## Objetivo

Explicitar, em formato tabular, as políticas condicionais do sistema — cada coluna de condições combinadas leva a um resultado único. O formato expõe **todas as combinações**, inclusive as que as entrevistas não trataram: células marcadas com **⚠️ A DEFINIR** são exatamente as respostas que precisamos obter dos stakeholders (referências Q-XX do documento de dúvidas e lacunas).

**Convenções:** S = sim · N = não · — = indiferente (não afeta o resultado) · ⚠️ = pendente de definição.

---

## TD-01 — Efetivação da inscrição e reserva de vaga

Aplicada quando o participante solicita inscrição em um evento ou atividade. Implementa RN-01, RN-02, RN-09, RN-10 e RN-11; corresponde às transições iniciais do diagrama de estados.

| Condições | R1 | R2 | R3 | R4 | R5 |
| --- | :-: | :-: | :-: | :-: | :-: |
| Há vaga disponível? | S | S | S | N | N |
| Evento é pago? | N | S | S | — | — |
| Pagamento confirmado? | — | N | S | — | — |
| Deseja entrar na lista de espera? | — | — | — | S | N |
| **Ações** | | | | | |
| Confirmar inscrição (efetivada) | ✔ | | ✔ | | |
| Colocar em "Aguardando Pagamento" | | ✔ | | | |
| **Reservar a vaga** | ✔ | **⚠️ Q-01** | ✔ | | |
| Incluir na lista de espera | | | | ✔ | |
| Recusar solicitação | | | | | ✔ |
| Enviar comprovante (RN-08) | ✔ | ⚠️ Q-06¹ | ✔ | | |

¹ Pendente definir se em eventos pagos há um "recibo do pedido" antes do comprovante de efetivação (tensão T-04).

**Ponto crítico (R2):** se a vaga **for** reservada ao iniciar o pagamento, é obrigatório definir o prazo de expiração; se **não for**, pode haver mais pagamentos em andamento do que vagas — e é preciso definir o que ocorre com quem paga sem vaga disponível. As duas alternativas devem ser apresentadas na reunião de Q-01.

---

## TD-02 — Cancelamento de inscrição pelo participante

Aplicada quando o participante solicita o cancelamento em autoatendimento (RF-13). Implementa RN-05, RN-06 e RN-07.

| Condições | R1 | R2 | R3 | R4 |
| --- | :-: | :-: | :-: | :-: |
| Evento permite cancelamento? (RN-06) | N | S | S | S |
| Dentro do prazo-limite? **⚠️ Q-02** | — | S | N | ⚠️² |
| Inscrição em estado cancelável?³ | — | S | S | S |
| **Ações** | | | | |
| Bloquear cancelamento, informando a política | ✔ | | **⚠️ Q-02** | |
| Efetivar cancelamento | | ✔ | **⚠️ Q-02** | |
| Liberar vaga e acionar lista de espera (RN-07) | | ✔ | ⚠️ | |
| Avaliar reembolso → **TD-03** | | ✔ | ⚠️ | |
| Notificar participante (RF-22) | ✔ | ✔ | ✔ | |

² R4 reservada para o caso de **não existir** prazo-limite (cancelamento permitido até o início do evento) — uma das respostas possíveis de Q-02.
³ Estados canceláveis presumidos: `Confirmada` e `Aguardando Pagamento` (desistência). Cancelamento após `Concluída` não se aplica.

**Combinação não tratada nas entrevistas (R3):** o que ocorre com o pedido **fora do prazo** — bloqueio simples ou encaminhamento para análise da organização? Levar a Q-02.

**Caso omisso:** cancelamento de inscrição em **lista de espera** — presumido sempre permitido (não ocupa vaga), a confirmar.

---

## TD-03 — Direito e valor do reembolso

Aplicada após um cancelamento efetivado de inscrição paga. Implementa RN-12. **Esta é a tabela mais pendente — a estrutura abaixo é uma proposta de moldura para a reunião de Q-03.**

| Condições | R1 | R2 | R3 | R4 | R5 |
| --- | :-: | :-: | :-: | :-: | :-: |
| Evento é pago e pagamento foi confirmado? | N | S | S | S | S |
| Evento prevê reembolso? **⚠️ Q-03** | — | N | S | S | S |
| Cancelamento dentro do prazo de reembolso?⁴ **⚠️ Q-03** | — | — | S | N | ⚠️ |
| Antecedência dá direito a reembolso integral?⁴ **⚠️ Q-03** | — | — | S/N | — | ⚠️ |
| **Ações** | | | | | |
| Nenhum reembolso | ✔ | ✔ | | ✔ | |
| Reembolso integral | | | **⚠️** | | |
| Reembolso parcial (percentual a definir) | | | **⚠️** | | |
| Registrar e processar pela Equipe Financeira (RF-17) | | | ✔ | | |
| Notificar participante do resultado | ✔ | ✔ | ✔ | ✔ | |

⁴ As condições 3 e 4 são **hipóteses de estrutura** (prazo próprio de reembolso, distinto do prazo de cancelamento; escalonamento por antecedência). A reunião de Q-03 deve confirmar se existem, colapsá-las ou substituí-las.

**Perguntas que a tabela materializa:** reembolso é política por evento ou da Eventus? Integral, parcial ou escalonado? O prazo de reembolso coincide com o prazo de cancelamento (uma coluna a menos) ou é distinto? Quem paga taxas do meio de pagamento?

---

## TD-04 — Emissão de certificado

Aplicada quando o participante solicita o certificado (RF-18) após o evento. Implementa RN-13 e RN-14.

| Condições | R1 | R2 | R3 | R4 |
| --- | :-: | :-: | :-: | :-: |
| Evento já realizado? (RN-13) | N | S | S | S |
| Inscrição estava confirmada (não cancelada/expirada)? | — | N | S | S |
| Presença confirmada? **⚠️ Q-05** | — | — | S | N |
| **Ações** | | | | |
| Negar emissão, informando o motivo | ✔ | ✔ | | **⚠️ Q-05** |
| Emitir certificado | | | ✔ | **⚠️ Q-05** |

**Decisão pendente (R4):** se Q-05 definir emissão **automática**, a condição de presença desaparece e R3/R4 colapsam em uma única regra (basta inscrição confirmada + evento realizado); se exigir **presença**, R4 = negar, e o registro de presença (RF-19) entra no escopo. A tabela mostra que a decisão custa exatamente uma condição e um requisito funcional.

---

## TD-05 — Convocação da lista de espera

Aplicada quando uma vaga é liberada (cancelamento, expiração) em evento/atividade com lista de espera. Implementa RN-02 e RN-07. **Estrutura proposta — depende integralmente de Q-04.**

| Condições | R1 | R2 | R3 |
| --- | :-: | :-: | :-: |
| Há inscritos na lista de espera? | N | S | S |
| Primeiro da lista responde dentro do prazo? **⚠️ Q-04** | — | S | N |
| **Ações** | | | |
| Devolver vaga à disponibilidade pública | ✔ | | |
| Bloquear vaga e notificar o convocado (RF-14, RF-22) | | ✔ | ✔ |
| Efetivar inscrição do convocado → **TD-01** (fluxo de pagamento, se pago) | | ✔ | |
| Expirar convocação e convocar o próximo | | | ✔ |

**Pendências de Q-04 embutidas:** ordem de convocação (presumida: chegada), prazo de resposta, se a vaga fica bloqueada durante a convocação (presumido: sim), e se o convocado de evento pago entra em "Aguardando Pagamento" com prazo próprio.

---

## Resumo das pendências por tabela

| Tabela | Política | Completude | Questões |
| --- | --- | --- | --- |
| TD-01 | Efetivação e reserva de vaga | Estrutura completa; 1 célula crítica pendente | 🔴 Q-01, Q-06 |
| TD-02 | Cancelamento | Estrutura completa; resultado de "fora do prazo" pendente | 🔴 Q-02 |
| TD-03 | Reembolso | **Moldura proposta — condições a confirmar** | 🔴 Q-03 |
| TD-04 | Certificado | Completa; colapsa em decisão binária de Q-05 | 🟡 Q-05 |
| TD-05 | Lista de espera | Moldura proposta — parâmetros a confirmar | 🟡 Q-04 |

**Uso recomendado:** levar TD-01, TD-02 e TD-03 impressas/projetadas à reunião conjunta Organizadores + Equipe Financeira e preencher as células ⚠️ ao vivo — cada célula preenchida elimina uma pendência 🔴 e destrava a especificação dos casos de uso de inscrição, cancelamento e reembolso.
