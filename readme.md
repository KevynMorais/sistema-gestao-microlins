# Entrega 1 — Modelo Conceitual (DER)
### Modelagem de um sistema de gestão de informações para uma organização de pequeno porte

## Metadados

- **Nomes dos alunos e RGM:**
  - João Pedro Paulino Cassimiro (4810945-2)
  - Pedro Enrico Damasceno (48329487)
  - Vinicius Paes Landim (48178501)
  - Thais Oliveira (46578269)
  - Kevyn Morais Barros (48328936)

## 1. Caracterização da Organização

- **Nome e natureza da organização:** Microlins, uma escola de cursos profissionalizantes com fins lucrativos.
- **Contexto e porte:** A organização possui médio porte. O quadro de funcionários conta com 26 colaboradores: 4 na secretaria, 2 na coordenação, 10 no departamento financeiro, 7 professores (3 no período da manhã, 3 no período da tarde e 1 exclusivo para terças e quintas), 2 profissionais de limpeza e 1 balconista. A instituição comporta 1.275 alunos semanais, gerando um faturamento mensal estimado de R$ 368.475,00.
- **Problemas e necessidades identificados:** A escola sofre de grave desorganização administrativa física e virtual. O sistema atual é obsoleto e instável (apresenta falhas onde alunos perdem seus horários gravados). Há perda frequente de matrículas, ausência de histórico de pagamentos consolidado e incapacidade do sistema atual de justificar faltas operacionais, mesmo possuindo a funcionalidade em tela.
- **Justificativa da escolha:** Trata-se de uma escola de médio porte ideal para modelagem de dados operacionais estruturados. A quantidade delimitada de setores e o alto impacto das falhas atuais no faturamento e na experiência do aluno tornam a transição para um banco de dados relacional uma solução técnica urgente e de alto valor.
- **Evidências da organização:** Endereço físico: Rua Gregorio Ramalho, 267. [Inserir aqui link do Google Maps/Instagram e telefone de contato do local].

---

## 2. Processos de Negócio

- **Principais processos mapeados:**
  - **Atendimento e Matrícula:** A secretaria capta o aluno, registra seus dados e gera uma matrícula que formaliza o ingresso.
  - **Organização de Grade de Aulas:** Alocação dos alunos matriculados nas turmas regulares (15 alunos, de segunda a sexta) e extras (25 alunos, terças e quintas), vinculando-os aos horários e salas exatas.
  - **Controle Financeiro:** Geração e monitoramento de cobranças de mensalidades vinculadas diretamente à matrícula do aluno, registrando o histórico para evitar perdas documentais.
  - **Gestão de Frequência e Atribuição:** A coordenação supervisiona a relação de professores vinculados a cursos específicos que, por sua vez, são ofertados através das turmas geradas.

---

## 3. Requisitos do Sistema

### 3.1 Requisitos Funcionais
- O sistema deve permitir o cadastro de dados pessoais e de contato (endereço completo) do aluno.
- O sistema deve registrar e vincular matrículas individuais a cobranças geradas no módulo financeiro.
- O sistema deve gerenciar e alocar turmas respeitando capacidades máximas e os turnos exatos de abertura (blocos de 2 horas).
- O sistema deve processar justificativas de faltas integradas à ficha do aluno.

### 3.2 Requisitos Não Funcionais
- **Integridade:** Os dados financeiros devem ser armazenados de forma imutável (sem perdas de histórico).
- **Confiabilidade:** O banco de dados deve barrar a sobreposição de horários e a desassociação não intencional de alunos (correção dos "bugs" de grade).

---

## 4. Regras de Negócio

- **Regras operacionais:**
  - Uma turma só ocorre se estiver atrelada a um professor cadastrado lecionando aquele curso específico.
  - Um aluno não pode realizar aulas fora das dependências e computadores designados (limite rígido de 15 alunos por sala comum e 25 alunos na sala de terças/quintas).
  - O faturamento e o acesso à escola dependem de uma matrícula "Ativa" gerada pela secretaria.
- **Restrições organizacionais:**
  - A operação está rigorosamente contida no intervalo das 08:00 às 18:00.
  - Módulos de grade sofrem transição inquebrável a cada 2 horas. Turmas extras de terça e quinta estão restritas entre as 10:00 e as 16:00.

---

## 5. Dicionário de Dados Conceitual (Preliminar)

Abaixo estão os atributos mapeados para as entidades do sistema acadêmico da Microlins, baseados no Modelo Conceitual. **Nota:** As tabelas não incluem chaves estrangeiras (FK), pois, por se tratar de um dicionário derivado do modelo conceitual, os vínculos são documentados nos relacionamentos[cite: 9].

