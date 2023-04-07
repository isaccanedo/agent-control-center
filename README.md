# Centro de controle do agente AppDynamics [ ACC ]

[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/Appdynamics/agent-control-center)

O objetivo deste utilitário é uma extensão da interface web do AppDynamics para visualizar o status dos agentes no Appdynamics, com a capacidade de verificar seu histórico de saúde e realizar a atualização da versão do agente.

## Requisitos

- Máquina Virtual (4 vCPU e 8GB de memória)
- Docker
- Docker-compose

## Execução do utilitário

A primeira etapa é criar as imagens do contêiner localmente executando o comando **./build-docker.sh all**

A segunda etapa é iniciar os contêineres executando o comando **./start.sh**

Para interromper o ACC, execute o comando **./stop.sh**

## Como usar

Depois de iniciar o Agent Control Center, vá para o endereço **http://localhost** em seu navegador da Web.

Para logar no ACC é necessário criar um token de acesso na interface do AppDynamics, caso você já possua o token passe para o próximo tópico.

Na interface de administração do AppDynamics clique em "API Clients" e depois em "Create".

![01](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Create-API-Token-01.png?raw=true)

Digite os seguintes campos:

- Nome do Cliente: será utilizado na tela de Login
- Segredo do Cliente: Clique no botão "Gerar Segredo" e copie o valor informado, ele será utilizado na tela de Login. Salve em local seguro, pois esse valor não ficará mais visível.
- Expiração do token padrão: altere para 24 horas
- Funções: clique no botão "Adicionar" e adicione as funções disponíveis

Clique no botão Salvar.

![02](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Create-API-Token-02.png?raw=true)

Agora que o login pode ser feito, preencha os campos conforme solicitado, incluindo os dados do Token criado na etapa anterior.

![03](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Login-01.png?raw=true)

Após o login, é necessário configurar a Chave de Acesso e o Nome da Conta Global. Clique no item Controlador no menu lateral e preencha os valores que podem ser encontrados na interface de licença do AppDynamics.

![04](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Controller-01.png?raw=true)

Alguns agentes serão atualizados usando playbook ansible e outros agentes por meio de suas próprias APIs.

For agents updated with ansible it is necessary to configure access to the server where the agent is running. This access is safe and performed within the client's environment, no external access is necessary and only the customer will have access to the ACC server where the access key will be configured.

To configure access (certificate), follow these steps:

- Place a certificate of access to the server where the agent is running on the server where the ACC is running, for example in the path: /home/user_services/.ssh/user_services.cer
- Click on KEYS menu item
- Click on "Add" new key

Now agents can be updated!

![05](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Keys-01.png?raw=true)

To list the agents, click on the Agents item in the side menu.

![06](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/AgentsfromAppD-01.png?raw=true)

To update the agent version, click on the "play" corresponding to the agent.

The interface will automatically identify the agent type and ask for the information needed to update the agent. Enter the requested data and click on "Create Task"

![07](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/UpdateAgent-02.png?raw=true)

An Ansilbe or API task will be created, depending on the type of the recognition agent automatically.

To see the result of the update, click on the Task item in the menu and then on the task to be viewed.

![08](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Task-01.png?raw=true)

![09](https://github.com/Appdynamics/agent-control-center/blob/main/docimages/Task-02.png?raw=true)

IMPORTANT: the application needs to be restarted to recognize the new agent version.
