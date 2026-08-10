# Wireframes (baixa fidelidade) — Sistema de Gestão de Eventos

**Documentos relacionados:** [casos-de-uso.md](casos-de-uso.md) · [glossario.md](glossario.md) · [duvidas-e-lacunas.md](../analise/duvidas-e-lacunas.md)
**Versão:** 1.0
**Status:** Proposta para validação com stakeholders

## Objetivo

Materializar as telas-chave em baixa fidelidade para validação com Participantes e Organizadores — o instrumento mais eficaz com stakeholders não técnicos. A baixa fidelidade é **intencional**: o foco da validação é conteúdo, fluxo e regras (o que a tela mostra e permite), não o visual. Cada tela referencia o caso de uso que a origina e sinaliza com ⚠️ os elementos que dependem de questões em aberto.

---

## W-01 — Catálogo de Eventos (UC-05)

Público-alvo: Participante. ⚠️ A confirmar se é acessível sem login (nota ¹ do UC-05).

```text
+----------------------------------------------------------------------+
|  EVENTUS                                     [ Entrar ] [ Cadastrar ]|
+----------------------------------------------------------------------+
|  Eventos disponíveis                                                 |
|                                                                      |
|  Buscar: [__________________]  Tipo: [Todos v]  Data: [___/___] [OK] |
|                                                                      |
|  +----------------------------------------------------------------+ |
|  | CONGRESSO | Congresso Brasileiro de Tecnologia                  | |
|  | 12-14/mar/2027 · Centro de Convenções SP · R$ 350,00            | |
|  | Vagas: DISPONIVEIS          [ Ver detalhes e inscrever-se ]     | |
|  +----------------------------------------------------------------+ |
|  +----------------------------------------------------------------+ |
|  | WORKSHOP  | Oficina de Design de Serviços                       | |
|  | 20/mar/2027 · On-line · GRATUITO                                | |
|  | Vagas: ULTIMAS VAGAS (3)    [ Ver detalhes e inscrever-se ]     | |
|  +----------------------------------------------------------------+ |
|  +----------------------------------------------------------------+ |
|  | CORPORATIVO | Encontro de Lideranças                            | |
|  | 02/abr/2027 · Hotel Nacional · R$ 200,00                        | |
|  | Vagas: LOTADO               [ Entrar na lista de espera ]  ⚠️Q-04| |
|  +----------------------------------------------------------------+ |
+----------------------------------------------------------------------+
```

**Decisões embutidas a validar:** exibir contagem de vagas restantes ("últimas vagas") ou apenas disponível/lotado? ⚠️ A definição de "lotado" depende de Q-01 (reservas contam?).

---

## W-02 — Detalhe do Evento e Inscrição (UC-06, passos 2–5)

```text
+----------------------------------------------------------------------+
|  < Voltar ao catálogo                                                |
|  Congresso Brasileiro de Tecnologia          12-14/mar/2027 · SP     |
+----------------------------------------------------------------------+
|  Sobre o evento: Lorem ipsum...                                      |
|  Valor da inscrição: R$ 350,00                                       |
|                                                                      |
|  +-- POLÍTICAS DO EVENTO (sempre visíveis antes de inscrever) -----+ |
|  | Cancelamento: permitido até ___/___/____  ⚠️Q-02                 | |
|  | Reembolso: [política do evento]           ⚠️Q-03                 | |
|  +---------------------------------------------------- (mitiga T-01)| |
|                                                                      |
|  Selecione suas atividades (opcional):                               |
|  DIA 12/mar                                                          |
|  [x] 09h-12h  Workshop A - IA Aplicada           (12 vagas)          |
|  [ ] 09h-12h  Workshop B - Cloud                 (LOTADO)            |
|      [ Lista de espera da atividade ] ⚠️Q-04                         |
|  [x] 14h-17h  Workshop C - DevOps                (30 vagas)          |
|                                                                      |
|  ! Atenção: A e B ocorrem no mesmo horário       ⚠️Q-07              |
|    (premissa atual: alerta sem bloquear)                             |
|                                                                      |
|                          [ Confirmar inscrição ]                     |
+----------------------------------------------------------------------+
```

**Elementos de regra na tela:** políticas exibidas **antes** da inscrição (mitigação de T-01/T-02 — UC-06 passo 2); alerta de conflito de horário conforme premissa de Q-07; lista de espera por atividade a confirmar (Q-04).

---

## W-03 — Pagamento da Inscrição (UC-06/A1)

