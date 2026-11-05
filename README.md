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

## 3. Números da organização

Fonte: **responsável da organização**.

| Indicador | Valor informado | Observação |
| :---- | :---- | :---- |
| Salas | 4 (3 com 15 computadores; 1 com capacidade para 25 e sem computadores, só ter/qui) | informado pelo responsável |
| Duração dos cursos | cerca de 2 anos | informado pelo responsável |
| Colaboradores | 25 no total | informado pelo responsável |
| Colaboradores por setor | 8 professores, 3 secretárias, 2 diretores, 1 coordenador geral, 2 balconistas, 7 no financeiro e 2 na limpeza | informado pelo responsável |
| Alunos | 477 por mês | informado pelo responsável |
| Faturamento mensal | de R$ 192.193,33 a R$ 287.526,67 (depende do contrato do aluno) | informado pelo responsável |

## 4. Problemas identificados

Cada problema aponta as entidades do DER que o resolvem e as consultas do [`script.sql`](docs/script.sql) que o demonstram. As consultas **G01 a G14** são gerenciais e as **A01 a A17** são de auditoria.

| ID | Problema | Entidades no DER | Consultas no script |
| :---- | :---- | :---- | :---- |
| P1 | Alunos perdem o horário gravado no sistema | MATRICULA, TURMA, TURMA_HORARIO | `A08` e `A16` (matrícula presa a uma turma com horário; matrícula ativa em turma encerrada) |
| P2 | Perda frequente de matrículas | MATRICULA, ALUNO, FUNCIONARIO | `G07` (evasão por curso) e `G10` (matrículas por funcionário) |
| P3 | Sem histórico consolidado de pagamentos | COBRANCA, PAGAMENTO, MATRICULA | `G01`, `G02`, `G05`, `G08`, `G09`, `G13` e `G14` |
| P4 | Sistema não justifica faltas, mesmo tendo a tela | FREQUENCIA, AULA | `G04`, `G06` e `G12` (`fre_situacao = FALTA_JUSTIFICADA`, `fre_justificativa` e `fre_data_justificativa`) |
| P5 | Sobreposição e lotação de salas e horários | TURMA, SALA, TURMA_HORARIO | `G03`, `G11`, `A03` e `A12` |
| P6 | Endereços digitados de forma desorganizada | ALUNO | Prevenido por `NOT NULL` em `alu_cep`, `alu_logradouro`, `alu_numero` e `alu_bairro` (o banco não aceita endereço incompleto) |

Exemplo (P3, consulta G14 do script — maiores devedores e contato para cobrança):

```sql
-- G14 Quem são os 10 maiores devedores e qual o contato para cobrança (responsável, se menor)?
-- Atende: P3 (sem histórico consolidado de pagamentos: maiores devedores)
WITH devedores AS (
    SELECT m.alu_id,
           COUNT(*) AS cobrancas_em_atraso,
           SUM(cb.cob_valor - IFNULL(p.principal_pago, 0)) AS saldo_devedor,
           MIN(cb.cob_data_vencimento) AS vencimento_mais_antigo
    FROM COBRANCA cb
    JOIN MATRICULA m ON m.mat_id = cb.mat_id
    LEFT JOIN (SELECT cob_id, SUM(pag_valor_pago - pag_multa - pag_juros) AS principal_pago
               FROM PAGAMENTO GROUP BY cob_id) p ON p.cob_id = cb.cob_id
    WHERE cb.cob_status IN ('ABERTA','VENCIDA')
      AND cb.cob_data_vencimento < @data_ref
    GROUP BY m.alu_id
)
SELECT a.alu_nome AS aluno,
       IFNULL(r.res_nome, a.alu_nome) AS contato_para_cobranca,
       IFNULL(r.res_telefone, a.alu_telefone) AS telefone_para_cobranca,
       d.cobrancas_em_atraso,
       d.saldo_devedor,
       d.vencimento_mais_antigo
FROM devedores d
JOIN ALUNO a ON a.alu_id = d.alu_id
LEFT JOIN RESPONSAVEL r ON r.res_id = a.res_id
ORDER BY d.saldo_devedor DESC, a.alu_nome
LIMIT 10;
```

## 5. Processos de negócio

### 5.1 Processos modelados

