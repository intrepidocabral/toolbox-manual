
## Modos de operação

São 4 os modos de operação do vim.

### Normal (standard mode)

Este modo é o padrão do vim. Neste modo você pode ver o conteúdo de um arquivo, copiar algumas partes do texto e navegar por ele.

Ex.:

  $ vim teste

[[Image:Vim1.png]]

### Inserção (insert mode)

Este modo é o mais usado no vim. Com ele você pode editar o arquivo. Para ativar o modo inserção você deve teclar i (i minúsculo).

Ex.:

[[Image:Vim2.png]]

### Visual (visual mode)

Este modo é acionado com a letra v (v minúsculo). Nesse modo você pode formatar o texto, selecionar, copiar, etc.

Ex.:
[[Image:Vim3.png]]

### Comando (command mode)

Em geral é usando com : (dois pontos) + um comando. Ver comandos básicos. Ex.:

[[Image:Vim4.png]]


## Instalação

É muito simples instalar. Tomando como base uma distro Debian:

 #apt-get install vim vim-addon-manager vim-doc vim-dbg

Pronto!

Outros pacotes importantes:

 # apt-get install vim-snippets vim-ultisnips exuberant-ctags vim-gnome



### Repetição

    Digitei um texto no modo inserção
    Aperte o Esc (o vim vai considerar uma ação);
    Aperte o . (ponto) e ele irá repetir a ação (vai copiar o que foi escrito várias vezes, tantas quanto você clicar em ponto);
    Para multiplicar a repetição, digite um número e depois .. Ex: 2. + enter. Ele vai copiar duas vezes. 

Ex.:

 vim teste
 i (habilita o modo insert)
 Escrever um exemplo...
 Esc + .
 ...
 Escrever um exemplo...  
 Escrever um exemplo...
 Escrever um exemplo...


### Alterando capslock (maiúsculas e minúsculas)

    Entre no vim e coloque o cursor do mouse na linha que quer alterar
    Coloque o cursor do terminal no ponto de inicio de uma seleção e entre no modo visualização (pressionando v) e selecione o texto com as setas;
    Digitando o U maiúsculo, todos os caracteres selecionados ficarão em maiúscula;
    Digitando o u minúsculo, todos os caracteres selecionados ficarão em minúsculas;
    Digitando o ~ (til), todos os caracteres selecionados alternarão seu modo (o que for minusculo fica maiúsculo e o que for maiúsculo vira minúsculo)

### Substituição

    Entre no vim e posicione o cursor onde quer substituir o texto em blocos;
    Acione o modo de visualização em bloco tecle ctrl + V;
    Pressione c minúsculo para deletar;
    Digite os caracteres novos desejados;
    Pressione s para alterar em toda a seleção de bloco. Pronto! 

### Macros

### Snippets


## Customizando o vim 

* Vídeos
:* Vídeo Bóson Treinamentos: Editor VI Linux 1 https://www.youtube.com/watch?v=bXdX5X3JoI8
:* Vídeo Bóson Treinamentos: Editor VI Linux 2 https://www.youtube.com/watch?v=16M82mDbg80
:* Vídeo Bóson Treinamentos: Editor VI Linux 3 https://www.youtube.com/watch?v=Ksv3mBJ0quA
:* Vídeo Bóson Treinamentos: Editor VI Linux 4 https://www.youtube.com/watch?v=o6pVIuPJX8k
:* Vídeo Bóson Treinamentos: Editor VI Linux 5 https://www.youtube.com/watch?v=2bHUKlFcnW0
:* Vídeo Bóson Treinamentos: Editor VI Linux 6 https://www.youtube.com/watch?v=v6y0ZlNAihM
:* Vídeo Bóson Treinamentos: Editor VI Linux 7 https://www.youtube.com/watch?v=3JcPRySHmXI
:* Vídeo Bóson Treinamentos: Editor VI Linux 8 https://www.youtube.com/watch?v=TntNl95kfkM
:* Vídeo Bóson Treinamentos: Editor VI Linux 9 https://www.youtube.com/watch?v=_NXc5vZdR3E
:* Vídeo Bóson Treinamentos: Editor VI Linux 10 https://www.youtube.com/watch?v=fJ4a0GSWpa0
:* Vídeo 1 - Editor Vim - instalação: https://www.youtube.com/watch?v=Ry-Zl7EOFuc
:* Vídeo 2 - Editor Vim - abrindo e criando novos arquivos: https://www.youtube.com/watch?v=XiGtc1gR4PU
:* Vídeo 3 - Editor Vim - sair sem salva: https://www.youtube.com/watch?v=HIOnXTTdX-w
:* Vídeo 4 - Editor Vim - salvando arquivos em diferentes diretórios: https://www.youtube.com/watch?v=Bvq37muiB90
:* Vídeo 5 - Editor Vim - alternando arquivos no vim: https://www.youtube.com/watch?v=vi2UYFmNc6U
:* Vídeo 6 - Editor Vim - instalação: https://www.youtube.com/watch?v=Wpf79MYXa28
:* Vídeo 7 - Editor Vim - anexando arquivos com vim: https://www.youtube.com/watch?v=hpRgcFbXDYQ
:* Vídeo 8 - Editor Vim - inserindo comandos bash no vim: https://www.youtube.com/watch?v=rdTohi1DzSw
:* 17 dicas para o vim https://www.youtube.com/watch?v=DyUq81mXCVA

## Referências

* http://vimcasts.org
* http://aurelio.net/vim/
* https://github.com/skwp/dotfiles
* http://klauslaube.com.br/2013/03/04/vim-o-meu-editor-favorito.html
* https://dotfiles.github.io
* http://vimawesome.com


