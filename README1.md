# Techcorp

Cenário: Você foi contratado por uma empresa fictícia chamada TechCorp para gerenciar o banco de dados de seus funcionários e projetos. Sua tarefa é criar e manipular tabelas no PostgreSQL para organizar as informações da empresa.

### Passo 1: Criar o Banco de Dados
- Crie um banco de dados chamado techcorp.


```
postgres=# set client_encoding = 'UTF8' ;
SET
postgres=# CREATE DATABASE techcorp;
CREATE DATABASE
```

- Acesse o banco de dados.
```
postgres-# \c techcorp
psql (16.6, servidor 15.10)
Agora você está conectado ao banco de dados "techcorp" como usuário "postgres".
```

### Passo 2: Criar as Tabelas
- Crie uma tabela chamada funcionarios com as seguintes colunas:
  id (chave primária, numeração automática)
  nome (nome do funcionário, texto com até 50 caracteres)
  cargo (cargo do funcionário, texto com até 50 caracteres)
  salario (salário do funcionário, número com duas casas decimais)
  data_admissao (data de admissão do funcionário)

```
techcorp(# CREATE TABLE projetos (
techcorp(#     id SERIAL PRIMARY KEY,
techcorp(#     nome_projeto VARCHAR(100),
techcorp(#     id_funcionario INT,
techcorp(#     data_inicio DATE,
techcorp(#     data_fim DATE,
techcorp(#     CONSTRAINT fk_funcionario FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id)
techcorp(# );
techcorp(#
```

- consulta tabela criada

```

techcorp=# \dt
Lista de relaþ§es
Esquema |     Nome     |  Tipo  |   Dono
---------+--------------+--------+----------
public  | funcionarios | tabela | postgres
(1 linha)
```

- Crie uma tabela chamada projetos com as seguintes colunas:
  id (chave primária, numeração automática)
  nome_projeto (nome do projeto, texto com até 100 caracteres)
  id_funcionario (chave estrangeira que referencia o id da tabela funcionarios)
  data_inicio (data de início do projeto)
  data_fim (data de término do projeto)

```
techcorp=# CREATE TABLE projetos (
techcorp(#     id SERIAL PRIMARY KEY,
techcorp(#     nome_projeto VARCHAR(100) NOT NULL,
techcorp(#     id_funcionario INT NOT NULL,
techcorp(#     data_inicio DATE NOT NULL,
techcorp(#     data_fim DATE NOT NULL,
techcorp(#     CONSTRAINT fk_funcionario FOREIGN KEY (id_funcionario) REFERENCES funcionarios (id)
techcorp(# );
CREATE TABLE
```


- consulta de tabelas criadas
```
techcorp=# \dt
Lista de relaþ§es
Esquema |     Nome     |  Tipo  |   Dono
---------+--------------+--------+----------
public  | funcionarios | tabela | postgres
public  | projetos     | tabela | postgres
(2 linhas)
```


### Passo 3: Inserir Dados
- Insira os seguintes funcionários na tabela funcionarios:
  ('João Silva', 'Analista', 3500.00, '2023-01-15'),
  ('Maria Oliveira', 'Gerente', 7500.00, '2022-05-10'),
  ('Carlos Santos', 'Desenvolvedor', 4500.00, '2023-03-01'),
  ('Ana Costa', 'Desenvolvedor', 4000.00, '2023-02-20'),
  ('Pedro Lima', 'Estagiário', 1500.00, '2023-04-01');

```
techcorp=# INSERT INTO funcionarios (nome, cargo, salario, data_admissao) VALUES
techcorp-# ('João Silva', 'Analista', 3500.00, '2023-01-15'),
techcorp-# ('Maria Oliveira', 'Gerente', 7500.00, '2022-05-10'),
techcorp-# ('Carlos Santos', 'Desenvolvedor', 4500.00, '2023-03-01'),
techcorp-# ('Ana Costa', 'Desenvolvedor', 4000.00, '2023-02-20'),
techcorp-# ('Pedro Lima', 'Estagiário', 1500.00, '2023-04-01');
INSERT 0 5
```

- consultando dados inseridos na tabela funcionarios;

```
techcorp=# SELECT * FROM funcionarios;
id |      nome      |     cargo     | salario | data_admissao
----+----------------+---------------+---------+---------------
1 | João Silva     | Analista      | 3500.00 | 2023-01-15
2 | Maria Oliveira | Gerente       | 7500.00 | 2022-05-10
3 | Carlos Santos  | Desenvolvedor | 4500.00 | 2023-03-01
4 | Ana Costa      | Desenvolvedor | 4000.00 | 2023-02-20
5 | Pedro Lima     | Estagiário    | 1500.00 | 2023-04-01
(5 linhas)
```

- Insira os seguintes projetos na tabela projetos:
  ('Sistema de Gestão', 1, '2023-02-01', '2023-06-30'),
  ('E-commerce', 3, '2023-03-15', '2023-09-15'),
  ('Aplicativo Mobile', 4, '2023-04-01', '2023-12-31'),
  ('Relatório Financeiro', 2, '2023-01-01', '2023-05-31');

