# Hadoop_Atividade_02

Objetivo: 
Criar um ecossistema dentro do Hadoop com o armazenamento de dados 


Primeiros passos

1 - Definir o arquivo será utilizado 
Para a atividade escolhemos um dataset de Jogos de Futebol do Brasil. Contendo mais de 14 mil linhas 

2 - Definir Organização dentro do HDFS 
Dentro do Hadoop File System nós escolhemos seguir com a seguinte organização 

Jogos/Tipo/Torneio/Semanas

Sendo considerado a periodicidade Semanal para seguir mais ou menos com as rodadas de cada campeonato 

2.1 - Criação das pastas e inserção de dados dentro do Hadoop File System 
Para inserir os dados nós iremos primeiro criar as pastas necessárias com o comando dentro do Bash: 

```
hadoop fs -mkdir Nome_do_diretório
```

Após utilizar este comando para crias as pastas nós ficaremos com os seguintes parâmetros.
Utilizando o comando: 


```
hadoop fs -ls Nome_do_diretório
```

para ver as pastas listadas dentro do diretório

Nós ficaremos os as seguintes pastas 






