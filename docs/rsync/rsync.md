Rsync, como o nome sugere, é um programa que sincroniza remotamente os dados entre duas máquinas. Por ser baseado no antigo rcp (remote copy), o software herdou as propriedades de criptografia do protocolo SSH, o que torna sua transmissão de dados mais segura que o FTP. 

Além das propriedades de segurança, o rsync utiliza o protocolo remote-update, o que aumenta assustadoramente sua velocidade e diminui a quantidade de dados transferidos, pois são trocados entre os servidores somente as diferenças entre dois grupos de arquivos. 

Voltando ao nosso estudo de caso introdutório, se alteramos uma dúzia de arquivos numa porção de centenas, ao executar um rsync do seu desktop para o servidor, somente os arquivos alterados serão enviados por upload e você ainda não corre o risco de algum espertinho utilizando um sniffer1 na rede capturar sua senha de FTP em plain text. 

Resumindo, existem pelo menos quatro situações onde o rsync pode te ajudar:
- copiando (ou sincronizando) arquivos entre dois diretórios locais;
- copiando (ou sincronizando) arquivos de sua máquina local para um servidor remoto;
- copiando (ou sincronizando) arquivos de um servidor remoto para sua máquina local;
- listando os arquivos de um diretório no servidor remoto (como um "remote ls").

=== Situação Problema ===
Vamos imaginar um cenário onde você programou um mega portal que possui centenas de arquivos que somados ocupam cerca de 300 MB em disco rígido. Existem duas cópias do portal, uma no seu desktop de trabalho e outra no servidor Linux em produção. 

Certo dia você resolve fazer uma baita reforma no site e passa uma porção enorme de tempo alterando seus scripts PHP, HTML, folhas de estilo, imagens e tudo mais que se possa imaginar e agora precisa atualizar a nova versão offline com a versão que existe no servidor em produção. 

O grande problema é que você passou horas programando e já não recorda quais arquivos foram alterados. E agora, que solução te vem à cabeça? Enviar os 300 MB por FTP para o servidor? Ou passar outro bocado de horas selecionando os arquivos que você "lembra" que alterou e fazendo seu upload um a um? Que nada, isso é um mártir exclusivo para usuários de Windows. Quem programa em desktops Linux e claro, hospeda seus projetos em servidores Linux pode contar com a ferramenta dos sonhos, o rsync. 


== Download e instalação ==

Rsync é quase que um pacote default em todas as distribuições linux. Aquelas que não o instalam numa instalação do tipo básica, com certeza possuem o pacote em algum lugar em seus CDs de instalação. Consulte os mesmos para maiores informações. 

No Debian, a instalação do mesmo se faz com apenas um comando: 
```
  # apt-get install rsync 
```

Se você preferir, pode obter o software direto na fonte. Seu site oficial é:
* http://rsync.samba.org

E seu download pode ser obtido em:

- ftp://rsync.samba.org/pub/rsync


Para a comunicação entre duas máquinas com rsync funcionar, será necessário:

- o programa rsync instalado em ambas as máquinas;
- o servidor SSH (sshd) rodando no servidor.

'''Nota:''' se a comunicação for bilateral (ambas as máquinas enviam e recebem arquivos) o serviço SSH precisará estar rodando em ambas as máquinas.

== Sincronizando diretórios locais ==

'''Uso:'''
 rsync [opções] origem destino 

Você tem um diretório recheado com arquivos importantes e deseja manter uma cópia fiel do mesmo em outra localidade. Para copiar /HOME/USUARIO/ARTIGOS para para /MEDIA/BACKUPS/ARTIGOS, executamos: 

  $ rsync -Cravzp /HOME/USUARIO/ARTIGOS /MEDIA/BACKUPS/ARTIGOS

'''Nota:''' esse comando pressupoe que /MEDIA/BACKUPS/ARTIGOS está criado e tenho permissões de escrita no mesmo. 

