
## Login e conexão com base

#### Login usando socket (peer)


```
$ psql
user=>
```

#### Logar usando usuário e senha

Para logar usando root e um usuário específico e uma base. Esse método irá exigir senha: 

```
# sudo -u NOME-DO-USUARIO psql NOME-DA-BASE
```

Para logar com um usuário específico:
  $ psql -h <host> -p <port> -U <username> -W <password> <database>


#### Conecta numa base específica:

Depois de logado, é possível usar o comando:

```
user=> \connect database_name
```

#### Logout
```
$ \q
```

#### Tabelas

* listar todas as bases de dados, depois de logado:
```
    \list ou \l
```

* listar todas as tabelas dentro de uma base, depois de logado:
```
    \dt
```

* listar todas as colunas de uma tabela, depois de conectado a uma base:
```
  \d+ nome-da-coluna;
```

* listar todas as bases de dados, depois de logado:
```
    \list ou \l
```


* listar todas as tabelas dentro de uma base, depois de logado:
```
    => \dt
```

* listar todas as colunas de uma tabela, depois de conectado a uma base:
```
  => \d+ nome-da-coluna;
```

## Seleção de dados

Depois de logado numa determinada base de dados, fazer uma seleção é muito fácil! Para ver todos os registros de uma tabela, basta digitar: 
```
  => select * from NOME-TABELA1;
```

Para selecionar a partir de alguma(s) determinada(s) coluna(s), você pode tentar:

```
  => select nome-coluna1, nome-coluna2 from nome-da-tabela;
```

* Para ordenar: 
```
  => select NOME-COLUNA1, NOME-COLUNA2 from NOME-TABELA1 order by NOME-COLUNA3;
```

Para copiar o resultado de uma seleção, use o \copy: 
```
  $ \copy (select * from NOME-COLUNA order by accounts_timtecuser) to '/home/timtec-ifsul/user.csv' with csv;
```

Se o objetivo for selecionar a partir de uma referencia pré-conhecida, você pode usar o where:

```
  select * from NOME-TABELA1 where CAMPO-TABELA1 = 'NUMERO-OU-STRING';
```

Ou ainda buscar por um trecho inicial ou final. Aqui estamos buscando todos os nome que começam com a letra p: 

```
  select * from NOME-TABELA1 where NAME LIKE 'p%';
```

Seleção por data: 

```
  SELECT * FROM coluna1 WHERE create_timestamp <= '2015-12-14';
```

Selecionando multiplos registros: 

```
  SELECT * FROM NOME-TABELA1 WHERE CAMPO-TABELA1 in (1, 2, 5);
```

Selecionando com range numerico:


```
  select id, name from NOME-DA-TABELA where NOME-DO-CAMPO between 1500 AND 2100;
```

## Criando um usuário

```
  # sudo -u postgres createuser -d nome-do-user
```

Create a user with a password:

```
  CREATE USER davide WITH PASSWORD 'jw8s0F4';
```

Create a user with a password that is valid until the end of 2004. After one second has ticked in 2005, the password is no longer valid.

```
   CREATE USER miriam WITH PASSWORD 'jw8s0F4' VALID UNTIL '2005-01-01';
```

Create an account where the user can create databases:

```
  CREATE USER manuel WITH PASSWORD 'jw8s0F4' CREATEDB;
```

## Dump

Para fazer dump de uma base inteira para um arquivo .sql vc pode usar o comando:

```
  pg_dump dbname > outfile
```

Para recuperar o dump, user este comando: 

```
  psql dbname < infile
```

## Escrita

```
  UPDATE nome-da-tabela set campo-da-tabela='dado a ser escrito' where id = '2';
```

## Gerando uma saída CSV

```
  \copy (select * from agent a inner join usr u on u.id = a.user_id where a.name='') to '~/2016_04_logins_em_branco.csv' with csv
```

== Remover registros duplicados ==

```
  DELETE FROM tablename
  WHERE id IN (SELECT id
              FROM (SELECT id,
                             ROW_NUMBER() OVER (partition BY column1, column2, column3 ORDER BY id) AS rnum
                     FROM tablename) t
              WHERE t.rnum > 1);
```

Remover duplicados por linha:

```
  delete
  from NOME-DA-TABELA
  where id in (
    select
        id
    from (  select 
                id,
                ROW_NUMBER() over (partition by email order by last_login desc) n
            from ifs_ifuser u1 
            where exists (  select 1 from ifs_ifuser 
                            where email = u1.email and id <> u1.id)
        ) t
    where n > 1
  );
```

## Gerando documentação 

É comum ser necessário gerar documentação do tipo UML ou data dictionary a partir de um schema.sql ou gerar um schema.sql a partir de um modelo de uml estruturado. Para isso você pode usar o [[Postgres - Autodoc]].

## Referências 
* http://www.postgresql.org/docs/9.1/static/backup-dump.html



