# Critérios de Aceitação (Gherkin) — Sistema de Gestão de Eventos

**Documentos relacionados:** [casos-de-uso.md](casos-de-uso.md) · [tabelas-de-decisao.md](tabelas-de-decisao.md) · [diagrama-estados-inscricao.md](diagrama-estados-inscricao.md) · [duvidas-e-lacunas.md](../analise/duvidas-e-lacunas.md)
**Versão:** 1.0
**Status:** Proposta para validação com stakeholders

## Objetivo e escopo

Critérios de aceitação verificáveis para os **fluxos críticos**, complementando os casos de uso — cada cenário deriva de uma regra das [tabelas de decisão](tabelas-de-decisao.md) ou de uma transição do [diagrama de estados](diagrama-estados-inscricao.md), com rastreabilidade nas tags.

**Convenções de tags:**
- `@UC-XX`, `@TD-XX/RX`, `@RN-XX` — rastreabilidade ao caso de uso, à regra da tabela de decisão e à regra de negócio.
- `@premissa-QXX` — cenário escrito sobre uma **premissa ainda não validada**; o cenário vale como proposta e deve ser revisto (não descartado) após a resposta da questão. Cenários sem essa tag estão prontos para aceite.
- Valores concretos (prazos, percentuais) em cenários com premissa usam placeholders `<...>` quando o valor é a própria pendência.

---

## F-01 — Inscrição e controle de vagas

```gherkin
# language: pt
Funcionalidade: Inscrição em evento com controle de vagas
  Como participante
  Quero me inscrever em eventos com vagas controladas automaticamente
  Para garantir minha participação sem depender de planilhas da organização

  Contexto:
    Dado que estou autenticado como participante

  @UC-06 @TD-01/R1 @RN-09
  Cenário: Inscrição em evento gratuito com vaga disponível
    Dado um evento gratuito publicado com 10 vagas e 4 inscrições confirmadas
    Quando eu solicito inscrição nesse evento
    Então minha inscrição fica no estado "Confirmada"
    E o número de vagas disponíveis passa a ser 5
    E eu recebo o comprovante de inscrição

  @UC-06 @TD-01/R2 @RN-10 @premissa-Q01
  Cenário: Inscrição em evento pago aguarda confirmação do pagamento
    Dado um evento pago publicado com vagas disponíveis
    Quando eu solicito inscrição nesse evento
    Então minha inscrição fica no estado "Aguardando Pagamento"
    E uma vaga fica reservada para mim até o prazo de expiração <prazo Q-01>
    E eu recebo as instruções de pagamento
    E eu ainda não recebo o comprovante de inscrição

  @UC-06 @TD-01/R3 @RN-10
  Cenário: Confirmação do pagamento efetiva a inscrição
    Dado que minha inscrição está "Aguardando Pagamento"
    Quando a Equipe Financeira confirma o meu pagamento
    Então minha inscrição fica no estado "Confirmada"
    E eu recebo o comprovante de inscrição

  @UC-06 @RNF-10 @RN-01
  Cenário: Duas solicitações simultâneas disputando a última vaga
    Dado um evento com exatamente 1 vaga disponível
    Quando dois participantes solicitam inscrição simultaneamente
    Então exatamente uma inscrição fica "Confirmada" ou reserva a vaga
    E o outro participante é informado da lotação e recebe a oferta de lista de espera
    E em nenhum momento o total de vagas ocupadas excede o limite do evento

  @UC-06 @diagrama:AguardandoPagamento->Expirada @premissa-Q01
  Cenário: Pagamento não confirmado no prazo expira a inscrição
    Dado que minha inscrição está "Aguardando Pagamento" com reserva até <prazo Q-01>
    Quando o prazo expira sem confirmação do pagamento
    Então minha inscrição fica no estado "Expirada"
    E a vaga é liberada
    E a lista de espera do evento é acionada, se houver
    E eu sou notificado da expiração

  @UC-06 @TD-01/R5
  Cenário: Solicitação recusada em evento lotado sem interesse na lista de espera
    Dado um evento lotado
    Quando eu solicito inscrição e recuso a lista de espera
    Então nenhuma inscrição é registrada para mim nesse evento
```