Costumo utilizar a seqüência de opções Cravzp por considerar que nelas estão inclusas todas as funcionalidades que necessito. Você pode optar em confiar cegamente em minhas palavras ou dar uma breve conferida na página de manual do software (man rsync) para descobrir o significado de cada opção.

== Enviando arquivos locais para um servidor remoto ==

Um pré-requisito para enviar seus arquivos para o servidor remoto é possuir uma conta de usuário no sistema. Sendo assim, sua forma de uso é: 

  rsync [opções] origem usuario@host:destino 

Supondo que o diretório /var/backups/artigos está localizado no servidor remoto cujo endereço IP é 10.0.0.5 e minha conta de usuário possui login "fabio", executamos: 

  $ rsync -Cravzp /home/fabio/artigos/ fabio@10.0.0.5:/var/backups/artigos/ 

Surgirá um prompt de senha, digite-a e pronto, os arquivos serão copiados.

Para simplificar, poderia ser usado esse comando: 

  rsync -avzP /HOME/USUARIO-desktop/DIRETORIO1 notebook@192.168.0.6:/HOME/USUARIO-notebook/DIRETORIO2

== Enviando arquivos do servidor para sua máquina local ==

Esta situação também requer um login para autenticação no servidor, a menos que o mesmo esteja configurado para aceitar conexões de usuários guest, fato comum em servidores mirrors, porém este assunto está fora do escopo do artigo. Se você entendeu como funciona o comando anterior, basta inverter a ordem dos parâmetros: 

  $ rsync -Cravzp fabio@10.0.0.5:/var/backups/artigos/ /home/fabio/artigos/

== Sincronizando pastas entre máquinas (remota para local e vice-versa) == 

Para um rede local, a sincronização pode ser feita assim: 

 $ rsync -CravzpPu usuario@192.168.0.106:/home/usuario/diretorio1 /home/diretorio2

Onde '''usuario@192.168.0.106:/home/usuario/diretorio1''' é o servidor e '''/home/diretorio2''' é uma máquina local.

Se você quer, além de atualizar modificações e arquivos, manter as deleções atualizadas, você pode usar: 

 $ rsync -rtvucP --delete /home/usuario/diretorio1 usuario@192.168.0.106:/home/usuario/diretorio2

== Listando arquivos do servidor ==

Esta é forma de uso mais simples do rsync e seu pré-requisito é o de possuir login de autenticação no servidor (ou guest). Sintaxe: 

  rsync [opções] usuario@host:diretorio 

Se você deseja listar o diretório /etc do servidor, pode usar o comando: 

  $ rsync -Cravzp fabio@10.0.0.5:/etc/ 

O "pulo do gato" dessa situação é a omissão do diretório de destino.

