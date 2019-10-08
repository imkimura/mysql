
# Bem Vindo a um Tutorial de Comandos MySQL

Primeiro de tudo temos o SQL é dividido em 5 partes:

- DML (**Data Manipulation Language** - Linguagem de Manipulação de Dados)  São os comandos que interagem com os dados dentro das tabelas.
>-- São comandos: > INSERT, DELETE e UPDATE <
- DQL (**Data Query Language** - Linguagem de Consulta de dados) São os comandos de consulta
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

>INSERT INTO [***nome da tabela***]  ([***colunas da tabela***])
>VALUES ([***valores da tabela***])

Exemplo:
>INSERT INTO cargo (id_cargo,descricao)
	    VALUES (1,'Analista de Sistemas'),
		               (2,'Database Manager');

### **1.2 Update**
 Um update básico seria:
>UPDATE [***nome da tabela***] 
	  SET [***nome coluna***] = [***um valor***] 
	  WHERE [***condição***]

Exemplo:
> UPDATE cargo 
	      SET descricao ='Programador'
 	      WHERE id_cargo = 3;

###  **1.3 Delete**
Um delete básico seria:
>DELETE {FROM} [***nome da tabela***]
           {WHERE [***condicao***]}

Exemplo:
> DELETE FROM cargo 
	       WHERE id_cargo = 2; 

** *obs: **deleta apenas o dado condicionado***
Podemos tambem utilizar:
>DELETE cargo;

** *obs: **irá deletar os dados da tabela toda, mas a tabela ainda existe :>***

