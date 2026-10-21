
Consultas SQL
--------------------------------------------------------------------------------------
1/*Consultar todos os campos da tabela produto*/

SELECT*FROM produto;

--------------------------------------------------------------------------------------
2/*Consultar nome do produto, marca e estoque*/

SELECT nome_produto, marca, estoque
FROM produto;

---------------------------------------------------------------------------------------------
3/* Consultar nome, categoria, preço unitário e data de cadastro, em ordem alfabética por marca*/

SELECT nome_produto, categoria, preco_unitario, data_cadastro
FROM produto
ORDER BY marca ASC;

----------------------------------------------------------------------------------------------
4/* Consultar nome do produto, marca e estoque, da data de cadastro mais antiga para a mais recente*/

SELECT nome_produto, marca, estoque
FROM produto
ORDER BY data_cadastro ASC;

--------------------------------------------------------------
5/*Consultar todos os campos da tabela cliente*/

SELECT * FROM cliente;

--------------------------------------------------------------
6/* Consultar nome, e-mail, cidade e estado do cliente*/

SELECT nome_cliente, email, cidade, estado
FROM cliente;
---------------------------------------------------------------
7/* Consultar nome, cidade e estado em ordem alfabética por estado*/

SELECT nome_cliente, cidade, estado
FROM cliente
ORDER BY estado ASC;
----------------------------------------------------------------
8/* Consultar nome, e-mail e estado, do cadastro mais antigo para o mais recente*/

Considerando que a tabela tenha um campo `data_cadastro`:

SELECT nome_cliente, email, estado
FROM cliente
ORDER BY data_cadastro ASC;

-----------------------------------------------------------------
9/* Consultar todos os campos da tabela venda*/

SELECT * FROM venda;
----------------------------------------------------------------
10/* Consultar nome do cliente, data da venda, preço unitário e forma de pagamento*/

SELECT cliente.nome_cliente, venda.data_venda,  venda.preco_unitario_venda, venda.forma_pagamento
from cliente
inner JOIN venda
on venda.id_cliente =cliente.id_cliente;

---------------------------------------------------------------
11/* Consultar nome do produto, data da venda, quantidade e status*/

SELECT produto.nome_produto, venda.data_venda,
venda.quantidade, venda.status_venda
FROM produto
INNER JOIN venda
ON venda.id_produto = produto.id_produto;
-------------------------------------------------------------
12/*Consultar nome do produto, preço e forma de pagamento, somente para PIX ou Boleto*/

SELECT produto.nome_produto, venda.preco_unitario_venda,
venda.forma_pagamento
FROM produto
INNER JOIN venda
ON venda.id_produto = produto.id_produto
WHERE venda.forma_pagamento = 'PIX'
OR venda.forma_pagamento = 'Boleto';

------------------------------------------------------------------
13/*Consultar nome do cliente, nome do produto, data da venda e quantidade*/

SELECT cliente.nome_cliente, produto.nome_produto,
venda.data_venda, venda.quantidade
FROM cliente
INNER JOIN venda
ON venda.id_cliente = cliente.id_cliente
INNER JOIN produto
ON venda.id_produto = produto.id_produto;
---------------------------------------------------------------
14/*Consultar nome do produto, desconto e forma de pagamento, da venda mais antiga para a mais nova*/

SELECT produto.nome_produto, venda.desconto_percentual,
venda.forma_pagamento
FROM produto
INNER JOIN venda
ON venda.id_produto = produto.id_produto
ORDER BY venda.data_venda ASC;

----------------------------------------------------------------
15/* Consultar nome do produto, nome do cliente, desconto e forma de pagamento, em ordem alfabética por status*/


SELECT produto.nome_produto, cliente.nome_cliente,
venda.desconto_percentual, venda.forma_pagamento
FROM produto
INNER JOIN venda
ON venda.id_produto = produto.id_produto
INNER JOIN cliente
ON venda.id_cliente = cliente.id_cliente
ORDER BY venda.status_venda ASC;

--------------------------------------------------------------
16/*Consultar nome do cliente, e-mail, nome do produto, marca, categoria, forma de pagamento e status, da maior venda para a
 menor, apenas com status Cancelada ou Concluída*/

SELECT cliente.nome_cliente, cliente.email,
produto.nome_produto, produto.marca, produto.categoria,
venda.forma_pagamento, venda.status_venda
FROM cliente
INNER JOIN venda
ON venda.id_cliente = cliente.id_cliente
INNER JOIN produto
ON venda.id_produto = produto.id_produto
WHERE venda.status_venda = 'Cancelada'
OR venda.status_venda = 'Concluída'
ORDER BY (venda.preco_unitario_venda * venda.quantidade) DESC;

-----------------------------------------------------------------------------------------------------------------------------