== Opções de Comando == 

 -v, --verbose               imprime no pront de comando o que está sendo executado
 -q, --quiet                 suprime mensagens de erro
     --no-motd               suppress daemon-mode MOTD (see caveat)
 -c, --checksum              pula arquivos iguais com base no checksum, e não no tempo de modificação e no tamanho do arquivo
 -a, --archive               modo de arquivos, maneira compacta de escolher (-r) recursividade, (-l) preservação de links, 
                             (-p) preservação de permissões, (-t)preservação dos tempos dos arquivos, (-g) preservação dos grupos, 
                             (-o) preservação dos donos dos arquivos e (-D) preserva arquivos especiais e arquivos do sistema (Device). 
                             Esse comando seria igual ao -rlptgoD (não -H,-A,-X)
     --no-OPTION             turn off an implied OPTION (e.g. --no-D)
 -r, --recursive             transforma o comando em recursivo para todos os subdiretórios
 -R, --relative              use relative path names
     --no-implied-dirs       don't send implied dirs with --relative
 -b, --backup                make backups (see --suffix & --backup-dir)
     --backup-dir=DIR        make backups into hierarchy based in DIR
     --suffix=SUFFIX         backup suffix (default ~ w/o --backup-dir)
 -u, --update                pula arquivos que são mais novos no destino
     --inplace               faz update dos arquivos novos da origem no destino
     --append                acrescentar dados em arquivos menores
     --append-verify         acrescentar dados antigos em arquivo de checksum
 -d, --dirs                  transfer directories without recursing
 -l, --links                 copy symlinks as symlinks
 -L, --copy-links            transform symlink into referent file/dir
     --copy-unsafe-links     only "unsafe" symlinks are transformed
     --safe-links            ignore symlinks that point outside the tree
 -k, --copy-dirlinks         transform symlink to dir into referent dir
 -K, --keep-dirlinks         treat symlinked dir on receiver as dir
 -H, --hard-links            preserve hard links
 -p, --perms                 preserva as permissões dos arquivos
 -E, --executability         preserve executability
     --chmod=CHMOD           affect file and/or directory permissions
 -A, --acls                  preserve ACLs (implies -p)
 -X, --xattrs                preserve extended attributes
 -o, --owner                 preserve owner (super-user only)
 -g, --group                 preserve group
     --devices               preserve device files (super-user only)
     --specials              preserve special files
 -D                          same as --devices --specials
 -t, --times                 preserve modification times
 -O, --omit-dir-times        omit directories from --times
     --super                 receiver attempts super-user activities
     --fake-super            store/recover privileged attrs using xattrs
 -S, --sparse                handle sparse files efficiently
 -n, --dry-run               perform a trial run with no changes made
 -W, --whole-file            copy files whole (w/o delta-xfer algorithm)
 -x, --one-file-system       don't cross filesystem boundaries
 -B, --block-size=SIZE       force a fixed checksum block-size
 -e, --rsh=COMMAND           specify the remote shell to use
     --rsync-path=PROGRAM    specify the rsync to run on remote machine
     --existing              skip creating new files on receiver
     --ignore-existing       skip updating files that exist on receiver
     --remove-source-files   sender removes synchronized files (non-dir)
     --del                   an alias for --delete-during
     --delete                delete extraneous files from dest dirs
     --delete-before         receiver deletes before transfer (default)
     --delete-during         receiver deletes during xfer, not before
     --delete-delay          find deletions during, delete after
     --delete-after          receiver deletes after transfer, not before
     --delete-excluded       also delete excluded files from dest dirs
     --ignore-errors         delete even if there are I/O errors
     --force                 force deletion of dirs even if not empty
     --max-delete=NUM        don't delete more than NUM files
     --max-size=SIZE         don't transfer any file larger than SIZE
     --min-size=SIZE         don't transfer any file smaller than SIZE
     --partial               keep partially transferred files
     --partial-dir=DIR       put a partially transferred file into DIR
     --delay-updates         put all updated files into place at end
 -m, --prune-empty-dirs      prune empty directory chains from file-list
     --numeric-ids           don't map uid/gid values by user/group name
     --timeout=SECONDS       set I/O timeout in seconds
     --contimeout=SECONDS    set daemon connection timeout in seconds
 -I, --ignore-times          don't skip files that match size and time
     --size-only             skip files that match in size
     --modify-window=NUM     compare mod-times with reduced accuracy
 -T, --temp-dir=DIR          create temporary files in directory DIR
 -y, --fuzzy                 find similar file for basis if no dest file
     --compare-dest=DIR      also compare received files relative to DIR
     --copy-dest=DIR         ... and include copies of unchanged files
     --link-dest=DIR         hardlink to files in DIR when unchanged
 -z, --compress              comprime os arquivos durante a transferencia
     --compress-level=NUM    explicitly set compression level
     --skip-compress=LIST    skip compressing files with suffix in LIST
 -C, --cvs-exclude           auto-ignora arquivos CSV
 -f, --filter=RULE           add a file-filtering RULE
 -F                          same as --filter='dir-merge /.rsync-filter'
                             repeated: --filter='- .rsync-filter'
     --exclude=PATTERN       exclude files matching PATTERN
     --exclude-from=FILE     read exclude patterns from FILE
     --include=PATTERN       don't exclude files matching PATTERN
     --include-from=FILE     read include patterns from FILE
     --files-from=FILE       read list of source-file names from FILE
 -0, --from0                 all *from/filter files are delimited by 0s
 -s, --protect-args          no space-splitting; wildcard chars only
     --address=ADDRESS       bind address for outgoing socket to daemon
     --port=PORT             specify double-colon alternate port number
     --sockopts=OPTIONS      specify custom TCP options
     --blocking-io           use blocking I/O for the remote shell
     --stats                 give some file-transfer stats
 -8, --8-bit-output          leave high-bit chars unescaped in output
 -h, --human-readable        output numbers in a human-readable format
     --progress              show progress during transfer
 -P                          same as --partial --progress
 -i, --itemize-changes       output a change-summary for all updates
     --out-format=FORMAT     output updates using the specified FORMAT
     --log-file=FILE         log what we're doing to the specified FILE
     --log-file-format=FMT   log updates using the specified FMT
     --password-file=FILE    read daemon-access password from FILE
     --list-only             list the files instead of copying them
     --bwlimit=KBPS          limit I/O bandwidth; KBytes per second
     --write-batch=FILE      write a batched update to FILE
     --only-write-batch=FILE like --write-batch but w/o updating dest
     --read-batch=FILE       read a batched update from FILE
     --protocol=NUM          force an older protocol version to be used
     --iconv=CONVERT_SPEC    request charset conversion of filenames
     --checksum-seed=NUM     set block/file checksum seed (advanced)
 -4, --ipv4                  prefer IPv4
 -6, --ipv6                  prefer IPv6
     --version               print version number
 (-h) --help                 show this help (see below for -h comment)

