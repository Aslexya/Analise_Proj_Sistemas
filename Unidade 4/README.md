# Unidade IV — Diagramas UML de Atividades e de Objetos

**Disciplina:** Análise e Projeto de Sistemas (APS)  
**Professora:** Kadidja Valéria Reginaldo de Oliveira  
**Instituição:** UDF — Centro Universitário do Distrito Federal  
**Projeto:** ReservaFácil — Sistema de Reserva de Mesas Online para Restaurantes  
**Integrantes:** Renan Akira Rodrigues de Souza, Fernando Rebouças e Paulo Henrique Santos Azevedo  

---

## 1. Objetivo dos Diagramas

Documentar o comportamento dinâmico do processo de solicitação de reservas (**Diagrama de Atividades**) e representar uma fotografia estática de instâncias reais em execução (**Diagrama de Objetos**), garantindo coerência entre os requisitos levantados e o Diagrama de Classes do sistema **ReservaFácil**.

## 2. Ferramentas Utilizadas

- **PlantUML** (arquivos-fonte editáveis `.puml`)
- **Exportação gráfica de alta resolução** (`.png`)

## 3. Artefatos Versionados

| Artefato | Arquivo Editável (Fonte) | Exportação Visual |
|---|---|---|
| Diagrama de Atividades | [`atividades/diagrama-atividades-reserva.puml`](atividades/diagrama-atividades-reserva.puml) | [`atividades/diagrama-atividades-reserva.png`](atividades/diagrama-atividades-reserva.png) |
| Diagrama de Objetos | [`objetos/diagrama-objetos-reserva.puml`](objetos/diagrama-objetos-reserva.puml) | [`objetos/diagrama-objetos-reserva.png`](objetos/diagrama-objetos-reserva.png) |

---

## 4. Cenários e Rastreabilidade aos Requisitos

### 4.1 Diagrama de Atividades — Solicitação de Reserva de Mesa
- **Cenário representado:** O cliente informa data, horário e quantidade de pessoas; o sistema valida o expediente e verifica a disponibilidade de mesas. Caso haja disponibilidade (`[Sim]`), o cliente seleciona a mesa, informa observações especiais opcionais e confirma a reserva, fazendo com que o sistema bloqueie a mesa e emita o comprovante. Caso todas as mesas estejam ocupadas (`[Não]`), o sistema insere o cliente na fila de espera digital e o notifica quando ocorrer liberação.
- **Responsáveis (Raias):** `Cliente` e `Sistema ReservaFácil`.
- **Requisitos e Regras Relacionados:** `RF03` (Agendar e Confirmar Reserva), `RF05` (Gerenciar Fila de Espera), `RF07` (Solicitar Reserva Especial), `RF08` (Consultar Disponibilidade), `RN03`, `RN05` e `RN08`.

### 4.2 Diagrama de Objetos — Reserva de Aniversário Confirmada
- **Cenário representado:** O cliente *Lucas Mendes* (`cliente1 : Cliente`) possui uma reserva confirmada (`reserva205 : Reserva`) para 4 pessoas no dia `14/11/2026` às `20:00` com solicitação especial de aniversário, alocando a mesa `M-08` (`mesa08 : Mesa`) gerenciada pela gerente de salão *Mariana Costa* (`admin1 : FuncionarioAdmin`).
- **Coerência com o Diagrama de Classes:** Os links `cliente1 — reserva205` (`realiza`), `reserva205 — mesa08` (`aloca`) e `admin1 — mesa08` (`gerencia`) respeitam diretamente as associações e multiplicidades definidas no modelo de classes.
- **Requisitos e Regras Relacionados:** `RF02`, `RF03`, `RF07`, `RNF05`, `RN02`, `RN03` e `RN08`.
