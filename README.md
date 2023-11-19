<img src="Logo.png" align="Center" alt="Hands On Data" style="height: 100px; width:115px;"/>

<p>  <br>
  </p>
  
# Basic and advanced SQL commands for queries and usage learning  
<p>  <br>
  </p>

###### by [Richard Gomes de Araújo](https://github.com/RichardGomesDeAraujo) - 20/05/2023
[![Github Badge](https://img.shields.io/badge/-Github-000?style=flat-square&logo=Github&logoColor=white&link=https://github.com/RichardGomesDeAraujo)](https://github.com/RichardGomesDeAraujo)
[![Linkedin Badge](https://img.shields.io/badge/-LinkedIn-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/richardaraujoanalistadedados/)](https://www.linkedin.com/in/richardaraujoanalistadedados/)
[![Youtube Badge](https://img.shields.io/badge/-YouTube-ff0000?style=flat-square&labelColor=ff0000&logo=youtube&logoColor=white&link=https://www.youtube.com/channel/UCc_jlqHut_GkXc8ahgQHOOw)](https://www.youtube.com/channel/UCc_jlqHut_GkXc8ahgQHOOw)
<p>  <br>
  </p>
  
# Índice
- [**Creating a Database**](README.md#Database)
- [**Creating Tables**](README.md#Tables)
- [**Create View**](README.md#View)
- [**Sub Query**](README.md#SubQuery)
- [**CTE-Commom Table Expression**](README.md#CTE)
- [**Update**](README.md#Update)
- [**DateDiff**](README.md#DateDiff)
- [**Max Min**](README.md#MaxMin)
- [**Avg**](README.md#Average)
- [**Ranking**](README.md#Ranking)
- [**Procedure**](README.md#Procedure)
- [**RowNumber**](README.md#RowNumber)
- [**AccumulatedBalance**](README.md#RowNumber)
- [**CaseWhenThenElseEnd**](README.md#RowNumber)
- [**NULLIF**](README.md#NULLIF)
- [**ISNULL**](README.md#ISNULL)
- [**Coalesce**](README.md#Coalesce)
- [**iif**](README.md#iif)

<p>  <br>
  </p>

# SQLServerChallenge02
Basic SQL queries for studies

<p>  <br>
  </p>
  
>## Database
>### Creating a Database

```SQL
    > CREATE DATABASE SQLServerChallenge02
```

###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## Tables
>### Creating Tables

>### First Table
```SQL
    > CREATE TABLE funcionarios
      ( 
      id_funcionario INT IDENTITY NOT NULL,
      nome VARCHAR(30) NOT NULL,
      admissao DATE NOT NULL,
      dpto VARCHAR(30) NOT NULL,
      cargo VARCHAR(30) NOT NULL,
      salario_base MONEY NOT NULL 
      ) 
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>### Second Table
```SQL
    > CREATE TABLE cargos
      ( 
      id_cargo INT NOT NULL,
      cargo VARCHAR(30) NOT NULL 
      )
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>### Third Table
```SQL
    > CREATE TABLE lancamentos
      ( 
      id_funcionario INT NOT NULL,
      salario_mes MONEY NOT NULL,
      decimo MONEY NOT NULL,
      ferias MONEY NOT NULL,
      fgts MONEY NOT NULL,
      inss MONEY NOT NULL,
      he MONEY NOT NULL,
      vt MONEY NOT NULL,
      sal_off MONEY NOT NULL 
      )
```  
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
    
 >## Insert
 >### Inserting Data To My First Table
```SQL
    > INSERT INTO funcionarios
      VALUES
      ('CELSO ACIR','2015-09-14','FOLGUISTA',1521,'PRODUÇÃO'),
      ('CLAUDIO FORTES','2014-05-02','FOLGUISTA',1521,'PRODUÇÃO'),
      ('SAMARA APARECIDA','2021-05-12','AUX.ADMINISTRATIVO',1411,'ADMINISTRATIVO'),
      ('MARIO PEDRO','2020-06-19','GERENTE',4108,'ADMINISTRATIVO'),
      ('AMANDA GARCIA','2018-11-01','AUX.DPTO PESSOAL',1411.70,'ADMINSTRATIVO'),
      ('GISLAINE TEIXEIRA','2012-12-01','ASSIST DE LOGISTICA',2409.20,'INDIRETO'),
      ('LUCAS MACIEL','2014-01-14','AUX.ADMINISTRATIVO',1403.70,'ADMINISTRATIVO')
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>### Inserting Data To My Second Table
```SQL
    > INSERT INTO cargos
      VALUES
      (2004,'AUX.ADMINISTRATIVO'),
      (2006,'AUX.DPTO PESSOAL'),
      (2012,'FOLGUISTA'),
      (2014,'GERENTE'),
      (2003,'ASSIST DE LOGISTICA')
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>### Inserting Data To My Third Table
```SQL
    > INSERT INTO lancamentos_folha
      VALUES
      (1,1301,130,70,120,110,0,250,0),
      (2,1301,130,70,120,110,0,250,0),
      (3,1200,120,60,110,100,200,250,0),
      (4,3500,350,210,250,300,0,250,0),
      (5,1200.50,240.35,167.15,266,250,350,250,0),
      (6,2000,200,150,160,215,50,250,0),
      (7,1150,150,114,142,162,65,250,0)
```  
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## View
>### Creating a View To Organize The Data With The Useful Columns
>### Stablishing Relation Between The Table With JOIN Clause

```SQL
    CREATE VIEW vw_bd
    AS
    SELECT 
      l.id_funcionario,
      l.decimo,
      l.ferias,
      l.FGTS,
      l.HE,
      l.sal_off,
      l.salario_mes,
      l.INSS,
      l.VT,
      f.nome,
      f.salario_base,
      f.admissao,
      f.cargo,
      f.dpto
    FROM 
      lancamentos_folha AS l
    JOIN funcionarios AS f 
      ON f.id_funcionario = l.id_funcionario
    JOIN cargos AS c 
      ON c.cargo = f.cargo
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## SubQuery
>### Creating A Second View With A Calculated Columns
>### View With A Sub-query
```SQL
    SELECT 
      dpto,
      qtd,
      nominal,
      SUM(nominal+impostos+beneficios) AS efetivo
    FROM
        ( SELECT
            dpto,
            COUNT(nome) AS qtd,
            SUM(salario_base) AS nominal,
            SUM(decimo+ferias+FGTS+INSS) AS impostos,
            SUM(VT+sal_off+HE) AS beneficios
          FROM 
            vw_bd
          GROUP BY 
            dpto ) AS bd
    GROUP BY 
      dpto, 
      qtd, 
      nominal
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
  
>## CTE
>### (Commom Table Expression) 
>### CTE is an alternative way of coding instead of with subqueries
```SQL
WITH tbl AS
(
  SELECT
    dpto,
    COUNT(nome) AS qtd,
    SUM(salario_base) AS nominal,
    SUM(decimo+ferias+FGTS+INSS) AS impostos,
    SUM(VT+sal_off+HE) AS beneficios
  FROM 
    vw_bd
  GROUP BY 
    dpto
)
SELECT 
  dpto,
  qtd,
  nominal,
  SUM(nominal+impostos+beneficios) AS efetivo
FROM 
  tbl
GROUP BY 
  dpto, 
  qtd, 
  nominal
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
  
>## Update
>### Updating The Data Inserted With An Error
```SQL
    UPDATE funcionarios
    SET dpto = 'ADMINISTRATIVO'
    WHERE dpto = 'ADMINSTRATIVO'
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## DateDiff
>### Creating A Query To Calculate The Service Time From Employees
```SQL
    SELECT 
      id_funcionario,
      nome,
      admissao,
      DATEDIFF(YEAR,admissao,GETDATE()) AS tempo_servico
    FROM 
      vw_bd
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## MaxMin 
>### Creating A Query To Return The Maximum And Minimum Value
```SQL
    SELECT 
      MAX(salario_base) AS maior_salario,
      MIN(salario_base) AS menor_salario
    FROM 
      vw_bd
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## Creating A Query With A Sub-Query To Visualize Data About The Maximum And Minimum Value
```SQL
    SELECT
      nome,
      cargo,
      admissao,
      salario_base
    FROM 
      vw_bd
    WHERE 
      salario_base = 
      (
      SELECT 
        MAX(salario_base) AS maior_salario
      FROM 
        vw_bd AS bd
      )
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## Average
>### Creating A Query To Return The Medium Value
```SQL
    SELECT 
      AVG(salario_base) AS media_salarial
    FROM 
      vw_bd
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## Ranking
>### Creating A View With Sub-Query To Show The Ranking
```SQL
    SELECT
      nome,
      cargo,
      salario_base,
      ranking
    FROM
      (
      SELECT 
        nome,
        cargo,
        salario_base,
        RANK() OVER(ORDER BY salario_base DESC) AS ranking
      FROM 
        vw_bd
      ) AS bd
    WHERE 
      ranking <= 3
  ```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## Procedure
>### Creating A Procedure To Search Data
  ```SQL
      CREATE PROCEDURE Buscar
      @nomefuncionario VARCHAR(30)
      AS
      SET @nomefuncionario = '%'+@nomefuncionario+'%'
      SELECT
        id_funcionario,
        nome,
        dpto,
        salario_base
      FROM 
        vw_bd
      WHERE 
        nome LIKE @nomefuncionario

      EXEC Buscar'MARIO PEDRO'
  ```
  ###### [⏪](README.md#Índice)
  <p>  <br>
  </p>
  
>## RowNumber
>### Creating A SQL to Return the Accumulated Balance

```SQL
      SELECT
        Periodo,
        Debito,
        Credito,
        SaldoDia,
        Qtd,
        SUM(SaldoDia) OVER(PARTITION BY MONTH(Qtd) ORDER BY Qtd) as SaldoAcumulado
      FROM 
        (
        SELECT
          Periodo,
          Debito,
          Credito,
          CASE WHEN Debito = 0 THEN Credito ELSE (Debito - Credito) END AS SaldoDia,
          ROW_NUMBER() OVER(ORDER BY Periodo) AS Qtd
        FROM 
          SaldoAcumulado
        ) AS Tbl
```
###### [⏪](README.md#Índice)
<p>  <br>
  </p>
 
>## NULLIF
>### Change values into NULL if a select rule is true
  ```SQL
     SELECT
        id_funcionario,
        nome,
        dpto,
        salario_base,
        NULLIF(nome, "SAMARA APARECIDA") as Valor_Nulo
      FROM
        funcionarios
  ```
  ###### [⏪](README.md#Índice)
  <p>  <br>
  </p>
 
>## ISNULL
>### Change values if the value is NULL
  ```SQL
     SELECT
        id_funcionario,
        nome,
        dpto,
        salario_base,
        ISNULL(dpto, "Departamento não Cadastrado") as Dpto_Nulo
      FROM
        funcionarios
  ```
  ###### [⏪](README.md#Índice)
  <p>  <br>
  </p>
   
>## Coalesce
>### Bring the first argument not null between some columns
  ```SQL
     SELECT
        id_funcionario,
        nome,
        dpto,
        salario_base,
        coalesce(tel1, tel2, tel3) as Telefone
        isnull(coalesce(tel1, tel2, tel3), "Não tem telefone") as Telefone_Se_Nulo
      FROM
        funcionarios
  ```
  ###### [⏪](README.md#Índice)
  <p>  <br>
  </p>
   
>## iif
>### The use case of IIF is the same case use of CASE WHEN
  ```SQL
     SELECT
          Periodo,
          Debito,
          Credito,
          CASE WHEN Debito = 0 THEN Credito ELSE (Debito - Credito) END AS SaldoDia,
          iif(Debito = 0, Credito, Debito - Credito) as SaldoDia_iif
      FROM 
          SaldoAcumulado
  ```
  ###### [⏪](README.md#Índice)
  <p>  <br>
  </p>