Rsync can also be run as a daemon, in which case the following options are accepted:
    --daemon                run as an rsync daemon
    --address=ADDRESS       bind to the specified address
    --bwlimit=KBPS          limit I/O bandwidth; KBytes per second
    --config=FILE           specify alternate rsyncd.conf file
    --no-detach             do not detach from the parent
    --port=PORT             listen on alternate port number
    --log-file=FILE         override the "log file" setting
    --log-file-format=FMT   override the "log format" setting
    --sockopts=OPTIONS      specify custom TCP options
 -v, --verbose               increase verbosity
 -4, --ipv4                  prefer IPv4
 -6, --ipv6                  prefer IPv6
 -h, --help                  show this help (if used after --daemon

== Clientes ==

O '''rsync''' possui alguns clientes gráficos, embora seu poder maior esteja na linha de comando. Entre os clientes mais famosos estão: 

* Grsync
:* http://www.opbyte.it/grsync
:* https://en.wikipedia.org/wiki/Grsync

* GAdmin-Rsync
:* http://freecode.com/projects/gadmin-rsync
:* http://mange.dynalias.org/linux/gadmin-rsync

* LuckBackup
:* http://luckybackup.sourceforge.net
:* https://www.youtube.com/watch?v=j392gUlWumg

== Tutoriais ==

[http://wiki.nosdigitais.teia.org.br/Backup_de_computador_pela_rede_com_rsync Tutorial Backup de Computador pela rede com Rsync]

== Referências ==
* Usando o Grsync e Rsync para Backup e Sincronização https://rafaelocremix.wordpress.com/2011/08/25/usando-o-grsync-para-backup-e-sincronizacao/
* http://www.vivaolinux.com.br/artigo/Transferindo-arquivos-com-o-rsync
* https://rsync.samba.org
* https://en.wikipedia.org/wiki/Grsync
* http://www.opbyte.it/grsync/ 
* http://www.jveweb.net/en/archives/2010/11/synchronizing-folders-with-rsync.html

