# Requisitos Não Funcionais — Sistema de Gestão de Eventos

**Documento de origem:** [Elicitacao-Gestao-de-Eventos.md](../elicitacao/Elicitacao-Gestao-de-Eventos.md)
**Documento relacionado:** [requisitos-funcionais.md](requisitos-funcionais.md)
**Versão:** 1.0
**Status:** Em análise

## Nota importante sobre a origem destes requisitos

A própria elicitação registra (Seção 4 — Observações) que **não foram levantados requisitos relacionados à segurança, desempenho, disponibilidade, acessibilidade e privacidade dos dados**. Portanto, os requisitos abaixo são **propostos pela equipe de análise** a partir de duas fontes:

1. **Derivação do contexto e dos requisitos funcionais** — necessidades implícitas nas declarações dos stakeholders (ex.: "tempo real", controle de vagas concorrente, dados de participantes visíveis a palestrantes);
2. **Boas práticas e obrigações legais** — em especial a LGPD (Lei nº 13.709/2018), aplicável por o sistema tratar dados pessoais de participantes.

**Todos os valores quantitativos (metas) são propostas iniciais e devem ser validados e ajustados junto aos stakeholders.**

## Convenções

- **Identificação:** RNF-XX (numeração sequencial), agrupados por categoria (ISO/IEC 25010 como referência).
- **Origem:** *Derivado* (decorre de um RF ou de declaração da elicitação) ou *Proposto* (boa prática/obrigação legal, sem base direta na elicitação).

---

## 1. Segurança

### RNF-01 — Autenticação e controle de acesso por perfil
O acesso ao sistema deve exigir autenticação, e as funcionalidades devem ser autorizadas conforme o perfil do usuário (participante, organizador, equipe financeira, palestrante, administrador), aplicando o princípio do menor privilégio.
- **Origem:** Derivado de RF-23 e da existência de cinco perfis com interesses distintos.

### RNF-02 — Proteção de dados em trânsito e em repouso
Toda a comunicação entre cliente e servidor deve ser criptografada (TLS 1.2 ou superior). Credenciais devem ser armazenadas com hash criptográfico adequado (ex.: bcrypt/argon2); dados sensíveis de pagamento não devem ser armazenados além do necessário.
- **Origem:** Proposto (boa prática; sistema trata dados pessoais e pagamentos).

### RNF-03 — Registro de auditoria
O sistema deve registrar trilha de auditoria das operações críticas (inscrição, cancelamento, confirmação de pagamento, reembolso, emissão de certificado, alterações em eventos), contendo autor, data/hora e operação realizada.
- **Origem:** Derivado de RF-24 e do interesse de controle da Equipe Financeira e dos Organizadores.

### RNF-04 — Autenticidade dos certificados
Os certificados emitidos devem possuir mecanismo de verificação de autenticidade (ex.: código de validação consultável no sistema).
- **Origem:** Derivado de RF-18 (boa prática para documentos com valor externo).

---

## 2. Privacidade (LGPD)

### RNF-05 — Conformidade com a LGPD
O sistema deve tratar os dados pessoais dos participantes em conformidade com a Lei nº 13.709/2018 (LGPD), incluindo: coleta com finalidade explícita, consentimento quando aplicável, e atendimento aos direitos dos titulares (acesso, correção e exclusão de dados).
- **Origem:** Proposto (obrigação legal).

### RNF-06 — Minimização de dados expostos a palestrantes
As informações de participantes visíveis aos palestrantes (RF-21) devem se limitar ao mínimo necessário à condução da atividade. ⚠️ *O conjunto exato de campos depende de definição com os stakeholders e do parecer sobre LGPD.*
- **Origem:** Derivado de RF-21 e da observação da Seção 4 da elicitação.

### RNF-07 — Retenção e descarte de dados
Devem ser definidos e implementados prazos de retenção para dados pessoais e financeiros, com descarte ou anonimização após o prazo. ⚠️ *Prazos a definir com stakeholders e área jurídica.*
- **Origem:** Proposto (obrigação legal).

---

## 3. Desempenho e Capacidade

### RNF-08 — Tempo de resposta
As operações interativas (consulta de eventos, inscrição, acompanhamento) devem responder em até **3 segundos** no percentil 95, sob carga normal.
- **Origem:** Proposto (meta inicial a validar).

### RNF-09 — Atualização do painel em tempo real
O painel de acompanhamento dos organizadores (RF-06) deve refletir novas inscrições e cancelamentos com defasagem máxima de **30 segundos**.
- **Origem:** Derivado de RF-06 ("em tempo real" — meta a validar; ver documento de ambiguidades).

