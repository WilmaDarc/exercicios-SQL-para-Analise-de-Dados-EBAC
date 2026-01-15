<img src="https://github.com/user-attachments/assets/df0f71b5-7bae-4751-a85c-92f9cfbf61af" /> 

---

# **Módulo 2** | SQL: Trabalhando com Tabelas

Professora [Mariane Neiva](https://www.linkedin.com/in/mariane-neiva/)<br>
Aluna [Wilma Darc Alves de Farias](www.linkedin.com/in/wilma-farias-66a15962)<br>

Data: 3 de janeiro de 2026.

---

## Atividades

### **1. Explorando os dados da tabela de clientes**

#### [**1.1. Query 1**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_1_M2.csv)
```sql
SELECT id,
	idade,
	sexo,
	dependentes
FROM clientes;
```

#### [**1.2. Query 2**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_2_M2.csv)
```sql
SELECT id,
	valor_transacoes_12m
FROM clientes
WHERE escolaridade = 'mestrado'
	and sexo = 'F';
```

#### [**1.3. Query 3**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_3_M2.csv)
```sql
SELECT sexo,
	AVG(idade) AS "media_idade_por_sexo"
FROM clientes
GROUP BY sexo;
```

### **2. Inserindo novos dados**

#### [**2.1. Query 4**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_4_M2.csv)
```sql
SELECT *
FROM clientes;
```

### **3. Criando e trabalhando com partições**

#### [**3.1. Query 5**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_5_M2.csv)
```sql
CREATE EXTERNAL TABLE clientes_part(
	id BIGINT,
	idade BIGINT,
	dependentes BIGINT,
	escolaridade STRING,
	tipo_cartao STRING,
	limite_credito DOUBLE,
	valor_transacoes_12m DOUBLE,
	qtd_transacoes_12m BIGINT
)
PARTITIONED BY (sexo string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
	'separatorChar' = ',',
	'quoteChar' = '"',
	'escapeChar' = '\\'
)
STORED AS TEXTFILE
LOCATION ''
```

```sql
MSCK REPAIR TABLE clientes_part;
```

```sql
select *
from clientes_part
where sexo = 'F';
```

#### [**3.2. Query 6**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_6_M2.csv)
```sql
SELECT id,
	idade,
	limite_credito
FROM clientes_part
WHERE sexo = 'M'
ORDER BY limite_credito DESC;
```

### **4. Adicionando colunas**

#### [**4.1. Query 7**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%202%20-%20Tabelas%20em%20SQL/query_7_M2.csv)
```sql
ALTER TABLE clientes
ADD COLUMNS (estado string)
```

```sql
SELECT *
from clientes
```
