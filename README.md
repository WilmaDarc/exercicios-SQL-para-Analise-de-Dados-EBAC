<img src="https://github.com/user-attachments/assets/df0f71b5-7bae-4751-a85c-92f9cfbf61af" />


---

# **Módulo 1** | SQL: Base de dados & Linguagem SQL

Professor [André Perez](https://www.linkedin.com/in/andremarcosperez/)<br>
Aluno [Wilma Darc Alves de Farias](www.linkedin.com/in/wilma-farias-66a15962)<br>

Data: 10 de maio de 2023.

---

## Atividades

### **1 Criação da tabela de clientes**

```sql
CREATE EXTERNAL TABLE clientes(
	id BIGINT,
	idade BIGINT,
	sexo STRING,
	dependentes BIGINT,
	escolaridade STRING,
	tipo_cartao STRING,
	limite_credito DOUBLE,
	valor_transacoes_12m DOUBLE,
	qtd_transacoes_12m BIGINT
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
	'separatorChar' = ',',
	'quoteChar' = '"',
	'escapeChar' = '\\'
)
STORED AS TEXTFILE
LOCATION 'https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/tree/main/Mo%CC%81dulo%201%20-%20Base%20de%20dados%20%26%20Linguagem%20SQL'
```

### **2. Explorando os dados da tabela de clientes**

#### [**2.1. Query 1**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Query%201.csv)
```sql
SELECT *
FROM clientes;
```

#### [**2.2. Query 2**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Query%202.csv)
```sql
SELECT id,
	idade,
	limite_credito
FROM clientes
WHERE sexo = 'M'
ORDER BY idade DESC;
```

#### [**2.3. Query 3**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Query%203.csv)
```sql
SELECT sexo,
	AVG(idade) AS "media_idade_por_sexo"
FROM clientes
GROUP BY sexo;
```
