## Migração de página wordpress

### Importar Tema Wordpress
Primeiramente instalamos o FileZilla na máquina para fazer o download da página wordpress na máquina virtual.
```
$ sudo apt install filezilla
```
Com o programa já aberto no campo 'Host' inserimos o host da página (url/ip)

* No caso Host: https://awc.institutotim.org.br

No KeePassX em ssh (servidor) encontramos o usuário do servidor e a senha

* User: <b>user</b>
* Senha: <b>****</b>
* Porta: <b>22</b> (padrão)

No menu inferior teremos 4 abas, as da esquerda são o conjunto local e as da direita o conjunto do conteúdo remoto (no servidor).

Na aba <b>"Endereço remoto"</b> iremos navegar pelos arquivos dentro do servidor".<br>
O que nos interessa no momento é o tema wordpress, para encontrá-lo seguiremos o seguinte caminho:
```
/var/www/awc.institutotim.org.br/wp-content/themes
```
Agora que encontramos a pasta do tema que precisamos, no endereço local selecionamos a pasta para onde vamos enviar este aquivo.
```
vagrant_.../vagrant
```
Clicar e arrastar o arquivo theme e aguardar o download ser finalizado<br>
<b>PRONTO</b> o tema já está disponível no Dashboard do Wordpress e é só habitá-lo

### Exportar e importar a base de dados
Primeiramente devemos fazer login no servidor via terminal, mas como fazer isso?
```
$ ssh user@host
```
* Em caso de dúvida, as informações poderão estar presentes no KeePassX

Mas como encontraremos essas informações par inserir no comando? Damos um cat no arquivo wp-config.php.
```
$ cat /var/www/html/wp-config.php
```
Agora procuremos o bloco de configurações do banco de dados:
```
/** The name of the database for WordPress */

define('DB_NAME', 'db_name');

/** MySQL database username */

define('DB_USER', 'db_user');

/** MySQL database password */
define('DB_PASSWORD', 'db_password');

/** MySQL hostname */
define('DB_HOST', 'db_host');
```
Agora que temos os dados do banco, vamos importar o arquivo .sql com os dados da aplicação:
```
$ mysqldump -h wp_host -u wp_user -p db_name > yyyy_MM_dd_database_nome.sql
```
O arquivo .sql foi gerado, ou seja, o arquivo foi exportado.<br>
Para importá-lo, dar o comando CTRL + D para sair do servidor, voltar para nossa máquina e selecionar a pasta destino para o arquivo .sql
```
mysql -h meu_host -u meu_user -pminha_senha --default_character_set utf8 meu_banco < yyyy_MM_dd_database_nome.sql
```
### FINALIZADO
