# SQLite Database: Mercado

This README provides an overview of creating and interacting with a SQLite database named `mercado.db`. The database contains a `produtos` table with columns for product details, including ID, name, price, and quantity. Below are the SQL commands and their purposes.

```sql
-- Open the Database
.open mercado.db
.header on 
.mode table

-- Drop Table
DROP TABLE IF EXISTS produtos;

-- Create Table
CREATE TABLE produtos(
    id_produto integer primary key auto increment,
    nome char(50) not null,
    preco real,
    quantidade integer
);

-- Insert Data
INSERT INTO produtos VALUES (null, 'Produto 1', 4.99, 100);
INSERT INTO produtos VALUES (null, 'Produto 2', 5.99, 200);
INSERT INTO produtos VALUES (null, 'Produto 3', 14.99, 300);
INSERT INTO produtos VALUES (null, 'Produto 4', 122.99, 400);

-- Basic Queries
SELECT * FROM produtos;
SELECT nome, preco FROM produtos;

-- Filtering with Conditions
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

-- Sorting Results
SELECT * FROM produtos WHERE quantidade < 400 ORDER BY nome;
SELECT * FROM produtos WHERE quantidade ORDER BY preco DESC;
