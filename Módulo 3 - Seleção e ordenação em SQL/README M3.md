<img src="https://github.com/user-attachments/assets/df0f71b5-7bae-4751-a85c-92f9cfbf61af" /> 

---

# **Módulo 3** | SQL: Selecionando & Ordenando

Professora [Mariane Neiva](https://www.linkedin.com/in/mariane-neiva/)<br>
Aluna [Wilma Darc Alves de Farias](www.linkedin.com/in/wilma-farias-66a15962)<br>

Data: 03 de janeiro de 2026.

---

## Atividades

### **2. Selecionando dados**

```sql
CREATE EXTERNAL TABLE transacoes (
	id_cliente BIGINT,
	id_transacao BIGINT,
	valor FLOAT,
	id_loja STRING
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
	'separatorChar' = ',',
	'quoteChar' = '"',
	'escapeChar' = '\\'
)
STORED AS TEXTFILE
LOCATION ''
```

#### [**2.1. Query 1**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%203%20-%20Sele%C3%A7%C3%A3o%20e%20ordena%C3%A7%C3%A3o%20em%20SQL/query1.csv)
```sql
SELECT *
FROM transacoes
```

#### [**2.2. Query 2**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%203%20-%20Sele%C3%A7%C3%A3o%20e%20ordena%C3%A7%C3%A3o%20em%20SQL/query2.csv)
```sql
SELECT id_cliente,
	valor,
	id_loja AS nome_loja
FROM transacoes;
```

#### [**2.3. Query 3**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%203%20-%20Sele%C3%A7%C3%A3o%20e%20ordena%C3%A7%C3%A3o%20em%20SQL/query3.csv)
```sql
SELECT DISTINCT id_loja AS nome_loja
FROM transacoes;
```

### **3. Ordenando e limitando dados**

#### [**3.1. Query 4**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/M%C3%B3dulo%203%20-%20Sele%C3%A7%C3%A3o%20e%20ordena%C3%A7%C3%A3o%20em%20SQL/query4.csv)
```sql
SELECT id_cliente,
	valor
FROM transacoes
ORDER BY valor DESC
LIMIT 2;
```
