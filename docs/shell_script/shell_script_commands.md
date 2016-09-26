Este artigo traz uma lista de comandos básicos usados para controlar alguns dos programas essenciais dos sistemas GNU/Linux. Aprenda-os e você conseguirá usar seu sistema de modo muito mais fácil, útil e rápido, resolvendo problemas ou criando soluções para facilitar seu trabalho. 

Todo comando é necessariamente uma ordem a um programa que compõe o sistema e todo comando, desde o mais simples ao mais complexo, nos sistemas GNU/Linux atua dizendo o que um determinado programa deve ou não deve fazer, daí o nome comando. 

Vamos usar como exemplo o interpretador de comandos Bash. O bash é um interpretador de comandos, uma espécie de tradutor entre o sistema operacional e o usuário, normalmente conhecido como shell. Permite a execução de seqüências de comandos direto no prompt do sistema ou escritas em arquivos de texto, conhecidos como shell scripts. O comando mais util do bash para acompanhar os demais comandos abaixo e' o history, que mostra a historia de comandos digitados. 

O sistema usado como modelo é o Debian Lenny com interface gráfica gnome. Para usar o interpretador de comandos em um sistema com interface gráfica, você poderá proceder de três maneiras. Escolha a forma: 
Tecle alt + F2 e digite gnome-terminal. Um prompt de comandos irá se abrir;
Menu do sistemas vá para “aplicações” > “acessórios” > “terminal”;
Tecle ctrl + alt + F1(ou F2, F3...até F6. Para voltar ao modo gráfico tecle F7).

É importante lembrar que boa parte dos comandos aqui descritos só podem ser executados com permissão de root.

## Comandos para Shell Script

### Usuários e Grupos

### adduser

Adiciona um usuário novo no sistema

```
usuario-sistema@debian:/$ adduser jose
Adding user 'jose' ...
Adding new group `jose' (1004) ...
Adding new user `jose' (1003) with group 'jose' ...
Creating home directory `/home/jose' ...
Copying files from `/etc/skel' ...
Digite a nova senha UNIX: *****
Redigite a nova senha UNIX: ******
passwd: senha atualizada com sucesso
Modificando as informações de usuário para jose
Informe o novo valor ou pressione ENTER para aceitar o padrão
       Nome Completo []: José Silva
       Número da Sala []:
       Fone de Trabalho []:
       Fone Doméstico []:
       Outro []:
Is the information correct? [Y/n] y
```

#### deluser

### addgroups

Adiciona um grupo novo no sistema

```
root@debian-servidor:/# addgroup teste
Adding group `teste' (GID 1003) ...
Concluído.
root@debian-servidor:/#
```

#### cat

Le o conteúdo de um arquivo e exibe na tela

```
root@debian-servidor:/# cat /etc/apt/sources.list
deb http:// security.debian.org/ lenny/updates contrib main
deb-src http:// security.debian.org/ lenny/updates contrib main
deb http:// ftp.br.debian.org/debian lenny main contrib non-free
deb-src http:// ftp.br.debian.org/debian lenny main contrib non-free
deb-src http:// ftp.br.debian.org/debian-multimedia/ stable main
deb http:// ftp.br.debian.org/debian-multimedia/ stable main
root@debian-servidor:/#
```

#### cd

#### chfn

#### chmod 

#### clear

#### cp

#### date


#### df	
#### dmesg	
#### dnsdomainname	
#### du	
#### echo	
#### find	
#### finger	
#### free

## grep

Buscando uma string dentro de um conjunto de arquivos: 

```
  grep -R [string buscada] [diretório base]
```

Exemplos:

```
  grep -R  "Meu Texto" ./

  grep -R  "texto procurado" "/home/A Minha Pasta"
```

O resultado da busca será cada ocorrência do texto em cada arquivo encontrado, o que poderá gerar um pouco de repeteco. Podemos melhorar isto com uma abordagem que achei em um fórum, que é o recorte da saída de cada ocorrência, a fim de captar somente o nome do arquivo onde o texto está, e então fazer um agrupamento. Segue o comando:

```
  grep -R  "Meu Texto" /home/blablabla/ | cut -d: -f1 | uniq
```

* Neste caso, o “cut” será do início do texto até o sinal de “:” (definido por “-d:“) e a primeira parte do texto (definida por -f1) será agrupada por uniq.

Referência: 

* http://www.vivaolinux.com.br/dica/Localizar-arquivo-contendo-texto-especificado-no-Linux

groupdel	
groups	
halt	
head	
hostname	
id	
ifconfig	
ifdown	
ifup	
jobs	
kill	
killall	
killall5	
less	
ln	
locate	
logname	
ls	
lsmod	

#### Como tornar um arqui .sh executável:

```
cd /caminho/arquivo
chmod +x arquivo.sh
./arquivo.sh
```

## Referências

* https://tmuxcheatsheet.com/
