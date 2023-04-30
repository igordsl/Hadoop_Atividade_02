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

NACIONAL
<img src='https://user-images.githubusercontent.com/64543476/235367299-ca5e0c82-30e8-45d2-8e00-2dac3e5ced69.jpeg'></img>

REGIONAL
<img src='https://user-images.githubusercontent.com/64543476/235367303-9cdf335c-861e-42f3-ba00-78a97eb2a492.jpeg'></img>








