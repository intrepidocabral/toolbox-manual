## Conectando com servidor remoto

```
  $ ssh nome-do-usuario@endereco-do-servidor
```

Exemplo: 

```
  $ ssh linux@uol.com.br
```

## Upload de arquivos 

```  
  $ scp /diretorio_de_origem/arquivo.formato usuario_do_servidor@192.168.0.1:/diretorio_do_arquivo/destino/
```

## Verificando fingerprint

O comando de verificação de fingerprint de uma máquina seria esse:

```
  # ssh-keygen -lf /etc/ssh/ssh_host_ecdsa_key.pub
```

Lembrando que ssh_host_ecdsa_key.pub é a chave pública mais usada, mas existem outras. 

* http://www.howtogeek.com/74827/learn-the-ins-and-out-of-openssh-on-your-linux-pc/

## SSHFS 

* https://wiki.archlinux.org/index.php/Sshfs


Muitas vezes criamos chaves criptográficas assimétricas com o OpenSSL e com o OpenSSH. No momento da criação de tais chaves, são solicitadas senhas para as mesmas. A dúvida é a seguinte: como proceder para trocar tais senhas?

## Changing a Passphrase with ssh-keygen 

The -p option requests changing the passphrase of a private key file instead of creating a new private key. The program will prompt for the file containing the private key, for the old passphrase, and twice for the new passphrase. Use -f {filename} option to specifies the filename of the key file. For example, change directory to $HOME/.ssh. Open the Terminal app and then type:

```
  $ cd ~/.ssh/
```

To change DSA passphrase, enter:

```
$ ssh-keygen -f id_dsa -p
```

To change RSA passphrase, enter:

```
$ ssh-keygen -f id_rsa -p
```

Apenas duas observações importantes:

* Ao executar os comandos anteriores, será pedida a senha atual da chave e, a seguir, a nova senha (com confirmação).

* A chave gerada não terá as mesmas permissões de segurança da chave anterior. Assim, verifique as permissões anteriores com # ls -l e, depois, troque as permissões na chave nova com # chmod.

Vários servidores Git autenticam usando chaves públicas SSH. Para fornecer uma chave pública, cada usuário no seu sistema deve gerar uma se eles ainda não a possuem. Este processo é similar entre os vários sistemas operacionais unix/linux. Primeiro, você deve checar para ter certeza que você ainda não possui uma chave. Por padrão, as chaves SSH de um usuário são armazenadas no diretório ~/.ssh. Você pode facilmente verificar se você tem uma chave indo para esse diretório e listando o seu conteúdo:

```
  $ cd ~/.ssh
  $ ls
    authorized_keys2  id_dsa       known_hosts
    config            id_dsa.pub
```

Você está procurando por um par de arquivos com nomes que podem variar de usuário para usuário, mas a estrutura será '''nome_chave''' e '''nome_chave.pub''', onde algo é normalmente id_dsa ou id_rsa. O arquivo .pub é a sua chave pública, e o outro arquivo é a sua chave privada. Se você não tem estes arquivos (ou não tem nem mesmo o diretório .ssh), você pode criá-los executando um programa chamado ssh-keygen, que é fornecido com o pacote SSH em sistemas Linux/Mac. Funciona assim em sistemas linux: 

```
  $ ssh-keygen -t rsa
  Generating public/private rsa key pair.
  Enter file in which to save the key ('''/home/nome-do-usuario/.ssh/id_rsa'''):
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in '''/home/nome-do-usuario/.ssh/id_rsa'''.
  Your public key has been saved in '''/home/nome-do-usuario/.ssh/id_rsa.pub'''.
  The key fingerprint is:
  '''43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a nome-do-usuario@servidor'''
```

Primeiro ele confirma onde você quer salvar a chave (.ssh/id_rsa), e então pergunta duas vezes por uma senha, que você pode deixar em branco se você não quiser digitar uma senha quando usar a chave.

Agora, cada usuário que executar o comando acima precisa enviar a chave pública para você ou para o administrador do seu servidor Git (assumindo que você está usando um servidor SSH cuja configuração necessita de chaves públicas). Tudo o que eles precisam fazer é copiar o conteúdo do arquivo .pub e enviar para você via e-mail. As chaves públicas são parecidas com isso.

```
  $ cat ~/.ssh/id_rsa.pub
  ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
  GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
  Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
  t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
  mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
  NrRFi9wrf+M7Q== '''nome-do-usuario@servidor'''
```

Para um tutorial mais detalhado sobre criação de chaves SSH em vários sistemas operacionais, veja o guia do GitHub sobre chaves SSH no endereço http://github.com/guides/providing-your-ssh-key.

## Encerrar ssh

Se você estiver usando ssh via terminal e precisa encerrar a seção (mesmo que a conexão tenha caido e o terminal esteja travado), tente: 

```
 Enter ~ ~ .
 ```

## Referências 

* https://git-scm.com/book/pt-br/v1/Git-no-Servidor-Gerando-Sua-Chave-P%C3%BAblica-SSH
* http://www.cyberciti.biz/faq/howto-ssh-changing-passphrase/


