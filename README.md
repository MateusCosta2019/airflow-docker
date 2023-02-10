# Executando Airflow com Docker
O Apache Airflow é uma plataforma de gerenciamento de workflows que é basicamente o passo a passo necessário para executar um processo. O Airflow é amplamente utilizado na área de engenharia de dados para orquestrar e automatizar pipelines de dados. O Airflow permite que os engenheiros criem, gerenciem e monitorem pipelines de dados de forma eficiente e escalável, é possível definir tarefas de forma clara e visual, agendar a execução de tarefas e garantir a integridade dos dados ao longo do pipeline.  Vale ressaltar que Aifrlow é uma ferramenta OpenSource. Originalmente, a plataforma foi projetada para ser executada em sistemas Unix e, portanto, a instalação e configuração do Airflow no sistema Windows pode ser um pouco mais complicada. Se você deseja testar o Airflow localmente em seu sistema Windows, a maneira mais simples de fazê-lo é usando imagens do Docker. 

# Pré-requisitos

Antes de começar, é importante lembrar que para realizar a instalação da ferramenta você precisa ter instalado em sua máquina:
-   Docker Community Edition
-   Docker Compose

# Step-byStep
Se você já possui o Docker instalado na sua máquina, a primeira coisa que você precisa para continuar a instalação do Airflow é o arquivo docker-compose.yaml. Crie um diretório chamado Airflow, digite:

     mkdir airflow
     cd airflow
  
 Com o diretório criado, é hora de baixar a imagem docker. Para isso, você pode digitar:

    `Invoke-WebRequest -Uri 'https://airflow.apache.org/docs/apache-airflow/2.5.1/docker-compose.yaml' -OutFile 'docker-compose.yaml'`
Assim como descrito na documentação oficial do Airflow, o arquivo yaml contém várias definições de serviços:

-   airflow-scheduler - O agendador monitora todas as tarefas e DAGs e aciona as instâncias de tarefas assim que suas dependências são concluídas.
-   airflow-webserver - O servidor web está disponível em [http://localhost:8080](http://localhost:8080/).
-   airflow-worker - O trabalhador que executa as tarefas dadas pelo escalonador.
-   airflow-init - O serviço de inicialização.
-   postgres - O banco de dados.
-   redis - O broker Redis que encaminha mensagens do agendador para o trabalhador.

Antes de inicializar o airflow precisamos criar mais algumas pastas:
- ./dags- você pode colocar seus arquivos DAG aqui.
- ./logs- contém logs de execução de tarefas e agendador.
- ./plugins- você pode colocar seus plugins personalizados aqui.

para isso execute os seguintes comandos no cmd na pasta do airflow criada anteriomente:

    mkdir ./dags 
    mkdir ./logs 
    mkdir ./plugins

Após realizar as configurações do ambiente é hora de inicializar nosso banco de dados do Airflow e nosso container, para isso execute o comando:

    docker-compose up airflow-init

esse comando basicamente executará o airflow db init e criara o usuário adm. do banco que no nosso caso é o postgress, você pode configurar para rodar com MySQL caso desejar. Por padrão a conta criada possui o login e senha (airflow). a ultima coisa que precisamos fazer para em fim rodar nossos serviços do airflow é executar o comando: 

    docker-compose up

Vale ressaltar que por precisar iniciar diversos serviços o comando acima pode demorar um pouco mas você pode verificar se sua imagem está funcionando usando o comando (em uma nova guia do seu cmd):

    docker ps


Após todo esse processo, você acessar o airflow através do endereço localhost:8080 realizar login e utilizar o serviços da plataforma.

## Conclusão

Com o uso do Docker e o arquivo Docker Compose, conseguimos automatizar o processo de instalação e configuração do Airflow, facilitando a instalação em sistemas Windows. Além disso, também aprendemos sobre os serviços que compõem a plataforma Airflow, como o escalonador de tarefas, o servidor web, o trabalhador, o serviço de inicialização e o banco de dados.

Após seguir todos os passos deste tutorial, você já estará com o Apache Airflow funcionando corretamente em seu sistema Windows, pronto para criar, gerenciar e monitorar seus workflows de dados.