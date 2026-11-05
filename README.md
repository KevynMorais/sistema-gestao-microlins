# Microlins — Modelagem de Banco de Dados para Gestão Escolar

## Integrantes

| Nome | RGM | Links GitHub |
| :---- | :---- | :---- |
| João Pedro Paulino Cassimiro | 48109452 | https\://github.com/Joao-cyber037 |
| Pedro Enrico Damasceno | 48329487 | https\://github.com/PedroDamasceno1312 |
| Vinicius Paes Landim Dias | 48178501 | https\://github.com/viniciusdias10 |
| Thais Oliveira | 46578269 | https\://github.com/thaisvinicarvalho-coder |
| Kevyn Morais Barros | 48328936 | https\://github.com/KevynMorais |

## Índice

1. [Organização real](#1-organização-real)  
2. [Entrevista](#2-entrevista)  
3. [Números da organização](#3-números-da-organização)  
4. [Problemas identificados](#4-problemas-identificados)  
5. [Processos de negócio](#5-processos-de-negócio)  
6. [Requisitos e regras (RF, RNF, RN)](#6-requisitos-e-regras-rf-rnf-rn)  
7. [Ferramentas utilizadas](#7-ferramentas-utilizadas)  
8. [Modelo conceitual (DER)](#8-modelo-conceitual-der)  
9. [Seções técnicas 1.2 a 1.6](#9-seções-técnicas)  
10. [Tabela de apontamentos da Issue \#1](#10-apontamentos-da-issue-1)  
11. [Links dos arquivos](#11-links-dos-arquivos)  
12. [Uso de Inteligência Artificial](#12-uso-de-inteligência-artificial)

---

## 1\. Organização real

- **Nome:** Microlins (escola de cursos profissionalizantes)  
- **Endereço:** Rua Gregorio Ramalho, 267  
- **Google Meu Negócio:** https\://share.google/Vl8QkhGN6fTIHxk5N  
- **Responsável (nome):** Jose Jeronimo Junior 
- **Responsável (telefone):** +55 11 95934-0753
- **Fotos do local:** `/evidencias/organizacao/` e linkar aqui, por exemplo `![Fachada](evidencias/organizacao/fachada.jpg)`

## 2\. Entrevista

> Esta seção registra **o que foi dito** (entrevistado) separado **do que foi visto** (observação do grupo).

| Campo | Registro |
| :---- | :---- |
| Quem foi entrevistado | José Jerônimo Júnior, coordenador geral |
| Quando (data e horário) | 10/09/2026, às 13h30 |
| Onde | Microlins Itaquera, Rua Gregório Ramalho, 267 |
| Forma de contato |Primeira entrevista foi presencial, algumas duvidas foram perguntadas via Whastsapp |
| Foto da entrevista/visita | ⚠️ PREENCHER (`evidencias/entrevista/`) |


### 2.1 O que foi dito (relato do responsável)

Informações passadas pelo responsável

- Dia de vencimento, valor e número de parcelas dependem do contrato de cada matrícula e são definidos pelo responsável da escola.  
- Cancelamento: multa de 20% sobre o valor restante do contrato, sem prazo de desistência após a assinatura.  
- Trancamento: até 3 meses por ano.  
- Atraso: multa de 20% sobre a mensalidade, com novo acréscimo de 20% sobre o acréscimo; bloqueio do aluno após 1 mês.  
- Troca de turma: livre e gratuita.  
- Faltas: máximo de 3 por módulo, senão o aluno repete; falta não justificada custa R\$ 40,00 para repor; falta justificada tem reposição gratuita em qualquer dia e horário. A presença é registrada pelo professor.  
- A escola emite certificado.  
- Idade mínima de 14 anos; o contrato sempre é assinado pelo responsável; o aluno pode estar em quantas turmas e cursos quiser; o professor pode dar aula em 2 turmas ao mesmo tempo.  
- 4 salas: 3 com 15 computadores (15 alunos por horário) e 1 com capacidade para 25, que só funciona às terças e quintas (aula extra).  
- Cada curso dura em torno de 2 anos.  
- Dados dos alunos são coletados só para o contrato e, depois, para contato com o responsável ou acionamento de emergência.

### 2.2 O que foi observado (pelo grupo, no local)

O integrante João Pedro visitou a unidade, viu todas as salas de aula e teve acesso aos computadores (com exceção da sala da diretora), ao endereço IP da rede, ao rack e ao servidor da unidade. O coordenador José Jerônimo Júnior também permitiu o acesso ao sistema de controle que a organização usa (HUB).

## 3\. Números da organização

Fonte: **responsável da organização**

| Indicador | Valor informado | Observação |
| :---- | :---- | :---- |
| Salas | 4 (3 com 15 computadores; 1 com capacidade para 25, só ter/qui) | informado pelo responsável |
| Duração dos cursos | cerca de 2 anos | informado pelo responsável |
| Colaboradores | 25 no total | informado pelo responsável |
| Colaboradores por setor | 8 professores, 3 secretárias, 2 diretores, 1 coordenador geral, 2 balconistas, 7 no financeiro e 2 na limpeza | informado pelo responsável |
| Alunos | 477 por mês | informado pelo responsável |
| Faturamento mensal | de R$ 192.193,33 a R$ 287.526,67 (depende do contrato do aluno) | informado pelo responsável |

## 4\. Problemas identificados

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

## 5\. Processos de negócio

### 5.1 Processos modelados

| Processo | Fluxo | Dados envolvidos |
| :---- | :---- | :---- |
| Captação e atendimento | Interessado procura a escola (balcão/telefone) → atendimento pela secretaria → decide se matricula | SECRETARIA |
| Matrícula e contrato | Aluno com no mínimo 14 anos → contrato com dia de vencimento, valor e nº de parcelas definidos pelo responsável da escola → assinado pelo responsável legal do aluno → matrícula `ATIVA` | ALUNO, RESPONSÁVEL, MATRÍCULA |
| Alocação em turmas e grade | Matrícula é alocada em uma ou mais turmas, sem limite, em sala e horário. Salas comuns: 15 alunos; sala extra (ter/qui): 25 | TURMA, SALA, MATRÍCULA\_TURMA |
| Troca de turma | Aluno pede troca → turma atual é encerrada e a nova aberta, sem custo, mantendo histórico | MATRÍCULA\_TURMA |
| Geração de mensalidades | Conforme o contrato, uma cobrança por parcela com o vencimento definido | FINANCEIRO, MATRÍCULA |
| Recebimento, atraso e bloqueio | Pagamento registrado → baixa. Se atrasar: acréscimo de 20% e novo acréscimo conforme regra RN13 → com 1 mês de atraso a matrícula fica `BLOQUEADA` | FINANCEIRO, MATRÍCULA |
| Frequência | Professor registra presença por aula → falta pode receber justificativa | FREQUÊNCIA, PROFESSOR |
| Reposição de aulas | Falta justificada: reposição grátis em qualquer dia e horário. Falta não justificada: reposição custa R\$ 40,00 (gera cobrança). Mais de 3 faltas no módulo: aluno repete o módulo | REPOSIÇÃO, FREQUÊNCIA, FINANCEIRO |
| Trancamento | Matrícula é trancada por até 3 meses por ano de contrato. | TRANCAMENTO, MATRÍCULA |
| Cancelamento | Matrícula é cancelada a qualquer momento; multa de 20% do valor restante do contrato; cobranças futuras canceladas; histórico mantido | MATRÍCULA, FINANCEIRO |
| Conclusão e certificado |  Atingida a frequência mínima do curso, a matrícula passa a `CONCLUIDA` e o certificado é emitido com código de autenticação e percentual apurado | MATRICULA, FREQUENCIA, CURSO, CERTIFICADO |
| Atribuição de professores | Professor habilitado em curso é alocado em turmas; pode dar aula em até 2 turmas ao mesmo tempo | PROFESSOR, PROFESSOR\_CURSO, TURMA |

### 5.2 Processos fora do modelo e justificativa

| Processo | Por que ficou de fora |
| :---- | :---- |
| Compra de material didático/apostilas | O valor do material está embutido na mensalidade e as apostilas são fornecidas pela empresa MovEDU; a escola não controla estoque nem compra |
| Cobrança de reposição (R$ 40,00), multa de cancelamento (20%) e bloqueio por atraso | O responsável informou as regras, mas o dicionário v1.5 não tem entidade para elas. A reposição existe como `AULA` do tipo `REPOSICAO`; o valor da multa e o bloqueio são calculados pela secretaria a partir de `COBRANCA` e `PAGAMENTO` (consultas G09 e G14). Ficam como evolução do modelo |
| Contas a pagar e fornecedores (energia, água, internet, aluguel, MovEDU, manutenção de ar-condicionado e equipamentos) | Segundo o coordenador José Jerônimo Júnior, essas contas são de responsabilidade da matriz da Microlins, não da unidade Itaquera. A unidade não as controla, então não há dados nem processo a modelar no sistema da unidade |
| Manutenção de laboratórios e computadores | Mesma situação: a manutenção é tratada pela matriz, fora do controle da unidade. Não tem relação com matrícula, turma, frequência ou cobrança |
| Folha de pagamento e limpeza | Mesma situação: folha e contratação do pessoal de apoio são tratadas pela matriz. O modelo só guarda o professor e o funcionário que geram turmas e matrículas |

> Confirmação do coordenador José Jerônimo Júnior, Confirmado em 04/11/2026, por WhatsApp evidência em `evidencias/entrevista/`.
> Cobrança e reposição foram confirmadas presencialmente durante a entrevista

## 6\. Requisitos e regras (RF, RNF, RN)

### 6.1 Requisitos funcionais

| ID | Requisito | Implementação |
| :---- | :---- | :---- |
| RF01 | Cadastrar aluno (contato e endereço completo) e responsável | `ALUNO`, `RESPONSAVEL` |
| RF02 | Gerar matrícula do aluno em uma turma e vinculá-la a cobranças | `MATRICULA`, `COBRANCA.mat_id` |
| RF03 | Alocar turmas em sala, professor e dias respeitando a capacidade e os blocos de 2h | `TURMA`, `TURMA_HORARIO`, `SALA`, consulta `A03` |
| RF04 | Registrar frequência (pelo professor) e justificar faltas | `FREQUENCIA` |
| RF05 | Cancelar, trancar e concluir matrícula sem apagar histórico | `MATRICULA.mat_status`, `mat_data_encerramento`, `mat_motivo_encerramento` |
| RF06 | Programar reposição de aulas | `AULA.aul_tipo = 'REPOSICAO'` |
| RF07 | Trocar o aluno de turma mantendo histórico | encerramento da matrícula anterior e nova `MATRICULA` |
| RF08 | Registrar pagamentos totais ou parciais com multa e juros | `PAGAMENTO` |
| RF09 | Emitir certificado ao atingir a frequência mínima | `CERTIFICADO`, `CURSO.cur_frequencia_minima` |

### 6.2 Requisitos não funcionais

| ID | Requisito | Implementação |
| :---- | :---- | :---- |
| RNF01 | Integridade: chaves estrangeiras com `ON DELETE RESTRICT`, histórico preservado | `FOREIGN KEY` em todas as tabelas |
| RNF02 | Consistência de domínio: status, tipos e horários com valores válidos | `CHECK ... IN (...)` para os domínios, `NOT NULL` e `DEFAULT` |
| RNF03 | Acentuação correta | `utf8mb4` com collation `utf8mb4_0900_ai_ci` |
| RNF04 | LGPD: finalidade restrita, consentimento e minimização | ver 6.4 |
| RNF03 | LGPD: finalidade restrita e minimização | ver 6.4 |

### 6.3 Regras de negócio

Valores e prazos foram informados pelo responsável da organização (ver 2.1). A coluna **Garantia** diz onde a regra é aplicada: no `CREATE TABLE`, em uma consulta de auditoria (`A##` do `script.sql`) ou na operação da escola.

| ID | Regra | Por que importa | Garantia |
| :---- | :---- | :---- | :---- |
| RN01 | Operação entre 08:00 e 18:00 | A escola só funciona nesse intervalo | `CHECK` em `TURMA` e `A10` |
| RN02 | Turma ocupa bloco de 2 horas | Padrão da grade | `CHECK ck_turma_bloco_2h` em `TURMA` |
| RN03 | Turma extra só ocorre às terças e quintas, entre 10:00 e 16:00 | A sala extra só abre nesses dias | `A14` |
| RN04 | Existem 4 salas: 3 com 15 lugares e 1 com 25 (só ter/qui). A capacidade vale por sala em cada dia e horário, somando todas as turmas ali | Cada aluno precisa de um computador | `A03` e `G03` |
| RN05 | Turma só existe com professor habilitado no curso | Impede aula sem docente qualificado | `PROFESSOR_CURSO` e `A02` |
| RN06 | Professor pode dar aula em até 2 turmas ao mesmo tempo | Prática da escola | `A12` |
| RN07 | Aluno pode estar em quantas turmas e cursos quiser (uma matrícula por turma) | Flexibilidade informada pelo responsável | `MATRICULA` (N matrículas por aluno) |
| RN08 | Idade mínima de 14 anos na data da matrícula | Política da escola | `A13` |
| RN09 | O contrato é assinado por um responsável | O responsável é o contato e o signatário | `A01` |
| RN10 | Valor da mensalidade, número de parcelas e frequência mínima são definidos pelo curso | Simplificação do modelo (o responsável disse que variam por contrato; ver 9.5) | `CURSO` |
| RN11 | Cancelamento, trancamento e conclusão mudam o status com data e motivo, sem apagar histórico | Preserva o histórico | `MATRICULA.mat_status` |
| RN12 | Cancelamento: multa de 20% do valor restante do contrato, sem prazo de desistência | Política da escola | Operação da secretaria (fora do modelo; ver 5.2) |
| RN13 | Atraso: multa de 20% da parcela (`pag_multa`) e novo acréscimo de 20% sobre essa multa (`pag_juros`) | Define o valor devido | `PAGAMENTO` e `G13` |
| RN14 | Com 1 mês de atraso o aluno é bloqueado | Política de inadimplência | Operação, apoiada por `G09` e `G14` |
| RN15 | Trancamento de até 3 meses por ano | Política da escola | Operação da secretaria (informativa) |
| RN16 | Falta justificada conta como presença no cálculo da frequência | Direito do aluno | `G04`, `G12` e inserção em lote (4.3 do script) |
| RN17 | Cobrança aberta após o vencimento passa a `VENCIDA` | Controle de inadimplência | `UPDATE` 4.1 do script |
| RN18 | Máximo de 3 faltas por módulo; no modelo, o critério é o percentual mínimo de frequência do curso | Regra acadêmica (o módulo não é entidade) | `CURSO.cur_frequencia_minima` e `G04` |
| RN19 | Falta não justificada: reposição custa R$ 40,00 | Receita e controle de faltas | Operação da escola (fora do modelo; ver 5.2) |
| RN20 | Falta justificada: reposição gratuita em qualquer dia e horário | Direito do aluno | `AULA.aul_tipo = 'REPOSICAO'` |
| RN21 | Quem registra a presença é o professor da turma | Responsabilidade clara | `TURMA.pro_id` |
| RN22 | Dados pessoais só com finalidade restrita e consentimento registrado | LGPD | `A04` |
| RN23 | Certificado exige a frequência mínima do curso | Validade da conclusão | `A05`, `A06` e `A07` |
| RN24 | Cobrança `PAGA` tem o principal quitado, sem pagamento a maior | Integridade financeira | `A11` |
| RN25 | A frequência pertence à matrícula da mesma turma da aula | Consistência acadêmica | `A08` |
| RN26 | Aula regular ocorre somente nos dias da turma | Grade respeitada | `A09` |
| RN27 | Só se oferta turma com curso ativo e professor ativo | Catálogo vigente | `A15` |
| RN28 | Turma encerrada ou cancelada não mantém matrícula ativa | Evita matrícula "fantasma" | `A16` |
| RN29 | Matrícula ativa gera cobranças | Sem receita esquecida | `A17` |

**Pontos de atenção (para o grupo discutir, não para esconder):**

- **RN13:** o Código de Defesa do Consumidor (art. 52, §1º) limita a multa por atraso a 2%, e decisões judiciais aplicam esse limite a mensalidades escolares. A escola informou 20%. O trabalho registra a regra **como a escola pratica**, mas deixa claro que ela pode ser contestada. Esta não é opinião jurídica.
- **RN12:** a multa de 20% sobre o saldo restante e a ausência de prazo de desistência também podem ser questionadas em contratos de consumo. Mesmo tratamento: registrar a prática.

### 6.4 LGPD

| Medida | Aplicação |
| :---- | :---- |
| Finalidade | Dados do aluno são usados só para o contrato, contato com o responsável e acionamento de emergência (informado pela escola) |
| Minimização | Coletar apenas CPF, nome, nascimento, telefone, e-mail (opcional) e endereço do aluno; CPF, nome, telefone e parentesco do responsável |
| Menores de idade | Alunos a partir de 14 anos; o responsável assina o contrato e é o contato (`RESPONSAVEL`, ligado por `ALUNO.res_id`) |
| Consentimento | `alu_consentimento_lgpd` e `alu_data_consentimento`, verificados pela consulta `A04` ⚠️ CONFIRMAR se o contrato atual tem cláusula de dados |
| Acesso restrito | Papéis por entidade e operação definidos no dicionário de dados (seção 6): atendimento, professor, financeiro, coordenação e auditoria |
| Rastreabilidade | Log de acesso do SGBD e versionamento do dicionário (art. 6º, X) |

### 6.5 Código das regras

```sql
-- RN01 e RN02
ALTER TABLE turma
  ADD CONSTRAINT ck_turma_expediente CHECK (horario_inicio >= '08:00:00' AND horario_fim <= '18:00:00'),
  ADD CONSTRAINT ck_turma_bloco2h   CHECK (TIMEDIFF(horario_fim, horario_inicio) = '02:00:00');

DELIMITER //

-- RN03: turma extra só ter/qui entre 10h e 16h
CREATE TRIGGER trg_turma_horario BEFORE INSERT ON turma FOR EACH ROW
BEGIN
  IF NEW.tipo = 'EXTRA' AND (NEW.dia_semana NOT IN ('TERCA','QUINTA')
      OR NEW.horario_inicio < '10:00:00' OR NEW.horario_fim > '16:00:00') THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Turma extra: apenas ter/qui entre 10h e 16h';
  END IF;
END//

-- RN05: professor habilitado no curso do módulo
CREATE TRIGGER trg_turma_professor BEFORE INSERT ON turma FOR EACH ROW
BEGIN
  IF NOT EXISTS (
    SELECT 1 FROM modulo mo JOIN professor_curso pc ON pc.id_curso = mo.id_curso
    WHERE mo.id_modulo = NEW.id_modulo AND pc.id_professor = NEW.id_professor) THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Professor não habilitado neste curso';
  END IF;
END//

-- RN06: professor em no máximo 2 turmas simultâneas
CREATE TRIGGER trg_turma_prof_simultaneas BEFORE INSERT ON turma FOR EACH ROW
BEGIN
  IF (SELECT COUNT(*) FROM turma
      WHERE id_professor = NEW.id_professor AND dia_semana = NEW.dia_semana
        AND horario_inicio < NEW.horario_fim AND NEW.horario_inicio < horario_fim) >= 2 THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Professor já está em 2 turmas neste horário';
  END IF;
END//

-- RN04: capacidade da sala por dia/horário (soma de todas as turmas da sala)
CREATE TRIGGER trg_mt_capacidade BEFORE INSERT ON matricula_turma FOR EACH ROW
BEGIN
  DECLARE v_sala INT; DECLARE v_dia VARCHAR(10); DECLARE v_ini TIME;
  DECLARE ocupadas INT; DECLARE cap INT;
  SELECT id_sala, dia_semana, horario_inicio INTO v_sala, v_dia, v_ini
    FROM turma WHERE id_turma = NEW.id_turma;
  SELECT capacidade INTO cap FROM sala WHERE id_sala = v_sala;
  SELECT COUNT(*) INTO ocupadas FROM matricula_turma mt JOIN turma t ON t.id_turma = mt.id_turma
    WHERE t.id_sala = v_sala AND t.dia_semana = v_dia AND t.horario_inicio = v_ini
      AND mt.data_fim IS NULL;
  IF ocupadas >= cap THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Sala lotada neste horário';
  END IF;
END//

-- RN08: idade mínima de 14 anos
CREATE TRIGGER trg_matricula_idade BEFORE INSERT ON matricula FOR EACH ROW
BEGIN
  IF TIMESTAMPDIFF(YEAR, (SELECT data_nascimento FROM aluno WHERE id_aluno = NEW.id_aluno),
                   NEW.data_registro) < 14 THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Idade mínima de 14 anos';
  END IF;
END//

-- RN11: não cobrar matrícula cancelada (exceto a multa de cancelamento)
CREATE TRIGGER trg_financeiro_matricula BEFORE INSERT ON financeiro FOR EACH ROW
BEGIN
  IF NEW.tipo <> 'MULTA_CANCELAMENTO'
     AND (SELECT status FROM matricula WHERE id_matricula = NEW.id_matricula) = 'CANCELADA' THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Matrícula cancelada';
  END IF;
END//

-- RN12: histórico financeiro imutável
CREATE TRIGGER trg_financeiro_no_delete BEFORE DELETE ON financeiro FOR EACH ROW
BEGIN
  SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cobranças não podem ser apagadas; use status CANCELADA';
END//

CREATE TRIGGER trg_financeiro_no_update_pago BEFORE UPDATE ON financeiro FOR EACH ROW
BEGIN
  IF OLD.status_pagamento = 'PAGO' AND (NEW.valor <> OLD.valor OR NEW.status_pagamento <> 'PAGO') THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cobrança paga é imutável';
  END IF;
END//

-- RN13 (1ª etapa): acréscimo de 20% da mensalidade. ⚠️ 2ª etapa pendente de confirmação
CREATE FUNCTION fn_encargos_atraso(p_valor DECIMAL(10,2)) RETURNS DECIMAL(10,2) DETERMINISTIC
BEGIN
  RETURN ROUND(p_valor * 0.20, 2);   -- ⚠️ trocar 0.20 por parâmetro da tabela `parametro`
END//

-- RN14: bloqueio após 1 mês de atraso (agendar para rodar diariamente)
CREATE PROCEDURE sp_bloquear_inadimplentes()
BEGIN
  UPDATE matricula m SET m.status = 'BLOQUEADA'
  WHERE m.status = 'ATIVA' AND EXISTS (
    SELECT 1 FROM financeiro f
    WHERE f.id_matricula = m.id_matricula
      AND f.status_pagamento IN ('PENDENTE','ATRASADO')
      AND f.data_vencimento < DATE_SUB(CURDATE(), INTERVAL 1 MONTH));
END//

-- RN15: multa de cancelamento = 20% do valor restante do contrato
CREATE FUNCTION fn_multa_cancelamento(p_id INT) RETURNS DECIMAL(10,2) READS SQL DATA
BEGIN
  DECLARE total DECIMAL(10,2); DECLARE pago DECIMAL(10,2);
  SELECT valor_parcela * qtd_parcelas INTO total FROM matricula WHERE id_matricula = p_id;
  SELECT COALESCE(SUM(valor), 0) INTO pago FROM financeiro
    WHERE id_matricula = p_id AND tipo = 'MENSALIDADE' AND status_pagamento = 'PAGO';
  RETURN ROUND(0.20 * (total - pago), 2);   -- ex.: 8000 - 1200 = 6800 → 1360,00
END//

CREATE TRIGGER trg_matricula_cancelamento AFTER UPDATE ON matricula FOR EACH ROW
BEGIN
  IF NEW.status = 'CANCELADA' AND OLD.status <> 'CANCELADA' THEN
    UPDATE financeiro SET status_pagamento = 'CANCELADA'
      WHERE id_matricula = NEW.id_matricula AND tipo = 'MENSALIDADE'
        AND status_pagamento = 'PENDENTE' AND data_vencimento > CURDATE();
    INSERT INTO financeiro (id_matricula, tipo, valor, status_pagamento, data_vencimento)
      VALUES (NEW.id_matricula, 'MULTA_CANCELAMENTO',
              fn_multa_cancelamento(NEW.id_matricula), 'PENDENTE', CURDATE());
  END IF;
END//

-- RN16: trancamento de até 3 meses por ano civil
CREATE TRIGGER trg_trancamento_limite BEFORE INSERT ON trancamento FOR EACH ROW
BEGIN
  IF (SELECT COALESCE(SUM(TIMESTAMPDIFF(MONTH, data_inicio, data_fim)), 0) FROM trancamento
      WHERE id_matricula = NEW.id_matricula AND YEAR(data_inicio) = YEAR(NEW.data_inicio))
     + TIMESTAMPDIFF(MONTH, NEW.data_inicio, NEW.data_fim) > 3 THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Limite de 3 meses de trancamento por ano';
  END IF;
END//

DELIMITER ;
```

## 7. Ferramentas utilizadas    

- **DER e modelo lógico:** brModelo (arquivo `modelo/microlins.brM3`)
- **Banco de dados:** MySQL 8.0.16
- **Dicionário de dados:** arquivo HTML único (`docs/dicionario-dados-microlins.html`)
- **Versionamento:** Git / GitHub

## 8\. Modelo conceitual (DER)

sistema-gestao-microlins/DER_microlins.png

## 9\. Seções técnicas

### 9.1 (1.1) Visão conceitual

Entidades: ALUNO, RESPONSÁVEL, SECRETARIA, PROFESSOR, CURSO, MÓDULO, TURMA, SALA, HORÁRIO\_FUNCIONAMENTO, MATRÍCULA, MATRÍCULA\_TURMA, FINANCEIRO, FREQUÊNCIA, REPOSIÇÃO, TRANCAMENTO. A MATRÍCULA é a entidade central: nada financeiro ou acadêmico existe sem ela.

### 9.2 (1.2) Conversão do modelo conceitual para o lógico

| Conceitual | Lógico | Regra aplicada |
| :---- | :---- | :---- |
| Entidade | Tabela | 1 entidade \= 1 tabela |
| Relacionamento 1:N | FK no lado N | `matricula.id_aluno`, `financeiro.id_matricula` |
| Relacionamento N:N | Tabela associativa | `professor_curso`, `matricula_turma` |
| Atributo de endereço | Colunas atômicas | cep, logradouro, numero, bairro |

### 9.3 (1.3) Chaves primárias e estrangeiras

| Tabela | PK | FKs |
| :---- | :---- | :---- |
| aluno | id\_aluno | — |
| responsavel | id\_responsavel | — |
| secretaria | id\_secretaria | — |
| professor | id\_professor | — |
| curso | id\_curso | — |
| modulo | id\_modulo | id\_curso |
| professor\_curso | (id\_professor, id\_curso) | id\_professor, id\_curso |
| sala | id\_sala | — |
| horario\_funcionamento | id\_horario | — |
| turma | id\_turma | id\_modulo, id\_professor, id\_sala, id\_horario |
| matricula | id\_matricula | id\_aluno, id\_curso, id\_responsavel, id\_secretaria |
| matricula\_turma | (id\_matricula, id\_turma, data\_inicio) | id\_matricula, id\_turma |
| trancamento | id\_trancamento | id\_matricula |
| financeiro | id\_cobranca | id\_matricula |
| frequencia | id\_frequencia | id\_matricula, id\_turma, id\_professor |
| reposicao | id\_reposicao | id\_frequencia, id\_sala, id\_cobranca |

```sql
CREATE TABLE aluno (
  id_aluno INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(120) NOT NULL,
  data_nascimento DATE NOT NULL,
  telefone VARCHAR(20) NOT NULL,
  cep VARCHAR(9) NOT NULL, logradouro VARCHAR(150) NOT NULL,
  numero VARCHAR(10) NOT NULL, bairro VARCHAR(100) NOT NULL,
  consentimento_lgpd BOOLEAN NOT NULL DEFAULT FALSE,
  data_consentimento DATE
);
CREATE TABLE responsavel (
  id_responsavel INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(120) NOT NULL,
  telefone VARCHAR(20) NOT NULL,
  documento VARCHAR(20) NOT NULL
);
CREATE TABLE sala (
  id_sala INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(20) NOT NULL UNIQUE,
  capacidade INT NOT NULL CHECK (capacidade IN (15, 25))
);
CREATE TABLE modulo (
  id_modulo INT PRIMARY KEY AUTO_INCREMENT,
  id_curso INT NOT NULL,
  nome VARCHAR(100) NOT NULL,
  ordem INT NOT NULL,
  FOREIGN KEY (id_curso) REFERENCES curso(id_curso)
);
CREATE TABLE turma (
  id_turma INT PRIMARY KEY AUTO_INCREMENT,
  id_modulo INT NOT NULL, id_professor INT NOT NULL,
  id_sala INT NOT NULL, id_horario INT NOT NULL,
  tipo ENUM('REGULAR','EXTRA') NOT NULL,
  dia_semana ENUM('SEGUNDA','TERCA','QUARTA','QUINTA','SEXTA') NOT NULL,
  horario_inicio TIME NOT NULL, horario_fim TIME NOT NULL,
  FOREIGN KEY (id_modulo) REFERENCES modulo(id_modulo),
  FOREIGN KEY (id_professor) REFERENCES professor(id_professor),
  FOREIGN KEY (id_sala) REFERENCES sala(id_sala),
  FOREIGN KEY (id_horario) REFERENCES horario_funcionamento(id_horario)
);
CREATE TABLE matricula (
  id_matricula INT PRIMARY KEY AUTO_INCREMENT,
  id_aluno INT NOT NULL, id_curso INT NOT NULL,
  id_responsavel INT NOT NULL, id_secretaria INT NOT NULL,
  data_registro DATE NOT NULL,
  dia_vencimento TINYINT NOT NULL CHECK (dia_vencimento BETWEEN 1 AND 31),
  valor_parcela DECIMAL(10,2) NOT NULL CHECK (valor_parcela > 0),
  qtd_parcelas INT NOT NULL CHECK (qtd_parcelas > 0),
  status ENUM('ATIVA','TRANCADA','BLOQUEADA','CANCELADA') NOT NULL DEFAULT 'ATIVA',
  FOREIGN KEY (id_aluno) REFERENCES aluno(id_aluno),
  FOREIGN KEY (id_curso) REFERENCES curso(id_curso),
  FOREIGN KEY (id_responsavel) REFERENCES responsavel(id_responsavel),
  FOREIGN KEY (id_secretaria) REFERENCES secretaria(id_secretaria)
);
CREATE TABLE matricula_turma (
  id_matricula INT NOT NULL, id_turma INT NOT NULL,
  data_inicio DATE NOT NULL, data_fim DATE,
  PRIMARY KEY (id_matricula, id_turma, data_inicio),
  FOREIGN KEY (id_matricula) REFERENCES matricula(id_matricula),
  FOREIGN KEY (id_turma) REFERENCES turma(id_turma)
);
CREATE TABLE trancamento (
  id_trancamento INT PRIMARY KEY AUTO_INCREMENT,
  id_matricula INT NOT NULL,
  data_inicio DATE NOT NULL, data_fim DATE NOT NULL,
  FOREIGN KEY (id_matricula) REFERENCES matricula(id_matricula)
);
CREATE TABLE financeiro (
  id_cobranca INT PRIMARY KEY AUTO_INCREMENT,
  id_matricula INT NOT NULL,
  tipo ENUM('MENSALIDADE','REPOSICAO','MULTA_CANCELAMENTO') NOT NULL,
  valor DECIMAL(10,2) NOT NULL CHECK (valor > 0),
  valor_encargos DECIMAL(10,2) NOT NULL DEFAULT 0,
  status_pagamento ENUM('PENDENTE','PAGO','ATRASADO','CANCELADA') NOT NULL,
  data_vencimento DATE NOT NULL, data_pagamento DATE,
  FOREIGN KEY (id_matricula) REFERENCES matricula(id_matricula)
);
CREATE TABLE frequencia (
  id_frequencia INT PRIMARY KEY AUTO_INCREMENT,
  id_matricula INT NOT NULL, id_turma INT NOT NULL, id_professor INT NOT NULL,
  data_aula DATE NOT NULL, presente BOOLEAN NOT NULL,
  justificativa VARCHAR(255), data_justificativa DATE,
  FOREIGN KEY (id_matricula) REFERENCES matricula(id_matricula),
  FOREIGN KEY (id_turma) REFERENCES turma(id_turma),
  FOREIGN KEY (id_professor) REFERENCES professor(id_professor),
  UNIQUE (id_matricula, id_turma, data_aula),
  CHECK (justificativa IS NULL OR (presente = 0 AND data_justificativa IS NOT NULL))
);
CREATE TABLE reposicao (
  id_reposicao INT PRIMARY KEY AUTO_INCREMENT,
  id_frequencia INT NOT NULL, id_sala INT NOT NULL,
  data_hora DATETIME NOT NULL,
  id_cobranca INT,   -- NULL quando a falta foi justificada (reposição gratuita)
  FOREIGN KEY (id_frequencia) REFERENCES frequencia(id_frequencia),
  FOREIGN KEY (id_sala) REFERENCES sala(id_sala),
  FOREIGN KEY (id_cobranca) REFERENCES financeiro(id_cobranca)
);
-- demais tabelas (curso, professor, professor_curso, secretaria, horario_funcionamento): ver script.sql
```

### 9.4 (1.4) Normalização

| Forma normal | Verificação |
| :---- | :---- |
| 1FN | Todos os atributos atômicos; endereço decomposto em 4 colunas |
| 2FN | Sem dependência parcial: tabelas de PK composta (`professor_curso`, `matricula_turma`) só têm atributos que dependem da chave inteira |
| 3FN | Capacidade vive em `sala`; curso é derivado de `modulo`; valor total do contrato é calculado (`valor_parcela × qtd_parcelas`) em vez de armazenado |

 `horario_funcionamento` só guarda a janela diária da escola; horário real da turma fica em `turma`.

### 9.5 (1.5) Justificativas técnicas e alternativas

| Decisão | Alternativa descartada | Por que |
| :---- | :---- | :---- |
| MATRÍCULA como entidade central | Ligar ALUNO direto a TURMA e FINANCEIRO | Perderia histórico quando o aluno trocasse de turma e não haveria onde ancorar o contrato |
| 1 matrícula \= 1 aluno | Cardinalidade da Entrega 1 (matrícula com vários alunos) | O contrato é do aluno e assinado pelo responsável |
| 1 matrícula → N cobranças | 1 cobrança por matrícula | Mensalidades, reposições e multa são recorrentes; é o que forma o histórico |
| MATRÍCULA\_TURMA (N:N com datas) | `id_turma` direto em MATRÍCULA | O aluno pode estar em várias turmas e trocar livremente; o histórico evita "perder horário" |
| Condições do contrato em MATRÍCULA | Tabela CONTRATO separada | Cada matrícula tem um contrato e o responsável define vencimento, valor e parcelas; tabela separada seria 1:1 sem ganho. Se o grupo quiser aditivos, vira CONTRATO |
| MÓDULO como entidade | Tratar o curso como bloco único | A regra de 3 faltas é por módulo e o curso dura cerca de 2 anos |
| Capacidade em SALA e contada por horário | Capacidade fixa em TURMA | Um computador por aluno; o limite é físico, da sala |
| Cancelar e trancar por status | `DELETE` | Histórico imutável |
| Reposição como entidade com cobrança opcional | Atributo de FREQUÊNCIA | Reposição tem data, sala e custo próprios |
| Regras em triggers no SGBD | Validar só na aplicação | O sistema atual falha justamente por validação frágil; regra no banco é à prova da interface |

### 9.6 (1.6) BI e IA, com rastreabilidade

| Pergunta de negócio | Indicador | Origem (tabelas) | Problema ligado |
| :---- | :---- | :---- | :---- |
| Quanto da receita está em atraso? | Inadimplência % | financeiro | P3 |
| Quais salas/horários estão lotados ou vazios? | Taxa de ocupação | matricula\_turma, turma, sala | P1, P5 |
| Quais cursos têm mais cancelamentos? | Evasão por curso | matricula, curso | P2 |
| Quem excede 3 faltas no módulo? | Faltas por aluno/módulo | frequencia, turma | P4 |
| Quanto a escola arrecada com reposições e multas? | Receita por tipo | financeiro | P3 |
| Quem tem risco de evasão? (IA) | Score a partir de faltas e atrasos | frequencia, financeiro | P2, P3, P4 |

O Grupo não vai de fato implementar algum dashboard/modelo e apenas uma proposta.

## 10\. Apontamentos da Issue \#1

Um item para cada um dos 12 critérios da avaliação da Issue \#1. "FEITO" \= já está neste README. "PENDENTE" \= depende de ação do grupo fora deste arquivo.

| \# | Critério (apontamento da Issue) | O que mudou | Por quê |
| :---- | :---- | :---- | :---- |
| 1 | README: arquivo `readme.md` em minúsculas contaria como ausente | PENDENTE: renomear para `README.md` na raiz da `main`. Em Windows/macOS o Git ignora troca de caixa, então use `git mv readme.md tmp.md && git mv tmp.md README.md` | A rubrica exige o nome exato |
| 2 | Integrantes: 5 com nome e RGM | FEITO: tabela com RGM e coluna de usuário GitHub. PENDENTE: preencher usuários e cada integrante fazer commits reais do que produziu | Todos os commits atuais são de um só integrante, o que deixa a participação dos outros sem evidência |
| 3 | Organização real (3.1) e contato/entrevista (3.2): placeholder `[Inserir aqui...]`, sem fotos, sem relato (fator ×0,5) | FEITO: placeholder removido; seção 2.1 registra o relato do responsável. PENDENTE: link do Meu Negócio, nome do responsável, fotos, data da entrevista e observações do local | Sem evidência de entrevista a nota cai pela metade |
| 4 | Caracterização: evidências não preenchidas | FEITO: seção 3 com salas e duração dos cursos informadas pelo responsável. PENDENTE: nº de alunos, colaboradores e faturamento | Números do Gemini não valem como evidência de campo |
| 5 | Processos: 4 de uma linha, sem fluxo, cobertura de 21% | FEITO: 12 processos com fluxo e dados; frequência trata de frequência. PENDENTE: confirmar compras, contas a pagar e manutenção (5.2) | Faltavam inadimplência, frequência, cancelamento, trancamento, certificado |
| 6 | Requisitos e regras (conceitual): RF de justificativa sem processo; regra de capacidade misturada | FEITO: justificativa ligada aos processos de frequência e reposição; capacidade (RN04) separada de localização | Cada requisito precisa de um processo que o origine |
| 7 | Requisitos (documentação): poucos, mas corretos | FEITO: 7 RFs e 3 RNFs, cada um com a implementação | O critério já estava aceito; o ganho é rastreabilidade |
| 8 | Regras de negócio: cobertura de 35%, sem explicar por quê | FEITO: RN01 a RN22 com coluna "Por que importa" e código; valores reais informados pelo responsável. PENDENTE: confirmar RN07, RN13, RN16, RN18 | Cobrem financeiro, cancelamento, frequência, menor de idade e LGPD |
| 9 | Dicionário de dados: faltam fluxo de dados, SGBD, collation, notação formal, prefixos, data da versão, expressão formal e leitura por entidade, coluna Obrigatório, índices, log de acesso, acesso por operação e LGPD | PENDENTE: o dicionário fica só no HTML. Falta gerar a v1.3 com esses itens, as novas entidades e atributos prefixados (`nome` → `alu_nome`) | É o critério com mais itens faltando e nada disso se resolve no README |
| 10 | DER: `.jpeg` é XML do draw.io, SVG fora do formato, cardinalidades inviáveis, sem FREQUÊNCIA, ternário INCLUI(3) redundante | PENDENTE: exportar PNG/JPG de verdade; 1 matrícula \= 1 aluno; 1 matrícula \= N cobranças; incluir RESPONSÁVEL, MÓDULO, FREQUÊNCIA, REPOSIÇÃO, TRANCAMENTO, SALA, MATRÍCULA\_TURMA e `professor_curso`; remover o ternário | Com a cardinalidade atual o sistema não guarda mensalidades, o problema que o grupo diz resolver |
| 11 | Justificativa técnica: descreve sem discutir alternativas | FEITO: tabela com decisão, alternativa descartada e motivo (9.5) | A rubrica pede alternativas |
| 12 | Uso de IA: prompts truncados, fontes genéricas, "rejeitados" vazio no Claude | PARCIAL: tabela com uma linha por uso e item rejeitado. PENDENTE: colar os prompts reais completos e dizer fontes verificadas de verdade | Prompt com "..." e "validação humana interna" não demonstram verificação |

## 11\. Links dos arquivos

| Arquivo | Link |
| :---- | :---- |
| DER (imagem) | 'sistema-gestao-microlins/DER_microlins.png' |
| Arquivo do brModelo | ⚠️ `sistema-gestao-microli0ns/Modelo_logico_microlins.png` |
| Script SQL | [`script.sql`](http://script.sql) |
| Dicionário de dados | ⚠️ link para o arquivo separado (o dicionário saiu do README) |
| Evidências (fotos, entrevista) | ⚠️ `evidencias/` |

## 12\. Uso de Inteligência Artificial

> Uma linha por uso. Se o prompt abaixo estiver resumido, substituir pelo texto real.

| Ferramenta | Etapa | Prompt real | Resultado | Rejeitado/corrigido e por quê |
| :---- | :---- | :---- | :---- | :---- |
| Gemini | Código XML do DER (Draw.io) | "aja como um modelador de banco de dados, voce precisa fazer um diagrama..." | XML importável | Nó DIRETORIA removido: a operação é centrada em secretaria e financeiro |
| Gemini | Volumetria | "faça as contas para os alunos..." | 1.275 alunos e R\$ 368.475,00 de faturamento | **Números rejeitados:** eram estimativa da IA, substituídos pelos dados reais do responsável (seção 3\) |
| Gemini | Revisão do README | "esse é o esqueleto do readme.md... analise e me diga oque precisa" | Sugestões de estrutura e justificativa técnica | Aproveitado após validação do grupo |
| Claude (Kevyn) | Revisão do dicionário de dados em HTML (v1.0 → v1.1) | Pedido de análise profunda do HTML e remoção de menções redundantes ao DER | Acentuação, relacionamentos nas descrições, alerta sobre cardinalidade de INCLUI | Marcadores `[cite: 9]` vieram da ferramenta e foram removidos do README |
| Claude (esta conversa) | Reescrita do README conforme a Issue \#1 e adaptação do modelo às respostas do responsável | "esse e o atual readme.md do meu projeto do github quero que faça a analise e o atualize com os seguintes instruções nas imagens", seguido das respostas do responsável sobre as regras | README reescrito, regras em SQL, novo modelo lógico, consulta web sobre o limite de multa de mora do CDC | Regra RN10 antiga ("aluno e professor sem sobreposição de horário") foi descartada porque o responsável disse o contrário. ⚠️ PREENCHER o que o grupo rejeitou ou alterou depois de ler |

**Reflexão crítica:** a IA gera estrutura e código rápido, mas inventa números, assume regras teóricas e erra o negócio (como a restrição de horário, que a escola não tem). Tudo que vem de campo precisa vir do responsável, e o código gerado precisa ser executado antes de ser entregue.