---

## F-02 — Inscrição em múltiplas atividades

```gherkin
# language: pt
Funcionalidade: Seleção de atividades na inscrição
  Como participante
  Quero me inscrever em várias atividades do mesmo evento
  Para montar minha própria agenda

  @UC-06 @RN-04 @RF-10
  Cenário: Inscrição em duas atividades do mesmo dia em horários distintos
    Dado um evento com as atividades "A" (09h-12h) e "C" (14h-17h) no mesmo dia, ambas com vagas
    Quando eu me inscrevo no evento selecionando "A" e "C"
    Então minha inscrição inclui as duas atividades
    E as vagas de "A" e de "C" são decrementadas

  @UC-06 @RN-03 @premissa-Q07
  Cenário: Seleção de atividades com horários conflitantes gera alerta sem bloqueio
    Dado um evento com as atividades "A" e "B" ambas das 09h às 12h do mesmo dia
    Quando eu seleciono "A" e "B" na inscrição
    Então o sistema me alerta sobre o conflito de horário
    E permite que eu prossiga com a inscrição nas duas
    # Premissa Q-07: se a decisão for BLOQUEAR, o Então passa a ser
    # "o sistema impede a seleção simultânea e explica o motivo"

  @UC-06 @TD-01 @RN-01
  Cenário: Atividade lotada com evento ainda disponível
    Dado um evento com vagas e a atividade "B" lotada
    Quando eu tento selecionar a atividade "B"
    Então o sistema informa a lotação da atividade
    E me permite concluir a inscrição no evento sem a atividade "B"
```

---

## F-03 — Cancelamento de inscrição

```gherkin
# language: pt
Funcionalidade: Cancelamento de inscrição em autoatendimento
  Como participante
  Quero cancelar minha inscrição diretamente pelo sistema
  Para não depender de contato com a organização

  Contexto:
    Dado que estou autenticado como participante

  @UC-08 @TD-02/R2 @RN-05 @RN-07 @premissa-Q02
  Cenário: Cancelamento permitido dentro do prazo
    Dado uma inscrição "Confirmada" em evento que permite cancelamento
    E que hoje está dentro do prazo-limite de cancelamento <prazo Q-02>
    Quando eu solicito o cancelamento e confirmo na tela de consequências
    Então minha inscrição fica no estado "Cancelada"
    E a vaga é liberada
    E a lista de espera do evento é acionada, se houver
    E eu recebo a notificação do cancelamento

  @UC-08 @TD-02/R1 @RN-06
  Cenário: Evento não permite cancelamento
    Dado uma inscrição "Confirmada" em evento que NÃO permite cancelamento
    Quando eu tento cancelar a inscrição
    Então o sistema bloqueia a operação
    E exibe a política de cancelamento do evento
    E minha inscrição permanece "Confirmada"

  @UC-08 @TD-02/R3 @premissa-Q02
  Cenário: Tentativa de cancelamento fora do prazo
    Dado uma inscrição "Confirmada" em evento que permite cancelamento
    E que o prazo-limite de cancelamento já passou
    Quando eu tento cancelar a inscrição
    Então o sistema bloqueia a operação com orientação para contatar a organização
    # Premissa Q-02: bloqueio simples; alternativa em discussão é
    # encaminhar o pedido para análise da organização

  @UC-08 @T-02 @RN-12
  Cenário: Consequências de reembolso são exibidas antes da confirmação
    Dado uma inscrição paga "Confirmada" cancelável
    Quando eu inicio o cancelamento
    Então antes da confirmação final o sistema exibe se haverá reembolso e em que condição
    E somente após minha confirmação o cancelamento é efetivado

  @UC-08 @TD-02 @RN-10
  Cenário: Desistência de inscrição aguardando pagamento
    Dado uma inscrição "Aguardando Pagamento"
    Quando eu desisto da inscrição
    Então a inscrição fica "Cancelada" sem avaliação de reembolso
    E a vaga reservada é liberada
```

