# Gerenciamento de Vendas

Projeto de modelagem e migração de dados: informações que estavam em planilhas Excel foram estruturadas em um banco de dados relacional **MySQL**, com scripts SQL de criação de tabelas, carga de dados e consultas.

## Objetivo

Substituir o controle em planilhas por um banco de dados com **padronização, integridade referencial e consultas mais rápidas e confiáveis**, cobrindo duas áreas de uma loja de tecnologia:

- **Vendas:** clientes, pedidos, produtos, categorias e vendedores
- **Recursos Humanos:** cargos, funcionários e vendedores (com comissão e meta)

## Tecnologias

- MySQL
- SQL (DDL, DML e consultas)
- Excel (fonte original dos dados)

## Modelo de dados

### Banco `loja` (vendas)

| Tabela | Descrição |
|---|---|
| `TB_CLIENTE` | Dados cadastrais e endereço dos clientes |
| `TB_CLIENTE_TELEFONE` | Telefones (um cliente pode ter vários) |
| `TB_VENDEDOR` | Vendedores |
| `TB_CATEGORIA` | Categorias de produtos |
| `TB_PRODUTO` | Produtos, com categoria e preço |
| `TB_PEDIDO` | Cabeçalho dos pedidos (data, cliente, vendedor) |
| `TB_ITEM_PEDIDO` | Itens de cada pedido (produto, quantidade, preço) |

### Banco `funcionarios` (RH)

| Tabela | Descrição |
|---|---|
| `TB_CARGO` | Cargos, departamentos e piso salarial |
| `TB_FUNCIONARIO` | Funcionários, salário, admissão, desligamento e turno |
| `TB_VENDEDOR` | Vendedores ligados a um funcionário, com comissão e meta mensal |

### Relacionamentos principais

- Um **cliente** pode ter vários **telefones** e vários **pedidos** (1:N)
- Um **pedido** tem um **vendedor** e vários **itens** (1:N)
- **Pedidos** e **produtos** se relacionam por `TB_ITEM_PEDIDO` (N:N, chave composta)
- Um **produto** pertence a uma **categoria**
- Um **funcionário** tem um **cargo**, e um **vendedor** é um **funcionário**

## Como executar

1. Crie os bancos de dados:
   ```sql
   CREATE DATABASE loja;
   CREATE DATABASE funcionarios;
   ```
2. Execute o script `gerenciamentovendas.sql` no MySQL Workbench ou pelo terminal:
   ```bash
   mysql -u seu_usuario -p < gerenciamentovendas.sql
   ```
3. Confira se tudo foi criado:
   ```sql
   SHOW TABLES;
   SELECT COUNT(*) FROM TB_PEDIDO;
   ```

## Exemplos de consultas

```sql
-- Funcionários com salário entre R$ 1.000 e R$ 2.000
SELECT nome_funcionario, salario
FROM TB_FUNCIONARIO
WHERE salario BETWEEN 1000 AND 2000;

-- Itens de um pedido específico
SELECT * FROM TB_ITEM_PEDIDO
WHERE cod_pedido = 2000;
```

## Aprendizados

- Modelar tabelas a partir de planilhas exige decidir tipos de dados, chaves primárias e relacionamentos
- Limpar e padronizar os dados **antes** de importar evita muito retrabalho
- Chaves estrangeiras garantem a integridade entre pedidos, clientes, produtos e vendedores
- Organizar em vários bancos e tabelas facilita manutenção e consultas

## Aviso sobre os dados

Todos os dados deste repositório (nomes, CPFs, telefones, endereços) são **fictícios**, criados apenas para fins de estudo.

## Próximos passos

- Criar consultas analíticas (faturamento por vendedor, produtos mais vendidos, vendas por mês)
- Criar views e índices
- Gerar o diagrama ER no MySQL Workbench

## Autor

Seu Nome | [[LinkedIn](https://www.linkedin.com/in/seu-perfil)](https://www.linkedin.com/in/arthurrickss/)
