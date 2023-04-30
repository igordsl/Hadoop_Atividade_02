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

2.2 - Inserindo os dados necessários 
Para inserir os dados csv que foram baixados na nossa máquina pessoal primeiro podemos utilizar o comando direto no cmd 

```
docker cp BR-Football-Dataset.csv namenode:/BR-Football-Dataset.csv 
```

Porém como precisamos deles na periodicidade semanal nós podemos utilizar um Script SH para escrever condicional e preencher automaticamente os dados da semana. 
Dessa forma poderiamos utilizar o seguinte Script 

```
#O arquivo original
folder="/BR-Football-Dataset.csv"

# nome do diretório onde eu quero colocar
hdfs_dir="/Brazilian_Football/Type/National/Copa_do_Brasil"

#Definindo o padrão como Semana_Num
nome_arquivo="Semana_"

#Quantidade de vezes que irá repetir
n_weeks=20

# Loop de 1 a 20 para copiar e renomear os arquivos
for i in $(seq 1 $n_weeks) 
do
    # Define o nome do arquivo original
    dir_hdfs="/Brazilian_Football/Type/National/Copa_do_Brasil/$nome_arquivo$i"

    #COMANDO hdfs para inserir os dados
    hdfs dfs -put $folder $dir_hdfs

    #print do sistema para monitoramento
    echo "Inserindo arquivo no diretorio de $dir_hdfs"

done
```

Mostrando a mensagem do CMD e também como ficará cada arquivo: 

<img src='https://user-images.githubusercontent.com/64543476/235368172-35d96848-378a-4bf7-a9ac-352c7cbf56f8.png'></img>

dentro do HUE para fácil visualização: 

<img src='https://user-images.githubusercontent.com/64543476/235368233-7e679cfd-9db7-4a8a-b77d-56ae49c07741.png'></img>

Então nós fazemos o mesmo Script para todos os campeonatos automático com a Semana para ter os resultados da rodada 

3 - BackUps 

4 - Ecossistema 