| Entidade | Atributo | Tipo Físico | Descrição / Regra de Negócio |
|----------|----------|-------------|------------------------------|
| **ALUNO**<br>*(Pessoa física atendida pela secretaria e vinculada a uma matrícula[cite: 9])* | `id_aluno` | INT | Identificador único do aluno (PK)[cite: 9]. |
| | `nome` | VARCHAR(120) | Nome completo do aluno[cite: 9]. |
| | `telefone` | VARCHAR(20) | Telefone de contato do aluno ou responsável[cite: 9]. |
| | `cep` | VARCHAR(9) | CEP do endereço do aluno[cite: 9]. |
| | `logradouro` | VARCHAR(150) | Rua ou avenida do endereço do aluno[cite: 9]. |
| | `numero` | VARCHAR(10) | Número do endereço do aluno[cite: 9]. |
| | `bairro` | VARCHAR(100) | Bairro do endereço do aluno[cite: 9]. |
| **SECRETARIA**<br>*(Registro de atendimento da secretaria, responsável por atender alunos, supervisionar professores e gerar matrículas[cite: 9])* | `id_secretaria` | INT | Identificador único do registro da secretaria (PK)[cite: 9]. |
| | `nome_atendente`| VARCHAR(120) | Nome do atendente responsável[cite: 9]. |
| | `turno` | VARCHAR(20) | Turno de trabalho do atendente (manhã, tarde ou noite)[cite: 9]. |
| **PROFESSOR**<br>*(Docente supervisionado pela secretaria e responsável por lecionar cursos[cite: 9])* | `id_professor` | INT | Identificador único do professor (PK)[cite: 9]. |
| | `nome` | VARCHAR(120) | Nome completo do professor[cite: 9]. |
| | `especialidade` | VARCHAR(100) | Área de especialização do professor[cite: 9]. |
| **CURSO**<br>*(Curso lecionado por um professor, organizado em turmas e associado a matrículas[cite: 9])* | `id_curso` | INT | Identificador único do curso (PK)[cite: 9]. |
| | `nome_curso` | VARCHAR(120) | Nome do curso[cite: 9]. |
| | `carga_horaria` | INT (horas) | Carga horária total do curso[cite: 9]. |
| **TURMA**<br>*(Turma de um curso, restrita a um horário de funcionamento e associada a matrículas[cite: 9])* | `id_turma` | INT | Identificador único da turma (PK)[cite: 9]. |
| | `sala` | VARCHAR(20) | Identificação da sala onde a turma ocorre[cite: 9]. |
| | `horario_inicio`| TIME | Horário de início das aulas da turma[cite: 9]. |
| | `horario_fim` | TIME | Horário de término das aulas da turma[cite: 9]. |
| **HORÁRIO_FUNCIONAMENTO**<br>*(Faixa de funcionamento por dia da semana, que restringe os horários das turmas[cite: 9])* | `id_horario` | INT | Identificador único do registro de horário (PK)[cite: 9]. |
| | `dia_semana` | VARCHAR(15) | Dia da semana ao qual o horário se refere[cite: 9]. |
| | `hora_abertura` | TIME | Horário de abertura da escola naquele dia[cite: 9]. |
| | `hora_fechamento`| TIME | Horário de fechamento da escola naquele dia[cite: 9]. |
| **FINANCEIRO**<br>*(Cobrança associada a uma ou mais matrículas[cite: 9])* | `id_cobranca` | INT | Identificador único da cobrança (PK)[cite: 9]. |
| | `valor` | DECIMAL(10,2) | Valor da cobrança[cite: 9]. |
| | `status_pagamento`| VARCHAR(20) | Situação do pagamento (ex.: pago, pendente, atrasado)[cite: 9]. |
| | `data_vencimento` | DATE | Data de vencimento da cobrança[cite: 9]. |
| **MATRÍCULA**<br>*(Registro gerado pela secretaria, vinculado a alunos, cobrança, curso e turma[cite: 9])* | `id_matricula` | INT | Identificador único da matrícula (PK)[cite: 9]. |
| | `data_registro` | DATE | Data em que a matrícula foi registrada[cite: 9]. |

---

## 6. Modelagem Conceitual (Entidades, Atributos, Relacionamentos)

- **Entidades reconhecidas:** O modelo integra entidades descritivas (ALUNO, PROFESSOR, CURSO), entidades transacionais (MATRÍCULA, FINANCEIRO) e entidades organizacionais (SECRETARIA, TURMA, HORÁRIO_FUNCIONAMENTO) para eliminar a perda de histórico.
- **Atributos e classificações:** Os atributos foram refinados. O endereço do aluno, antes agrupado de forma abstrata, foi decomposto em cep, logradouro, número e bairro para facilitar o controle e evitar registros sujos.
- **Relacionamentos pertinentes:** 
  - A SECRETARIA atende (1,1 para 0,N) o ALUNO e supervisiona (1,1 para 1,N) o PROFESSOR.
  - A SECRETARIA gera (1,1 para 0,N) a MATRÍCULA.
  - O PROFESSOR leciona (1,1 para 0,N) o CURSO que contém (1,1 para 1,N) a TURMA. A TURMA tem sua atividade submetida/restringida (1,N para 1,1) ao HORÁRIO_FUNCIONAMENTO.
  - **Atenção às cardinalidades INCLUI (1 e 2):** A modelagem atual indica que uma MATRÍCULA pode estar vinculada a mais de um ALUNO e que um registro FINANCEIRO pode estar vinculado a mais de uma MATRÍCULA[cite: 9]. (Padrão a ser reavaliado pelo grupo nas próximas entregas, pois foge do usual em sistemas escolares[cite: 9]).
