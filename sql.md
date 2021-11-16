Banco de dados - Repositório sistêmico de informações

- Local para armazenar informações de forma organizada / sistêmica.

Alguns tipos de bancos de dados:

- SQLite
- MariaDB
- MySQL
- PostgreSQL
- Oracle
- Firebase
- MongoDB
- redis

Regras para escrever nome de tabelas e campos:

- Começar sempre por letras do alfabeto
- Não utilizar caractéres especiais, lembrar de não usar "-" e sim "\_".
- Não conter espaços
- Não conter acentuação

OBS: Uma tabela pode ter mais de uma FOREING KEY, mas nunca mais de uma PRIMARY KEY.

PREPARANDO AMBIENTE PARA O SQL:

- Baixar o Beekeeper: beekeeperstudio.io
- Abrir o Beekeeper
- Adicionar arquivo SQLite
- Criar query

OBS: Comandos SQL sempre em maiúsculo

PARA RODAR: Selecionar linha com comando e clicar no Run

COMANDOS:

- SELECT = Buscar coisas no banco de dados (SELECT \* FROM aluno) sem "\"

COMO DEFINIR CAMPOS ESPECÍFICOS NO SELECT: SELECT nome, responsavel FROM aluno

WHERE busca elementos em uma tabela com um determinado argumento: SELECT \* FROM aluno WHERE matricula = 1 (PARA NÚMEROS)
SELECT \* FROM aluno WHERE nome like "j%" (PARA TEXTO) [SEMPRE USAR ASPAS PARA TEXTO]

SELEÇÃO COM OPERADORES RELACIONAIS:
SELECT \* FROM aluno WHERE cpf = 45678945645
SELECT \* FROM aluno WHERE matricula > 1
SELECT \* FROM aluno WHERE matricula <> 1
SELECT \* FROM aluno WHERE matricula != 1
Operadores: Like, =, >, <, >=, <=, <>, !=

OPERADORES MATEMÁTICOS: +, -, \*, /, %
SELECT \* FROM aluno WHERE matricula = 1 + 1

MÓDULO = RESTO DE UMA DIVISÃO
SELECT \* FROM aluno WHERE matricula = 4%3 // RESTO = 1

OPERADORES LÓGICOS: JUNTAR DUAS CONDIÇÕES

E
SELECT \* FROM aluno WHERE nome like "J%" AND matricula > 2

OU
SELECT \* FROM aluno WHERE matricula > 1 OR nome like "j%"

BETWEEN - BUSCA POR INTERVALOS
SELECT \* FROM funcionarios WHERE id_funcionario BETWEEN 4 and 7

NOT BETWEEN - BUSCA POR INTERVALOS
SELECT \* FROM funcionarios WHERE id_funcionario NOT BETWEEN 4 and 7

IN
SELECT \* FROM funcionarios WHERE id_departamento IN (1, 3, 5)

NOT IN
SELECT \* FROM funcionarios WHERE id_departamento NOT IN (1, 3, 5)

IS NULL
SELECT \* FROM funcionarios WHERE id_departamento IS NULL

IS NOT NULL
SELECT \* FROM funcionarios WHERE id_departamento IS NOT NULL

ADICIONA DADO
NSERT INTO aluno (nome, cpf, responsavel) VALUES ("Maria Luiza", 45678912345, "Wantuil Soares")

ALTERA DADO
UPDATE aluno SET nome="Mariano Soares", responsavel="Marcio Soares", cpf=12345678985 WHERE matricula = 2

DELETAR DADOS
DELETE FROM aluno WHERE matricula = 3

UNINDO TABELAS

OBS: ALIASES SÓ FUNCIONAM COM SELECT

JOIN
SELECT \* FROM funcionarios
JOIN departametos
ON departamentos.id_dept = funcionarios.id_departamento

JOIN COM WHERE
SELECT \* FROM funcionarios
JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept
WHERE departamentos.id_dept = 2

JOIN CAMPOS ESPECÍFICOS
SELECT funcionarios.nome, funcionarios.cpf, departamentos.descricao
FROM funcionarios
JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept

JOIN ALIASES
SELECT func.nome as "Nome", func.cpf as "CPF", dept.descricao as "Departamento"
FROM funcionarios as func
JOIN departamentos as dept
ON func.id_departamento = dept.id_dept

LEFT OUTER JOIN - PRIORIZA SEMPRE A TABELA DA ESQUERDA
SELECT \* FROM funcionarios
LEFT OUTER JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept

SELECT \* FROM departamentos
LEFT OUTER JOIN funcionarios
ON funcionarios.id_departamento = departamentos.id_dept

ORDER
SELECT \* FROM professor
ORDER BY nome

SELECT \* FROM professor
ORDER BY nome DESC

LIMIT - MOSTRA OS PRIMEIROS
SELECT \* FROM aluno LIMIT 2

OFFSET - IGNORA OS PRIMEIROS
SELECT \* FROM funcionarios
LIMIT 4 OFFSET 2

COUNT
SELECT COUNT(nome) FROM funcionarios
SELECT COUNT(id_departamento) FROM funcionarios

GROUP BY
SELECT COUNT(id_departamento)
FROM funcionarios
GROUP by id_departamento

SELECT id_departamento, COUNT(id_departamento)
FROM funcionarios
GROUP by id_departamento

JOIN, GROUP BY, COUNT
SELECT departamentos.descricao, COUNT(funcionarios.id_departamento)
FROM funcionarios
JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept
GROUP BY departamentos.id_dept

HAVING
SELECT departamentos.descricao, COUNT(funcionarios.id_departamento)
FROM funcionarios
JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept
GROUP BY departamentos.id_dept
HAVING COUNT(funcionarios.id_departamento) >= 2

SELECT departamentos.descricao, COUNT(funcionarios.id_departamento)
FROM funcionarios
JOIN departamentos
ON funcionarios.id_departamento = departamentos.id_dept
GROUP BY departamentos.id_dept
HAVING COUNT(funcionarios.id_departamento) IN (2, 4)

MEXENDO COM A TABELA (SETUP)

CREATE TABLE - CRIAR TABELA

CREATE TABLE alunos(
matricula INTEGER PRIMARY KEY AUTOINCREMENT,
nome TEXT,
cpf INTEGER UNIQUE,
responsavel TEXT
)

CREATE TABLE professores(
id_professor INTEGER PRIMARY KEY AUTOINCREMENT,
nome TEXT,
cpf INTEGER UNIQUE,
materia TEXT
)

FOREING KEY - CHAVE ESTRANGEIRA

CREATE TABLE aulas(
id_professor INTEGER ,
matricula INTEGER,
FOREING KEY(id_professor) REFERENCES professores(id_professor),
FOREING KEY(matricula) REFERENCES alunos(matricula)
)

ALTER TABLE - ALTERAR TABELA

ALTER TABLE aluno RENAME TO alunos
ALTER TABLE professor RENAME TO professores
ALTER TABLE aulas RENAME COLUMN id_aluno TO matricula_aluno

DROP TABLE - EXCLUIR TABELA

DROP TABLE alunos
DROP TABLE aulas
DROP TABLE professores
