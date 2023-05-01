# Hadoop_Atividade_02

## Objetivo da atividade
Criar um ecossistema dentro do Hadoop com o armazenamento de dados 


## Primeiros passos

## 1 - Definir o arquivo será utilizado 
O arquivo utilizado para a atividade é um dataset de Jogos de Futebol no Brasil. 
O dataset é em formato .csv e tem cerca de 14 mil valores registrados

## 2 - Definir Organização dentro do HDFS 
Dentro do Hadoop File System nós escolhemos seguir com a seguinte organização 

Jogos/Tipo/Torneio/Semanas

Sendo considerado a periodicidade Semanal para seguir mais ou menos com as rodadas de cada campeonato 
Jogos -> Arquivo Base 
Tipo -> Separação entre campeonatos Regionais e Nacionais 
Torneio -> Separação por torneio 
Semanas -> Separação com peridiocidade semanal para ser similar as rodadas do campeonato

### 2.1 - Criação das pastas e inserção de dados dentro do Hadoop File System 
Para inserir os dados nós iremos primeiro criar as pastas necessárias com o comando dentro do Bash: 

```
hadoop fs -mkdir Nome_do_diretório
```

Após utilizar este comando para crias as pastas nós ficaremos com os seguintes parâmetros.
Para ver os arquivos e pastas dentro do repositório podemos utilizar:

```
hadoop fs -ls Nome_do_diretório
```

Que nos traz os seguintes resultados

NACIONAL
<img src='https://user-images.githubusercontent.com/64543476/235367299-ca5e0c82-30e8-45d2-8e00-2dac3e5ced69.jpeg'></img>

REGIONAL
<img src='https://user-images.githubusercontent.com/64543476/235367303-9cdf335c-861e-42f3-ba00-78a97eb2a492.jpeg'></img>

### 2.2 - Inserindo os dados necessários 
Os dados foram inicialmente baixados na máquina local, então precisamos deixar o arquivo base dentro do Docker e posteriormente passar para dentro do HDFS.

Para fazer essa cópia nós podemos utilizar:

```
docker cp BR-Football-Dataset.csv namenode:/BR-Football-Dataset.csv 
```

Mas como iremos separar os arquivos de forma semanal, nós precisamos fazer isso de forma automático e não ficar separando e criando um único arquivo por vez. Para realizar esta atividade nós podemos utilizar o seguinte Script SH para realizar a função dentro do Docker utilizando o arquivo original. 

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

Checkpoint do cmd mostrando os valores inseridos em cada pasta 

<img src='https://user-images.githubusercontent.com/64543476/235368172-35d96848-378a-4bf7-a9ac-352c7cbf56f8.png'></img>

dentro do HUE para fácil visualização: 

<img src='https://user-images.githubusercontent.com/64543476/235368233-7e679cfd-9db7-4a8a-b77d-56ae49c07741.png'></img>

Agora nós apenas precisamos mudar o caminho final do HDFS para realizar a cópia correta desses arquivos com a nomemclatura certa. 

## 3 - BackUps 
Para realizar os Backups, nós decidimos construir as pastas de Backups para cada torneio em cada semana. Ou seja, o backup dos arquivos de CSV será feito de forma semanal junto com a entrega dos dados. Desta forma as pastas estão situadas nos diretórios:

/Jogos/Tipo/Torneio/BKP/Semana


* Vamos criar a pasta *BKP* para o armazenamento dos bakups 
```
hadoop fs -mkdir /Brazilian_Football/Type/National/BKP
hadoop fs -mkdir /Brazilian_Football/Type/Regional/BKP
```

* Agora faremos o backup de forma *semi-automático* seguindo essa estrutura:
```
hadoop fs -cp /Jogos/Tipo/Torneio_x/Semana_x /Jogos/Tipo/Torneio_x/BKP/
```

* Exemplo: 
```
hadoop fs -cp /Brazilian_Football/Type/National/Semana_1 /Brazilian_Football/Type/National/BKP/ 
hadoop fs -cp /Brazilian_Football/Type/Regional/Semana_1  /Brazilian_Football/Type/Regional/BKP/
```


## 4 - Ecossistema 
Como o intuito da atividade é simular um ecossitema real, nós pensamos que um possível ecossistema de dados para essas soluções da seguinte forma: 

<img src='https://user-images.githubusercontent.com/64543476/235394179-ed62597a-3535-4458-b68d-b8f08bf99848.png'></img>

Assim, nós conseguimos nós assegurar da entrega continua dos dados, a construção do BackUp e também a agilidade de esses dados seriam entregues para as áreas de negócios. 












