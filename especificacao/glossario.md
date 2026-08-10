# Glossário — Sistema de Gestão de Eventos

**Documentos relacionados:** [Elicitacao-Gestao-de-Eventos.md](../elicitacao/Elicitacao-Gestao-de-Eventos.md) · [duvidas-e-lacunas.md](../analise/duvidas-e-lacunas.md) · [modelo-conceitual.md](modelo-conceitual.md)
**Versão:** 1.0
**Status:** Proposta para validação com stakeholders

## Objetivo

Estabelecer um vocabulário único para o projeto, eliminando as ambiguidades identificadas na elicitação (itens A-01 a A-07 do documento de dúvidas e lacunas). Definições marcadas com ⚠️ contêm parcela pendente de decisão dos stakeholders (referência Q-XX).

**Regra de uso:** todos os artefatos do projeto (requisitos, casos de uso, telas, testes) devem empregar os termos exatamente como definidos aqui. Sinônimos informais usados nas entrevistas são registrados no campo "Também chamado de".

---

## Termos do domínio

### Atividade
Unidade da programação de um Evento — workshop, palestra, minicurso ou similar — com data, horário, local, palestrante(s) e, quando aplicável, número de vagas próprio. Um Evento pode ter várias Atividades, inclusive simultâneas (RN-03).
**Também chamado de:** workshop (nas entrevistas, usado como caso particular).

### Atividades simultâneas
Atividades de um mesmo Evento cujos horários se sobrepõem total ou parcialmente. A programação simultânea é permitida (RN-03); ⚠️ a inscrição de um mesmo Participante em Atividades simultâneas está pendente de definição (Q-07, ambiguidade A-05).

### Cancelamento
Ato do Participante de desfazer a própria Inscrição em autoatendimento (RN-05), permitido conforme a política do Evento (RN-06). **Não se confunde com Reembolso** — cancelar é desfazer a inscrição; reembolsar é devolver o valor pago, e um pode existir sem o outro (tensão T-02). ⚠️ Prazo-limite pendente (Q-02).

### Certificado
Documento emitido pelo sistema que atesta a participação em um Evento (⚠️ ou Atividade — escopo pendente, Q-05), disponível ao Participante somente após a realização (RN-13). ⚠️ Condição de emissão (automática × mediante Presença) pendente (Q-14/Q-05).

### Comprovante de inscrição
Documento gerado pelo sistema que confirma ao Participante a **efetivação** de sua Inscrição (RN-08). ⚠️ Em Eventos pagos, está pendente definir se existe também um *recibo do pedido*, anterior à confirmação do pagamento (T-04, Q-06). Não se confunde com Certificado.

### Convocação
Notificação enviada ao primeiro da Lista de Espera quando uma Vaga é liberada, ofertando-a por prazo determinado. ⚠️ Ordem, prazo e bloqueio da vaga pendentes (Q-04).

### Evento
Ocasião organizada pela Eventus — congresso, workshop avulso ou evento corporativo — com data(s), local, número de Vagas, condição de gratuidade e políticas próprias (cancelamento, ⚠️ reembolso). Pode conter uma ou mais Atividades.

### Evento gratuito / Evento pago
Classificação definida no cadastro do Evento (RN-09). No Evento gratuito, a Inscrição é efetivada sem Pagamento; no pago, a efetivação depende da confirmação do Pagamento (RN-10, ⚠️ Q-10 sobre abrangência).

### Evento lotado
Situação em que não há Vaga disponível para novas Inscrições. ⚠️ Depende da decisão de Q-01 saber se Vagas reservadas (pagamento em andamento) contam para a lotação (ambiguidade A-06).

### Inscrição
Vínculo entre um Participante e um Evento, criado a pedido do Participante e sujeito ao ciclo de vida definido no [diagrama de estados](diagrama-estados-inscricao.md) (Solicitada, Aguardando Pagamento, Confirmada, Em Lista de Espera, Convocada, Cancelada, Expirada, Reembolsada, Concluída). ⚠️ Se a Inscrição também se aplica individualmente a Atividades é decisão do modelo conceitual, a validar.