### RNF-10 — Concorrência no controle de vagas
O controle de vagas (RF-04) deve permanecer consistente sob inscrições simultâneas: em nenhuma hipótese o número de inscrições confirmadas pode exceder o número de vagas, mesmo em picos de acesso (ex.: abertura de inscrições de evento concorrido).
- **Origem:** Derivado de RF-04/RF-05 — requisito de integridade sob concorrência.

### RNF-11 — Capacidade
O sistema deve suportar a carga esperada de picos de abertura de inscrições sem degradação além das metas do RNF-08. ⚠️ *Volumetria (nº de eventos simultâneos, inscritos por evento, acessos concorrentes) não foi levantada — pendência para os stakeholders.*
- **Origem:** Proposto (depende de volumetria a levantar).

---

## 4. Disponibilidade e Confiabilidade

### RNF-12 — Disponibilidade
O sistema deve estar disponível **99,5%** do tempo em base mensal, com atenção especial aos períodos de inscrições abertas e de realização de eventos.
- **Origem:** Proposto (meta inicial a validar).

### RNF-13 — Backup e recuperação
Os dados devem ser copiados (backup) ao menos diariamente, com procedimento de recuperação testado. Metas iniciais: RPO ≤ 24h e RTO ≤ 4h. ⚠️ *Metas a validar.*
- **Origem:** Proposto (boa prática).

### RNF-14 — Integridade transacional
Operações que envolvem múltiplos efeitos (ex.: cancelamento → liberação de vaga → convocação da lista de espera → reembolso) devem ser executadas de forma consistente: nenhuma etapa pode deixar o sistema em estado intermediário inválido.
- **Origem:** Derivado de RF-13, RF-05 e RF-17.

---

## 5. Usabilidade e Acessibilidade

### RNF-15 — Facilidade de uso para o público geral
As funcionalidades do participante (consulta, inscrição, cancelamento, certificado) devem ser utilizáveis sem treinamento, uma vez que o público é externo e heterogêneo. O cancelamento em autoatendimento (RF-13) deve ser concluível em poucos passos, sem intervenção da organização.
- **Origem:** Derivado do contexto (motivação do projeto: "melhor experiência aos participantes") e de RF-13.

### RNF-16 — Acessibilidade digital
As interfaces voltadas ao público (catálogo, inscrição, certificados) devem atender às diretrizes **WCAG 2.1 nível AA**.
- **Origem:** Proposto (boa prática/inclusão; lacuna apontada na Seção 4 da elicitação).

### RNF-17 — Compatibilidade
As interfaces web devem funcionar nos navegadores modernos (Chrome, Firefox, Edge, Safari em versões correntes) e ser responsivas para uso em dispositivos móveis.
- **Origem:** Proposto (público externo acessa por dispositivos variados).

---

## 6. Manutenibilidade e Operação

### RNF-18 — Manutenibilidade
O sistema deve ser desenvolvido segundo os padrões de arquitetura, codificação e documentação definidos pela Equipe de TI da Eventus, que será responsável por sua manutenção. ⚠️ *Padrões e stack tecnológica a definir com a Equipe de TI.*
- **Origem:** Derivado do interesse da Equipe de TI ("Desenvolver e manter o sistema").

### RNF-19 — Monitoramento
O sistema deve expor logs e métricas operacionais que permitam à Equipe de TI monitorar disponibilidade, desempenho e erros em produção.
- **Origem:** Proposto (suporte aos RNF-08 e RNF-12).

### RNF-20 — Confiabilidade das notificações
O envio de notificações (RF-22) deve registrar o resultado de cada envio e reprocessar falhas transitórias, garantindo que comprovantes e convocações de lista de espera não sejam silenciosamente perdidos.
- **Origem:** Derivado de RF-11, RF-14 e RF-22.

---

## Resumo por categoria

| Categoria | Requisitos | Base na elicitação |
| --- | --- | --- |
| Segurança | RNF-01 a RNF-04 | Lacuna declarada (Seção 4) — propostos/derivados |
| Privacidade | RNF-05 a RNF-07 | Lacuna declarada (Seção 4) + RF-21 |
| Desempenho e capacidade | RNF-08 a RNF-11 | "Tempo real" (Organizadores) + lacuna declarada |
| Disponibilidade e confiabilidade | RNF-12 a RNF-14 | Lacuna declarada (Seção 4) |
| Usabilidade e acessibilidade | RNF-15 a RNF-17 | Contexto do projeto + lacuna declarada |
| Manutenibilidade e operação | RNF-18 a RNF-20 | Interesse da Equipe de TI |

**Pendências:** RNF-06, RNF-07, RNF-11, RNF-13 e RNF-18 possuem ⚠️ e dependem de definições dos stakeholders; além disso, **todas as metas quantitativas** (RNF-08, RNF-09, RNF-12, RNF-13) são propostas iniciais a validar. Esses pontos serão consolidados no documento de ambiguidades e pontos em aberto.
