# Levantamento — Microlins Itaquera

Este documento organiza o que o grupo levantou sobre a organização para construir o modelo de dados do **Sistema de Gestão Microlins**. O resumo está na seção 2 do [README.md](../README.md).

## 1. Fontes do levantamento

| Fonte | Quando | Como | Evidência |
| :---- | :---- | :---- | :---- |
| Entrevista com o coordenador geral José Jerônimo Júnior | 10/09/2026, às 13h30 | Presencial, na unidade (Rua Gregório Ramalho, 267) | [`entrevista com jose.jpeg`](entrevista%20com%20jose.jpeg) |
| Observação do local pelo integrante João Pedro | 10/09/2026 | Visita às salas, à recepção, ao rack e ao servidor, e acesso ao sistema de controle (HUB) | [`recepção.png`](recep%C3%A7%C3%A3o.png) |
| Confirmações com o coordenador | 04/11/2026, das 10h24 às 10h41 | Conversa de WhatsApp | [`conversa com coordenador1.png`](../evidencias/conversa%20com%20coordenador1.png) e [`conversa com coordenador2.png`](../evidencias/conversa%20com%20coordenador2.png) |

## 2. A organização

A Microlins é uma escola de cursos profissionalizantes. A unidade Itaquera é vinculada a uma **matriz**. A unidade Itaquera atende cerca de **477 alunos por mês** com **25 colaboradores** (8 professores, 3 secretárias, 2 diretores, 1 coordenador geral, 2 balconistas, 7 no financeiro e 2 na limpeza). O faturamento mensal informado vai de R$ 192.193,33 a R$ 287.526,67, conforme os contratos dos alunos.

A unidade controla o ciclo **acadêmico e de receita do aluno**. A matriz cuida das despesas e da folha de pagamento (ver seção 6).

## 3. Como a unidade funciona

### 3.1 Estrutura física e horários

- A unidade funciona das **08h às 18h**.
- São **4 salas**: 3 com 15 computadores (15 alunos por horário) e 1 com capacidade para 25 alunos, **sem computadores**, que só funciona às **terças e quintas** e recebe a turma extra, entre 10h e 16h.
- Cada turma ocupa um **bloco de 2 horas**.
- Um professor pode dar aula em **2 turmas ao mesmo tempo**.

### 3.2 Alunos e matrícula

- A idade mínima é **14 anos**.
- O **contrato é sempre assinado por um responsável**, mesmo quando o aluno é adulto.
- O aluno pode estar em **quantas turmas e cursos quiser**. Cada turma é uma matrícula.
- A troca de turma é **livre e gratuita**.
- Os dados do aluno são coletados só para o contrato e, depois, para contato com o responsável ou acionamento de emergência.
- O contrato tem **cláusulas de LGPD** (ver 3.6).
- Cada curso dura cerca de **2 anos**.

### 3.3 Cobrança e atraso

- Dia de vencimento, valor da mensalidade e número de parcelas dependem do contrato de cada matrícula.
- O material didático está **embutido na mensalidade**.
- **Atraso:** no primeiro dia de atraso a mensalidade recebe **20% de acréscimo**. A cada dia seguinte soma-se mais **20% do último acréscimo**. O coordenador exemplificou com uma mensalidade de R$ 290,00:

| Dia de atraso | Acréscimo do dia | Valor a pagar |
| :---- | :---- | :---- |
| 1º | 20% de 290,00 = 58,00 | 348,00 |
| 2º | 20% de 58,00 = 11,60 | 359,60 |
| 3º | 20% de 11,60 = 2,32 | 361,92 |
| 4º | 20% de 2,32 = 0,46 | 362,38 |

  Como cada acréscimo é 20% do anterior, o valor sobe todo dia, mas por valores cada vez menores, e a soma tende a **R$ 362,50 (125% da parcela)**. O grupo modelou o primeiro acréscimo em `pag_multa` e a soma dos acréscimos seguintes em `pag_juros`.
- Com **1 mês de atraso** o aluno é **bloqueado**.
- Segundo o coordenador, o acréscimo diário **não tem limite**: a cada dia que passa o valor aumenta.
- **Cancelamento:** multa de 20% sobre o valor restante do contrato, sem prazo de desistência após a assinatura.
- **Trancamento:** até 3 meses por ano.

### 3.4 Frequência, reposição e certificado

- O professor registra a presença de cada aluno em cada aula.
- Máximo de **3 faltas por módulo**; acima disso o aluno repete o módulo.
- **Falta justificada:** reposição gratuita, em qualquer dia e horário.
- **Falta não justificada:** a reposição custa R$ 40,00.
- A escola emite **certificado** ao final do curso.

### 3.5 Material didático (apostilas)

Em conversa de 04/11/2026, o coordenador explicou o fluxo: quando o aluno fecha o contrato, a **secretaria envia o contrato para a MovEDU**, empresa que fornece as apostilas, e o **professor pede a apostila** conforme o aluno avança nos módulos. A unidade não controla estoque nem compra de material.