- **Restrições e políticas organizacionais aplicadas ao modelo:** O vínculo financeiro tornou-se obrigatoriamente dependente da existência prévia de uma matrícula para impossibilitar pendências órfãs. A quebra estrutural evita que o aluno "perca seu horário" no sistema.

---

## 7. Diagrama Entidade-Relacionamento (DER)

*(O arquivo de imagem contendo o DER está anexado na raiz deste repositório).*

---

## 8. Justificativa Técnica

A decisão de arquitetura tomada utilizou a entidade `MATRÍCULA` como ponte (entidade associativa implícita) conectando o cliente (`ALUNO`), o controle monetário (`FINANCEIRO`) e a infraestrutura acadêmica (`TURMA`). Isso resolve diretamente o problema principal de "histórico de pagamentos perdido" e "alunos perdendo horário": nenhum vínculo financeiro ou de classe pode existir sem estar atrelado rigidamente a um registro formal rastreável de matrícula. 

Além disso, a abstração desmembrada do endereço do `ALUNO` (cep, logradouro, número, bairro) previne a digitação desorganizada que ocorria nos sistemas legados. A cardinalidade `(1,1)` conectando `TURMA` a `HORÁRIO_FUNCIONAMENTO` força o sistema a obedecer às políticas rigorosas de turnos (operações em blocos de 2 horas e limite diário entre 8h e 18h), blindando o software contra lançamentos fora do expediente.

---

## 9. Uso de Inteligência Artificial

| Item | O que registrar |
|------|------------------|
| **Ferramenta e etapa** | Google Gemini: Auxílio na geração do código base do diagrama DER no formato XML (Draw.io), cálculos de volumetria e suporte técnico estrutural em partes pontuais e mais complexas do README. |
| **Motivação** | Garantir uma diagramação padronizada livre de erros de renderização e estruturar ideias técnicas complexas de negócio com maior clareza. |
| **Prompt(s) utilizados** | "aja como um modelador de banco de dados, voce precisa fazer um diagrama...", "faça as contas para os alunos...", "esse é o esqueleto do readme.md... analise e me diga oque precisa". |
| **Resposta recebida** | Forneceu o código de infraestrutura XML importável, realizou a decomposição matemática (1.275 alunos e faturamento) e entregou sugestões textuais para os tópicos de justificativa técnica. |
| **Fontes consultadas e verificadas** | Validação humana interna para assegurar que as restrições da escola fossem processados fielmente ao que foi coletado em campo. |
| **Trechos rejeitados ou corrigidos** | A IA sugeriu um nó conectando DIRETORIA no primeiro protótipo, mas o grupo corrigiu apontando a centralização da operação apenas na SECRETARIA e FINANCEIRO. |
| **Justificativa da escolha final** | As adaptações finais mantiveram a estrutura coerente com o porte médio da instituição. |
| **Reflexão crítica** | A IA é excelente para gerar volumetria e cálculos, mas inicialmente abstrai regras muito teóricas. Precisou ser retroalimentada com a realidade para espelhar a escola. |
| **Ferramenta e etapa** | Claude: Utilizado pelo membro Kevyn para revisão de consistência e formatação do Dicionário de Dados em HTML (versão 1.0 para 1.1). |
| **Motivação** | Revisar o dicionário de dados em HTML buscando inconsistências técnicas, erros de apresentação e redundâncias textuais. |
| **Prompt(s) utilizados** | Solicitação de análise profunda da página HTML apontando inconsistências técnicas na documentação das entidades e solicitando a remoção de menções redundantes ao DER no subtítulo e rodapé. |
| **Resposta recebida** | A IA sugeriu correções de acentuação ortográfica (MATRÍCULA, HORÁRIO_FUNCIONAMENTO), orientou complementar as descrições citando os relacionamentos, justificou a ausência de chaves estrangeiras e sinalizou a cardinalidade incomum nos relacionamentos INCLUI (1) e (2). |
| **Fontes consultadas e verificadas** | O modelo conceitual original e os padrões exigidos no trabalho. |
| **Trechos rejeitados ou corrigidos** | Foram acatadas as limpezas de subtítulos e rodapés exatamente como solicitado no prompt. |
| **Justificativa da escolha final** | As melhorias sugeridas pela IA aumentaram a clareza didática do Dicionário de Dados sem alterar a estrutura base já aprovada pelo grupo, gerando a versão 1.1. |
| **Reflexão crítica** | A IA foi muito eficaz em atuar como revisora de código e consistência lógica (como ao notar as cardinalidades peculiares), facilitando o polimento final do artefato. |
