# Especificação dos Casos de Uso — Sistema ReservaFácil

## Visão Geral do Diagrama

![Diagrama de Casos de Uso](diagrama-casos-de-uso-reservafacil.png)

---

## UC01 – Cadastrar Usuário (`RF01`, `RN01`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente |
| **Descrição** | Permite que um novo cliente crie sua conta na plataforma web ou aplicativo móvel informando dados pessoais e preferências. |
| **Pré-condição** | O visitante não possui cadastro ativo no sistema e está conectado à plataforma. |
| **Fluxo Principal** | 1. O cliente acessa a opção *Cadastrar-se*.<br>2. O sistema exibe o formulário de cadastro.<br>3. O cliente informa nome completo, e-mail, telefone, senha e preferências opcionais.<br>4. O sistema valida os campos obrigatórios (`RN01`), registra o usuário e exibe a confirmação de cadastro. |
| **Fluxo Alternativo** | **3a.** Campos obrigatórios ausentes ou e-mail já cadastrado: o sistema exibe mensagem orientativa indicando o erro e solicita correção antes de concluir. |
| **Pós-condições** | Conta de cliente criada e habilitada para autenticação e realização de reservas. |

---

## UC02 – Consultar Disponibilidade de Mesas (`RF08`, `RN01`, `RN05`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente |
| **Descrição** | Permite que o cliente verifique em tempo real quais mesas e horários estão livres para determinada data e quantidade de pessoas. |
| **Pré-condição** | O restaurante possui mesas previamente cadastradas e horários de funcionamento configurados. |
| **Fluxo Principal** | 1. O cliente informa a data desejada, o horário pretendido e a quantidade de pessoas.<br>2. O sistema verifica o horário de funcionamento do estabelecimento (`RN05`) e consulta as mesas com capacidade compatível e status livre.<br>3. O sistema exibe a lista de horários e mesas disponíveis em até 2 segundos (`RQ01`). |
| **Fluxo Alternativo** | **2a.** Horário fora do expediente do restaurante: o sistema informa o intervalo de funcionamento válido.<br>**2b.** Nenhuma mesa disponível para o horário escolhido: o sistema informa a indisponibilidade e sugere horários alternativos ou entrada na fila de espera. |
| **Pós-condições** | O cliente visualiza as opções de mesas disponíveis para prosseguir com o agendamento. |

---

## UC03 – Agendar e Confirmar Reserva (`RF03`, `RN03`, `RN08`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente |
| **Descrição** | Permite que o cliente autenticado selecione uma mesa disponível e efetive a reserva para a data e horário desejados. |
| **Pré-condição** | O cliente está autenticado no sistema e executou a consulta de disponibilidade (`<<include>>` `UC02`). |
| **Fluxo Principal** | 1. O cliente seleciona a mesa disponível dentre as opções exibidas.<br>2. O cliente revisa os dados (data, horário, quantidade de pessoas) e confirma a solicitação.<br>3. O sistema valida novamente se não há conflito de horário (`RN08`), bloqueia a mesa para o período e altera o status da reserva para *Confirmada*.<br>4. O sistema emite o comprovante e notifica o cliente. |
| **Fluxo Alternativo** | **3a.** Outra reserva concluiu o bloqueio da mesa instantes antes: o sistema impede o overbooking (`RN08`) e solicita a escolha de outra mesa disponível. |
| **Pós-condições** | Reserva registrada e confirmada no banco de dados com a respectiva mesa reservada. |

---

## UC04 – Solicitar Reserva Especial (`RF07`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente |
| **Descrição** | Estende o agendamento de reserva (`<<extend>>` `UC03`) para permitir que o cliente registre solicitações personalizadas, como aniversários, eventos ou cardápio específico. |
| **Pré-condição** | O cliente iniciou o fluxo de agendamento de reserva (`UC03`). |
| **Fluxo Principal** | 1. Durante o preenchimento da reserva, o cliente marca a opção *Reserva Especial*.<br>2. O sistema disponibiliza campos para seleção do tipo de evento (aniversário, reunião, outro) e observações adicionais.<br>3. O cliente descreve suas necessidades e prossegue com a confirmação da reserva. |
| **Fluxo Alternativo** | **2a.** O cliente desiste da personalização: desmarca a opção e retorna ao fluxo padrão de reserva. |
| **Pós-condições** | Os requisitos especiais ficam vinculados à reserva para visualização da equipe do restaurante. |

