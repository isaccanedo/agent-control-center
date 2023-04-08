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

Para agentes atualizados com ansible é necessário configurar o acesso ao servidor onde o agente está rodando. Este acesso é seguro e realizado dentro do ambiente do cliente, não sendo necessário acesso externo e somente o cliente terá acesso ao servidor ACC onde será configurada a chave de acesso.

Para configurar o acesso (certificado), siga os seguintes passos:

- Coloque um certificado de acesso ao servidor onde o agente está rodando no servidor onde o ACC está rodando, por exemplo no caminho: /home/user_services/.ssh/user_services.cer
- Clique no item de menu CHAVES
- Clique em "Adicionar" nova chave

Agora os agentes podem ser atualizados!

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
