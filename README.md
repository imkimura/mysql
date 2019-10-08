


# Tutorial de Comandos MySQL

Primeiro de tudo temos o SQL é dividido em 5 partes:
- [DDL (**Data Definition Language** - Linguagem de Definição de Dados)](#1-data-definition-language-ddl)  São os comandos que interagem com os objetos do banco.
>-- São comandos: > CREATE, ALTER e DROP <
- [DML (**Data Manipulation Language** - Linguagem de Manipulação de Dados)](#2-data-manipulation-language-dml)  São os comandos que interagem com os dados dentro das tabelas.
>-- São comandos: > INSERT, DELETE e UPDATE <
- [DQL (**Data Query Language** - Linguagem de Consulta de dados)](#3-data-query-language) São os comandos de consulta
>-- São comandos: > SELECT (comando de consulta)
- DCL (**Data Control Language** - Linguagem de Controle de Dados) São os comandos para controlar a parte de segurança do banco de dados
>-- São comandos: > GRANT, REVOKE E DENY <
- DTL (**Data Transaction Language** - Linguagem de Transação de Dados) São os comandos para controle de transação
>-- São comandos: > BEGIN TRANSACTION, COMMIT E ROLLBACK <

## 1. Data Definition Language (DDL)
Uma linguagem de definição de dados permite que possamos Criar, Alterar e Deletar estruturas de dados, ou seja, os comandos **CREATE**, **ALTER** e **DROP**.
### 1.1 Create
Como o nome já diz ele tem a função de criar, no caso podemos utilizá-lo para criar esquemas e tabelas. Para criar e utilizar um banco de dados utilizamos:
```sql
CREATE DATABASE <nome do banco>;
USE <nome do banco>;
```
Já a tabela é um pouco diferente pois precisamos especificar os campos que irão compor esta tabela, como no exemplo abaixo:
```sql
CREATE TABLE <nome da tabela> (
<nome do campo> <tipo do campo> <null ou not null>
);
```
```sql
CREATE TABLE pessoa ( 
id_pessoa TINYINT NOT NULL AUTO_INCREMENT,
nome VARCHAR(55) NOT NULL,
sobrenome VARCHAR(65) NOT NULL,
cpf INT(15) NOT NULL
);
```
Note que no último exemplo foi criado um campo chamado "id_pessoa", este campo é quem irá ser a chave primária da tabela pois ele é único, para que isso possa facilitar nas consultas e para que não hajam pessoas repetidas na tabela. No entanto para que meu id vire minha chave primária, eu preciso declara-lo como minha chave antes portanto eu preciso de uma **CONSTRAINT**, que nada mais é que uma restrição. 
\
Para definir uma **CONSTRAINT** de chave primária eu preciso de duas coisas, um nome para ela e o campo ta tabela que estou  referenciando no caso ficaria mais ou menos assim:
```sql
CONSTRAINT pk_<nome da tabela>_<nome do campo>
PRIMARY KEY (<nome do campo na tabela>)
```
```sql
CREATE TABLE pessoa ( 
id_pessoa TINYINT NOT NULL AUTO_INCREMENT,
nome VARCHAR(55) NOT NULL,
sobrenome VARCHAR(65) NOT NULL,
cpf INT(15) NOT NULL,

CONSTRAINT pk_pessoa_id_pessoa
PRIMARY KEY (id_pessoa)
);
```
Eu posso criar outros tipos de ***CONSTRAINT*** como por exemplo as de UNIQUE, FOREIGN KEY e CHECK. Para criar uma constraint de FK a estrutura é um pouco diferente:

```sql
CONSTRAINT fk_<nomeDaTabela>_<nomeDaTabelaEstrangeira>_<nomeDoCampo>
FOREIGN KEY <nomeDoCamponaTabela>
REFERENCES <nomeDaTabelaEstrangeira>(<nomeDoCampoNaTabelaEstrangeira>)
```
```sql
CREATE TABLE pessoa ( 
id_pessoa TINYINT NOT NULL AUTO_INCREMENT,
nome VARCHAR(55) NOT NULL,
sobrenome VARCHAR(65) NOT NULL,
cpf INT(15) NOT NULL,
id_cachorro TINYINT NOT NULL,

CONSTRAINT pk_pessoa_id_pessoa
PRIMARY KEY (id_pessoa),

CONSTRAINT fk_pessoa_animal_id_cachorro
FOREIGN KEY id_cachorro
REFERENCES animal(id)

);
```
As estruturas das CONSTRAINT's de CHECK e UNIQUE são;
\
\
Exemplo de UNIQUE:
```sql
CONSTRAINT uk_<nome da tabela>_<nome do campo>
UNIQUE c
```

```sql
CONSTRAINT uk_pessoa_cpf
UNIQUE (cpf)
```
\
Exemplo de CHECK:
```sql
CONSTRAINT ck_<nome da tabela>_<nome do campo>
CHECK <condicao>
```
Aqui no exemplo abaixo ele esta verificando se o campo idade é maior que 18
```sql
CONSTRAINT ck_pessoa_idade
CHECK (idade > 18)
```
### 1.2 Alter Table
Faz modificações em objetos criados com o CREATE, como inserir ou remover uma nova coluna em uma tabela, alterar o tipo das colunas, etc. 

#### 1.2.1 Para Criar uma Nova Coluna
```sql
ALTER TABLE <nome_da_tabela> 
ADD COLUMN <nome do campo>  <tipo do campo>
```
```sql
ALTER TABLE funcionario 
ADD COLUMN cod_departamento TINYINT
```
#### 1.2.2 Para Excluir uma Coluna
```sql
ALTER TABLE <nome_da_tabela> 
DROP COLUMN <nome do campo>
```
```sql
ALTER TABLE funcionario 
DROP COLUMN cod_departamento
```
#### 1.2.3 Para Inserir uma Constraint

```sql
ALTER TABLE <nome tabela> 
ADD CONSTRAINT fk_<nomeDaTabela>_<nomeDaTabelaEstrangeira>_<nomeDoCampo> 
FOREIGN KEY <nomeDoCamponaTabela>
REFERENCES <nomeDaTabelaEstrangeira>(<nomeDoCampoNaTabelaEstrangeira>)
```
```sql
ALTER TABLE funcionario 
ADD CONSTRAINT fk_funcionario_departamento 
FOREIGN KEY(cod_departamento) 
REFERENCES departamento(cod_departamento)
```
#### 1.2.4 Para Excluir uma Constraint
```sql
ALTER TABLE <nomeDaTabela>
DROP FOREIGN KEY <nomeDaFK>
```
```sql
ALTER TABLE funcionario 
DROP FOREIGN KEY fk_funcionario_departamento
```
#### 1.2.5 Alterar nome da Tabela
```sql
ALTER TABLE <nomeDaTabela>
RENAME <novoNome>
```
```sql
ALTER TABLE funcionario 
RENAME funcionario_v2
```
#### 1.2.6 Alterar nome da Coluna
```sql
ALTER TABLE <nomeDaTabela>
RENAME COLUMN <nomeDoCampo> to <novoNome>
```
```sql
ALTER TABLE funcionario 
RENAME COLUMN nome to nm_funcionario
```

## 2. Data Manipulation Language (DML)

### **1.1 Insert**
Um insert básico seria:

```sql 
INSERT INTO <nome da tabela> (<colunas da tabela>)
VALUES (<valores da tabela>)
```
Exemplo:
```sql
INSERT INTO cargo (id_cargo,descricao)
VALUES (1,'Analista de Sistemas'),
       (2,'Database Manager');
```

### **1.2 Update**
 Um update básico seria:
```sql
UPDATE <nome da tablea> 
SET <nome coluna> = <um valor> 
WHERE <condição>
```

Exemplo:
```sql
UPDATE cargo 
SET descricao ='Programador'
WHERE id_cargo = 3;
```

###  **1.3 Delete**
Um delete básico seria:
```sql
DELETE [FROM] <nome da tabela>
[WHERE <condicao>]
```

Exemplo:
```sql
DELETE FROM cargo 
WHERE id_cargo = 2; 
```

** *obs: **deleta apenas o dado condicionado***
Podemos tambem utilizar:
```sql
DELETE cargo;
```

** *obs: **irá deletar os dados da tabela toda, mas a tabela ainda existe :>***


## 3. Data Query Language
Como o nome diz essa parte serve para fazer consultas nas tabelas
para isso utilizamos o "Select"

### 3.1 SELECT
Um select básico é :
```sql
SELECT * FROM <nome tabela>; 
```
Onde eu seleciono tudo de uma determinada tabela, no entanto podemos também selecionar campos específicos
```sql
SELECT nome, idade, sexo FROM pessoa;
```
Para melhorar nosso tipo de seleção no banco temos alguns comandos que 
ajudam a organizar melhor seu *SELECT* como > **ORDER BY, WHERE**<
\
\
O **ORDER BY** é utilizado para ordenar por algum valor como por exemplo
ordenar as pessoas por ordem alfabética:
```sql
SELECT * FROM pessoa ORDER BY nome;
```
Eu posso ordenar a tabela pelos primeiros e últimos adicionados (**ASC | DESC**) exemplo:
```sql
SELECT * FROM alunos ORDER BY id_aluno DESC;
```
*obs. **onde ele seleciona os alunos pelo id de forma descendente.*** 
\
\
O **WHERE** é muito utilizado para dar condições específicas ao **SELECT** que estamos fazendo no banco como por exemplo:
```sql
SELECT nome, carga_horaria FROM curso
WHERE nm_curso LIKE 'Ora%'; 
```
*obs. **onde eu seleciono cursos que tenham "Ora" no inicio do nome***
\
\
Eu também posso dar condições onde tal campo seja `null` e o campo seja igual a certos valores 
```sql
SELECT nome, CH FROM curso
WHERE CH IS NULL;
```
*obs. **Aqui temos um exemplo de select onde eu quero que a carga horaria seja nula***

```sql
SELECT nome, CH FROM CURSO
WHERE CH IN (24,32); 
```
*obs. **Aqui eu especifico que quero selecionar Cargas Horarias que sejam iguais a 24 ou 32***
\
\
Para aprimorar nossos selects temos algumas funções que ajudam na hora de fazer uma seleção, sendo elas:
- AVG (coluna) – média dos valores de uma coluna;
-  Count (coluna) – total de linhas selecionadas;
-  Max (coluna) – valor máximo de uma coluna;
 - Min (coluna) – valor mínimo de uma coluna;
 - Sum (coluna) – soma dos valores de uma coluna.
 
 
Em prática essas funções seriam utilizadas assim:
```sql
SELECT COUNT(*) FROM curso; 
```
*Nesse select se supormos que a table tem  6 cursos o resultado da consulta será:

|                |COUNT(*)                                                 |
|----------------|--------|
||6                       |

\
Neste outro exemplo eu estou pegando a média, o valor máximo, o valor mínimo e a soma dos valores da coluna salário 
```sql
SELECT AVG(salario), MAX(salario),MIN(salario), SUM(salario)
FROM emprego;
```
O **SELECT** também pode ser agrupado por um valor da tabela, supondo que eu queira selecionar todos os funcionários agrupados pelo setor o select seria mais ou menos assim:
```sql
SELECT nome, id_setor, cpf FROM funcionario 
GROUP BY id_setor;
```
Esse tipo de agrupamento nos permite fazer certos tipos de combinações com algumas funções como por exemplo:
```sql
SELECT id_setor, COUNT(*) FROM funcionario 
GROUP BY id_setor;
```
*obs. **Aqui eu estou contando quantos funcionários eu tenho por setor***
```sql
SELECT cargo, MAX(salario) FROM emprego 
WHERE cargo<>'PRESIDENTE' 
GROUP BY cargo 
ORDER BY MAX(salario) DESC;
```
*obs. **Aqui estou agrupando por cargo onde o cargo não seja de Presidente ordenando pelo maior salario ate o menor, ou seja, ele irá retornar o cargo e o salario máximo do mesmo***
\
\
Terminando a parte de SELECTs com funções vale destacar que para SELECT's onde exista agrupamento(**GROUP BY**) utilizamos o **HAVING** ao invés de **WHERE**
\
\
Exemplo:
```sql
SELECT departamento, AVG(salario) FROM emprego
GROUP BY departamento
HAVING AVG(salario) > 2000;
```
*obs. **Aqui eu estou fazendo um select que me retorne o departamento e sua media salarial onde a media seja maior que 2000***

####  3.1.1 JOINS
![enter image description here](https://pics.me.me/thumb_left-join-rightjoin-inner-join-fulouter-join-ingfsp-com-database-60216420.png)
\
\
Uma breve introdução a Join's, a própria palavra nós da breve noção do que essas funções são responsáveis, Join significa "Juntar-se", no caso de banco de dados o Join serve para nada mais que juntar tabelas através de  certas condições. Abaixo está uma imagem que representaria melhor.
\
\
![enter image description here](https://static.imasters.com.br/wp-content/uploads/2013/05/uuu.png)


#### 3.1.2 INNER JOIN
O **INNER JOIN** serve para juntar duas tabelas e mostrar seus valores em comum, ou seja, ele faz uma intersecção de duas tabelas. Para fazermos um INNER JOIN precisamos do nome da tabela que queremos pegar os dados comuns e o campo que irá fazer a interligação entre as tabelas.

```sql 
SELECT <campos> FROM <tabela a>
INNER JOIN <tabela b>
ON b.id = a.id
```
Um exemplo seria temos uma tabela de cachorro_dono, uma de cachorro e uma de dono e queremos mostrar o nome do dono e do pet
\
\
**Tabela Cachorro_Dono**
|id|id_pet|id_dono|
|--|------|-------|
|1 |1     |3      |


**Tabela Cachorro**
|id_cachorro|nome|
|-----------|----|
|1          |Han |


**Tabela Dono**
|id_dono|nome          |
|-------|--------------|
|3      |Luke Skywalker|

\
Para podermos então pegar o nome do dono e do pet teremos que juntar as tabelas, para fazer isso utilizamos:

```sql
SELECT d.nome as Dono, c.nome as Pet FROM cachorro_dono as cd
INNER JOIN cachorro as c
ON c.id_cachorro = cd.id_pet
INNER JOIN dono as d
ON d.id_dono = cd.id_dono
```
Nos retornando os valores:

|Dono          |Pet |
|--------------|----|
|Luke Skywalker|Totó|


##  Conclusões
Este tutorial é com total intuito de aprender e quem sabe ajudar alguém, por hoje é só caros padawans, e que a força esteja ao seu lado
\
\
![enter image description here](http://giphygifs.s3.amazonaws.com/media/jd6TVgsph6w7e/giphy.gif)
