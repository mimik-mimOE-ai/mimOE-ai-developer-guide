# Setting Up a Multiple Agent Machine Scenario

- [Setting Up a Multiple Agent Machine Scenario](#setting-up-a-multiple-agent-machine-scenario)
- [What You Need to Have On Hand](#what-you-need-to-have-on-hand)
- [What You'll be Doing](#what-youll-be-doing)
- [Configuring the new Agent Machine](#configuring-the-new-agent-machine)
  - [Step 1: Navigate to the working directory for this scenario](#step-1-navigate-to-the-working-directory-for-this-scenario)
  - [Step 2: Create the .env and setup.http files for each Agent Machine](#step-2-create-the-env-and-setuphttp-files-for-each-agent-machine)
  - [Step 3: Configure the .env files](#step-3-configure-the-env-files)
  - [Step 4: Execute the setup.http files in the Agent Machine working directories](#step-4-execute-the-setuphttp-files-in-the-agent-machine-working-directories)
- [Configuring the new Agent Collection on the Coordinator Machine](#configuring-the-new-agent-collection-on-the-coordinator-machine)
  - [Step 1: Navigate back to the root directory of the working directory](#step-1-navigate-back-to-the-root-directory-of-the-working-directory)
  - [Step 2: Create the .env file](#step-2-create-the-env-file)
  - [Step 3: Configure the .env file](#step-3-configure-the-env-file)
  - [Step 4: Execute the commands in setup.http](#step-4-execute-the-commands-in-setuphttp)
- [Getting an Instance of the User Console Up and running](#getting-an-instance-of-the-user-console-up-and-running)
  - [Step 1: Configuring the sitedata.js file](#step-1-configuring-the-sitedatajs-file)
  - [Step 2: Running the User Console web server](#step-2-running-the-user-console-web-server)


The purpose of Scenario 3 is to demonstrate how to add Agent Machines to the mimik Service Mesh and then to modify the existing Coordinator Machine by adding a new Agent Collection that supports Multi Agent Machines.

The machines in the scenario are the Agent Machines created previously in Scenario 1 and 2, plus a new Agent Machines you'll create in this scenario.

# What You Need to Have On Hand

This scenario requires that you have an additional machine on hand with either AMD/Intel or ARM processors. Each computer needs to be running the [latest version of edgeEngine](https://github.com/mimik-mimOE/mimOE-SE-Linux).

**We also assume** that you have done Scenario 1 and Scenario 2 previously and that the machines configured and added the mimik Service Mesh in those scenarios are operational and accessible.

# What You'll be Doing

In this scenario, you will provision a new Agent Machine using Visual Studio REST Client `setup.http` files.

Then, you'll define a new Agent Collection on the existing Coordinator Machine that has the new Agent Machine created in this scenario along with the two Agent Machines created previously in Scenario 1 and Scenario 2.

Finally, you'll create an instance of the User Console web server. You'll configure the User Console web server to work with the newly created Agent Collection. Once the User Console web server is configured, you'll be able to submit AI prompts to the mimik Service Mesh via the Coordinator Machine.

The Coordinator Machine will return a result that includes the response from each Agent Machine in the new Agent Collection. Also, the Coordinator Machine will return a unified response composed of the responses from each Agent Machine.

|IMPORTANT NOTE|
|:----:|
|The **maximum** number of Agent Machines an Agent Collection can have using the default LLM for this scenario, [gemma-2b-it-q4_k_m.gguf](https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/tree/main) is 3.|

# Configuring the new Agent Machine

Execute the following steps to get the new Agent Machines up and running.

## Step 1: Navigate to the working directory for this scenario

Execute the following command in a terminal window to navigate to the root directory of the file system of your local copy of the Developer Guide repository.

```
cd 03-multi-agent-architecture
```


## Step 2: Create the .env and setup.http files for each Agent Machine

The file named `env.template` contains the declaration of the environment variables that the two Agent Machine `setup.http` files need. Execute the following command in a terminal window to copy the contents of the `env.template` into the `.env` file for the new Agent Machine.

```
cp ./env.template .env
```


## Step 3: Configure the .env files

Add the required values to the environment variables in the `.env` files in `agent-machine-03` and `agent-machine-04`

Here is an example of a properly configured `.env` file:

```
# Environment variables for the Agent Machines
MODEL_URL=https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-q4_k_m.gguf?download=true
HOST_IP_ADDRESS=192.168.86.48
CLIENT_ID=a5efxxxx-1fce-469a-xxxx-3827xxxxa759
DEVELOPER_ID_TOKEN=eyJhbGcixxxxxxxxxxxIsInR5cCI6IkpXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhuYjFxb2YyY2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4NDxxxxxxxxxxxxWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwQGV4YW1wbGUuY29tIiwiYXVkIjoiYTVlZmUzY2ItMWZjZS00NjlhLWI4YWYtMzgyNzljODdhNzU5IiwiZXhwIjoxNzI2ODY5MDQ4LCJpYXQiOjE3MjQyNzcwNDgsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.YjEgCWTy0SpAP8pJwBG5P3ph2Z4mrCoexxxxxxxxxxxU8JhgLckim0vx2K-247nfnXyVx4orDR5ig8zBbnM0eGoizYVCvIxSsSD-UwuJoDNj3M1QTqsrzB__vlyzh8KRT6n5biTa4TT7ciUFHnTKiGYSdkMqomCc2muDrsnE9xG47g34qpLbnuKW3ZQJlcvkyeCxuVgD4TwNef_q4jlS22xhcCSvLaSLxP4M-xxxxxxxxxxxxxJpk2WNQ2DW-4CVnTMs6zZwBQcBtctE5o9WW8jdUofqs_o8aDVBJv89TW3nkdcLSiCSnAobw9SqoZginG9m1rejNqCr-pmAPLKIc-7u0Q
API_KEY=1234
```


## Step 4: Execute the setup.http files in the Agent Machine working directories

Go to the `setup.http` file in the working directory and execute the commands in the file using VS Code's REST Client extension

---

**NOTE:** When running `Step 1` in the `setup.http` make sure to save the value of the `nodeId` that gets returned from this command:

```
#### Step 1:
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getMe", "params": [], "id": 1}

```

You'll need the `nodeId` values when you add an additional Agent Collection to the Coordinator Machine.

The following code snippet is an example of the output returned from the command shown above. Notice that the `nodeId`, in this case, is `8bafdd2a35e17133011bbc98062f132a4c5aca249a82936d0d27a49a`.

```
HTTP/1.1 200 OK
Access-Control-Allow-Methods: GET, POST, DELETE, PUT, OPTIONS
Access-Control-Allow-Origin: *
Connection: close
Content-Length: 342
Content-Type: application/json
Date: Wed, 21 Aug 2024 22:44:00 GMT

{
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "accountId": "d4011bb5-81dd-4011-9471-d76b56e001d7__2972174601916518400",
    "linkLocalIp": "192.168.86.35",
    "name": "pi2",
    "nodeId": "8bafdd2a35e17133011bbc98062f132a4c5aca249a82936d0d27a49a",
    "supernodeTypeName": "_mk-v15-4996e4c2442cc796f2c0ddb4e5e1627d._tcp",
    "version": "v3.11.0.ml.71.g577be1f5 (developer edition)"
  }
}
```

---


# Configuring the new Agent Collection on the Coordinator Machine


## Step 1: Navigate back to the root directory of the working directory

Go back to the root directory of the file system for this repository.

## Step 2: Create the .env file

In a terminal window, execute the following command to copy the contents of the file `./coordinator-machine/env.template` into the file `./coordinator-machine/.env`.

```
cp ./03-multi-agent-architecture/coordinator-machine/env.template ./03-multi-agent-architecture/coordinator-machine/.env
```


## Step 3: Configure the .env file

Configure the `.env` file in the directory `03-multi-agent-architecture/coordinator-machine/` with the required information.

Here is the format of the `.env` file in need of values for the required environment variables:

```
# Environment variables for the Coordinator Machine
IP_ADDRESS_AGENT_1=<IP_ADDRESS_AGENT_1_MACHINE>
IP_ADDRESS_NVIDIA_AGENT=<IP_ADDRESS_NVIDIA_1_MACHINE>
IP_ADDRESS_AGENT_3=<IP_ADDRESS_AGENT_3_MACHINE>

HOST_IP_ADDRESS=<IP_ADDRESS_OF_COORDINATOR_MACHINE>

NODE_ID_AGENT_1=<NODE_ID_FOR_MACHINE_1_IN_AGENT_COLLECTION>
NODE_ID_NVIDIA_AGENT=<NODE_ID_FOR_MACHINE_2_IN_AGENT_COLLECTION>
NODE_ID_AGENT_3=<NODE_ID_FOR_MACHINE_3_IN_AGENT_COLLECTION>

NODE_ID_COORDINATOR=<NODE_ID_FOR_COORDINATOR_MACHINE>

MODEL_URL=https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-q4_k_m.gguf?download=true

CLIENT_ID=<YOUR_CLIENT_ID>
DEVELOPER_ID_TOKEN=<YOUR_DEVELOPER_ID>
API_KEY=1234
AGENT_COLLECTION_NAME=multi-agent-collection
```

Here is an example of a properly configured `.env` file for the Coordinator Machine for this scenario:

```
# Environment variables for the Coordinator Machine
IP_ADDRESS_AGENT_1=192.168.86.41
IP_ADDRESS_NVIDIA_AGENT=192.168.86.45
IP_ADDRESS_AGENT_3=192.168.86.35

HOST_IP_ADDRESS=192.168.86.21

NODE_ID_AGENT_1=85513d8f180efd7d645af637a2278081097b60ecba3c48cbf615aed9
NODE_ID_NVIDIA_AGENT=65769ff83022ce50028486c68a364f61e2feedcc750b2acd87b1605d
NODE_ID_AGENT_3=8bafdd2a35e17133011bbc98062f132a4c5aca249a82936d0d27a49a

NODE_ID_COORDINATOR=62de3e67c00fcce7abd6a6634eb4686653156454b97a5ed8849e975c

MODEL_URL=https://huggingface.co/lmstudio-ai/gemma-2b-it-GGUF/resolve/main/gemma-2b-it-q4_k_m.gguf?download=true
CLIENT_ID=a5efxxxx-1fce-469a-xxxx-3827xxxxa759
DEVELOPER_ID_TOKEN=eyJhbGcixxxxxxxxxxxIsInR5cCI6IkpXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhuYjFxb2YyY2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4NDxxxxxxxxxxxxWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwQGV4YW1wbGUuY29tIiwiYXVkIjoiYTVlZmUzY2ItMWZjZS00NjlhLWI4YWYtMzgyNzljODdhNzU5IiwiZXhwIjoxNzI2ODY5MDQ4LCJpYXQiOjE3MjQyNzcwNDgsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.YjEgCWTy0SpAP8pJwBG5P3ph2Z4mrCoexxxxxxxxxxxU8JhgLckim0vx2K-247nfnXyVx4orDR5ig8zBbnM0eGoizYVCvIxSsSD-UwuJoDNj3M1QTqsrzB__vlyzh8KRT6n5biTa4TT7ciUFHnTKiGYSdkMqomCc2muDrsnE9xG47g34qpLbnuKW3ZQJlcvkyeCxuVgD4TwNef_q4jlS22xhcCSvLaSLxP4M-xxxxxxxxxxxxxJpk2WNQ2DW-4CVnTMs6zZwBQcBtctE5o9WW8jdUofqs_o8aDVBJv89TW3nkdcLSiCSnAobw9SqoZginG9m1rejNqCr-pmAPLKIc-7u0Q
API_KEY=1234
AGENT_COLLECTION_NAME=multi-agent-collection
```

## Step 4: Execute the commands in setup.http

The file `setup.http` contains the commands for creating the Agent Collection that includes the Agent and Nvidia , along with the new Agent Machines created in this scenario.

Under Visual Studio Code, execute the code commands in `./coordinator-machine/setup.http`


# Getting an Instance of the User Console Up and running

![Scenario 3 User Console](./user-console/images/user-console-01.png);

Getting the User Console up and running is a two-step process. First, you need to configure the `sitedata.json` file with the necessary runtime information. Then you need to start the User Console web server.

## Step 1: Configuring the sitedata.js file

Set the IP address of the Coordinator Machine in the file named `./user-console/sitedata.js`. This information is stored in JSON format as follows:

---

```
config = {
  "API_KEY": "1234",
  "COORDINATOR_IP_ADDRESS": <IP_ADDRESS_OF_COORDINATOR_IP_ADDRESS>>
  "AGENT_COLLECTION_NAME": "standard-node-nvidia-collection"
};
```

Here is an example of a properly configured `sitedata.js` file.

---

```
config = {
  "API_KEY": "1234",
  "CCOORDINATOR_IP_ADDRESS": "192.168.86.21",
  "AGENT_COLLECTION_NAME": "standard-node-nvidia-collection"
};
```

Once the `sitedata.js` file has been configured, you're ready to start the web server.

## Step 2: Running the User Console web server

In a terminal window, navigate to the  `03-multi-agent-architecture/user-console` directory and start the web server by executing the following command:



---

```
python3 -m http.server 8005
```

**NOTE:** Although the default port number on which the User Console runs is `8000`, in this case, we're going to have the web server listen on port `8005` to avoid any collision with the User Console web server started in the previous scenarios.