### Inscrição efetivada
Inscrição no estado **Confirmada**: em Evento gratuito, imediatamente após a solicitação com Vaga disponível; em Evento pago, após a confirmação do Pagamento. Termo usado nas entrevistas como "inscrição liberada".

### Lista de espera
Fila de Participantes interessados em um Evento/Atividade lotado (RN-02), acionada quando uma Vaga é liberada (RN-07). ⚠️ Regras de funcionamento pendentes (Q-04); prioridade de escopo a confirmar (A-03).

### Pagamento
Valor devido pela Inscrição em Evento pago. **Pagamento confirmado** é aquele verificado pela Equipe Financeira (⚠️ manual ou automático via meio de pagamento — Q-10), condição para a efetivação da Inscrição (RN-10).

### Participante
Pessoa que se inscreve em Eventos. No sistema, usuário com perfil de acesso às funções de consulta de catálogo, Inscrição, Cancelamento, acompanhamento e emissão de Certificado.

### Presença
Registro de comparecimento do Participante ao Evento/Atividade. ⚠️ Entidade **condicional**: só integra o escopo se a emissão de Certificado depender dela (Q-05, RF-19). Forma de registro pendente.

### Reembolso
Devolução, total ou parcial (⚠️ Q-03), do valor pago por uma Inscrição cancelada, quando a política do Evento assim previr (RN-12). Processado pela Equipe Financeira (RF-17). Ver distinção em **Cancelamento**.

### Tempo real (painel do organizador)
Qualificação da atualização do painel de acompanhamento (RF-06). **Definição operacional adotada:** defasagem máxima de 30 segundos entre o fato (inscrição/cancelamento) e sua exibição (RNF-09). ⚠️ Meta proposta, a validar (A-01, Q-09).

### Vaga
Unidade de capacidade de um Evento ou Atividade (RN-01). **Vaga disponível:** ainda não ocupada nem reservada. **Vaga reservada:** ⚠️ bloqueada temporariamente durante um processo em andamento (pagamento iniciado, Convocação) — a existência e as regras da reserva dependem de Q-01/Q-04. **Vaga liberada:** devolvida à disponibilidade por Cancelamento ou expiração (RN-07).

---

## Atores

| Termo | Definição |
| --- | --- |
| **Participante** | Ver termo no domínio — público externo que se inscreve nos Eventos. |
| **Organizador** | Colaborador da Eventus responsável por cadastrar Eventos e Atividades, configurar políticas, acompanhar e gerenciar inscrições (⚠️ escopo de "gerenciar" a detalhar — A-07). |
| **Equipe Financeira** | Área da Eventus que confirma Pagamentos e processa Reembolsos. |
| **Palestrante** | Pessoa que conduz Atividades; acessa a programação e a lista de participantes **das próprias Atividades** (RN-15; ⚠️ campos visíveis pendentes — Q-08). |
| **Equipe de TI** | Área da Eventus que desenvolve, opera e mantém o sistema. Não é ator funcional do domínio. |
| **Eventus** | A empresa organizadora de eventos, dona do sistema. |

---

## Termos a NÃO utilizar (e seus substitutos)

| Evitar | Usar | Motivo |
| --- | --- | --- |
| "inscrição liberada" | Inscrição efetivada / Confirmada | Padronização com o diagrama de estados |
| "workshop" (genérico) | Atividade | "Workshop" é um tipo de Atividade; nas entrevistas foi usado para ambos |
| "cancelar" (referindo-se a reembolso) | Cancelamento **e/ou** Reembolso, conforme o caso | Os dois direitos são independentes (T-02) |
| "comprovante" (referindo-se a certificado) | Comprovante de inscrição × Certificado | Documentos distintos com momentos distintos |
