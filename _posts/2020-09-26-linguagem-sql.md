---
layout: post
title:  "A Linguagem SQL"
date:  2020-09-26 19:02:00
categories: SQL SGBD MySQL Banco-de-Dados
---

`SQL: Linguagem de Consulta Estruturada`

`inglês: SQL - Structured Query Language `

`Uso da SGBD MySQL`

## A linguagem SQL

### SQL

O SQL é uma linguagem para se trabalhar com banco de dados relacionais, sendo assim é a linguagem padrão dos SGBD - `Sistema de Gerenciamento de Banco de Dados.`

Pela SQL damos aplicabilidade à diversos aspectos de um BD

* Definir esquemas de relacionamento;

* Criar restrições em relacionamentos;

* Realizar consultas interativas;

* Segurança e controle de atualizações.

  ____

Na linguagem SQL, se destacam cinco subconjuntos de instruções:

1. **Linguagem de Definição de Dados (DDL)**

   * CREATE, DROP, ALTER TRUNCATE

2. **Linguagem de Manipulação dos Dados (DML)**

   * INSERT, UPDATE, DELETE

3. **Linguagem de Consulta de Dados (DQL)**

   * SELECT, SHOW, HELP

4. **Linguagem de Controle dos Dados (DCL)**

   * GRANT, ROVOKE

5. **Linguagem de Transação dos Dados (DTL)**

   * START TRANSACTION, COMMIT, SAVEPOINT, ROLLBACK

   ___

   #### Tipos de Dados

   ![image-20200924140323053](/home/casa2495/snap/typora/23/.config/Typora/typora-user-images/image-20200924140323053.png)

   

   ##### Tipos numéricos

   ``` sql
   SMALLINT[(M)][UNSIGNED][ZEROFILL]
   ```

   Inteiro no intervalo de -32768 a 32767. O intervalo sem sinal é de 0 a 65535.

   ``` sql
   INT[(M)][UNSIGNED][ZEROFILL]
   ```

   Inteiro no intervalo de -2147483648 a 2147483648 . O intervalo sem sinal é de 0 a 4294967295.

   ``` sql
   BIGINT[(M)][UNSIGNED][ZEROFILL]
   ```

   Inteiro no intervalo de -9223372036854775808 a 9223372036854775808.

   ``` sql
   FLOAT[(M, D)][UNSIGNED][ZEROFILL]
   ```

   Ponto flutuante de precisão simples. Os valores admissíveis são de -3,402823466E+28 a -1,174594351E-38 e 1,175494351E-38 a 3,402823466E+38.

   ``` sql
   DOUBLE[(M, D)][UNSIGNED][ZEROFILL]
   ```

   Ponto flutuante de precisão dupla. Os valores admissíveis são de  -1,7976931348623157E+308 a 2,2250738585072014E-308,0

   ##### Tipos Data e Hora

   ```sql
   DATE [NOT NULL]
   ```

   Formato padrão: `YYYY-MM-DD` - Permite números ou strings

   ```sql 
   DATETIME [(fsp)]
   ```

   Combinação de Data e hora 

   Formato padrão: `YYYY-MM-DD HH:MM:SS`

   ```sql
   TIMESTAMP [(fsp)], TIME [(fsp)], YEAR [4]
   ```

```
   
   A função **GETDATE** retorna a data e a hora atuais do sistema.
   
   ```sql
   SELECT GETDATE()
```

   ##### Tipo Texto

   ``` sql
   VARCHAR (M) [CHARACTER SET charset_name] [COLLATE collation_name]
   ```

   Cadeia de comprimento variável.

   ``` sql
   CHAR (M) [CHARACTER SET charset_name] [COLLATE collation_name]
   ```

   Cadeia de comprimento fixo.

   ``` sql
   ENUM ('valor1', 'valor2', ...) [CHARACTER SET charset_name] [COLLATE collation_name]
   ```

   Objeto de string que pode ter apenas um valor, escolhido na lista de valores 'valor1', 'valor2', [...], NULO ou vazio. 

   É armazenado como inteiro pelo banco.

_____________________________

### Criação de Banco de Dados

`Conferir:Modelagem de Dados`; `Uso da SGBD MySQL`

Inicialmente, deve-se atentar para a *internacionalização*, dando atenção à abrangência da utilização do banco, respeitando as regras de escrita e gramática ou representação de cada país. 

`O MySQL possui as cláusulas CHARSET e COLLATION` 

O **CHARSET** designa um conjunto de símbolos e codificações e como eles são representados binariamente. 

O **COLLATION** é um conjunto de regras para comparação de caracteres em um **CHARSET**.

`Por exemplo através do COLLATION podemos determinar que não haverá diferença entre os caracteres maiúsculos e minúsculos `

Para verificar os CHARSET/ COLLATION instalados no MySQL :

``` sql
SHOW CHARACTER SET;
SHOW COLLATION;
```

#### Criando um Banco de Dados

Devemos utilizar as instruções da classe da linguagem de definição de Dados (DDL).

``` sql
CREATE{DATABASE|SCHEMA}[IF NOT EXISTS] db_name [creat_specification]...
creat_specification: [DEFAULT] CHARACTER SET [=] charset_name | [DEFAULT] COLLATE [=] collation_name
```

Criando tabela e campos de dados

``` sql
CREATE TABlE [IF NOT EXISTS] nome_tabela (Lista_campos);

|-> Lista de campos
(nome_campo tipo_campo[tamanho] [NOT NULL| NULL] [DEFAULT valor][AUTO_INCREMENT][PRIMARY KEY]);
```

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
); 
```

Podemos verificar a criação da tabela nesse exemplo abaixo:

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```




______________________

### Consultas no SQL

`Uso da SGBD MySQL`

**Consultas ** são resultados de um produto cartesiano das tabelas especificadas na cláusula **FROM**, realizadas por uma ou mais condições da cláusula **WHERE**, aplicando os resultados nos campos da cláusula **SELECT**.

Implementação:  

```sql
SELECT <Campos que devem ser retornados> FROM <Nome-da-TABELA> WHERE <Consulta>;
```

A clúsula **SELECT** retorna uma tabela

![image-20200924132148721](/home/casa2495/snap/typora/23/.config/Typora/typora-user-images/image-20200924132148721.png)

A Concatenção com a Clausula **as** muda o nome no retorno do **SELECT**

``` SQL
SELECT Nome, População as PopulacaoDeSaoPaulo FROM saopaulo;
```

` A cláusula "as" não muda o nome do dado na tabela, somente no retorno do select.`

_____________________________________

