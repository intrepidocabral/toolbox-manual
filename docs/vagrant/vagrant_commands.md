Vagrant é uma ferramenta para a construção de ambientes de desenvolvimento completos. Ele funciona integrado ao Virtualbox e pode ajudar na criação e gerenciamento de máquinas virtuais via linha de comandos. Com um fluxo de trabalho fácil de usar e foco em automação, o Vagrant busca reduzir o tempo de instalação de um ambiente de desenvolvimento, aumentando a produtividade e fazendo com que as velhas "instalações locais" sejam coisas do passado. 

O projeto Vagrant foi iniciado em janeiro de 2010 por Mitchell Hashimoto. Por quase três anos, Vagrant era um projeto paralelo para Mitchell, um projeto que ele trabalhou nas horas vagas como um hobby. Durante este tempo, Vagrant cresceu e hoje é um software confiável, 100% open source (já disponível inclusive em repositórios Debian), utilizado desde desenvolvedores free-lance até equipes de grandes empresas.

Em novembro de 2012, uma empresa chamada HashiCorp foi formado por Mitchell para desenvolver Vagrant em tempo integral. Essa empresa oferece adições comerciais, formação e suporte profissional para o Vagrant.

## Tutoriais

### Vídeos
* Vagrant - Entendimentos básicos https://www.youtube.com/watch?v=uhYdTS0g7SU

## Plugins 
* https://github.com/vagrant-landrush/landrush


## Instalando uma nova máquina virtual 

```
  $ vagrant box add '''hashicorp/precise32'''
```

Para customizar o tipo de "box" (máquina virtual a ser instalada), você pode fazer uma busca por boxes disponíveis na rede. Veja algumas máquina disponíveis: https://atlas.hashicorp.com/boxes/search

Você também pode indicar uma url para a operação:

```
  $ vagrant box add https://atlas.hashicorp.com/chef/boxes/ubuntu-14.04.box
```

Iniciando uma máquina Ubuntu 14.04

```
  $ vagrant init ubuntu/trusty64; vagrant up
```

Ex: https://atlas.hashicorp.com/ubuntu/boxes/trusty64

## Gerenciando boxes 
* https://docs.vagrantup.com/v2/cli/box.html

## Gerando arquivo Vagrantfile 

Para o vagrant rodar, a aplicação precisa de um arquivo Vagrantfile em determinado diretório. Recomenda-se a criação de um diretório na pasta /home e dentro dessa pasta a insersão do arquivo. Você pode gerar o arquivo com o comando: 

```
  $ vagrant init
```

Depois desse processo é necessário customizar o arquivo para que ele possa ouvir a box correta. Você deve abrí-lo e mudar o nome indicado em negrito para o nome de sua box: 
 
```
  Vagrant.configure("2") do |config|
    config.vm.box = "'''hashicorp/precise32'''"
  end
```

## Ativando uma máquina virtual 

Depois de baixar um box e customizar o arquivo vagrantfile, você precisa ativar sua máquina virtual. 

```
  $ vagrant up
```

## Acessando a máquina virtual vagrant
```
  $ vagrant ssh
```

== Configurando rede ==
Você pode fazer o vagrant responder localmente na máquina de origem redirecionando portas. Veja um exemplo de comandos a serem adicionados no vagrantfile para redirecionar a saída de uma aplicação web do vagrant para a porta 4567 no host de origem:

```
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "chef/ubuntu-14.04"
  config.vm.network :forwarded_port, guest: 80, host: 4567
```

## Compartilhando pastas entre máquina hospedeira e máquina virtual

No Vagrantfile, esteja atento para a seguinte directiva: 

```
  # argument is a set of non-required options.
  config.vm.synced_folder "/maquina/hospedeira", "/maquina/virtual/vagrant",
  owner: "nome-do-usuario-dono-dos-arquivos-na-maquina-virtual", group: "nome-do-grupo-dos-arquivos-na-maquina-virtual"
```

Ver mais em https://docs.vagrantup.com/v2/synced-folders/basic_usage.html

## Apagando uma máquina virtual 
```
  $ vagrant destroy
```

# Referencias ==

* https://www.vagrantup.com
* Código do Vagrant: https://github.com/mitchellh/vagrant



