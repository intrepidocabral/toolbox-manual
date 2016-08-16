## Usando GIT com chave no github

0 - Verifique se você já tem uma chave criada. Se tiver, você tem de saber a senha dela. Se não tiver, crie uma. Se tiver e não souber a senha, pode criar uma nova também. O comando abaixo mostra se há alguma chave criada (arquivo .pub é a chave pública)
```
[18:34 system@system .ssh] > ls -la ~./.ssh
total 24K
drwx------  2 system system 4,0K Ago 16 18:34 .
drwxr-xr-x 55 system system 4,0K Ago 16 14:45 ..
-rw-------  1 system system 1,8K Ago 16 18:34 id_rsa_robertkapa_desktop
-rw-r--r--  1 system system  395 Ago 16 18:34 id_rsa_robertkapa_desktop.pub
-rw-r--r--  1 system system 6,1K Ago 16 18:27 known_hosts
```

1 - Crie um par de chaves, caso não tenha ou caso tenha perdido a senha
```
$ ssh-keygen -t rsa
```

Estas chaves vão ficar no seu diretório /home/usuario/.ssh.

2 - Copie a chave pública para o github

De o comando cat no arquivo da chave pública e você irá ver um resultado como esse. 
```
[18:39 system@system .ssh] > cat id_rsa_robertkapa_desktop.pub 
ssh-rsa ALAHAUFHIFUAHIFAJFDLKDJFÇFJLKJKGLSFDGJ938743985714895NALAHAUFHIFUAHIFAJFDLKDJFÇFJLKJKGLSFDGJ938743985714895NALAHAUFHIFUAHIFAJFDLKDJFÇFJLKJKGLSFDGJ938743985714895N system@system
```

Logado no github, no painel, procure o settings de seu profile. Vá na opção ssh e coloque uma "new ssh key": https://github.com/settings/ssh

3 - Na pasta do projeto, execute a seguinte linha:

```
git remote set-url origin git@github.com:<Username>/<Project>.git
```

4 - Pronto! Tente dar um push no repositório e você verá que o github pede a senha da chave e não pede mais seu usuário. Isso da primeira vez, depois quando você der git push ele não pede nem a senha da chave. 

