# 📋 Ficha de Elicitação de Requisitos

**Curso:** Engenharia de Software  
**Disciplina:** Análise e Projeto de Sistemas  
**Instituição:** UDF Centro Universitário  
**Grupo/integrantes:** Fernando Rebouças | Paulo Henrique | Renan Akira

**Turma:** D2 - Engenharia de Software  
**Data:** 24/09/2026  
**Versão:** 1.0

---

## 1. Identificação do projeto

| **Campo** | **Preenchimento** |
|:---|:---|
| **Nome do projeto** | ReservaFácil — Sistema de Reservas de Restaurante |
| **Objetivo do projeto** | Clientes de restaurantes frequentemente enfrentam dificuldades para realizar reservas de mesas, principalmente em horários de grande movimento, finais de semana e datas comemorativas. Muitas vezes, as reservas são feitas por telefone ou mensagens, dificultando a organização dos horários, o controle da disponibilidade das mesas e o gerenciamento dos pedidos. Além disso, a falta de confirmação e de informações sobre as reservas pode gerar conflitos de horários, filas e insatisfação dos clientes. **Resultado esperado:** desenvolver um sistema que permita aos clientes consultar horários disponíveis, realizar reservas antecipadamente e acompanhar suas solicitações, enquanto o restaurante consegue organizar melhor suas mesas, horários e atendimento. |
| **Contexto e escopo** | Sistema destinado ao gerenciamento de reservas de um restaurante, permitindo que clientes consultem a disponibilidade de mesas, escolham datas e horários, informem a quantidade de pessoas e realizem reservas. O sistema também deverá permitir que funcionários e administradores gerenciem as reservas, confirmem solicitações, realizem alterações e acompanhem a ocupação do restaurante. Nesta etapa, o trabalho se concentra na análise do problema e no levantamento dos requisitos, não estando incluídos sistemas externos de pagamento, integração com aplicativos de entrega ou desenvolvimento de dispositivos físicos. |

---

## 2. Stakeholder e fonte

| **Campo** | **Preenchimento** |
|:---|:---|
| **Stakeholder (nome ou papel)** | ST01 — Clientes que frequentam o restaurante e desejam realizar reservas antecipadamente (stakeholder principal). |
| **Relação com o projeto** | Usuário principal: são diretamente beneficiados pela possibilidade de consultar horários disponíveis e reservar mesas sem precisar entrar em contato diretamente com o restaurante. Influência: alta. |
| **Contato ou setor (se aplicável)** | Clientes do restaurante e público interessado em realizar reservas. |
| **Técnica e data da elicitação** | Observação do problema e levantamento de necessidades dos clientes; setembro de 2026. |
| **Responsável pelo registro** | Grupo do projeto (Fernando Rebouças, Paulo Henrique e Renan Akira). |

---

## 3. Requisito elicitado

| **Campo** | **Preenchimento** |
|:---|:---|
| **ID do requisito** | REQ-001 (corresponde ao RF01 do levantamento do grupo). |
| **Necessidade relatada pelo stakeholder** | N01 — "Consultar disponibilidade de mesas antes de realizar uma reserva": o cliente deseja saber se existem mesas disponíveis no restaurante para a data, horário e quantidade de pessoas desejadas antes de confirmar sua reserva. |
| **Descrição consolidada** | O sistema deve permitir que o cliente consulte a disponibilidade de mesas do restaurante, informando a data, o horário pretendido e a quantidade de pessoas, apresentando as opções de horários disponíveis antes da realização da reserva. |
| **Justificativa ou benefício esperado** | É uma das funções centrais do sistema. Evita que o cliente precise entrar em contato diretamente com o restaurante para descobrir a disponibilidade, reduz filas e espera, evita conflitos de horários e facilita o planejamento das visitas. Também contribui para uma melhor organização do atendimento e da ocupação das mesas pelo restaurante. |
| **Tipo** | Funcional. |
| **Dependências ou dúvidas** | 1. A fonte responsável pelo controle e atualização da disponibilidade das mesas ainda precisa ser definida (RES01).<br>2. O intervalo de funcionamento do restaurante e os horários disponíveis para reservas deverão ser configurados pela administração.<br>3. Os critérios de disponibilidade dependerão da quantidade de mesas, capacidade de cada mesa e duração estimada dos atendimentos.<br>4. Ainda não está definido se a consulta de disponibilidade exigirá cadastro ou login, ou se poderá ser realizada por qualquer visitante.<br>5. Requisitos de qualidade relacionados: RQ01 (desempenho), RQ03 (usabilidade), RQ04 (atualização das informações) e RQ05 (compatibilidade). |

