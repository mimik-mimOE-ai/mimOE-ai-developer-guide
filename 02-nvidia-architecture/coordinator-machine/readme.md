# Updating the Coordinator Machine to support the Nvidia Agent Machine.

- [Updating the Coordinator Machine to support the Nvidia Agent Machine.](#updating-the-coordinator-machine-to-support-the-nvidia-agent-machine)
- [What you will be doing](#what-you-will-be-doing)
- [What you'll need before you start](#what-youll-need-before-you-start)
- [Updating the Coordinator Machine](#updating-the-coordinator-machine)
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


This document describes how to update the Coordinator Machine you created and configured in the previous scenario to support accessing a new Agent Collection that you will create in this part of the demonstration scenario. The new Agent Collection will include the Nvidia device that you added to the mimik Service Mesh in the first part of this scenario.

# What you will be doing

As mentioned above, in this part of the demonstration scenario you will be working with the existing Coordinator Machine you created in the previous scenario. The task at hand will be to execute the steps described in `setup.http` file that is included in the directory in which this readme file is stored.

# What you'll need before you start

Before you start you'll need to make sure the Coordinator Machine you created in the previous scenario is up and running. (The `setup.http` file for this set of steps includes a step that checks to make sure the Coordinator Machine is active.)

Also, you'll need to have on hand the `nodeId` of the Agent Machine created in the previous scenario as well as the `nodeId` of the Nvidia Agent Machine you created earlier in this scenario.

# Updating the Coordinator Machine

Getting the Coordinator Machine up and running involves creating and configuring the `.env` that the `setup.http` uses to get its runtime information. Then, once the `.env` file is configured, you'll run the steps in the `setup.http` file. The following sections describe the details.


## Creating and configuring the .env file

Before you start configuring the `.env` file you need to have a `client Id token` and a `developer Id token` on hand. You get these tokens from the mimik Developer Console as described in a previous readme file [here](../../errata/getting-id-tokens.md).

Also, you will need to have the `nodeId` for the Agent Machine you set up in the previous scenario,the `nodeId` for the Nvida device set up in this scenario, and the `nodeId` for the Coordinator Machine setup in the previous scenario. 

Make sure you have these tokens on hand before you continue.

You'll need to provide a value for the `AGENT_COLLECTION_NAME` that will be the unique identifier of the Agent Collection in this scenario. The Coordinator Machine will interact with this named Agent Collection within this scenario to process prompts. (The `AGENT_COLLECTION_NAME`  is a unique, arbitrary value.) You can learn more about the nature and use of Agent Collections [here](../../readme.md#understanding-agent-collections).

Once you have the following on hand...

* `client Id token`
* `developer Id token`
* the `nodeId` for the Agent Machine you set up in the previous scenario
* the `nodeId` for the Nvida device set up in this scenario
* the `nodeId` for the Coordinator Machine setup in the previous scenario

... you will copy the contents of the file `env.template` into the and `.env` file that will be located in the same directory as the `setup.http` file.


### Step 1

From within the directory where this readme file is located, execute the following command in a terminal window to copy the contents of the file `env.template` into the and `.env`.

```
cp env.template .env
```

### Step 2

The following is an example of a `.env` file that has placeholders for the required environment variable values.

---

```
# Environment variables for the Controller machine
NODE_ID_AGENT_1=TO_BE_DETERMINED
NODE_ID_NVIDIA_AGENT=TO_BE_DETERMINED
NODE_ID_COORDINATOR=TO_BE_DETERMINED
MODEL_URL=https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-q4_k_m.gguf?download=true
HOST_IP_ADDRESS=<IP_ADDRESS_OF_THE_COORDINATOR_COMPUTER>
CLIENT_ID=<YOUR_CLIENT_ID_TOKEN>
DEVELOPER_ID_TOKEN=<YOUR_DEVELOPER_ID_TOKEN>
API_KEY=1234
AGENT_COLLECTION_NAME=<ARBITRARY_AGENT_COLLECTION_NAME>
```

Add the values for the `client Id token`, `developer Id token` and various `nodeId`s as described above.

Also, you will need to provide the IP address of the Coordinator Machine that provisioned in the previous scenario. In addition you will need to provide a unique, arbitrary value for the `AGENT_COLLECTION_NAME` environment variable.

Here is an example of a properly configured `.env` file.

```
NODE_ID_AGENT_1=65769ff83022ce50028486c68a364f61e2feedcc750b2acd87b1605d
NODE_ID_NVIDIA_AGENT=85513d8f180efd7d645af637a2278081097b60ecba3c48cbf615aed9
NODE_ID_COORDINATOR=62de3e67c00fcce7abd6a6634eb4686653156454b97a5ed8849e975c
MODEL_URL=https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-q4_k_m.gguf?download=true
HOST_IP_ADDRESS=192.168.86.21
CLIENT_ID=xxxxe3cb-1fce-xxxx-b8af-38xxxx87a759
DEVELOPER_ID_TOKEN=eyJhbGcixxxxxxxxxxxxNiIsInR5cCI6IkpXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhuYjFxb2YyY2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4xxxxxxxxxx1haWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwQGV4YW1wbGUuY29tIiwiYXVkIxxxxxxxxxxzY2ItMWZjZS00NjlhLWI4YWYtMzgyNzljODdhNzU5IiwiZXhwIjoxNzI1NDY5MTMxLCJpYXQiOjE3MjI4NzcxMzEsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.TbspXGBqejwYxxxxxxxxxxEbHQpMQ1snwrKPzrFVOTBFom_i5n-r13Cr8oxaxxxxxxxxxxxx1HYnN2XTgP0cp6_nwSl7hSM00AR5hwFtmnhyHKV2NLkqb90t-YrwSNErdWqLLeh8GDcNYO7XLG69FgJuTtUMbsmV_QsW70imgKozr_hNqAPXg6SgApaMJPdbe-5Z94ZFsqkYb8diD2-675RQXozPHWIoPNkebNCAMGLupKZEnLIhsHHobNvlb7ZmxUZGhEpxGwcY9qxQ4N3E-tlZFVJ7hzSx0OXgUJGowJDHY04NUg8dreqnCUq2o0-TpGDSxxxxxxxxxxkWLD6fQA
AGENT_COLLECTION_NAME=standard-node-nvidia-collection
```

Once you've configured the `.env` file, run the commands in the `setup.http` file from within Visual Studio Code.

The next section describes in detail the purpose of each command.

## Running the commands in the setup.http file

The following code snippet shows the various REST Client file variables and their values.

---

```
### Configuration 
@host = http://{{$dotenv HOST_IP_ADDRESS}}:8083
@developerIdToken={{$dotenv DEVELOPER_ID_TOKEN}}
@clientId={{$dotenv CLIENT_ID}}
@apiKey={{$dotenv API_KEY}}

@agentCollectionName={{$dotenv AGENT_COLLECTION_NAME}}

### Microservice
@maiTarName = mai-v1-1.7.0.tar

###Settings
@tokenScope=openid edge:mcm edge:clusters edge:account:associate
@modelUrl={{$dotenv MODEL_URL}}

### Node Info
### Set the following values using the information returned from each constituent node's setup.http file.
@nodeId1_AI-CHAT-1 = {{$dotenv NODE_ID_AGENT_1}}
@nodeId2_AI-CHAT-2 = {{$dotenv NODE_ID_NVIDIA_AGENT}}

@nodeId_COORDINATOR = {{$dotenv NODE_ID_COORDINATOR}}
```
### Step 1

**Step 1** makes sure the Coordinator Machine is accessible on the mimik Service Mesh.

---

```
#### Step 1: Query the target device. This call returns the NODE_ID for the device and verify that the device is accessible.
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getMe", "params": [], "id": 1}
```

### Step 2

**Step 2** gets an `edgeToken`.

---

```
#### Step 2: Get edgeIdToken
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getEdgeIdToken", "params": [], "id": 1}

#### Save Token  to the local file variable
@edgeIdToken={{jsonrpc.response.body.$.result.id_token}}
```

### Step 3

**Step 3:** gets an `accessToken` so as to be able to configure the Coordinator Machine.

---

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

####
@edgeToken={{mid.response.body.$.access_token}}
```

### Step 4


**Step 4** associates the Access Token to the machine.

---
```
#### Step 4: Associate device with account 
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "associateAccount", "params": ["{{edgeToken}}"], "id": 1}
```

### Step 5

**Step 5** verifies that the microservices installed in the previous scenario are up and running

---

```
#### Step 5: Verify that the miscroservices are running
GET {{host}}/mcm/v1/containers
Authorization: Bearer {{edgeToken}}
```

### Step 6

**Step 6** Verifies that the LLM that was installed in the previous scenario is available

---

```
### Step 6: Verify that the model has been deployed 
GET {{host}}/api/mim/v1/models
Content-Type: application/json
Authorization: bearer {{apiKey}}
```

### Step 7

**Step 7** creates a new Agent Collection on the Coordinator Machine

**BE ADVISED:** This is a very important step!

---

```
#### Step 7: Declare the named Agent Collection using the file variable agentCollectionName as the unique identifier along with the machines and associated models that make up the collection
POST {{host}}/api/mai/v1/models
Content-Type: application/json
Authorization: bearer {{apiKey}}

{
  "id": "{{agentCollectionName}}",
  "object": "model",
  "modelfile": {
    "prompts": [
      {
        "url": "{{nodeId1_AI-CHAT-1}}@mmesh/{{clientId}}/mim/v1/chat/completions",
        "model": "lmstudio-ai/gemma-2b-it-GGUF",
        "apikey": "Bearer {{apiKey}}",
        "required": true
      },
      {
        "url": "{{nodeId2_AI-CHAT-2}}@mmesh/{{clientId}}/mim/v1/chat/completions",
        "model": "lmstudio-ai/gemma-2b-it-GGUF",
        "apikey": "Bearer {{apiKey}}",
        "required": false
      }
    ],
    "summary": {
      "template": "Given the responses from assistants below, synthesize the information to create a unified, concise summary. Provide a coherent answer that integrates these perspectives.\n-----\n\n${{mergedContent}}",
      "url": "{{nodeId_COORDINATOR}}@mmesh/{{clientId}}/mim/v1/chat/completions",
      "model": "lmstudio-ai/gemma-2b-it-GGUF",
      "apikey": "Bearer {{apiKey}}",
      "required": true
    }
  },
  "owned_by": "mimik"
}
```

### Step 8

**Step 8** exercises the Agent Collection by sending in an initial prompt

**IMPORTANT:** Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API's.

---

```
######
#### Step 8: Exercise the Agent Collection by sending in an initial prompt
### Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API's
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

### Step 9

**Step 9** sends in a follow-up prompt

**IMPORTANT:** Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API's.

---

```
######
#### Step 9: Send in a follow up prompt
### Execute using VS Code's Copy Request as cURL because VS Code doesn't know how to handle streaming API's
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

### Step 10

**Step 10** views the logs. (This step is an optional step.)

---

```
### Step 10: view the logs
GET {{host}}/api/mai/v1/logs
Authorization: bearer {{apiKey}}
```

---

Now that you've reviewed the details presented in the code snippets above, go to the `setup.http` file at `02-nvidia-architecture/coordinator-machine/setup.http` and execute the commands therein.

After completing the process to get the Coordinator Machine up and running you will get the User Console web server up and running. The User Console web server will be configured to use the Coordinator Machine as the target against which to submit prompts against the Agent Collection created in this scenario.