```text
+----------------------------------------------------------------------+
|  Inscrição solicitada - Congresso Brasileiro de Tecnologia           |
+----------------------------------------------------------------------+
|  Situação: AGUARDANDO PAGAMENTO                                      |
|                                                                      |
|  +------------------------------------------------------------+     |
|  |  Sua vaga está reservada até 14/02 23h59   ⚠️Q-01           |     |
|  |  (premissa: reserva com prazo de expiração)                |     |
|  +------------------------------------------------------------+     |
|                                                                      |
|  Valor: R$ 350,00                                                    |
|  Forma de pagamento:  ⚠️Q-10 (Pix? cartão? boleto? manual?)          |
|  [ instruções de pagamento aqui ]                                    |
|                                                                      |
|  Após a confirmação do pagamento você receberá o comprovante         |
|  de inscrição por ___________ ⚠️Q-06 (canal a definir)               |
|                                                                      |
|  [ Já paguei ]                [ Desistir da inscrição ]              |
+----------------------------------------------------------------------+
```

**Nota (T-04):** esta tela é o candidato a "recibo do pedido" — documento anterior ao comprovante de efetivação. Validar em Q-06.

---

## W-04 — Minhas Inscrições (UC-07)

Os selos de situação espelham os estados do [diagrama](diagrama-estados-inscricao.md).

```text
+----------------------------------------------------------------------+
|  EVENTUS                 Olá, Ana        [ Minhas inscrições ] [Sair]|
+----------------------------------------------------------------------+
|  Minhas inscrições                                                   |
|                                                                      |
|  +----------------------------------------------------------------+ |
|  | Congresso Bras. de Tecnologia            [ CONFIRMADA ]         | |
|  | 12-14/mar/2027 · 2 atividades selecionadas                      | |
|  | [ Ver comprovante ] [ Cancelar inscrição ]                      | |
|  +----------------------------------------------------------------+ |
|  | Encontro de Lideranças                   [ LISTA DE ESPERA #4 ] | |
|  | 02/abr/2027                              ⚠️Q-04 (exibir posição?)| |
|  | [ Sair da lista ]                                               | |
|  +----------------------------------------------------------------+ |
|  | Oficina de Design de Serviços            [ AGUARDANDO PAGTO ]   | |
|  | Reserva expira em 14/02 ⚠️Q-01                                   | |
|  | [ Ver instruções de pagamento ] [ Desistir ]                    | |
|  +----------------------------------------------------------------+ |
|  | Seminário 2026 (realizado)               [ CONCLUÍDA ]          | |
|  | [ Emitir certificado ]  ⚠️Q-05                                   | |
|  +----------------------------------------------------------------+ |
+----------------------------------------------------------------------+
```

---

## W-05 — Confirmação de Cancelamento (UC-08, passos 4–5)

Modal exibido antes de efetivar o cancelamento — ponto central da mitigação de T-02.

```text
        +------------------------------------------------------+
        |  Cancelar inscrição?                            [ X ] |
        +------------------------------------------------------+
        |  Evento: Congresso Brasileiro de Tecnologia           |
        |                                                       |
        |  Ao confirmar:                                        |
        |  - Sua vaga será liberada para outros participantes   |
        |  - REEMBOLSO: ________________________  ⚠️Q-03        |
        |    (ex.: "integral", "80% do valor", "sem reembolso   |
        |     -- fora do prazo") - SEMPRE explícito antes de    |
        |     confirmar                                         |
        |                                                       |
        |  Esta ação não pode ser desfeita.                     |
        |                                                       |
        |  [ Manter inscrição ]      [ Confirmar cancelamento ] |
        +------------------------------------------------------+
```

---

## W-06 — Painel do Organizador (UC-03)

```text
+----------------------------------------------------------------------+
|  EVENTUS · Organizador          [ Meus eventos ] [ Novo evento ]     |
+----------------------------------------------------------------------+
|  Congresso Brasileiro de Tecnologia          atualizado há 12s ⚠️A-01|
|                                                                      |
|  +---------------+  +---------------+  +---------------+             |
|  |  INSCRITOS    |  |  VAGAS        |  |  LISTA ESPERA |             |
|  |     412       |  |   88 / 500    |  |      23       |             |
|  +---------------+  +---------------+  +---------------+             |
|  Aguardando pagamento: 35 ⚠️Q-01 (contam como vaga ocupada?)         |
|                                                                      |
|  Por atividade:                                                      |
|  | Atividade            | Vagas | Inscritos | Espera |               |
|  | Workshop A - IA      |  40   |    40     |   12   | LOTADO        |
|  | Workshop B - Cloud   |  40   |    28     |   --   |               |
|  | Workshop C - DevOps  |  60   |    31     |   --   |               |
|                                                                      |
|  [ Exportar lista ] [ Gerenciar participantes ⚠️A-07 ]               |
+----------------------------------------------------------------------+
```

**Ponto de validação:** o painel exibe "aguardando pagamento" como categoria separada — torna visível aos Organizadores a consequência da decisão de Q-01.

---

## W-07 — Cadastro de Evento: Políticas (UC-01)

Recorte da etapa de políticas — a parte do cadastro que depende das definições pendentes.