| Processo | Fluxo | Entidades envolvidas |
| :---- | :---- | :---- |
| Preparação da oferta | Coordenação cadastra cursos, salas, horários de funcionamento e professores (com habilitação) → abre a turma, com sala, professor e dias | CURSO, SALA, HORARIO_FUNCIONAMENTO, PROFESSOR, PROFESSOR_CURSO, TURMA, TURMA_HORARIO |
| Cadastro do aluno | Interessado procura a escola (balcão/telefone) → atendimento cadastra o aluno com endereço completo e consentimento LGPD → se menor, vincula o responsável | ALUNO, RESPONSAVEL |
| Material didático | Ao fechar o contrato, a secretaria envia o contrato do aluno à MovEDU → o professor pede a apostila conforme o aluno avança nos módulos (o valor está embutido na mensalidade) | MATRICULA, TURMA (a MovEDU não é entidade do modelo) |
| Matrícula e contrato | Aluno com no mínimo 14 anos → funcionário gera a matrícula em uma turma aberta, respeitando a capacidade da sala → contrato assinado pelo responsável → matrícula `ATIVA` | MATRICULA, FUNCIONARIO, TURMA, ALUNO |
| Geração de cobranças | A matrícula gera a taxa e as parcelas de mensalidade conforme o curso (valor e número de parcelas) | COBRANCA, CURSO |
| Recebimento, atraso e baixa | Cada pagamento baixa uma cobrança (parcial ou total) → em atraso, incidem multa de 20% e juros de 20% sobre a multa → a cobrança vencida fica `VENCIDA` | PAGAMENTO, COBRANCA |
| Aulas e frequência | A turma programa as aulas (regulares ou de reposição) → o professor registra presença ou falta de cada matrícula → a falta pode receber justificativa | AULA, FREQUENCIA |
| Troca de turma | Aluno pede troca → a matrícula atual é encerrada com data e motivo e uma nova é gerada na outra turma, sem custo, mantendo o histórico | MATRICULA |
| Cancelamento e trancamento | A matrícula muda de status (`CANCELADA` ou `TRANCADA`) com data e motivo de encerramento; nada é apagado | MATRICULA, COBRANCA |
| Conclusão e certificado | Atingida a frequência mínima do curso, a matrícula passa a `CONCLUIDA` e o certificado é emitido com código de autenticação e percentual apurado | MATRICULA, FREQUENCIA, CURSO, CERTIFICADO |
| Atribuição de professores | Professor habilitado no curso é alocado às turmas; pode lecionar até 2 turmas ao mesmo tempo | PROFESSOR, PROFESSOR_CURSO, TURMA |

### 5.2 Processos fora do modelo e justificativa

| Processo | Por que ficou de fora |
| :---- | :---- |
| Compra e entrega de apostilas | O valor do material está embutido na mensalidade. A secretaria envia o contrato à MovEDU, que fornece as apostilas; a unidade não controla estoque nem compra |
| Cobrança de reposição (R$ 40,00), multa de cancelamento (20%) e bloqueio por atraso | O responsável informou as regras, mas o dicionário v1.5 não tem entidade para elas. A reposição existe como `AULA` do tipo `REPOSICAO`; o valor da multa e o bloqueio são calculados pela secretaria a partir de `COBRANCA` e `PAGAMENTO` (consultas G09 e G14). Ficam como evolução do modelo |
| Contas a pagar e fornecedores (energia, água, internet, aluguel) | Segundo o coordenador José Jerônimo Júnior, em conversa de 04/11/2026, as contas de água e luz e os demais pagamentos são feitos pela matriz da Microlins, não pela unidade Itaquera |
| Manutenção de laboratórios e computadores | A diretora chama uma empresa contratada pela Microlins e o pagamento é feito pela matriz (conversa de 04/11/2026) |
| Limpeza | É feita por empresa contratada pela Microlins e paga pela matriz (conversa de 04/11/2026) |
| Folha de pagamento | Tratada pela matriz. O modelo só guarda o professor e o funcionário que geram turmas e matrículas |

> Evidência das confirmações: [`evidencias/conversa com coordenador1.png`](evidencias/conversa%20com%20coordenador1.png) e [`evidencias/conversa com coordenador2.png`](evidencias/conversa%20com%20coordenador2.png), de 04/11/2026.
