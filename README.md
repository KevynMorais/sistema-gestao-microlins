# Sistema de Gestão Microlins — Modelagem de Banco de Dados (Entrega 2)

## Integrantes

| Nome | RGM | GitHub |
| :---- | :---- | :---- |
| João Pedro Paulino Cassimiro | 48109452 | https://github.com/Joao-cyber037 |
| Pedro Enrico Damasceno | 48329487 | https://github.com/PedroDamasceno1312 |
| Vinicius Paes Landim Dias | 48178501 | https://github.com/viniciusdias10 |
| Thais Oliveira | 46578269 | https://github.com/thaisvinicarvalho-coder |
| Kevyn Morais Barros | 48328936 | https://github.com/KevynMorais |

## Índice

1. [Organização real](#1-organização-real)
2. [Entrevista](#2-entrevista)
3. [Números da organização](#3-números-da-organização)
4. [Problemas identificados](#4-problemas-identificados)
5. [Processos de negócio](#5-processos-de-negócio)
6. [Requisitos e regras (RF, RNF, RN)](#6-requisitos-e-regras-rf-rnf-rn)
7. [Ferramentas utilizadas](#7-ferramentas-utilizadas)
8. [Modelo conceitual (DER) e modelo lógico](#8-modelo-conceitual-der-e-modelo-lógico)
9. [Seções técnicas](#9-seções-técnicas)
10. [Apontamentos da Issue #1](#10-apontamentos-da-issue-1)
11. [Links dos arquivos](#11-links-dos-arquivos)
12. [Uso de Inteligência Artificial](#12-uso-de-inteligência-artificial)

---

## 1. Organização real

- **Nome:** Microlins (escola de cursos profissionalizantes), unidade Itaquera
- **Endereço:** Rua Gregório Ramalho, 267 — Itaquera, São Paulo/SP
- **Google Meu Negócio:** https://share.google/Vl8QkhGN6fTIHxk5N
- **Responsável (nome):** José Jerônimo Júnior (coordenador geral)
- **Responsável (telefone):** +55 11 95934-0753
- **Fotos do local:** ![Recepção da unidade](levantamento/recep%C3%A7%C3%A3o.png)
- **Justificativa da escolha:** unidade real, com acesso garantido ao coordenador, a todas as salas e ao sistema de controle (HUB), e com processos acadêmicos, financeiros e de frequência que cobrem o ciclo completo do aluno. O vinculo com a unidade é apenas de aluno.

## 2. Entrevista

> Esta seção registra **o que foi dito** (entrevistado) separado do **que foi visto** (observação do grupo).

| Campo | Registro |
| :---- | :---- |
| Quem foi entrevistado | José Jerônimo Júnior, coordenador geral |
| Quando (data e horário) | 10/09/2026, às 13h30 |
| Onde | Microlins Itaquera, Rua Gregório Ramalho, 267 |
| Integrante que participou | João Pedro Paulino Cassimiro |
| Forma de contato | Entrevista presencial no local e confirmações posteriores por WhatsApp, em 04/11/2026 (prints: [conversa 1](evidencias/conversa%20com%20coordenador1.png) e [conversa 2](evidencias/conversa%20com%20coordenador2.png)) |
| Foto da entrevista/visita | ![Entrevista no local](levantamento/entrevista%20com%20jose.jpeg) |

### 2.1 O que foi dito (relato do responsável)

- Dia de vencimento, valor e número de parcelas dependem do contrato de cada matrícula e são definidos pelo responsável da escola.
- Cancelamento: multa de 20% sobre o valor restante do contrato, sem prazo de desistência após a assinatura.
- Trancamento: até 3 meses por ano.
- Atraso: no primeiro dia de atraso a mensalidade recebe acréscimo de 20% (parcela de R$ 290,00 passa a R$ 348,00); a cada dia seguinte soma-se mais 20% do último acréscimo (2º dia: 20% de R$ 58,00 = R$ 11,60, total R$ 359,60). Bloqueio do aluno após 1 mês de atraso.
- Troca de turma: livre e gratuita.
- Faltas: máximo de 3 por módulo, senão o aluno repete; falta não justificada custa R$ 40,00 para repor; falta justificada tem reposição gratuita em qualquer dia e horário. A presença é registrada pelo professor.
- A escola emite certificado.
- Idade mínima de 14 anos; o contrato sempre é assinado pelo responsável; o aluno pode estar em quantas turmas e cursos quiser; o professor pode dar aula em 2 turmas ao mesmo tempo.
- Funcionamento das 08h às 18h, com turmas em blocos de 2 horas. A turma extra só ocorre às terças e quintas, entre 10h e 16h.
- 4 salas: 3 com 15 computadores (15 alunos por horário) e 1 com capacidade para 25 alunos, sem computadores, que só funciona às terças e quintas (aula extra).
- Cada curso dura em torno de 2 anos. O material didático está embutido na mensalidade: a secretaria envia o contrato do aluno à MovEDU, que fornece as apostilas, e o professor pede a apostila conforme o aluno avança nos módulos (confirmado por WhatsApp em 04/11/2026).
- Dados dos alunos são coletados só para o contrato e, depois, para contato com o responsável ou acionamento de emergência.

### 2.2 O que foi observado (pelo grupo, no local)

O integrante João Pedro visitou a unidade, viu todas as salas de aula e teve acesso aos computadores (com exceção da sala da diretora), ao endereço IP da rede, ao rack e ao servidor da unidade. O coordenador José Jerônimo Júnior também permitiu o acesso ao sistema de controle que a organização usa (HUB).

### 2.3 Levantamento

O levantamento completo, organizado por tema (estrutura da unidade, matrícula, cobrança e atraso, frequência, material, processos fora do modelo e regras), está em [`levantamento/levantamento.md`](levantamento/levantamento.md). Resumo:

- **Fontes:** entrevista presencial de 10/09/2026, observação do local e confirmações por WhatsApp em 04/11/2026.
- **Achado principal:** a unidade controla o ciclo acadêmico e a receita do aluno; contas, manutenção, limpeza e folha de pagamento são da matriz.
- **Regras levantadas:** horário das 08h às 18h, 4 salas, idade mínima de 14 anos, contrato assinado por responsável, atraso com acréscimo diário, cancelamento com multa de 20%, trancamento de até 3 meses por ano e reposição de faltas.
- **O que mudou em relação à Entrega 1:** matrícula de 1 aluno por turma e novas entidades (responsável, aula, frequência, pagamento e certificado).
