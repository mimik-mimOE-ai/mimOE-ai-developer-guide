# Setting up a Coordinator Machine for a Single Agent Collection Scenario

- [Setting up a Coordinator Machine for a Single Agent Collection Scenario](#setting-up-a-coordinator-machine-for-a-single-agent-collection-scenario)
- [What you need to have on hand](#what-you-need-to-have-on-hand)
- [What you'll be doing](#what-youll-be-doing)
- [Getting the Coordinator Machine up and running](#getting-the-coordinator-machine-up-and-running)
  - [Creating and configuring the .env file](#creating-and-configuring-the-env-file)
    - [Step 1](#step-1)
    - [Step 2](#step-2)
  - [Running the commands in the setup.http file](#running-the-commands-in-the-setuphttp-file)
    - [Step 1](#step-1-1)
    - [Step 2](#step-2-1)
    - [Step 3](#step-3)
    - [Step 4](#step-4)
    - [Step 5](#step-5)
    - [Step 6](#step-6)
    - [Step 7](#step-7)
    - [Step 8](#step-8)
    - [Step 9](#step-9)
    - [Step 10](#step-10)
    - [Step 11](#step-11)
    - [Step 12](#step-12)
    - [Step 13](#step-13)
    - [Step 14](#step-14)
    - [Step 15](#step-15)
    - [Step 16](#step-16)


The purpose of this document is to explain the steps to take to get a Coordinator Machine up and running for a Single Agent Collection demonstration scenario.

**NOTE:** This Coordinator Machine will be used in all of the demonstration scenarios described in this documentation. Thus, you will only do the complete setup of the Coordinator Machine once. In later scenarios, you will declare additional Agent Collections in this Coordinator Machine.

# What you need to have on hand

In order to implement this scenario you will need:

* A Ubuntu 22.04 machine running the [mimOE.ai release of edgeEngine](https://github.com/mimik-mimOE/mimOE-SE-Linux/).
* The Ubuntu machine needs to have port 8083 exposed

# What you'll be doing

In this scenario, you will:

* Create and configure the `.env` with the required environment variables
* Execute the commands in the accompanying `setup.http` file according the instructions described in the document.

# Getting the Coordinator Machine up and running

Getting the Coordinator Machine up and running involves creating and configuring the `.env` that the `setup.http` uses to get its runtime information. Then, once the `.env` file is configured, you'll run the steps in the `setup.http` file. The following sections describe the details.

## Creating and configuring the .env file

Before you start configuring the `.env` file you need to have a `client Id token` and a `developer Id token` on hand. You get these tokens from the mimik Developer Console as described in a previous readme file [here](../../readme.md#getting-the-clientid-token-and-the-developerid-token). Make sure you have these tokens on hand before you continue.

Also, you'll need to provide a value for the `AGENT_COLLECTION_NAME` that will be the unique identifier of the single Agent Machine collection that the Coordinator Machine will interact with to process prompts. (The `AGENT_COLLECTION_NAME`  is a unique, arbitrary value.) You can learn more about the nature and use of Agent Collections [here](../../readme.md#understanding-agent-collections).

Once you have the `client Id token` and a `developer Id token` on hand you are going to copy the contents of the file `env.template` into the and `.env` file that will be located in the same directory as the `setup.http` file.

### Step 1

From within the directory where this readme file is located, execute the following command in a terminal window to copy the contents of the file `env.template` into the and `.env`.

```
cp env.template .env
```

The `.env` file will have the following content

```
# Environment variables for the Coordinator Machine
NODE_ID_AGENT_1=<NODE_ID_OF_THE_AGENT_MACHINE>
NODE_ID_COORDINATOR=<NODE_ID_OF_THE_COORDINATOR_MACHINE>
MODEL_URL=https://huggingface.co/lmstudio-community/gemma-1.1-2b-it-GGUF/resolve/main/gemma-1.1-2b-it-Q8_0.gguf?download=true
HOST_IP_ADDRESS=<IP_ADDRESS_OF_THE_COORDINATOR_COMPUTER>
CLIENT_ID=<YOUR_CLIENT_ID_TOKEN>
DEVELOPER_ID_TOKEN=<YOUR_DEVELOPER_ID_TOKEN>
API_KEY=1234
AGENT_COLLECTION_NAME=<ARBITRARY_NAME_OF_AGENT_AGGREGATION>
```

Here is an example of the `.env` file with environment variable values added:

```
# Environment variables for the Controller machine
NODE_ID_AGENT_1=85513d8f180efd7d645af637a2278081097b60ecba3c48cbf615aed9
NODE_ID_COORDINATOR=62de3e67c00fcce7abd6a6634eb4686653156454b97a5ed8849e975c

MODEL_URL=https://huggingface.co/lmstudio-community/gemma-1.1-2b-it-GGUF/resolve/main/gemma-1.1-2b-it-Q8_0.gguf?download=true
HOST_IP_ADDRESS=192.168.86.21
CLIENT_ID=a5efxxxx-1fce-469a-xxxx-38279c87xxxx
DEVELOPER_ID_TOKEN=eyJhbGciOiJSUzI1NiIsIxxxxxxxxxxXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhxxxxxxxxxx2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4NDAwIiwiZW1haWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwxxxxxxxxxxUuY29tIiwiYXVkIjoiYTVlZmUzY2ItMWZjZS00NjlhLWI4xxxxxxxxxxljODdhNzU5IiwiZXhwIjoxNxxxxxxxxxxxLCJpYXQiOjE3MjI4NzcxMzEsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.TbspXGBqejwYLjTSAVVy4YEbHQpMQ1snwrKPzrFVOTBFom_i5n-r13Cr8oxaxcw4CpvhyZak1HYnN2XTgP0cp6_nwSl7hSM00AR5hwFtmnhyHKV2NLkqb90t-YrwSNErdWqLLeh8GDcNYO7XLG69FgJuTtUMbsmV_QsW70imgKozr_hNqAPXg6SgApaMJPdbe-5Z94ZFsqkYb8diD2-675RQXozPHWIoPNkebNCAMGLupKZEnLIhsHHobNvlb7ZmxUZGhEpxGwcY9qxQ4N3E-tlZFVJ7hzSx0OXgUJGxxxxxxxxxxg8dreqnCUq2o0-TpGDSBNuw2Nxm1RkWLD6fQA
API_KEY=1234
AGENT_COLLECTION_NAME=single-agent-collection
```

### Step 2

You will need to add the values for your `client Id token`,  `developer Id token`, `nodeId` of the Agent Machine, and `nodeId` of the Coordinator Machine, to the `.env` file according to the placeholders described above.

Also, you will need to provide the IP address of the Coordinator Machine that you will provision using the `setup.http`. In addition you will need to provide a unique, arbitrary value for the `AGENT_COLLECTION_NAME` environment variable.

Once you've configured the `.env` file, run the commands in the `setup.http` file from within Visual Studio Code.

The next section describes in detail the purpose of each command.

## Running the commands in the setup.http file

The following code snippets describe the details about the commands that will be executed from within the `setup.http` file.

The first few lines of the `setup.http` file as shown below creates the REST Client file variables that the `setup.http` file needs.

```
### Configuration 
@host = http://{{$dotenv HOST_IP_ADDRESS}}:8083
@developerIdToken={{$dotenv DEVELOPER_ID_TOKEN}}
@clientId={{$dotenv CLIENT_ID}}
@apiKey={{$dotenv API_KEY}}

@agentCollectionName={{$dotenv AGENT_COLLECTION_NAME}}

### Microservices
@maiTarName = mai-v1-1.7.0.tar
@mlmTarName = mim-v1-1.6.0.tar
###Settings
@tokenScope=openid edge:mcm edge:clusters edge:account:associate
@modelUrl={{$dotenv MODEL_URL}}

### Node Info
### Set the following values using the information returned from each constituent node's setup.http file.
@nodeId_AGENT_MACHINE_1 = {{$dotenv NODE_ID_AGENT_1}}
@nodeId_COORDINATOR = {{$dotenv NODE_ID_COORDINATOR}}
```

### Step 1

**Step** 1 as shown below is a command that queries the edgeEngine instance running on the targeted Agent Machine to get run time information.

**NOTE:** Step 1 will return a `nodeId` as described in a previous readme [here](../../readme.md#getting-a-nodeid). Save the `nodeId` value once it's returned. You'll need it when you are configuring the Coordinator Machine later on.

```
### Setup API's 

#### Step 1: Get Target Device Information. This call returns the NODE_ID for the device
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getMe", "params": [], "id": 1}
```

### Step 2

**Step 2**, described below, returns the value for the `edgeId` token and assigns it the file variable `@edgeIdToken`. The `edgeId` token is required to get an Access Token from the edgeEngine instance running on the targeted Agent Machine.

To learn more about the purpose and use of an Access Token, read the details in the [mimik Developer Documentation](https://devdocs.mimik.com/key-concepts/03-index#accesstoken).

```
#### Step 2: Get edgeIdToken
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getEdgeIdToken", "params": [], "id": 1}

#### Save ID Token to a local file variable
@edgeIdToken={{jsonrpc.response.body.$.result.id_token}}
```

### Step 3

**Step 3** executes the POST command that gets an Access Token that will associated in the next step.

```
#### Step 3: Get Access Token
# @name mid
POST https://devconsole-mid.mimik.com/token
Content-Type: application/x-www-form-urlencoded

client_id={{clientId}}
&grant_type=id_token_signin
&id_token={{developerIdToken}}
&scope={{tokenScope}}
&edge_id_token={{edgeIdToken}}

#### Save Access Token to a local file variable
@edgeToken={{mid.response.body.$.access_token}}
```

### Step 4

**Step 4** associates the Access Token retrieved previously to the running instance of edgeEngine. The Access Token enables the Agent Machine to be part of the mimik Service Mesh. To learn more about the details of the mimik Service mesh, read the webpage [Understanding the edgeEngine Service Mesh](https://devdocs.mimik.com/key-concepts/06-index) in the mimik Developer Documentation.

```
#### Step 4: Associate device with account 
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "associateAccount", "params": ["{{edgeToken}}"], "id": 1}
```

### Step 5

**Step 5** Deploys the `mAI` microservice

```
### Step 5: Deploy mAI microservice
POST {{host}}/mcm/v1/images
Content-Type: multipart/form-data; boundary=$Boundary$
Authorization: Bearer {{edgeToken}}

--$Boundary$
Content-Disposition: form-data; name="image"; filename="{{maiTarName}}"

< ../deploy/{{maiTarName}}
--$Boundary$--
```

### Step 6

**Step 6** Starts the `mAI` microservice is installed.

```
#### Step 6: Start the mAI Microservice
POST {{host}}/mcm/v1/containers
Authorization: Bearer {{edgeToken}}

{
    "name": "mai-v1",
    "image": "mai-v1",
    "env": {
      "MCM.BASE_API_PATH": "/mai/v1",
      "MCM.API_ALIAS": "true",
      "EDGE_ACCESS_TOKEN": "{{edgeToken}}",
      "API_KEY": "{{apiKey}}",
      "MCM.OTEL_SUPPORT": "true"
    }
}
```

### Step 7

**Step 7** deploys the `mILM` microservice

```
### Step 7: Deploy mILM microservice
POST {{host}}/mcm/v1/images
Content-Type: multipart/form-data; boundary=$Boundary$
Authorization: Bearer {{edgeToken}}

--$Boundary$
Content-Disposition: form-data; name="image"; filename="{{mlmTarName}}"

< ../deploy/{{mlmTarName}}
--$Boundary$--
```

### Step 8

**Step 8** starts the `mILM` microservice

```
#### Step 8: Start mILM microservice 
POST {{host}}/mcm/v1/containers
Authorization: Bearer {{edgeToken}}

{
    "name": "mim-v1",
    "image": "mim-v1",
    "env": {
      "MCM.BASE_API_PATH": "/mim/v1",
      "API_KEY": "{{apiKey}}",
      "MCM.API_ALIAS": "true",
      "MCM.OTEL_SUPPORT": "true"
    }
}
```

### Step 9

**Step 9** downloads the AI model directly on the Coordinator Machine.

**IMPORTANT:** Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API.

```
### Step 9: Download model (Google Gemma 2b)
### Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API
POST {{host}}/api/mim/v1/models
Content-Type: application/json
Authorization: bearer {{apiKey}}

{
  "id": "lmstudio-ai/gemma-2b-it-GGUF",
  "object": "model",
  "url": "{{modelUrl}}",
  "owned_by": "lmstudio-ai"
}
```

### Step 10

**Step 10** verifies that both the `mAI` and `mILM` microservices have been deployed.

```
#### Step 10: Get Images to verify deployment
GET {{host}}/mcm/v1/images
Authorization: Bearer {{edgeToken}}
```

### Step 11

**Step 11** verifies that both the `mAI` and `mILM` microservices are running.

```
#### Step 11: Get Containers to verify they're running
GET {{host}}/mcm/v1/containers
Authorization: Bearer {{edgeToken}}
```

### Step 12

**Step 12** verifies that the model has been downloaded

```
### Step 12: View deployed models 
GET {{host}}/api/mim/v1/models
Content-Type: application/json
Authorization: bearer {{apiKey}}
```

### Step 13

**Step 13** declares the Agent Collection and the synthesis prompt

```
#### Step 13: Declare the Agent Collection and the synthesis prompt
POST {{host}}/api/mai/v1/models
Content-Type: application/json
Authorization: bearer {{apiKey}}

{
  "id": "{{agentCollectionName}}",
  "object": "model",
  "modelfile": {
    "prompts": [
      {
        "url": "{{nodeId_AGENT_MACHINE_1}}@mmesh/{{clientId}}/mim/v1/chat/completions",
        "model": "lmstudio-ai/gemma-2b-it-GGUF",
        "apikey": "Bearer {{apiKey}}",
        "required": true
      },
    ],
    "summary": {
      "template": "Given the responses from assistants below, synthesize the information to create a unified, concise summary. Provide a coherent answer that integrates these perspectives.\n-----\n\n${{mergedContent}}",
      "url": "{{@nodeId_COORDINATOR}}@mmesh/{{clientId}}/mim/v1/chat/completions",
      "model": "lmstudio-ai/gemma-2b-it-GGUF",
      "apikey": "Bearer {{apiKey}}",
      "required": true
    }
  },
  "owned_by": "mimik"
}
```

### Step 14

**Step 14** exercises the Coordinator Machine by submitting an initial prompt.

**IMPORTANT:** Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API.

```
#### Step 14: Excercise the Coordinator Machine by submitting an initial prompt
### Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API
POST {{host}}/api/mai/v1/chat/completions
Content-Type: application/json
Authorization: bearer {{apiKey}}

{ 
  "model": "{{agentCollectionName}}",
  "messages": [ 
    { "role": "user", "content": "Give me the 3 most popular sports in the United States." }
  ], 
  "stream": true
}
```

### Step 15

**Step 15** exercises the Coordinator Machine by submitting the follow-up prompt.

**IMPORTANT:** Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API. 

```
#### Step 15: Excercise the Coordinator Machine by submitting the followup prompt
### Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API
POST {{host}}/api/mai/v1/chat/completions
Content-Type: application/json
Authorization: bearer {{apiKey}}

{ 
  "model": "{{agentCollectionName}}",
  "messages": [ 
    { "role": "user", "content": "What are the teams in the most popular sports." }
  ], 
  "stream": true
}
```

### Step 16

**Step 16** views the logs

```
### Step 16: view the logs
GET {{host}}/api/mai/v1/logs
Authorization: bearer {{apiKey}}
```

---

Now that you've reviewed the details presented in the code snippets above, go to the `setup.http` file at `01-single-agent-architecture/coordinator-machine/setup.http` and execute the commands therein.

After completing the process to get the Coordinator Machine up and running you will get the User Console web server up and running. The User Console web server will be configured to use the Coordinator Machine as the target against which to submit prompts.



