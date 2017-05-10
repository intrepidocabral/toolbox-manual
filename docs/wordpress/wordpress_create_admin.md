# Criar usuário Admin através do banco de dados

É possível criar um usuário com permissão de administrador no Wordpress através do banco de dados utilizando a query abaixo, substituindo `[name]`, `[username]` e `[password]` pelos respectivos valores.


```
mysql> INSERT INTO `wp_users` (`user_login`, `user_pass`, `user_nicename`, `user_email`, `user_url`, `user_registered`, `user_activation_key`, `user_status`, `display_name`)
VALUES ('[username]', MD5('[password]'), '[name]', 'email@email.com', 'http://www.site.com/', '2011-06-07 00:00:00', '', '0', '[name]');

mysql> INSERT INTO `wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`)
VALUES (NULL, (select id from wp_users where user_login = '[username]'), 'wp_capabilities', 'a:1:{s:13:"administrator";s:1:"1";}');

mysql> INSERT INTO `wp_usermeta` (`umeta_id`, `user_id`, `meta_key`, `meta_value`)
VALUES (NULL, (select id from wp_users where user_login = '[username]'), 'wp_user_level', '10');
```

Verificar se o banco de dados está utilizando o prefixo padrão do wordpress no nome das tabelas `wp_`. Caso o prefixo não seja `wp_` é necessário alterar na query.

É possível listar as tabelas utilizando o comando `SHOW TABLES`.
