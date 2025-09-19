Documentação do meu aprendizado em PostgreSQL. Do zero ao avançado: fundamentos de banco de dados, criação de tabelas, consultas complexas, joins, índices, transações, funções, triggers, otimização de performance e backup/recuperação. Todo código comentado para aprendizado prático.

**PostgreSQL** é um sistema de gerenciamento de banco de dados relacional (SGBD) poderoso, open-source e orientado a objetos. Ele é amplamente utilizado por empresas e desenvolvedores para armazenar e gerenciar dados de forma eficiente e segura.

A principal vantagem do PostgreSQL é sua conformidade com o SQL padrão e a capacidade de lidar com operações complexas de dados. Ele também oferece extensibilidade, permitindo adicionar novos tipos de dados, operadores e funções.

# Instalação do PostgreSQL

A instalação do PostgreSQL varia conforme o sistema operacional. Aqui estão as etapas gerais:

## Windows

Acesse o site oficial do PostgreSQL: [postgresql](https://www.postgresql.org/download/windows/)

Baixe o instalador e siga as instruções. Após a instalação, o PostgreSQL estará pronto para uso.

## MacOS

Use o Homebrew:

```bash 
brew install postgresql
```

Ou baixe o instalador do PostgreSQL em [postgresql](https://www.postgresql.org/download/macosx/)

## Linux (Ubuntu/Debian)

Execute os seguintes comandos no terminal:

```bash
sudo apt update  
sudo apt install postgresql postgresql-contrib
```

Após a instalação, você pode acessar o PostgreSQL pelo terminal ou pelo **pgAdmin**, uma ferramenta gráfica que facilita o gerenciamento de bancos de dados.

# Introdução ao SQL

O SQL (Structured Query Language) é uma linguagem usada para gerenciar dados em bancos de dados relacionais. Alguns conceitos fundamentais incluem:

**Banco de dados**: Conjunto de dados organizados.

**Tabela**: Estrutura de armazenamento de dados dentro de um banco de dados.

**Registro (ou Linha)**: Cada entrada ou item em uma tabela.

**Coluna**: Cada tipo de dado em uma tabela (como nome, idade, etc.).

# Primeiros comandos SQL:

```sql
CREATE DATABASE: Cria um novo banco de dados.

CREATE DATABASE meu_banco_de_dados;

CREATE TABLE: Cria uma nova tabela dentro de um banco de dados.

 CREATE TABLE usuarios (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    idade INT  
);

INSERT INTO: Insere dados em uma tabela.

INSERT INTO usuarios (nome, idade) VALUES ('João', 30);

SELECT: Consulta dados de uma tabela.

SELECT \* FROM usuarios; 

DROP TABLE: Exclui uma tabela do banco de dados.

DROP TABLE usuarios;
```

# Introdução ao PostgreSQL

## Configuração do PostgreSQL e Conceitos Básicos de Bancos de Dados

### Configuração do PostgreSQL

Uma vez que o PostgreSQL esteja instalado, você pode começar a trabalhar com ele de duas formas principais:

**pgAdmin**: Uma interface gráfica para gerenciar bancos de dados PostgreSQL, útil para quem prefere não trabalhar diretamente com comandos de terminal.

**Linha de Comando (psql)**: Um terminal interativo onde você pode executar comandos SQL diretamente no PostgreSQL.

**pgAdmin**, basta abrir a ferramenta após a instalação e conectar-se ao servidor PostgreSQL, fornecendo o nome de usuário e senha criados durante a instalação.

**psql**, você pode iniciar o terminal no diretório onde o PostgreSQL está instalado e digitar:

```bash
psql \-U postgres
```

Isso abrirá o terminal do PostgreSQL, onde você poderá rodar comandos SQL diretamente.

### Conceitos Básicos de Bancos de Dados Relacionais

Bancos de dados relacionais organizam os dados em **tabelas** compostas por linhas e colunas. A **chave primária** (PRIMARY KEY) é usada para identificar de maneira única cada registro dentro de uma tabela, enquanto a **chave estrangeira** (FOREIGN KEY) é usada para criar um relacionamento entre duas tabelas.

**Tabela**: Estrutura de dados organizados em colunas e linhas.

**Linha**: Cada entrada individual na tabela, representando uma instância de dados.

**Coluna**: Cada tipo de dado na tabela (ex: nome, idade).

**Chave primária**: Campo (ou conjunto de campos) que identifica de maneira única uma linha em uma tabela.

**Chave estrangeira**: Campo que cria um relacionamento entre duas tabelas, apontando para a chave primária de outra tabela.

# Introdução ao PostgreSQL

## Primeiros Comandos SQL

Agora que você já configurou o PostgreSQL e aprendeu os conceitos básicos, vamos praticar alguns comandos SQL essenciais para manipular dados no banco.

### Comandos SQL Essenciais:

**CREATE DATABASE**: Cria um novo banco de dados no PostgreSQL.

```sql
 CREATE DATABASE nome\_do\_banco;
```

**CREATE TABLE**: Cria uma nova tabela no banco de dados. Aqui, vamos criar uma tabela de exemplo chamada clientes:

```sql
 CREATE TABLE clientes (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    email VARCHAR(100),  
    data\_nascimento DATE  
);
```

**INSERT INTO**: Insere dados em uma tabela. Exemplo de inserção de um registro na tabela clientes:

```sql
INSERT INTO clientes (nome, email, data\_nascimento)  
VALUES ('Maria Silva', 'maria@exemplo.com', '1985-04-12');
```

**SELECT**: Consulta dados de uma tabela. Vamos consultar todos os registros da tabela clientes:

```sql
SELECT * FROM clientes;
```

Esse comando vai retornar todos os dados da tabela. Você também pode usar condições para filtrar os resultados, como:

```sql
SELECT nome, email FROM clientes WHERE nome = 'Maria Silva';
```

**DROP TABLE**: Exclui uma tabela do banco de dados. Tenha cuidado ao usar esse comando, pois ele apaga permanentemente a tabela e seus dados.

```sql
DROP TABLE clientes;
```

**ALTER TABLE**: Modifica a estrutura de uma tabela. Por exemplo, para adicionar uma nova coluna telefone à tabela clientes:

```sql
ALTER TABLE clientes ADD COLUMN telefone VARCHAR(15);
```

**UPDATE**: Atualiza os dados de uma tabela. Exemplo de como alterar o email de um cliente:

```sql
UPDATE clientes SET email \= 'novo\_email@exemplo.com' WHERE nome \= 'Maria Silva';
``` 

**DELETE**: Exclui registros de uma tabela. Exemplo de como excluir um cliente pelo nome:

```sql
DELETE FROM clientes WHERE nome = 'Maria Silva';
```

# Manipulação de Dados

## Comandos de Manipulação de Dados

Aqui, vamos aprender a manipular dados dentro das tabelas do PostgreSQL com comandos mais específicos.

#### Comando UPDATE

O comando UPDATE é usado para modificar dados em uma tabela existente. Você pode alterar um ou mais campos de uma linha de acordo com uma condição.

Exemplo: Atualizando o email de um cliente na tabela clientes:

```sql
UPDATE clientes  
SET email = 'novo_email@exemplo.com'  
WHERE nome = 'Maria Silva';
```

Esse comando atualiza o campo email do cliente onde o nome é "Maria Silva". A cláusula WHERE é essencial para evitar que todos os registros da tabela sejam alterados.

#### Comando DELETE

O comando DELETE serve para excluir registros de uma tabela. Cuidado ao usar esse comando, pois os dados são apagados permanentemente.

Exemplo: Excluindo um cliente da tabela clientes:

```sql
DELETE FROM clientes  
WHERE nome = 'Maria Silva';
```

Esse comando exclui o registro de "Maria Silva" da tabela clientes. Se você omitir a cláusula WHERE, todos os registros da tabela serão excluídos!

#### Comando TRUNCATE

O comando TRUNCATE é usado para excluir todos os registros de uma tabela, mas sem apagar a estrutura da tabela. Diferente do DELETE, o TRUNCATE é mais rápido e não registra as exclusões de maneira detalhada.

Exemplo:

```sql
TRUNCATE TABLE clientes;
```

Isso remove todos os registros da tabela clientes, mas a tabela ainda estará disponível para novos dados.

# Filtrando Dados

Agora, vamos aprender como filtrar dados de forma eficiente com a cláusula WHERE e outros operadores.

## Filtrando com WHERE

A cláusula WHERE permite especificar condições para selecionar apenas os registros que atendem a esses critérios.

Exemplo: Encontrar todos os clientes com mais de 30 anos:

```sql
SELECT \* FROM clientes  
WHERE idade \> 30;
```

### **Operadores Comuns em WHERE**

**BETWEEN**: Usado para filtrar valores dentro de um intervalo.

```sql
SELECT \* FROM clientes  
WHERE idade BETWEEN 20 AND 30;
```

**IN**: Filtra valores que estão dentro de uma lista específica.

```sql
SELECT \* FROM clientes  
WHERE nome IN ('Maria Silva', 'João Souza');
```

**LIKE**: Usado para buscar padrões em dados textuais.

```sql
SELECT \* FROM clientes  
WHERE nome LIKE 'Maria%';
```

**IS NULL**: Filtra registros com valores nulos.

```sql
SELECT \* FROM clientes  
WHERE telefone IS NULL;
```

### **Ordenando e Limitando Resultados**

**ORDER BY**: Ordena os resultados em ordem crescente ou decrescente. Por padrão, a ordenação é crescente (ASC), mas você pode especificar a ordenação decrescente (DESC).

```sql
SELECT \* FROM clientes  
ORDER BY nome DESC;
```

**LIMIT**: Limita o número de registros retornados. Exemplo para obter apenas os 5 primeiros resultados:

```sql
SELECT \* FROM clientes  
LIMIT 5;
```

# Funções Agregadas

Funções agregadas são usadas para realizar cálculos sobre um conjunto de dados, como soma, média e contagem.

**COUNT()**: Conta o número de registros que atendem a uma condição.

```sql
SELECT COUNT(\*) FROM clientes;
```

**SUM()**: Soma os valores de uma coluna numérica.

```sql
SELECT SUM(idade) FROM clientes;
```

**AVG()**: Calcula a média dos valores de uma coluna numérica.

```sql
SELECT AVG(idade) FROM clientes;
```

**MIN()** e **MAX()**: Retorna o menor ou maior valor de uma coluna.

```sql
SELECT MIN(idade) FROM clientes;  
SELECT MAX(idade) FROM clientes;
```

### **Agrupando Dados com GROUP BY**

O GROUP BY é usado para agrupar dados com base em uma coluna e aplicar funções agregadas.

Exemplo: Contando o número de clientes por idade:

```sql
SELECT idade, COUNT(*) FROM clientes  
GROUP BY idade;
```

### **Filtrando Agrupamentos com HAVING**

Após usar GROUP BY, você pode filtrar os resultados agregados usando HAVING.

Exemplo: Mostrar idades que têm mais de 2 clientes:

```sql
SELECT idade, COUNT(*) FROM clientes  
GROUP BY idade  
HAVING COUNT(*) > 2;
```

# Relacionamentos e Normalização

## Chaves Primárias e Estrangeiras

Um banco de dados relacional é composto por tabelas que podem se relacionar entre si. Vamos aprender como criar esses relacionamentos usando **chaves primárias** e **chaves estrangeiras**.

### Chave Primária (Primary Key)

A **chave primária** é um campo (ou conjunto de campos) que identifica de forma única cada registro em uma tabela. Não pode haver valores duplicados nem nulos em uma chave primária.

Exemplo: Vamos criar uma tabela clientes com uma chave primária:

```sql
CREATE TABLE clientes (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    email VARCHAR(100),  
    idade INT  
);
```

O campo id é a chave primária e será único para cada registro da tabela.

### Chave Estrangeira (Foreign Key)

A **chave estrangeira** é um campo (ou conjunto de campos) que estabelece um relacionamento entre duas tabelas. Ela faz referência à chave primária de outra tabela.

Exemplo: Criando uma tabela pedidos que se relaciona com a tabela clientes através da chave estrangeira:

```sql
CREATE TABLE pedidos (  
    id SERIAL PRIMARY KEY,  
    cliente\_id INT,  
    data\_pedido DATE,  
    FOREIGN KEY (cliente\_id) REFERENCES clientes(id)  
);
```

Aqui, o campo cliente_id em pedidos é uma chave estrangeira que faz referência ao campo id de clientes. Isso cria uma relação entre as duas tabelas, garantindo que um pedido sempre esteja vinculado a um cliente existente.

### Relacionamentos entre Tabelas

**Um para Muitos (1:N)**: Um cliente pode fazer muitos pedidos, mas cada pedido pertence a um único cliente.

**Muitos para Muitos (N:M)**: Um exemplo seria uma tabela de alunos e uma tabela de cursos. Um aluno pode se matricular em muitos cursos, e um curso pode ter muitos alunos. Para isso, você cria uma tabela intermediária, como alunos\_cursos.

Exemplo de relacionamento **muitos para muitos**:

```sql
CREATE TABLE cursos (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100)  
);

CREATE TABLE alunos (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100)  
);

CREATE TABLE alunos\_cursos (  
    aluno\_id INT,  
    curso\_id INT,  
    PRIMARY KEY (aluno\_id, curso\_id),  
    FOREIGN KEY (aluno\_id) REFERENCES alunos(id),  
    FOREIGN KEY (curso\_id) REFERENCES cursos(id)  
);
```

### Normalização de Banco de Dados

A **normalização** é o processo de organizar os dados de forma a minimizar redundâncias e melhorar a integridade dos dados. Ela é dividida em várias formas normais, sendo as mais comuns a 1NF, 2NF e 3NF.

### 1NF (Primeira Forma Normal)

Uma tabela está em 1NF quando:

Todos os campos contêm apenas valores atômicos (sem múltiplos valores em uma célula).

Não há duplicação de linhas.

Exemplo: Uma tabela não normalizada poderia ter múltiplos telefones em uma célula, como:

| Cliente | Telefones     |
| :------ | :------------ |
| João    | 123, 456      |

Para normalizar isso, você deve dividir os telefones em registros separados:

| Cliente | Telefone |
| :------ | :--------|
| João    | 123      |
| João    | 456      |


### 2NF (Segunda Forma Normal)

Uma tabela está em 2NF quando:

Está em 1NF.

Todos os atributos não-chave dependem completamente da chave primária (não há dependências parciais).

Exemplo: Suponha que temos uma tabela de pedidos onde a chave primária é composta por id_cliente e id_pedido. Se você armazenar o nome do cliente em cada linha da tabela de pedidos, isso viola a 2NF, pois o nome do cliente depende apenas do id_cliente, e não da chave primária completa. A solução seria separar o nome do cliente em uma tabela à parte.

### 3NF (Terceira Forma Normal)

Uma tabela está em 3NF quando:

Está em 2NF.

Não há dependências transitivas, ou seja, atributos não-chave não devem depender de outros atributos não-chave.

Exemplo: Se você tem uma tabela onde o endereço do cliente é armazenado, e o endereço depende do nome do cliente (não diretamente da chave primária), isso viola a 3NF. Você deve separar o endereço em uma tabela separada.

## Prática de Relacionamentos e Normalização**

**Passo 1**: Crie um banco de dados com pelo menos 3 tabelas.

**Passo 2**: Defina as chaves primárias e estrangeiras.

**Passo 3**: Normaliza a estrutura de dados, se necessário.

# Consultas Avançadas

## Consultas Avançadas

### Joins

Os **joins** são usados para combinar registros de duas ou mais tabelas, com base em uma condição comum. Vamos explorar os tipos mais comuns de joins.

### INNER JOIN

O **INNER JOIN** retorna apenas os registros que têm correspondência em ambas as tabelas.

Exemplo: Vamos unir as tabelas clientes e pedidos, onde o id\_cliente da tabela pedidos corresponde ao id da tabela clientes:

```sql
SELECT clientes.nome, pedidos.data\_pedido  
FROM clientes  
INNER JOIN pedidos ON clientes.id \= pedidos.cliente\_id;
```

Esse comando vai retornar os nomes dos clientes e as datas de seus pedidos, mas apenas para os clientes que têm pedidos registrados.

### LEFT JOIN

O **LEFT JOIN** (ou **LEFT OUTER JOIN**) retorna todos os registros da tabela da esquerda (primeira tabela), e os registros correspondentes da tabela da direita (segunda tabela). Se não houver correspondência, os valores da tabela da direita serão NULL.

Exemplo:

```sql
SELECT clientes.nome, pedidos.data\_pedido  
FROM clientes  
LEFT JOIN pedidos ON clientes.id \= pedidos.cliente\_id;
```

Esse comando retorna todos os clientes, mesmo aqueles que não têm pedidos. Para esses clientes, a coluna data\_pedido será NULL.

### RIGHT JOIN

O **RIGHT JOIN** (ou **RIGHT OUTER JOIN**) é similar ao LEFT JOIN, mas retorna todos os registros da tabela da direita (segunda tabela), e os registros correspondentes da tabela da esquerda (primeira tabela). Se não houver correspondência, os valores da tabela da esquerda serão NULL.

Exemplo:

```sql
SELECT clientes.nome, pedidos.data\_pedido  
FROM clientes  
RIGHT JOIN pedidos ON clientes.id \= pedidos.cliente\_id;
```

Esse comando retorna todos os pedidos, incluindo aqueles feitos por clientes que talvez não estejam mais na tabela clientes (caso tenham sido deletados, por exemplo).

### FULL OUTER JOIN

O **FULL OUTER JOIN** retorna todos os registros quando há uma correspondência em uma das tabelas. Ou seja, ele retorna todos os registros das duas tabelas, e coloca NULL quando não houver correspondência.

Exemplo:

```sql
SELECT clientes.nome, pedidos.data\_pedido  
FROM clientes  
FULL OUTER JOIN pedidos ON clientes.id \= pedidos.cliente\_id;
```

Esse comando retorna todos os clientes e todos os pedidos, independentemente de terem correspondência na outra tabela.


## Subconsultas (Subqueries)

As **subconsultas** são consultas aninhadas dentro de outra consulta. Elas podem ser usadas em várias partes de uma consulta SQL, como na cláusula SELECT, FROM ou WHERE.

### Subconsulta no SELECT

Você pode usar uma subconsulta para retornar um valor para cada linha da consulta principal.

Exemplo:

```sql
SELECT nome,   
       (SELECT COUNT(\*) FROM pedidos WHERE pedidos.cliente\_id \= clientes.id) AS num\_pedidos  
FROM clientes;
```

Esse comando retorna o nome de cada cliente e o número de pedidos que ele fez. A subconsulta conta os pedidos para cada cliente individualmente.

### Subconsulta no WHERE

Você pode usar subconsultas dentro da cláusula WHERE para restringir os resultados de acordo com valores de outra consulta.

Exemplo:

```sql
SELECT nome  
FROM clientes  
WHERE id IN (SELECT cliente\_id FROM pedidos WHERE data\_pedido \> '2025-01-01');
```

Esse comando retorna os nomes dos clientes que fizeram pedidos após 1º de janeiro de 2025\.

### Subconsulta com EXISTS

A palavra-chave **EXISTS** verifica se a subconsulta retorna algum resultado. Se retornar, a consulta externa será executada.

Exemplo:

```sql
SELECT nome  
FROM clientes  
WHERE EXISTS (SELECT 1 FROM pedidos WHERE pedidos.cliente\_id \= clientes.id);
```

Esse comando retorna os nomes dos clientes que têm pelo menos um pedido.

# Consultas Complexas

Agora que já aprendemos os conceitos básicos de joins e subconsultas, vamos combinar esses elementos para criar consultas mais complexas.

## Consultas com Joins e Funções Agregadas

Exemplo: Encontrar o total de pedidos feitos por cada cliente.

```sql
SELECT clientes.nome, COUNT(pedidos.id) AS total\_pedidos  
FROM clientes  
LEFT JOIN pedidos ON clientes.id \= pedidos.cliente\_id  
GROUP BY clientes.nome;
```

Esse comando retorna o nome de cada cliente e o número total de pedidos feitos por ele. Se o cliente não tiver pedidos, o valor será 0\.

## Consultas com GROUP BY e HAVING

Vamos usar GROUP BY e HAVING para filtrar resultados após o agrupamento.

Exemplo: Encontrar os clientes que fizeram mais de 3 pedidos:

```sql
SELECT clientes.nome, COUNT(pedidos.id) AS total\_pedidos  
FROM clientes  
INNER JOIN pedidos ON clientes.id \= pedidos.cliente\_id  
GROUP BY clientes.nome  
HAVING COUNT(pedidos.id) \> 3;
```

Esse comando retorna os nomes dos clientes que fizeram mais de 3 pedidos.

Esses são os conceitos essenciais para criar consultas SQL avançadas usando **joins**, **subconsultas** e funções agregadas. Experimente combinar esses conceitos em suas próprias consultas!

# Indexação e Performance

## O que são índices?

Os **índices** são estruturas de dados usadas para melhorar a velocidade das operações de leitura no banco de dados. Eles funcionam como um índice de um livro: em vez de procurar por informações em cada linha da tabela, o índice permite localizar os dados mais rapidamente.

### Criando um Índice

Você pode criar um índice em uma ou mais colunas de uma tabela. A sintaxe básica para criar um índice é:

CREATE INDEX nome_do_indice ON nome_da_tabela (coluna);

Exemplo: Criando um índice na coluna email da tabela clientes para melhorar a busca por e-mails:

CREATE INDEX idx_email ON clientes (email);

Agora, quando você fizer uma consulta que envolva a coluna email, o PostgreSQL usará esse índice para encontrar os dados mais rapidamente.

### Índice Único (Unique Index)

O índice único garante que os valores na coluna ou nas colunas indexadas sejam únicos. Isso é útil quando você quer garantir que não haja duplicação de valores, como no caso de e-mails.

Exemplo:

```sql
CREATE UNIQUE INDEX idx_email_unico ON clientes (email);
```

Esse comando cria um índice que não permite valores duplicados na coluna email.

### Analisando a Performance das Consultas com EXPLAIN

O comando EXPLAIN permite que você visualize o plano de execução de uma consulta SQL, ou seja, como o PostgreSQL irá buscar os dados para atender sua consulta. Isso é essencial para entender como suas consultas podem ser otimizadas.

### Usando EXPLAIN

Adicione o comando EXPLAIN antes de sua consulta para ver o plano de execução.

Exemplo:

```sql
EXPLAIN SELECT nome, email FROM clientes WHERE idade > 30;
```

O PostgreSQL mostrará informações sobre como ele planeja executar a consulta, como o uso de índices ou a leitura sequencial de dados.

### Interpretando o Plano de Execução

O plano de execução pode incluir os seguintes termos:

**Seq Scan**: Leitura sequencial de dados (sem uso de índice). Normalmente, isso acontece quando não há um índice disponível para a consulta.

**Index Scan**: Uso de um índice para buscar dados, o que é mais eficiente que a leitura sequencial.

**Bitmap Index Scan**: Usa um índice em uma forma mais eficiente, especialmente em consultas complexas.

**Join Types**: O PostgreSQL usa diferentes tipos de join, como Nested Loop, Merge Join e Hash Join.

O uso do EXPLAIN ajuda a identificar pontos onde o PostgreSQL pode estar fazendo leituras ineficientes e onde os índices podem melhorar a performance.

### Estratégias de Particionamento de Tabelas

Quando você lida com grandes volumes de dados, pode ser interessante **particionar** suas tabelas para melhorar o desempenho. O particionamento envolve dividir uma tabela grande em várias tabelas menores (partições).

Existem dois tipos principais de particionamento:

**Particionamento por faixa (Range Partitioning)**: Divide os dados em faixas de valores (por exemplo, por datas).

**Particionamento por lista (List Partitioning)**: Divide os dados com base em uma lista de valores (por exemplo, por região).

### Criando uma Tabela Particionada

Exemplo: Vamos particionar uma tabela vendas por mês.

1. **Criando a tabela principal** (sem dados):

```sql
CREATE TABLE vendas (  
    id SERIAL PRIMARY KEY,  
    data\_venda DATE,  
    valor DECIMAL  
) PARTITION BY RANGE (data\_venda);
```

2. **Criando partições**:

```sql
CREATE TABLE vendas\_2023\_01 PARTITION OF vendas  
    FOR VALUES FROM ('2023-01-01') TO ('2023-02-01');

CREATE TABLE vendas\_2023\_02 PARTITION OF vendas  
    FOR VALUES FROM ('2023-02-01') TO ('2023-03-01');
```

Cada partição armazena os dados para um mês específico. Isso pode melhorar a performance de consultas que filtram dados por mês.

# Procedimentos e Funções

## Procedimentos e Funções

### O que são funções em PostgreSQL?

No PostgreSQL, funções são blocos de código SQL que podem ser reutilizados para realizar tarefas repetitivas ou complexas. Elas ajudam a automatizar processos e melhorar a organização do código.

### Criando uma Função Simples

As funções em PostgreSQL podem ser criadas usando a linguagem **PL/pgSQL**, uma extensão do SQL que permite adicionar lógica de controle (como loops e condicionais).

Aqui está um exemplo de uma função simples que calcula o desconto em um valor de compra:

```sql
CREATE OR REPLACE FUNCTION calcular\_desconto(valor DECIMAL, percentual DECIMAL)  
RETURNS DECIMAL AS $$  
BEGIN  
    RETURN valor \- (valor \* percentual / 100);  
END;  
$$ LANGUAGE plpgsql;
```

Essa função recebe dois parâmetros: valor (o valor da compra) e percentual (o percentual de desconto), e retorna o valor com o desconto aplicado.

### Chamando a Função

Para usar a função, basta chamá-la com os parâmetros necessários:

```sql
SELECT calcular_desconto(1000, 10);  \-- Isso retorna 900
```

### Criando Triggers

Uma **trigger** (ou gatilho) é uma função especial que é automaticamente executada (ou "disparada") quando ocorre um evento específico no banco de dados, como a inserção, atualização ou exclusão de registros.

### Criando uma Trigger

Exemplo: Vamos criar uma trigger que registra quando um cliente é atualizado na tabela clientes.

1. **Função da Trigger**:

```sql
CREATE OR REPLACE FUNCTION log\_alteracao\_cliente()  
RETURNS TRIGGER AS $$  
BEGIN  
    INSERT INTO log\_cliente\_alterado (cliente\_id, data\_alteracao)  
    VALUES (NEW.id, NOW());  
    RETURN NEW;  
END;  
$$ LANGUAGE plpgsql;
```

Essa função insere um registro na tabela log_cliente_alterado toda vez que um cliente for atualizado.

**Definindo a Trigger**:

```sql
CREATE TRIGGER trigger\_alteracao\_cliente  
AFTER UPDATE ON clientes  
FOR EACH ROW  
EXECUTE FUNCTION log\_alteracao\_cliente();
```

A trigger será executada **após** a atualização de um cliente, e registrará a alteração na tabela log\_cliente\_alterado.

### Prática com Funções e Triggers

**Passo 1**: Crie uma função simples que realiza uma operação no banco de dados (como calcular um valor ou fazer uma verificação).

**Passo 2**: Crie uma trigger para registrar ou automatizar uma ação (como uma atualização de log ou validação de dados).

Exemplo prático: Crie uma função que atualize o saldo de um cliente após um pagamento, e uma trigger que registre a data de cada pagamento.

# Backup, Restauração e Segurança

## Backup e Restauração no PostgreSQL

Fazer backups regulares do seu banco de dados é essencial para garantir que você possa restaurar dados em caso de falhas ou problemas.

### Criando um Backup com pg_dump

O pg_dump é a ferramenta do PostgreSQL usada para gerar backups de um banco de dados. Ele cria um arquivo de exportação que pode ser usado para restaurar o banco de dados em caso de necessidade.

Exemplo de backup completo de um banco de dados chamado meu_banco:

```sql
pg_dump meu_banco > backup_meu_banco.sql
```

Isso cria um arquivo backup_meu_banco.sql com o conteúdo do banco de dados, incluindo estrutura das tabelas, dados e outros objetos.

Se você quiser criar um backup apenas de uma tabela específica:

```sql
pg_dump -t minha_tabela meu_banco > backup_tabela.sql
```

### Restaurando um Backup com psql

Para restaurar um banco de dados a partir de um arquivo de backup, você usa o comando psql:

1. Crie o banco de dados (se não existir):

```sql
CREATE DATABASE meu_banco_restaurado;
```

2. Restaure o backup:

```sql
psql meu_banco_restaurado < backup_meu_banco.sql
```

Isso irá aplicar o conteúdo do backup ao banco de dados meu\_banco\_restaurado.

### Backup e Restauração em Ambiente de Produção

Para ambientes de produção, o PostgreSQL também oferece opções para backups incrementais e backups físicos utilizando ferramentas como pg\_basebackup, que cria uma cópia completa do banco de dados em tempo real.

### Controle de Acesso e Permissões

A segurança no PostgreSQL depende do gerenciamento adequado de usuários e permissões. Aqui estão os conceitos principais para controlar o acesso ao banco de dados.

### Criando um Novo Usuário

Para criar um novo usuário no PostgreSQL, você pode usar o comando CREATE USER. Por exemplo, para criar um usuário chamado novo\_usuario com uma senha:

```sql
CREATE USER novo_usuario WITH PASSWORD 'senha_forte';
```

### Atribuindo Permissões

Você pode conceder permissões a usuários para acessar e manipular dados no banco de dados. As permissões comuns incluem:

**SELECT**: Permite ler dados.

**INSERT**: Permite inserir novos dados.

**UPDATE**: Permite atualizar dados existentes.

**DELETE**: Permite excluir dados.

Exemplo: Concedendo permissões de leitura e escrita na tabela clientes para o usuário novo_usuario:

GRANT SELECT, INSERT, UPDATE, DELETE ON clientes TO novo\_usuario;

### Revogando Permissões

Se você precisar remover uma permissão, pode usar o comando REVOKE:

```sql
REVOKE DELETE ON clientes FROM novo_usuario;
```

### Definindo Roles (Funções)

Em vez de conceder permissões individualmente a cada usuário, você pode criar **roles** (funções) que agruparão permissões comuns. Em seguida, você pode atribuir essas roles aos usuários.

Exemplo de criação de uma role com permissões:

```sql
CREATE ROLE gerente;  
GRANT SELECT, INSERT, UPDATE ON clientes TO gerente;
```

Agora, ao criar um usuário, você pode atribuí-lo a essa role:

```sql
CREATE USER novo\_usuario WITH PASSWORD 'senha\_forte';  
GRANT gerente TO novo\_usuario;
```

### Segurança com SSL e Criptografia

Segurança adicional pode ser implementada com o uso de **SSL** (Secure Sockets Layer) e **criptografia** de dados.

### **Configuração de SSL**

O PostgreSQL oferece suporte a conexões seguras usando SSL. Para habilitar o SSL no PostgreSQL, você precisa configurar os arquivos postgresql.conf e pg\_hba.conf.

1. No arquivo postgresql.conf, ative o SSL:

```sql
ssl = on
```

2. No arquivo pg_hba.conf, configure as conexões para exigir SSL:

```txt
hostssl all all 0.0.0.0/0 md5
```

Depois de fazer essas configurações, você precisará reiniciar o servidor PostgreSQL para aplicar as mudanças.

### Criptografia de Dados

Para proteger dados sensíveis, você pode usar a criptografia. O PostgreSQL não oferece criptografia nativa para dados em colunas, mas você pode usar extensões, como o **pgcrypto**, para criptografar dados específicos.

Exemplo de como criptografar um campo usando pgcrypto:

1. Primeiro, instale a extensão:

```sql
CREATE EXTENSION pgcrypto;
```

2. Para criptografar um dado, como um número de cartão de crédito:

```sql
UPDATE clientes  
SET numero\_cartao \= pgp\_sym\_encrypt('1234567890123456', 'minha\_chave\_secreta')  
WHERE id \= 1;
```

Esse comando criptografa o número do cartão de crédito usando a chave fornecida.

# Tópicos Avançados

## Transações e Controle de Concorrência

No PostgreSQL, as **transações** permitem agrupar várias operações em uma única unidade de trabalho, garantindo que todas as operações sejam realizadas com sucesso ou, se ocorrer um erro, nenhuma delas seja aplicada.

### Transações no PostgreSQL

Uma transação começa com o comando BEGIN e termina com COMMIT (se for bem-sucedida) ou ROLLBACK (se ocorrer um erro e você quiser desfazer as operações).

Exemplo de uma transação simples:

```sql
BEGIN;

UPDATE conta SET saldo \= saldo \- 100 WHERE id \= 1;  
UPDATE conta SET saldo \= saldo \+ 100 WHERE id \= 2;

COMMIT;
```

Essas duas operações (transferir 100 unidades de uma conta para outra) são tratadas como uma única transação. Se uma das operações falhar, você pode usar ROLLBACK para desfazer ambas as operações.

### Controle de Concorrência

O PostgreSQL usa **níveis de isolamento** para gerenciar como as transações interagem entre si. Os principais níveis de isolamento são:

1. **READ COMMITTED** (Padrão): Cada transação vê apenas os dados que foram confirmados até o momento.

2. **REPEATABLE READ**: Garante que, dentro de uma transação, as leituras de dados sejam consistentes, mesmo que outras transações alterem os dados.

3. **SERIALIZABLE**: O nível mais alto de isolamento, garantindo que as transações sejam executadas como se fossem feitas uma por vez (sem concorrência real).

Exemplo de como definir o nível de isolamento:

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

### Locking (Bloqueios)

O PostgreSQL usa **bloqueios** para evitar que várias transações alterem os mesmos dados simultaneamente. Dependendo do nível de isolamento, o PostgreSQL pode bloquear uma linha ou tabela inteira enquanto uma transação a está modificando.

Exemplo:

```sql
BEGIN;

UPDATE conta SET saldo = saldo - 100 WHERE id = 1;  
-- A linha da conta 1 é bloqueada para outras transações até o commit

COMMIT;
```

### Views e Materialized Views

As **views** são consultas armazenadas no banco de dados que podem ser usadas como se fossem tabelas. Elas não armazenam dados, apenas a consulta que será executada quando a view for acessada.

### Criando uma View

Exemplo de criação de uma view para mostrar o saldo total de cada cliente:

```sql
CREATE VIEW saldo_cliente AS  
SELECT cliente_id, SUM(valor) AS total_saldo  
FROM transacoes  
GROUP BY cliente_id;
```

Você pode consultar a view como se fosse uma tabela:

```sql
SELECT \* FROM saldo\_cliente;
```

### Materialized Views

Ao contrário das views comuns, as **materialized views** armazenam o resultado da consulta, melhorando o desempenho em consultas frequentes. No entanto, elas não são atualizadas automaticamente. Para atualizar a materialized view, você precisa usar o comando REFRESH MATERIALIZED VIEW.

Exemplo de criação de uma materialized view:

```sql
CREATE MATERIALIZED VIEW saldo\_cliente\_materializado AS  
SELECT cliente\_id, SUM(valor) AS total\_saldo  
FROM transacoes  
GROUP BY cliente\_id;
```

Para atualizar a materialized view:

```sql
REFRESH MATERIALIZED VIEW saldo_cliente_materializado;
```

### Extensões no PostgreSQL

O PostgreSQL possui uma arquitetura de extensões muito flexível, permitindo que você adicione funcionalidades extras ao banco de dados, como suporte a dados geoespaciais, busca de texto completo, criptografia, entre outras.

### PostGIS: Dados Geoespaciais

O **PostGIS** é uma extensão que permite trabalhar com dados geoespaciais no PostgreSQL, como coordenadas de latitude e longitude.

Para instalar o PostGIS, basta executar:

```sql
CREATE EXTENSION postgis;
```

Após isso, você pode começar a trabalhar com tipos de dados geoespaciais, como **POINT**, **LINESTRING**, **POLYGON**, etc.

Exemplo de como criar uma tabela para armazenar coordenadas geográficas:

```sql
CREATE TABLE locais (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    coordenadas GEOMETRY(Point, 4326\)  
);
```

### pg\_trgm: Busca de Texto

A extensão **pg\_trgm** permite realizar buscas de texto mais eficientes, utilizando trigramas (sequências de três caracteres).

Para instalar o pg\_trgm:

```sql
CREATE EXTENSION pg\_trgm;
```

Isso permite fazer buscas eficientes em colunas de texto com funções como LIKE e ILIKE.

Exemplo de consulta que usa pg\_trgm para encontrar palavras semelhantes:

```sql
SELECT \* FROM produtos  
WHERE nome % 'laptop';
```

### Otimização Avançada e Tuning

A otimização de consultas no PostgreSQL pode ser complexa, mas algumas técnicas podem melhorar significativamente o desempenho.

### Usando EXPLAIN ANALYZE

O EXPLAIN ANALYZE fornece um plano de execução real, mostrando como a consulta foi realmente executada, incluindo o tempo gasto em cada parte da consulta.

Exemplo:

```sql
EXPLAIN ANALYZE SELECT \* FROM clientes WHERE idade \> 30;
```

Isso retornará detalhes sobre o tempo de execução e como o PostgreSQL encontrou os dados (usando índice, varredura sequencial, etc.).

### Vacuuming e Análises de Tabelas

Com o tempo, o PostgreSQL pode acumular dados "mortos" (registros que foram excluídos ou atualizados), o que pode afetar o desempenho. O comando **VACUUM** ajuda a limpar esses dados e otimizar o banco de dados.

Para executar o vacuum manualmente:

```sql
VACUUM;
```

Você também pode executar uma **análise** para atualizar as estatísticas de desempenho do banco:

```sql
ANALYZE;
```

# Projeto Prático

## Escolha de um Projeto e Planejamento

Agora que você adquiriu todos os conhecimentos necessários para trabalhar com PostgreSQL, é hora de aplicar tudo o que aprendeu em um projeto prático. Um bom projeto pode ser a chave para consolidar os conceitos e ganhar confiança no uso do PostgreSQL.

### Passo 1: Escolha de um Projeto
Escolha um projeto que tenha um desafio real e que permita explorar os conceitos que você aprendeu. Aqui estão algumas sugestões de projetos:

1. **Sistema de Gerenciamento de Estoque**:

   * Tabelas para produtos, fornecedores, categorias e transações de venda.

   * Relacionamentos entre produtos e categorias, transações de venda e clientes.

   * Funcionalidade para calcular o estoque disponível e registrar compras e vendas.

2. **Sistema de Gerenciamento de Biblioteca**:

   * Tabelas para livros, autores, membros e empréstimos.

   * Relacionamentos entre livros e autores, e empréstimos feitos por membros.

   * Funcionalidades para calcular multas, gerenciar o histórico de empréstimos e controlar a disponibilidade de livros.

3. **Sistema de Cadastro de Clientes e Pedidos**:

   * Tabelas para clientes, produtos, pedidos e itens de pedidos.

   * Relacionamento entre clientes e pedidos, e entre pedidos e produtos.

   * Implementar a funcionalidade de acompanhamento de status dos pedidos e calcular o total de vendas.

**Passo 2: Planejamento do Projeto**  
 Antes de começar a codificar, planeje a estrutura do seu banco de dados. Comece com os seguintes passos:

* **Defina as tabelas principais** do sistema (por exemplo, clientes, pedidos, produtos, etc.).

* **Determine os relacionamentos** entre as tabelas (por exemplo, um cliente pode ter vários pedidos, um pedido pode ter vários produtos, etc.).

* **Escolha os tipos de dados** adequados para cada campo (por exemplo, VARCHAR para texto, INT para números inteiros, DATE para datas).

* **Crie um diagrama de ER** (Entidade-Relacionamento) para visualizar a estrutura do banco de dados e os relacionamentos.

### Implementação do Projeto

Agora, você deve começar a criar as tabelas e relações no PostgreSQL. Aqui está um exemplo de como pode começar, usando o projeto de **Sistema de Gerenciamento de Biblioteca** como base.

1. **Criando Tabelas**:

```sql
\-- Tabela de autores  
CREATE TABLE autores (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    nacionalidade VARCHAR(50)  
);

\-- Tabela de livros  
CREATE TABLE livros (  
    id SERIAL PRIMARY KEY,  
    titulo VARCHAR(255),  
    autor\_id INT,  
    ano\_publicacao INT,  
    categoria VARCHAR(50),  
    FOREIGN KEY (autor\_id) REFERENCES autores(id)  
);

\-- Tabela de membros  
CREATE TABLE membros (  
    id SERIAL PRIMARY KEY,  
    nome VARCHAR(100),  
    email VARCHAR(100)  
);

\-- Tabela de empréstimos  
CREATE TABLE emprestimos (  
    id SERIAL PRIMARY KEY,  
    livro\_id INT,  
    membro\_id INT,  
    data\_emprestimo DATE,  
    data\_devolucao DATE,  
    FOREIGN KEY (livro\_id) REFERENCES livros(id),  
    FOREIGN KEY (membro\_id) REFERENCES membros(id)  
);
```

2. **Inserindo Dados**:

```sql
\-- Inserindo autores  
INSERT INTO autores (nome, nacionalidade) VALUES  
('J.K. Rowling', 'Britânica'),  
('George Orwell', 'Britânica');

\-- Inserindo livros  
INSERT INTO livros (titulo, autor\_id, ano\_publicacao, categoria) VALUES  
('Harry Potter e a Pedra Filosofal', 1, 1997, 'Fantasia'),  
('1984', 2, 1949, 'Distopia');

\-- Inserindo membros  
INSERT INTO membros (nome, email) VALUES  
('Ana Silva', 'ana@exemplo.com'),  
('Carlos Souza', 'carlos@exemplo.com');

\-- Inserindo empréstimos  
INSERT INTO emprestimos (livro\_id, membro\_id, data\_emprestimo, data\_devolucao) VALUES  
(1, 1, '2025-09-10', '2025-09-20'),  
(2, 2, '2025-09-12', '2025-09-22');
```

3. **Consultas e Funcionalidades**:  
Depois de criar as tabelas e inserir dados, você pode realizar consultas para verificar o funcionamento do seu banco de dados.

Exemplo de consulta para listar os livros emprestados:

```sql
SELECT livros.titulo, membros.nome, emprestimos.data\_emprestimo, emprestimos.data\_devolucao  
FROM emprestimos  
INNER JOIN livros ON emprestimos.livro\_id \= livros.id  
INNER JOIN membros ON emprestimos.membro\_id \= membros.id;
```

Esse comando retorna a lista de livros emprestados, juntamente com os membros que os pegaram e as datas de empréstimo e devolução.

### Conclusão do Projeto

você deve ter um sistema funcional no PostgreSQL que realiza as operações necessárias para o seu projeto (como inserção, atualização, consulta e exclusão de dados).

Aqui estão algumas dicas para tornar o projeto ainda mais interessante:

**Adicione restrições de integridade**: Garanta que dados inconsistentes não possam ser inseridos no banco (por exemplo, um livro não pode ser emprestado se não estiver disponível).

**Crie procedimentos armazenados ou triggers** para automatizar algumas operações (por exemplo, atualizar o status de um livro quando ele for emprestado ou devolvido).

**Use funções agregadas**: Para calcular o número total de livros emprestados ou o número de membros ativos.

# Conclusão

Parabéns por chegar até aqui! Você passou por todos os estágios necessários para aprender PostgreSQL de forma completa, desde os conceitos básicos até a aplicação prática em um projeto real.



