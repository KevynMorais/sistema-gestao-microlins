# Script SQL e massa de dados

Esta pasta contém o [`script.sql`](script.sql) do Sistema de Gestão Microlins. O relatório técnico completo está no [README.md da raiz](../README.md).

## A massa de dados está dentro do script

O `script.sql` é um arquivo único, que recria o banco do zero. A massa de dados (dados fictícios) está na **seção 3**, nos comandos `INSERT INTO`, logo depois da criação das tabelas. Não há arquivo de massa separado.

| Seção do script | Conteúdo |
| :---- | :---- |
| 1 | `CREATE DATABASE` e `USE` (o banco `microlins` é recriado a cada execução) |
| 2 | `CREATE TABLE` das 16 tabelas, com chaves, `NOT NULL`, `UNIQUE`, `CHECK` e `DEFAULT` |
| 3 | `INSERT INTO`: **massa de dados fictícia** |
| 4 | `UPDATE` e `DELETE` (manutenção realista, com verificação antes e depois) |
| 5 | Consultas gerenciais **G01 a G14** |
| 6 | Consultas de auditoria **A01 a A17** |

## Como executar

1. Use o **MySQL 8.0.16 ou superior** (o `CHECK` só é aplicado a partir dessa versão).
2. Abra o `script.sql` no MySQL Workbench.
3. Execute o arquivo **inteiro**, com o botão do raio e **sem selecionar nenhum trecho** (a variável `@data_ref` precisa existir na mesma sessão).
4. Confira no *Action Output* que não há mensagem de erro.

Pela linha de comando: `mysql -u root -p < script.sql`.

## O que a massa contém

| Tabela | Linhas | Tabela | Linhas |
| :---- | :---- | :---- | :---- |
| HORARIO_FUNCIONAMENTO | 5 | MATRICULA | 182 |
| SALA | 4 | AULA | 264 |
| CURSO | 10 | FREQUENCIA | 3.394 |
| PROFESSOR | 8 | COBRANCA | 863 |
| FUNCIONARIO | 8 | PAGAMENTO | 279 |
| PROFESSOR_CURSO | 16 | CERTIFICADO | 22 |
| RESPONSAVEL | 11 | TURMA_HORARIO | 31 |
| ALUNO | 100 | TURMA | 16 |

- Todos os nomes, CPFs, telefones e e-mails são **fictícios**.
- O volume e a justificativa por tabela estão na seção 9.8 do README raiz.
- O script traz casos variados (inadimplentes, pagamentos parciais, aprovados e reprovados por falta, turmas lotadas) e **anomalias plantadas de propósito**, uma para cada consulta de auditoria, listadas no cabeçalho do script.

## Rastreabilidade

O cabeçalho do script liga cada problema (P1 a P6) e cada regra de negócio (RN) à consulta que a demonstra, com a mesma numeração do README raiz.