---

## F-04 — Reembolso

```gherkin
# language: pt
Funcionalidade: Processamento de reembolso
  Como membro da Equipe Financeira
  Quero processar reembolsos conforme a política de cada evento
  Para devolver valores apenas nos casos devidos

  @UC-11 @TD-03/R1
  Cenário: Cancelamento de inscrição gratuita não gera reembolso
    Dado uma inscrição cancelada de evento gratuito
    Então nenhuma solicitação de reembolso é criada

  @UC-11 @TD-03/R2 @RN-12 @premissa-Q03
  Cenário: Evento sem previsão de reembolso
    Dado uma inscrição paga e confirmada de evento cuja política não prevê reembolso
    Quando o participante cancela a inscrição
    Então nenhum reembolso é devido
    E o participante foi informado disso antes de confirmar o cancelamento

  @UC-11 @TD-03/R3 @RN-12 @premissa-Q03
  Esquema do Cenário: Reembolso conforme política do evento
    Dado uma inscrição paga e confirmada de evento com política de reembolso "<politica>"
    E o cancelamento efetivado dentro das condições da política
    Quando a Equipe Financeira processa a solicitação de reembolso
    Então o reembolso de "<valor>" é registrado como "processado"
    E a inscrição fica no estado "Reembolsada"
    E o participante é notificado do resultado

    Exemplos: # estrutura hipotética TD-03 — preencher/validar na reunião de Q-03
      | politica            | valor              |
      | integral            | 100% do valor pago |
      | parcial <percentual>| <percentual> Q-03  |
```

---

## F-05 — Lista de espera

```gherkin
# language: pt
Funcionalidade: Lista de espera e convocação
  Como participante interessado em evento lotado
  Quero entrar na lista de espera e ser convocado quando surgir vaga
  Para ter chance de participar

  @UC-09 @TD-01/R4 @RN-02
  Cenário: Entrada na lista de espera de evento lotado
    Dado um evento lotado com lista de espera habilitada
    Quando eu solicito inscrição e aceito entrar na lista de espera
    Então minha inscrição fica no estado "Em Lista de Espera"
    E eu sou informado da minha posição na lista

  @UC-09 @TD-05/R2 @RN-07 @premissa-Q04
  Cenário: Convocação do primeiro da lista quando surge vaga
    Dado um evento lotado com 3 inscrições na lista de espera
    Quando uma inscrição confirmada é cancelada
    Então o primeiro da lista de espera é convocado e notificado
    E a vaga fica bloqueada para o convocado durante o prazo de resposta <prazo Q-04>
    E a vaga não aparece como disponível ao público

  @UC-09 @TD-05/R2 @premissa-Q04
  Cenário: Convocado de evento pago aceita a vaga
    Dado que fui convocado da lista de espera de um evento pago
    Quando eu aceito a convocação dentro do prazo
    Então minha inscrição fica "Aguardando Pagamento"
    E sigo o fluxo normal de pagamento com prazo próprio de expiração

  @UC-09 @TD-05/R3 @premissa-Q04
  Cenário: Convocação expira e o próximo da lista é chamado
    Dado que o primeiro da lista foi convocado com prazo de resposta <prazo Q-04>
    Quando o prazo esgota sem resposta
    Então a convocação dele fica "Expirada"
    E o segundo da lista é convocado automaticamente

  @UC-09 @TD-05/R1
  Cenário: Vaga liberada sem lista de espera volta ao público
    Dado um evento lotado sem inscrições na lista de espera
    Quando uma inscrição confirmada é cancelada
    Então a vaga volta a aparecer como disponível no catálogo
```

---

## F-06 — Certificados

