# SQLite Database: Market

This README provides a comprehensive overview of creating, managing, and interacting with a SQLite database named `market.db`. Below is the SQL script used to create the database, insert data, and perform various operations.

```sql
-- Open the Database
.open market.db
.header on 
.mode table

-- Drop Table if Exists
DROP TABLE IF EXISTS produtos;

-- Create Table
CREATE TABLE produtos(
    id_produto integer primary key auto increment,
    nome char(50) not null,
    preco real,
    quantidade integer
);

-- Insert Data into Table
INSERT INTO produtos VALUES (null, 'Produto 1', 4.99, 100);
INSERT INTO produtos VALUES (null, 'Produto 2', 5.99, 200);
INSERT INTO produtos VALUES (null, 'Produto 3', 14.99, 300);
INSERT INTO produtos VALUES (null, 'Produto 4', 122.99, 400);

-- Basic Queries
SELECT * FROM produtos;
SELECT nome, preco FROM produtos;

-- Filtering Data
SELECT * FROM produtos WHERE id_produto = 2;
SELECT * FROM produtos WHERE preco = 4.99;
SELECT * FROM produtos WHERE preco != 4.99;
SELECT * FROM produtos WHERE preco >= 14.99;
SELECT * FROM produtos WHERE (preco >= 5.99) AND (quantidade < 300);

-- Use of IN and NOT IN
SELECT * FROM produtos WHERE id_produto IN (1,3);
SELECT * FROM produtos WHERE id_produto NOT IN (1,3);

-- Range Queries
SELECT * FROM produtos WHERE quantidade BETWEEN 200 AND 400;
SELECT * FROM produtos WHERE quantidade NOT BETWEEN 200 AND 400;
SELECT * FROM produtos WHERE (quantidade BETWEEN 200 AND 400) AND (preco BETWEEN 4 AND 20);

-- Pattern Matching with LIKE
SELECT * FROM produtos WHERE nome LIKE 'p%2';
SELECT * FROM produtos WHERE nome LIKE '%u%';
SELECT * FROM produtos WHERE nome NOT LIKE '%u%';

-- Functions
SELECT datetime('now');
SELECT SUM(quantidade) AS Estoque FROM produtos;
SELECT MIN(quantidade) AS "Menor Estoque" FROM produtos;
SELECT MAX(preco) AS "Maior Preço" FROM produtos;
SELECT COUNT(*) AS total_produtos FROM produtos;

-- Filtering Data with Aggregation
SELECT COUNT(*) AS total_clientes_uk FROM produtos WHERE pais = 'UK';
SELECT AVG(idade) AS media_idade FROM clientes;
SELECT * FROM clientes WHERE nome LIKE 'j%' AND sobrenome LIKE '%a';

-- Sorting Results
SELECT * FROM produtos WHERE quantidade < 400 ORDER BY nome;
SELECT * FROM produtos ORDER BY preco DESC;