---

## UC05 – Entrar na Fila de Espera (`RF05`, `RN05`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente, Administrador/Funcionário |
| **Descrição** | Inclui o cliente em uma fila digital de espera quando 100% das mesas para o horário desejado estiverem ocupadas, notificando-o em caso de liberação. |
| **Pré-condição** | Todas as mesas compatíveis para a data e horário selecionados encontram-se ocupadas (`RN05`). |
| **Fluxo Principal** | 1. Diante da indisponibilidade de mesas, o cliente seleciona a opção *Entrar na Fila de Espera*.<br>2. O sistema registra a solicitação com data/hora de entrada, quantidade de pessoas e posição na fila.<br>3. Quando ocorre um cancelamento ou check-out antecipado, o sistema (ou funcionário) dispara uma notificação ao próximo cliente da fila. |
| **Fluxo Alternativo** | **3a.** O cliente notificado não confirma interesse dentro do prazo estipulado: o sistema avança a fila para o próximo interessado. |
| **Pós-condições** | Cliente posicionado na fila de espera e notificado automaticamente assim que surgir vaga. |

---

## UC06 – Cancelar Reserva (`RF04`, `RN04`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Cliente |
| **Descrição** | Permite que o cliente cancele uma reserva previamente confirmada, liberando a mesa novamente para outros clientes. |
| **Pré-condição** | O cliente está autenticado e possui uma reserva ativa com antecedência superior ao limite mínimo configurado (ex.: 1 hora, conforme `RN04`). |
| **Fluxo Principal** | 1. O cliente acessa a seção *Minhas Reservas* e seleciona a reserva ativa.<br>2. O cliente aciona a opção *Cancelar Reserva* e confirma a ação.<br>3. O sistema verifica o prazo mínimo de antecedência (`RN04`), altera o status da reserva para *Cancelada* e devolve a mesa imediatamente ao status *Disponível*. |
| **Fluxo Alternativo** | **3a.** Prazo inferior à antecedência mínima de 1 hora: o sistema bloqueia o cancelamento online e orienta o contato telefônico com o restaurante. |
| **Pós-condições** | Reserva cancelada e mesa liberada no calendário de disponibilidade. |

---

## UC07 – Cadastrar e Gerenciar Mesas (`RF02`, `RN02`, `RN07`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Administrador/Funcionário |
| **Descrição** | Permite à equipe administrativa cadastrar, editar ou inativar mesas do salão, definindo número identificador, capacidade e localização. |
| **Pré-condição** | O usuário está autenticado com perfil de Administrador ou Funcionário autorizado (`RN07`). |
| **Fluxo Principal** | 1. O administrador acessa o painel de gestão do salão.<br>2. Seleciona *Nova Mesa* (ou edita uma existente) e informa identificador único, capacidade máxima de lugares e setor/localização (`RN02`).<br>3. O sistema valida a unicidade do identificador e salva o registro da mesa. |
| **Fluxo Alternativo** | **3a.** Número de mesa duplicado ou capacidade inválida (`<= 0`): o sistema recusa o salvamento e exibe alerta de validação. |
| **Pós-condições** | Mesa disponível no inventário do restaurante para receber reservas. |

---

## UC08 – Registrar Check-in e Check-out (`RF06`, `RN06`)
| Campo | Descrição |
|---|---|
| **Ator(es)** | Administrador/Funcionário |
| **Descrição** | Registra a chegada presencial do cliente no restaurante (check-in) e sua saída ao término da refeição (check-out), atualizando o status da ocupação em tempo real. |
| **Pré-condição** | O funcionário está autenticado no painel operacional e localiza a reserva confirmada do cliente. |
| **Fluxo Principal** | 1. Na chegada do cliente, o funcionário localiza a reserva e aciona *Registrar Check-in*.<br>2. O sistema altera o status da reserva para *Em Atendimento* e da mesa para *Ocupada* (`RN06`).<br>3. Ao final do atendimento, o funcionário aciona *Registrar Check-out*.<br>4. O sistema encerra a reserva como *Concluída* e altera o status da mesa para *Liberada/Disponível*. |
| **Fluxo Alternativo** | **1a.** Cliente não comparece dentro da tolerância (*no-show*): o funcionário marca ausência e libera a mesa para a fila de espera. |
| **Pós-condições** | Controle presencial atualizado e mesa pronta para novo ciclo de ocupação. |