```gherkin
# language: pt
Funcionalidade: Emissão de certificado
  Como participante de evento realizado
  Quero emitir meu certificado pelo sistema
  Para comprovar minha participação

  @UC-12 @TD-04/R1 @RN-13
  Cenário: Certificado indisponível antes da realização do evento
    Dado uma inscrição "Confirmada" em evento ainda não realizado
    Quando eu tento emitir o certificado
    Então o sistema nega a emissão informando que o evento não foi realizado

  @UC-12 @TD-04/R2
  Cenário: Inscrição cancelada não dá direito a certificado
    Dado uma inscrição "Cancelada" de um evento já realizado
    Quando eu tento emitir o certificado
    Então o sistema nega a emissão informando o motivo

  @UC-12 @TD-04/R3 @RN-14 @premissa-Q05
  Cenário: Emissão de certificado com presença confirmada
    Dado uma inscrição "Concluída" em evento realizado
    E minha presença confirmada no evento
    Quando eu solicito o certificado
    Então o certificado é emitido com código de validação
    E fica disponível para download
    # Premissa Q-05: se a decisão for emissão AUTOMÁTICA, a condição
    # de presença é removida deste cenário e o cenário seguinte é excluído

  @UC-12 @TD-04/R4 @premissa-Q05
  Cenário: Emissão negada sem presença confirmada
    Dado uma inscrição "Concluída" em evento realizado que exige presença
    E que minha presença não foi registrada
    Quando eu solicito o certificado
    Então o sistema nega a emissão informando a ausência de registro de presença

  @UC-12 @RNF-04
  Cenário: Validação pública da autenticidade do certificado
    Dado um certificado emitido com código de validação
    Quando qualquer pessoa consulta esse código na página pública de validação
    Então o sistema confirma a autenticidade e exibe evento, participante e data de emissão
    # Campos exibidos na validação pública: conferir minimização com Q-08/LGPD
```

---

## F-07 — Painel do organizador

```gherkin
# language: pt
Funcionalidade: Acompanhamento de inscrições em tempo real
  Como organizador
  Quero acompanhar as inscrições dos meus eventos em tempo real
  Para controlar a ocupação sem planilhas

  @UC-03 @RNF-09 @premissa-Q09
  Cenário: Painel reflete nova inscrição dentro da defasagem máxima
    Dado o painel do evento aberto exibindo 411 inscritos
    Quando um participante efetiva a 412ª inscrição
    Então o painel passa a exibir 412 inscritos em no máximo 30 segundos
    # Meta de 30s proposta em RNF-09 — validar em Q-09

  @UC-03 @RN-16
  Cenário: Organizador só acessa os próprios eventos
    Dado que estou autenticado como organizador do evento "X"
    Quando eu tento acessar o painel do evento "Y", de outro organizador
    Então o acesso é negado
```

---

## Cobertura e pendências

| Funcionalidade | Cenários | Prontos para aceite | Sobre premissa (⚠️) |
| --- | --- | --- | --- |
| F-01 Inscrição e vagas | 6 | 4 | 2 (Q-01) |
| F-02 Múltiplas atividades | 3 | 2 | 1 (Q-07) |
| F-03 Cancelamento | 5 | 3 | 2 (Q-02) |
| F-04 Reembolso | 3 | 1 | 2 (Q-03) |
| F-05 Lista de espera | 5 | 2 | 3 (Q-04) |
| F-06 Certificados | 5 | 3 | 2 (Q-05) |
| F-07 Painel | 2 | 1 | 1 (Q-09) |
| **Total** | **29** | **16** | **13** |

**Leitura do quadro:** 16 cenários estão prontos para aceite — derivam de regras já definidas e não mudam com as respostas pendentes. Os 13 cenários `@premissa-QXX` codificam as premissas adotadas nos artefatos anteriores; nas reuniões, cada resposta ou **confirma o cenário como está** ou exige a troca indicada nos comentários `#` — nenhuma resposta invalida a estrutura, apenas preenche os placeholders `<...>` ou inverte o comportamento comentado.