### 3.6 Proteção de dados (LGPD)

O contrato da escola traz cláusulas de LGPD que, em resumo, tratam de três pontos:
- **Papéis:** a Microlins é a controladora dos dados e as responsabilidades ficam definidas.
- **Segurança:** exige medidas técnicas e administrativas de proteção, como criptografia e controle de acesso.
- **Consequências:** os dados pessoais do aluno são apagados imediatamente de todos os registros da Microlins quando o contrato termina, e a escola pode pagar multa indenizatória se não forem eliminados.

## 4. O que a observação no local mostrou

O integrante João Pedro viu todas as salas de aula, teve acesso aos computadores (com exceção da sala da diretora), ao endereço IP da rede, ao rack e ao servidor da unidade. O coordenador também permitiu o acesso ao sistema de controle que a organização usa, o **HUB**.

O que ficou registrado nas fotos do local:
- a recepção tem um balcão de atendimento ([`recepção.png`](recep%C3%A7%C3%A3o.png));
- há um quadro de acompanhamento de resultados (como retenção) na parede de uma sala administrativa ([`entrevista com jose.jpeg`](entrevista%20com%20jose.jpeg));
- o sistema atual (HUB) tem a tela de justificativa de faltas, mas ela não justifica as faltas (problema P4).

## 5. Problemas levantados

| ID | Problema | Origem |
| :---- | :---- | :---- |
| P1 | Alunos perdem o horário gravado no sistema | Entrevista |
| P2 | Perda frequente de matrículas | Entrevista |
| P3 | Sem histórico consolidado de pagamentos | Entrevista |
| P4 | O sistema não justifica faltas, mesmo tendo a tela | Entrevista e observação do HUB |
| P5 | Sobreposição e lotação de salas e horários | Entrevista |
| P6 | Endereços digitados de forma desorganizada | Entrevista |

## 6. Processos que ficaram fora do modelo

Em conversa de 04/11/2026, o coordenador confirmou que estes processos **não são responsabilidade da unidade**:

| Processo | O que foi dito | Decisão do grupo |
| :---- | :---- | :---- |
| Manutenção dos computadores | A diretora chama uma empresa contratada pela Microlins; o pagamento é feito pela matriz | Fora do modelo |
| Limpeza | É uma empresa contratada pela Microlins; o pagamento é feito pela matriz | Fora do modelo |
| Contas de água e luz | Pagas pela matriz | Fora do modelo |
| Folha de pagamento | Tratada pela matriz | Fora do modelo |
| Compra de apostilas | Feita pela MovEDU a partir do contrato enviado pela secretaria | Fora do modelo |

## 7. Regras informadas e como entraram no modelo

| Regra informada | Onde aparece no trabalho |
| :---- | :---- |
| Funcionamento das 08h às 18h; turma em bloco de 2h | `TURMA` e `HORARIO_FUNCIONAMENTO` (RN01, RN02) |
| Turma extra só ter/qui, entre 10h e 16h | RN03 |
| 4 salas; capacidade por sala e horário | `SALA` e RN04 |
| Professor em até 2 turmas ao mesmo tempo | RN06 |
| Idade mínima de 14 anos | RN08 |
| Contrato assinado por um responsável | `RESPONSAVEL` e RN09 |
| Atraso: 20% no primeiro dia e 20% do último acréscimo a cada dia | `PAGAMENTO` (`pag_multa`, `pag_juros`) e RN13 |
| Bloqueio após 1 mês de atraso | RN14 (operação da escola, apoiada pelas consultas G09 e G14) |
| Cancelamento com multa de 20% do valor restante | RN12 (operação da escola) |
| Trancamento de até 3 meses por ano | RN15 (operação da escola) |
| Falta justificada: reposição gratuita; não justificada: R$ 40,00 | `AULA` do tipo `REPOSICAO` e RN19/RN20 |
| Dados do aluno apagados quando o contrato termina | RN30 (operação da escola) |
| Máximo de 3 faltas por módulo | RN18 (no modelo, o critério é o percentual mínimo de frequência do curso) |

## 8. O que mudou em relação à Entrega 1

- A matrícula passou a ter **1 aluno e 1 turma**, com várias cobranças e vários pagamentos parciais. Antes, uma matrícula tinha vários alunos.
- Entraram no modelo **RESPONSAVEL, AULA, FREQUENCIA, PAGAMENTO e CERTIFICADO**, que a Entrega 1 não cobria.
- Saíram o nó DIRETORIA e as estimativas de volume feitas por IA (1.275 alunos e R$ 368.475,00), substituídas pelos números informados pelo coordenador.
- A restrição de horário do aluno foi descartada: o coordenador disse que o aluno pode estar em quantas turmas quiser.

## 9. Itens confirmados

- **LGPD:** o contrato tem as cláusulas descritas em 3.6.
- **Atraso:** o acréscimo diário não tem limite definido pela escola.
- **Sala extra:** a sala de 25 lugares não tem computadores.

Não há pendências de confirmação abertas.