```
techcorp=# INSERT INTO projetos (nome_projeto, id_funcionario, data_inicio, data_fim) VALUES
techcorp-# ('Sistema de Gestão', 1, '2023-02-01', '2023-06-30'),

techcorp-# ('E-commerce', 3, '2023-03-15', '2023-09-15'),
techcorp-# ('Aplicativo Mobile', 4, '2023-04-01', '2023-12-31'),

techcorp-# ('Relatório Financeiro', 2, '2023-01-01', '2023-05-31');
INSERT 0 4
```

- consultando dados inseridos na tabela projetos:

```
techcorp=# SELECT * FROM projetos;
id |     nome_projeto     | id_funcionario | data_inicio |  data_fim
----+----------------------+----------------+-------------+------------
1 | Sistema de Gestão    |              1 | 2023-02-01  | 2023-06-30
2 | E-commerce           |              3 | 2023-03-15  | 2023-09-15
3 | Aplicativo Mobile    |              4 | 2023-04-01  | 2023-12-31
4 | Relatório Financeiro |              2 | 2023-01-01  | 2023-05-31
(4 linhas)

```
### Passo 4: Consultas e Filtragem
Agora, para cada pergunta abaixo, escreva a query correspondente e execute no PostgreSQL.

- Exibir todos os funcionários e seus respectivos cargos.

```
techcorp=# SELECT nome, cargo FROM funcionarios;
nome      |     cargo
----------------+---------------
João Silva     | Analista
Maria Oliveira | Gerente
Carlos Santos  | Desenvolvedor
Ana Costa      | Desenvolvedor
Pedro Lima     | Estagiário
(5 linhas)
```

- Filtrar os funcionários com salário maior que R$ 4.000,00.
```
techcorp=# SELECT nome, cargo, salario FROM funcionarios WHERE salario > 4000.00;
nome      |     cargo     | salario
----------------+---------------+---------
Maria Oliveira | Gerente       | 7500.00
Carlos Santos  | Desenvolvedor | 4500.00
(2 linhas)
```

- Exibir os projetos que terminam após 30/06/2023.
```
techcorp=# SELECT nome_projeto, data_fim FROM projetos WHERE data_fim > '2023-06-30';
nome_projeto    |  data_fim
-------------------+------------
E-commerce        | 2023-09-15
Aplicativo Mobile | 2023-12-31
(2 linhas)
```

- Listar os funcionários que possuem o cargo de "Desenvolvedor" e salário maior ou igual a R$ 4.000,00.
```
techcorp=# SELECT nome, cargo, salario FROM funcionarios WHERE cargo = 'Desenvolvedor' AND salario >= 4000.00;
nome      |     cargo     | salario
---------------+---------------+---------
Carlos Santos | Desenvolvedor | 4500.00
Ana Costa     | Desenvolvedor | 4000.00
(2 linhas)
```

- Exibir os funcionários que foram admitidos antes de 01/03/2023.
```
techcorp=# SELECT nome, cargo, data_admissao FROM funcionarios WHERE data_admissao < '2023-03-01';
nome      |     cargo     | data_admissao
----------------+---------------+---------------
João Silva     | Analista      | 2023-01-15
Maria Oliveira | Gerente       | 2022-05-10
Ana Costa      | Desenvolvedor | 2023-02-20
(3 linhas)
```

### Passo 5: Atualizar e Deletar Dados
- Atualize o salário do funcionário "Ana Costa" para R$ 4.500,00.

```
techcorp=# UPDATE funcionarios SET salario = 4500.00 WHERE nome = 'Ana Costa';
UPDATE 1
techcorp=# SELECT * FROM funcionarios WHERE nome = 'Ana Costa';
id |   nome    |     cargo     | salario | data_admissao
----+-----------+---------------+---------+---------------
4 | Ana Costa | Desenvolvedor | 4500.00 | 2023-02-20
(1 linha)
```
- Delete o projeto "Relatório Financeiro".

```
techcorp=# DELETE FROM projetos WHERE nome_projeto = 'Relatório Financeiro';
DELETE 1
techcorp=# SELECT * FROM projetos WHERE nome_projeto = 'Relatório Financeiro';
id | nome_projeto | id_funcionario | data_inicio | data_fim
----+--------------+----------------+-------------+----------
(0 linha)
```

## Desafio Extra

- Liste os funcionários que possuem salário entre R$ 3.000,00 e R$ 5.000,00.


```
techcorp=# SELECT nome, cargo, salario FROM funcionarios WHERE salario BETWEEN 3000.00 AND 5000.00;
nome      |     cargo     | salario
---------------+---------------+---------
João Silva    | Analista      | 3500.00
Carlos Santos | Desenvolvedor | 4500.00
Ana Costa     | Desenvolvedor | 4500.00
(3 linhas)
```

- Exiba o tempo total (em dias) de cada projeto.

```
techcorp=# SELECT nome_projeto,  data_fim - data_inicio AS tempo_total_em_dias FROM projetos;
nome_projeto    | tempo_total_em_dias
-------------------+---------------------
Sistema de Gestão |                 149
E-commerce        |                 184
Aplicativo Mobile |                 274
(3 linhas)
```
