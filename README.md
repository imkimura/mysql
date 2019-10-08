
# Bem Vindo a um Tutorial de Comandos MySQL

Primeiro de tudo temos o SQL é dividido em 5 partes:

- [DML (**Data Manipulation Language** - Linguagem de Manipulação de Dados)](#1-data-manipulation-language-dml)  São os comandos que interagem com os dados dentro das tabelas.
>-- São comandos: > INSERT, DELETE e UPDATE <
- [DQL (**Data Query Language** - Linguagem de Consulta de dados)](#2-data-query-language) São os comandos de consulta
>-- São comandos: > SELECT (comando de consulta)
- DDL (**Data Definition Language** - Linguagem de Definição de Dados)  São os comandos que interagem com os objetos do banco.
>-- São comandos: > CREATE, ALTER e DROP <
- DCL (**Data Control Language** - Linguagem de Controle de Dados) São os comandos para controlar a parte de segurança do banco de dados
>-- São comandos: > GRANT, REVOKE E DENY <
- DTL (**Data Transaction Language** - Linguagem de Transação de Dados) São os comandos para controle de transação
>-- São comandos: > BEGIN TRANSACTION, COMMIT E ROLLBACK <

## 1. Data Manipulation Language (DML)

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


## 2. Data Query Language
Como o nome diz essa parte serve para fazer consultas nas tabelas
para isso utilizamos o "Select"

### 2.1 SELECT
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
O **WHERE** é muito utilizado para dar condições específicas ao **SELECT** que estamos fazendo no banco como por exemplo:
```sql
SELECT nome, carga_horaria FROM curso
WHERE nm_curso LIKE 'Ora%'; 
```
*obs. **onde eu seleciono cursos que tenham "Ora" no inicio do nome***
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
Terminando a parte de SELECTs com funções vale destacar que para SELECT's onde exista agrupamento(**GROUP BY**) utilizamos o **HAVING** ao inves de **WHERE**
\
Exemplo:
```sql
SELECT departamento, AVG(salario) FROM emprego
GROUP BY departamento
HAVING AVG(salario) > 2000;
```
*obs. **Aqui eu estou fazendo um select que me retorne o departamento e sua media salarial onde a media seja maior que 2000***


