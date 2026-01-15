<img src="https://github.com/user-attachments/assets/df0f71b5-7bae-4751-a85c-92f9cfbf61af" /> 
---

# **Módulo 5** | SQL: Agregações

Professora [Mariane Neiva](https://www.linkedin.com/in/mariane-neiva/)<br>
Aluna [Wilma Darc Alves de Farias](www.linkedin.com/in/wilma-farias-66a15962)<br>


Data: 3 de janeiro de 2026.

---

## Atividades

### **1. Criação da tabela**

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.heartattack (
	`age` int,
	`sex` int,
	`cp` int,
	`trtbps` int,
	`chol` int,
	`fbs` int,
	`restecg` int,
	`thalachh` int,
	`exng` int,
	`oldpeak` double,
	`slp` int,
	`caa` int,
	`thall` int,
	`output` int
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
	'serialization.format' = ',',
	'field.delim' = ','
)
LOCATION 's3://heart-attack-wilma-ebac/'
TBLPROPERTIES ('has_encrypted_data' = 'false');
```

### **2. Função COUNT e GROUP BY**

#### [**2.1. Query 1**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query1_M5.csv)
```sql
SELECT *
FROM heartattack
limit 10;
```

#### [**2.2. Query 2**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query2_M5.csv)
```sql
SELECT COUNT(age) AS QUANTIDADE_LINHAS
FROM heartattack;
```

#### [**2.3. Query 3**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query3_M5.csv)
```sql
SELECT COUNT(age) AS QUANTIDADE,
	CASE
		WHEN output = 1 THEN 'more chance of heart attack' ELSE 'less chance of heart attack'
	END AS output
FROM heartattack
GROUP BY output;
```

### **3. Funções MIN/MAX/SUM/AVG**

#### [**3.1. Query 4**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query4_M5.csv)
```sql
SELECT MAX(age),
	MIN(age),
	AVG(age),
	output
FROM heartattack
GROUP BY output;
```

#### [**3.2. Query 5**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query5_M5.csv)
```sql
SELECT MAX(age),
	MIN(age),
	AVG(age),
	output,
	sex
FROM heartattack
GROUP BY output,
	sex;
```

### **4. Função HAVING**

#### [**4.1. Query 6**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%205%20-%20Agregac%CC%A7o%CC%83es/query6_M5.csv)
```sql
SELECT COUNT(output),
	output,
	sex
FROM heartattack
GROUP BY output,
	sex
HAVING COUNT(output) > 25;
```
