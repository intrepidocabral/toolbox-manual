Por padrão o comando TAR não compacta e sim só guarda uma estrutura com arquivos ou somente vários arquivos dentro de um único arquivo. Então não adianta passar somente o TAR num arquivo pensando que ele vai reduzir de tamanho. Para isso acontecer o comando TAR tem que vir junto com a opção Z, que é responsável por compactar o conteúdo.

No diretório /home/usuario1 com um monte de subdiretório e um monte de arquivos dentro desse meu home (usuario1) e queria gerar um arquivo para transportar para outra máquina. De qualquer lugar posso soltar o comando:

$ tar -cvf usuario1.tar /home/usuario1/*

Pronto, assim ele vai me gerar um arquivo chamado usuario1.tar com tudo que tem dentro do /home/usuario1, porém quando voltar o backup ele não vai ter a estrutura (/home/usuario1/algumacoisa) e sim vai começar no (algumacoisa) perdendo o raiz /home/usuario1.

Pra eu gerar um arquivo TAR - só que COMPACTADO - tenho que colocar a opção z no meio do comando assim:

$ tar -czvf usuario1.tgz /home/usuario1/*

Ou ainda gerar um arquivo ZIPADO do arquivo tar, assim:

$ gzip usuario1.tar usuario1_zipado.gz

Fácil...

Para respeitar a estrutura do diretório /home/usuario1 é só colocar no comando um . assim:

$ tar -cvf evertongodoi.tar ./home/evertongodoi/*

e só... ele vai gerar o TAR contendo a estrutura /home/evertongodoi/algumacoisa...

aí... já criamos o arquivo TAR, agora se por acaso eu quiser ver o que tem dentro do arquivo eu faço assim:

$ tar -tvf evertongodoi.tar

E pra desmontar o tar a gente faz assim:

$ tar -xvf evertongodoi.tar

Só devemos ter cuidado para não desmontar o arquivo em qualquer lugar ,senão ele pode sobrepor alguma coisa.

E para desmontar um tar que está compactado com a opção Z é muito difícil:

$ tar -xzvf evertongodoi.tgz

Pronto...

Vejam só, tem umas opções muito legais como a -l (algum.txt), onde a gente coloca uma lista simples de arquivos que QUEREMOS fazer o TAR, ou ainda a opção -X (algum.txt) onde a gente coloca uma lista simples de arquivos que NÃO queremos que vai para o tar...

Tranqüilo, agora já dá pra fazer os scripts para backup gerando os arquivos que deseja serem copiados no tar para ficar somente um arquivo e fazer um FTP para outro server ou gravar em DAT, DVD ou CD.

É isso valeu aí galera, este artigo foi elaborado por mim e pelo meu grande amigo Pedro Malanga para ajudar a comunidade Viva o Linux e estamos aí para esclarecer qualquer dúvida sobre ele. 


zip:

gunzip nomedoarquivo.zip

rar:

unrar x nomedoarquivo.rar

tar:

tar -xvf nomedoarquivo.tar

tar.gz:

tar -vzxf nomedoarquivo.tar.gz

bz2:

bunzip nomedoarquivo.bz2

tar.bz2:

tar -jxvf nomedoarquivo.tar.bz2

[[Category: tar]]
[[Category: compactação de arquivos]]

