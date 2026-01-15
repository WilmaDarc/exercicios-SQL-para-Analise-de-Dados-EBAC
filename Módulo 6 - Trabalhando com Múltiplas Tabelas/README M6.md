<img src="https://github.com/user-attachments/assets/df0f71b5-7bae-4751-a85c-92f9cfbf61af" /> 

---

# **Módulo 6** | SQL: Trabalhando com Múltiplas Tabelas

Professora [Mariane Neiva](https://www.linkedin.com/in/mariane-neiva/)<br>
Aluna [Wilma Darc Alves de Farias](www.linkedin.com/in/wilma-farias-66a15962)<br>

Data: 3 de janeiro de 2026.

---

## Atividades

### **1. Criação da tabela**

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.cliente (
	`id_cliente` int,
	`nome` string,
	`valor_compra` double,
	`loja_cadastro` string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
	'serialization.format' = ',',
	'field.delim' = ','
)
LOCATION 's3://modulo6-wilma-ebac/cliente/'
TBLPROPERTIES ('has_encrypted_data' = 'false');
```

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS default.transacoes (
	`id_cliente` int,
	`id_transacao` int,
	`valor_compra` double,
	`id_loja` string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe'
WITH SERDEPROPERTIES (
	'serialization.format' = ',',
	'field.delim' = ','
)
LOCATION 's3://modulo6-wilma-ebac/transacoes/'
TBLPROPERTIES ('has_encrypted_data' = 'false');
```

### **2. Função UNION**

#### [**2.1. Query 1**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%206%20-%20Trabalhando%20com%20Mu%CC%81ltiplas%20Tabelas/query1_M6.csv)
```sql
SELECT id_cliente
FROM transacoes
UNION
SELECT id_cliente
FROM cliente;
```

### **3. Junções inner/cross**

#### [**3.1. Query 2**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%206%20-%20Trabalhando%20com%20Mu%CC%81ltiplas%20Tabelas/query2_M6.csv)
```sql
SELECT transacoes.id_cliente,
	cliente.nome
FROM transacoes
	INNER JOIN cliente ON transacoes.id_cliente = cliente.id_cliente;
```

#### [**3.2. Query 3**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%206%20-%20Trabalhando%20com%20Mu%CC%81ltiplas%20Tabelas/query3_M6.csv)
```sql
SELECT *
FROM cliente
	CROSS JOIN transacoes;
```

### **4. Junções: left / right**

#### [**4.1. Query 4**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%206%20-%20Trabalhando%20com%20Mu%CC%81ltiplas%20Tabelas/query4_M6.csv)
```sql
SELECT *
FROM transacoes
	LEFT JOIN cliente ON cliente.id_cliente = transacoes.id_cliente;
```

#### [**4.2. Query 5**](https://github.com/WilmaDarc/exercicios-SQL-para-Analise-de-Dados-EBAC/blob/main/Mo%CC%81dulo%206%20-%20Trabalhando%20com%20Mu%CC%81ltiplas%20Tabelas/query5_M6.csv)
```sql
SELECT *
FROM transacoes
	RIGHT JOIN cliente ON cliente.id_cliente = transacoes.id_cliente;
```