```text
+----------------------------------------------------------------------+
|  Novo evento - Etapa 3 de 4: Políticas                               |
+----------------------------------------------------------------------+
|  Inscrição:                                                          |
|  (o) Evento pago      Valor: [R$ 350,00]                             |
|  ( ) Evento gratuito                                                 |
|                                                                      |
|  Cancelamento pelo participante:            (RN-06)                  |
|  (o) Permitido até [__] dias antes do evento   ⚠️Q-02                |
|  ( ) Não permitido                                                   |
|                                                                      |
|  Reembolso:                                 (RN-12) ⚠️Q-03           |
|  ( ) Integral dentro do prazo de cancelamento                        |
|  ( ) Parcial: [__]%                                                  |
|  ( ) Sem reembolso                                                   |
|  (estrutura hipotética - validar TD-03 antes de implementar)         |
|                                                                      |
|  Lista de espera:                           (RN-02) ⚠️Q-04           |
|  [x] Habilitar lista de espera neste evento                          |
|                                                                      |
|  Certificado:                               (RN-14) ⚠️Q-05           |
|  ( ) Emissão automática após o evento                                |
|  ( ) Somente com presença confirmada                                 |
|                                                                      |
|  [ < Voltar ]                                  [ Próxima etapa > ]   |
+----------------------------------------------------------------------+
```

**Este wireframe é um instrumento de elicitação:** apresenta as políticas como *configuráveis por evento* (decisão de modelagem nº 3 do modelo conceitual). Se os stakeholders reagirem "isso é regra única da Eventus, não escolha por evento", a decisão se inverte — reação que queremos provocar na reunião.

---

## W-08 — Pagamentos Pendentes (UC-10)

```text
+----------------------------------------------------------------------+
|  EVENTUS · Financeiro                     [ Pendências ] [ Reembolsos]|
+----------------------------------------------------------------------+
|  Pagamentos aguardando confirmação        ⚠️Q-10 (premissa: manual)  |
|                                                                      |
|  | Participante | Evento         | Valor   | Reserva até  | Ação   | |
|  | Ana Souza    | Congresso Tec. | 350,00  | 14/02 ⚠️Q-01 |[Confir]| |
|  | Bruno Lima   | Congresso Tec. | 350,00  | 13/02 EXPIRA |[Confir]| |
|  | Carla Dias   | Encontro Lid.  | 200,00  | EXPIRADA !   |[ ver ] | |
|                                                                      |
|  ! Pagamento recebido após expiração: tratamento pendente            |
|    (UC-10/E1 - nova pergunta para reunião Q-01)                      |
+----------------------------------------------------------------------+
```

---

## W-09 — Participantes da Atividade (UC-14 — Palestrante)

```text
+----------------------------------------------------------------------+
|  EVENTUS · Palestrante                       [ Minha programação ]   |
+----------------------------------------------------------------------+
|  Workshop A - IA Aplicada · 12/mar 09h-12h · Sala 3                  |
|  Inscritos: 40 / 40                                                  |
|                                                                      |
|  | # | Nome            | [demais campos] ⚠️Q-08                     | |
|  | 1 | Ana Souza       |  ????                                      | |
|  | 2 | Bruno Lima      |  ????                                      | |
|  | 3 | ...             |                                            | |
|                                                                      |
|  Campos exibidos: SOMENTE os aprovados na definição de Q-08          |
|  (minimização LGPD - RNF-06 / RN-15). Este wireframe deliberada-     |
|  mente NÃO propõe campos além do nome.                               |
+----------------------------------------------------------------------+
```

---

## Cobertura e uso

| Wireframe | Caso de uso | Valida com | Questões que materializa |
| --- | --- | --- | --- |
| W-01 Catálogo | UC-05 | Participantes | Q-01 (lotado), Q-04 |
| W-02 Detalhe/Inscrição | UC-06 | Participantes + Organizadores | Q-02, Q-03, Q-04, Q-07 · T-01 |
| W-03 Pagamento | UC-06/A1 | Participantes + Financeira | Q-01, Q-06, Q-10 · T-04 |
| W-04 Minhas inscrições | UC-07 | Participantes | Q-01, Q-04, Q-05 |
| W-05 Modal cancelamento | UC-08 | Participantes + Financeira | Q-03 · T-02 |
| W-06 Painel organizador | UC-03 | Organizadores | Q-01 · A-01, A-07 |
| W-07 Políticas do evento | UC-01 | Organizadores + Financeira | Q-02, Q-03, Q-04, Q-05 |
| W-08 Pagamentos pendentes | UC-10 | Financeira | Q-01, Q-10 |
| W-09 Lista do palestrante | UC-14 | Palestrantes + jurídico | Q-08 |

**Uso recomendado nas reuniões:** os wireframes não são proposta de design — são **perguntas desenhadas**. W-07 (políticas por evento) e W-05 (reembolso explícito no cancelamento) devem abrir as reuniões de Q-02/Q-03; W-03 e W-08 apoiam a discussão de Q-01. Telas não desenhadas nesta versão (cadastro de atividades, emissão do certificado, gestão da lista de espera pelo organizador) serão produzidas após as respostas das questões correspondentes.
