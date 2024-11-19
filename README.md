
# Passo a passo: Criação de um banco de dados

Tutorial de como criar um banco de dados SQL que organiza as informações de 'livros', 'editora', 'autores' e 'assuntos'. Este guia será dividido em etapas para demonstrar desde a criação de tabelas, chaves e até manipulação/consulta de dados.

## Resumo de uma estrutura SQL
* __CREATE__ - Para criar banco de dados

* __ALTER__ - Modificar e alterar colunas

* __DROP__ - Para remover tabelas e banco

* __INSERT__ - Inserir  os dados na tabela

* __UPDATE__ - Atualiza registros

* __DELETE__ - Remover registro

* __SELECT__ - Para Consultar e visualizar dados

## Passo 1: criação do Banco de Dados e das Tabelas
#### 1.1 Criando o DB
```SQL
CREATE DATABASE biblioteca;
USE biblioteca;
```

#### 1.2 Criando a tabela 'editora'
```SQL
CREATE TABLE editora(
    id_editora INT PRIMARY KEY AUTO_INCREMENT,
    nome_editora VARCHAR(100) NOT NULL,
    pais VARCHAR(50)
);
```

#### 1.3 Criando a tabela 'autor'
```SQL
CREATE TABLE autor(
    id_autor INT PRIMARY KEY AUTO_INCREMENT,
    nome_autor VARCHAR(200),
    data_nascimento DATE
);
```

#### 1.4 Criando a tabela'assunto'
```SQL
CREATE TABLE assunto (
    id_assunto INT PRIMARY KEY AUTO_INCREMENT,
    descricao_assunto VARCHAR(500) NOT NULL
);
```

#### 1.5 Criando a tabela 'livro'
```SQL
CREATE TABLE livro (
    id_livro INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(150) NOT NULL,
    ano_publicacao YEAR,
    editora INT,
    autor INT, 
    assunto INT,
    FOREIGN KEY(editora) REFERENCES editora(id_editora),
    FOREIGN KEY(autor) REFERENCES autor(id_autor),  
    FOREIGN KEY(assunto) REFERENCES assunto(id_assunto)
);
```

#### 1.6 Criando tabela EXTRA
A tabela EXTRA vai servir para exemplificar a exclusão

```SQL
CREATE TABLE extra(
    id INT PRIMARY KEY AUTO_INCREMENT,
    produtos VARCHAR(50),
    quantidade INT(20),
    preco DOUBLE NOT NULL
);
```

## Passo 2: editar tabelas usando 'ALTER'
Após a criação da tabela, podemos adicionar novos campos. Vamos adicionar uma coluna 'email' na coluna 'autor'

```SQL
ALTER TABLE autor
ADD COLUMN email VARCHAR(100);`
```
## Passo 3: remover tabela usando 'DROP'
Se precisar remover uma tabela usamos o comando 'DROP'.
Neste exemplo vamos remover a tabela extra.

```SQL
DROP TABLE extra;`
```

## Passo 4: Inserir dados usando 'INSERT'
Agora que as tabelas estão prontas, vamos inserir dados nelas.

#### 4.1 inserindo dados na tabela 'editora'
```SQL
INSERT INTO editora (nome_editora, pais) VALUES
('Editora Intrinseca', 'Brasil'),
('Editora Geografica', 'Brasil'),
('Editora Beta', 'Portugal')
;
```

#### 4.2 inserindo dados na tabela 'autor'
```SQL
INSERT INTO autor(nome_autor, data_nascimento, email) VALUES
('Jorge Amado', '1912-08-10','jorginho@email.com'),
('Machado de Assis', '1939-06-21','machadinho@email.com'),
('Suzanne Collins', '1962-08-10', 'suzannetordo@email.com'),
('Rick Riordan','1964-06-05', 'peixinhodourado@email.com');
```
#### 4.3 inserindo dados na tabela 'assunto'
```SQL
INSERT INTO assunto(descricao_assunto) VALUES
('Aventura'),
('Romance'),
('Terror'),
('Fantasia');
```

#### 4.4 inserindo dados na tabela 'editora'
```SQL
INSERT INTO livro (titulo, ano_publicacao, editora, autor, assunto) VALUES
('Capitães de Areia', 1937, 2, 1, 1 ),
('Jogos Vorazes', 2008, 1, 3, 1),
('Percy Jackson', 2005, 2, 4, 4 ),
('Memorias Postumas de Bras Cubas', 1881, 3, 2, 2 );
```

## Passo 5: atualizando os dados usando 'UPDATE'
Podemos atualizar os dados com o comando UPDATE.
Vamos corrigir a data de publicação do livro 'Capitães de Areia'.

```SQL
UPDATE livro
SET ano_publicacao = 1938;
WHERE titulo = 'Capitães da Areia`;
```

### Passo 6: Excluindo os dados usando 'DELETE'
Para remover os registros de uma tabela usamos o comando 'DELETE'.
Vamos excluir o livro Memorias Postumas de Bras cubas'.

```SQL
DELETE FROM livro
WHERE id_livro = 8;
```
#### Passo 6.1: Excluir tudo da tabela sem o id
```SQL
DELETE FROM livro
```

## Passo 7:Consultando os dados usando 'SELECT'
É possivel selecionar os dados para visualizar da forma como quiser.
Para isso usamos o comando 'SELECT'

#### Passo 7.1:Selecionar todos os livros com suas editoras e autores
Vamos usar dados das tabelas 'livros', 'editora', 'autor' e ' assunto' usando o comando 'JOIN'

```SQL
DELETE FROM livro
WHERE id_livro = 8;
SELECT livro.titulo AS nome, 
editora.nome_editora AS editora, 
autor.nome_autor AS autor, 
assunto.descricao_assunto AS tema, 
livro.ano_publicacao AS ano
FROM livro
JOIN editora ON livro.editora = editora.id_editora
JOIN autor ON livro.autor = autor.id_autor
JOIN assunto ON livro.assunto = assunto.id_assunto;
```
