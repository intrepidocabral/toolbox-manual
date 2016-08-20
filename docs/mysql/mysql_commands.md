Nota: depois dos comandos, não esqueça de colocar ; (ponto e vírgula) para fazer efeito. 

## Entrando e saindo do Mysql
```
 # mysql -u nome_do_usuario -p 
```

O prompt vai ficar assim: 
```
 # mysql>
```

para sair basta usar o exit: 
```
 # mysql> exit + enter
```

=== Criando novo usuário ===

Com usuário root:

 # mysql> CREATE USER 'nome-do-usuario'@'localhost' IDENTIFIED BY 'senha-senha-senha';

=== Criando uma base de dados ===

 # mysql> create database nome_da_base;

=== Selecionar banco ===

 # mysql> USE nome_do_banco;

=== Mostrar tabelas ===

 # mysql> show tables;

=== Criando tabela ===

 # mysql> create TABLE endereco (
 id_endereco smallint NOT NULL,
 rua varchar(100) NOT NULL,
 bairro varchar(25) NOT NULL,
 cidade varchar(25),
 primary key(id_endereco)
 );

=== Visualizar colunas da tabela ===

 # mysql> DESC endereco;

=== Inserindo coluna na tabela ===

 # mysql> ALTER TABLE endereco ADD pais varchar(25);

=== Remover chave primária da tabela ===

# mysql> ALTER TABLE endereco DROP primary key; Inserindo chave primária na tabela:

# mysql> ALTER TABLE endereco ADD PRIMARY KEY(id_endereco);

=== Modificar definições de uma coluna ===

 # mysql> ALTER TABLE endereco MODIFY bairro varchar(50);

=== Excluir coluna da tabela ===

 # mysql> ALTER TABLE endereco DROP cidade;

=== Renomear tabela ===

 # mysql> ALTER TABLE endereco RENAME localizacao;

=== Deletar uma tabela ===

 # mysql> DROP TABLE localizacao;

=== Deletar uma base de dados ===

 # mysql> DROP DATABASE nome_da_base;

=== Backup de base de dados ===

  # mysqldump -u usuario_da_base -p nome_da_base > nome_da_base.sql

Restauração da base: 

  # mysql -u root -p [database_name] < dumpfilename.sql

[[Categoria:Mysql]]
[[Categoria:Linux]]

