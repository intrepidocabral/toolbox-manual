Postgres autodoc é um software via command line que le tabelas PostgreSQL e retornar ficheiros HTML, DOT, e 2 estilos de XML, os quais descrevem a base de dados.

O HTML é humanamente legível (através de um navegador). O primeiro estilo XML é efectivamente o formato de ficheiro do Dia, uma ferramenta de diagramas UML. O segundo estilo XML é semelhante ao HTML mas no formato Docbook 4. Permite-lhe misturar com outros documentos Docbook através das XREFs, gerar PDFs, HTML, RTF, ou outros documentos formatados. Entre estas ferramentas e o Javadoc com os XREFs apropriados, documentação sobre um projecto pode ser gerada rapidamente e ser facilmente actualizável e no entanto ter um aspecto bastante profissional com algum trabalho DSSSL.

## Instalação

Você precisa do Postgres rodando antes de rodar.
```
# apt-get update
# apt-get install postgresql
```

Depois instale o autodoc: 

```
  # apt-get install postgresql-autodoc
```

Outras ferramentas interessantes para processamento conjunto (faça a instalação também): 
```
  # apt-get install graphviz
  # apt-get install dia
```

Para gerar o modelo .dot:

```
  $ postgresql_autodoc -t dot -h nome-do-hostname -u nome-do-username -d nome-da-databasenam --password
```

Para gerar o modelo em png: 

```
  $ dot -Tpng '''nome-da-databasename.dot''' -o '''nome-do-modelo.png'''
```

## Referências 
* https://ribafs.wordpress.com/2008/04/02/mini-tutorial-sobre-a-ferramenta-postgresql-autodoc/
* http://www.onurguzel.com/graphical-visualization-of-databases-with-postgresql-autodoc/