---

## 4. Regras de negócio

| **ID** | **Regra de negócio relacionada** | **Fonte ou responsável pela validação** |
|:---|:---|:---|
| **RN-001** | O sistema deverá apresentar somente os horários que possuam disponibilidade de mesas para a data e quantidade de pessoas selecionadas pelo cliente. | Administração do restaurante (ST03). |
| **RN-002** | Uma reserva somente será considerada confirmada após o registro e a confirmação pelo sistema ou funcionário responsável, conforme o procedimento definido pelo restaurante. | Gerência do restaurante (ST03). |
| **RN-003** | Não será permitido realizar duas reservas incompatíveis para a mesma mesa e período de atendimento. | Administração do restaurante (ST03). |
| **RN-004** | O cliente deverá informar a quantidade de pessoas que participarão da reserva para que o sistema possa verificar a capacidade das mesas disponíveis. | Gerência do restaurante (ST03). |
| **RN-005** | Os horários disponíveis para reservas deverão respeitar o horário de funcionamento do restaurante. | Administração do restaurante (ST03). |

---

## 5. Prioridade

**Classificação MoSCoW (marque uma):**

- [x] **Must have** (essencial)
- [ ] **Should have** (importante)
- [ ] **Could have** (desejável)
- [ ] **Won't have nesta versão** (fora do escopo atual)

**Justificativa da prioridade:**

A consulta de disponibilidade é uma das funcionalidades fundamentais do sistema, pois permite que o cliente saiba antecipadamente se poderá realizar uma reserva na data e horário desejados. Sem essa funcionalidade, o cliente continuaria dependendo de ligações ou mensagens para descobrir se existem mesas disponíveis, mantendo os problemas que motivaram a criação do sistema.

---

## 6. Critérios de aceitação

Escreva condições verificáveis que permitam decidir se o requisito foi atendido.

| **ID** | **Dado/Quando** | **Então (resultado esperado)** | **Evidência ou forma de verificação** |
|:---|:---|:---|:---|
| **CA-01** | Dado um cliente que deseja realizar uma reserva, quando acessar o sistema e informar a data, o horário e a quantidade de pessoas. | O sistema deverá apresentar os horários que possuem mesas disponíveis para os critérios informados. | Teste funcional realizando consultas com diferentes datas, horários e quantidades de pessoas. |
| **CA-02** | Dado um cliente que acabou de acessar o sistema, quando desejar consultar a disponibilidade de mesas. | Deverá conseguir chegar ao resultado em até três interações (RQ03). | Teste de usabilidade com clientes, contando as interações necessárias até a apresentação dos horários disponíveis. |
| **CA-03** | Dado o sistema em condições normais de uso, quando o cliente solicitar a consulta de disponibilidade. | O resultado deverá ser exibido em até 2 segundos para 95% das requisições (RQ01). | Teste de desempenho com medição do tempo de resposta. |
| **CA-04** | Dado que o cliente realizou uma consulta de disponibilidade, quando o resultado for exibido. | O sistema deverá apresentar informações atualizadas sobre os horários e as mesas disponíveis. | Comparação entre os resultados apresentados e os registros de disponibilidade cadastrados no sistema. |
| **CA-05** | Dado que não existam mesas disponíveis para a data, horário e quantidade de pessoas selecionados, quando o cliente realizar a consulta. | O sistema deverá informar que não há disponibilidade e, quando possível, apresentar outros horários disponíveis. | Teste funcional utilizando períodos sem disponibilidade de mesas. |

---

## 7. Validação e rastreabilidade

| **Campo** | **Preenchimento** |
|:---|:---|
| **Situação** | [x] Pendente de validação<br>[ ] Validado<br>[ ] Necessita revisão |
| **Validado por / data** | Ainda não validado. A revisão por pares e a validação com o stakeholder estão pendentes. |
| **Observações e decisões** | Requisito classificado como Must have e incluído na primeira versão do sistema (ordem 1). Pendências levantadas na revisão: definir o intervalo de atualização da disponibilidade das mesas, estabelecer a duração padrão de cada reserva, determinar a capacidade das mesas e definir os critérios para apresentação dos horários disponíveis. |
| **Links relacionados** | Rastreabilidade: N01 → ST01 → REQ-001 (RF01), relacionado a RF02, RF03, RF04, RQ01, RQ03, RQ04 e RQ05. |

---

**Projeto:** ReservaFácil — Sistema de Reservas de Restaurante  
**Instituição:** UDF Centro Universitário  
**Disciplina:** Análise e Projeto de Sistemas
