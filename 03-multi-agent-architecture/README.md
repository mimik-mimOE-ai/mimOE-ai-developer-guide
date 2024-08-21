# Setting Up a Multiple Agent Machine Scenario

- [Setting Up a Multiple Agent Machine Scenario](#setting-up-a-multiple-agent-machine-scenario)
- [What You Need to Have On Hand](#what-you-need-to-have-on-hand)
- [What You'll be Doing](#what-youll-be-doing)
- [Configuring the Agent Machines](#configuring-the-agent-machines)
  - [Step 1: Create working directories for each Agent Machine](#step-1-create-working-directories-for-each-agent-machine)
  - [Step 2: Navigate to the subdirectory agent-machines](#step-2-navigate-to-the-subdirectory-agent-machines)
  - [Step 3: Create working directories for each Agent Machine](#step-3-create-working-directories-for-each-agent-machine)
  - [Step 4: Configure the .env files](#step-4-configure-the-env-files)
  - [Step 5: Create the setup.http file for each Agent Machine's working directory](#step-5-create-the-setuphttp-file-for-each-agent-machines-working-directory)
  - [Step 6: Execute the setup.http files in the Agent Machine working directories](#step-6-execute-the-setuphttp-files-in-the-agent-machine-working-directories)
- [Configuring the new Agent Collection on the Coordinator Machine](#configuring-the-new-agent-collection-on-the-coordinator-machine)
  - [Step 1: Create the .env file](#step-1-create-the-env-file)
  - [Step 2: Configure the .env file](#step-2-configure-the-env-file)
  - [Step 3: Execute the commands in setup.http](#step-3-execute-the-commands-in-setuphttp)
- [Getting an Instance of the User Console Up and running](#getting-an-instance-of-the-user-console-up-and-running)
  - [Step 1: Configuring the sitedata.js file](#step-1-configuring-the-sitedatajs-file)
  - [Step 2: Running the User Console web server](#step-2-running-the-user-console-web-server)


The purpose of Scenario 3 is to demonstrate how to add Agent Machines to the mimik Service Mesh and then to modify the existing Coordinator Machine by adding a new Agent Collection that supports Multi Agent Machines.

These Multi Agent Machines are the Agent Machines created previously in Scenario 1 and 2, plus the two new Agent Machines you'll create in this scenario.

# What You Need to Have On Hand

This scenario requires that you have on hand two computers with AMD/Intel processors. Each computer needs to be running the latest version of edgeEngine.

We also assume that you have done Scenario 1 and Scenario 2 previously and that the machines configured and added the mimik Service Mesh in those scenarios are operational and accessible.

# What You'll be Doing

In this scenario you will provision two Agent Machines using Visual Studio REST Client `setup.http` files. Then, you'll define a new Agent Collection on the existing Coordinator Machine. Finally, you'll create an instance of the User Console web server. You configure the User Console web server to work with the new Agent Collection. Once the User Console web server is configured, you'll be able to submit AI prompts to Coordinator Machine. The Coordinator Machine will return a result that include the response from each Agent Machine in the new Agent Collection. Also, the Coordinator Machine will return a unified response composed of the responses from each Agent Machine.

# Configuring the Agent Machines

Execute the following steps to get the 2 new Agent Machines up and running.

## Step 1: Create working directories for each Agent Machine

You'll need to create working directories for each of the new Agent Machines. 

From the root of this repository file system and execute the following command in a terminal window to create the working directories for the two Agent Machines.

```
mkdir 03-multi-agent-architecture/agent-machines/agent-machine-03 && mkdir 03-multi-agent-architecture/agent-machines/agent-machine-04
```

## Step 2: Navigate to the subdirectory agent-machines

```
cd 03-multi-agent-architecture/agent-machines
```

## Step 3: Create working directories for each Agent Machine

The file named `env.template` contains the declaration of the environment variables that the two Agent Machine `setup.http` files need. Execute the following command in a terminal window to copy the contents of the `env.template` into the `.env` file for one of the new Agent Machines.

```
cp ./env.template ./agent-machine-03/.env
```

Execute the following command in a terminal window to copy the contents of the `env.template` into the `.env` file for one of the other new Agent Machines.

```
cp ./env.template ./agent-machine-04/.env
```

## Step 4: Configure the .env files

Add the required values to the environment variables in the `.env` files in `agent_machine_03` and `agent_machine_04`

Here is an example of a properly configured `.env` file:

```
# Environment variables for the Agent Machines
MODEL_URL=https://huggingface.co/lmstudio-community/gemma-1.1-2b-it-GGUF/resolve/main/gemma-1.1-2b-it-Q8_0.gguf?download=true
HOST_IP_ADDRESS=192.168.86.48
CLIENT_ID=a5efxxxx-1fce-469a-xxxx-3827xxxxa759
DEVELOPER_ID_TOKEN=eyJhbGcixxxxxxxxxxxIsInR5cCI6IkpXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhuYjFxb2YyY2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4NDxxxxxxxxxxxxWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwQGV4YW1wbGUuY29tIiwiYXVkIjoiYTVlZmUzY2ItMWZjZS00NjlhLWI4YWYtMzgyNzljODdhNzU5IiwiZXhwIjoxNzI2ODY5MDQ4LCJpYXQiOjE3MjQyNzcwNDgsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.YjEgCWTy0SpAP8pJwBG5P3ph2Z4mrCoexxxxxxxxxxxU8JhgLckim0vx2K-247nfnXyVx4orDR5ig8zBbnM0eGoizYVCvIxSsSD-UwuJoDNj3M1QTqsrzB__vlyzh8KRT6n5biTa4TT7ciUFHnTKiGYSdkMqomCc2muDrsnE9xG47g34qpLbnuKW3ZQJlcvkyeCxuVgD4TwNef_q4jlS22xhcCSvLaSLxP4M-xxxxxxxxxxxxxJpk2WNQ2DW-4CVnTMs6zZwBQcBtctE5o9WW8jdUofqs_o8aDVBJv89TW3nkdcLSiCSnAobw9SqoZginG9m1rejNqCr-pmAPLKIc-7u0Q
API_KEY=1234
```

## Step 5: Create the setup.http file for each Agent Machine's working directory

The file `setup.template` has the structure and data that you'll copy into a `setup.http` file for each Agent Machine's working directory. You'll copy the contents of `setup.template` into a `setup.http` file in each Agent Machine's working directory.

In a terminal window, execute the following command to copy the contents of `setup.template` into the `setup.http` file for one of the new Agent Machines.

```
cp ./setup.template ./agent-machine-03/setup.http
```

In a terminal window, execute the following command to copy the contents of `setup.template` into the `setup.http` file for one of the other new Agent Machines.

```
cp ./setup.template ./agent-machine-04/setup.http
```

## Step 6: Execute the setup.http files in the Agent Machine working directories

Go to the `setup.http` file in the working directories for each of the new Agent Machines and run the commands therein.

---

**NOTE:** When running `Step 1` in the `setup.http` make sure to save the value of the `nodeId` that gets returned from this command:

```
#### Step 1:
# @name jsonrpc
POST {{host}}/jsonrpc/v1
Content-Content-Type: application/json

{"jsonrpc": "2.0", "method": "getMe", "params": [], "id": 1}

```

You'll need the two `nodeId` values when you add an additional Agent Collection to the Coordinator Machine.

---


# Configuring the new Agent Collection on the Coordinator Machine

## Step 1: Create the .env file

In a terminal window, execute the following command to copy the contents of the file `./coordinator-machine/env.template` into the file `./coordinator-machine/.env`.

```
cp ./coordinator-machine/env.template ./coordinator-machine/.env
```

## Step 2: Configure the .env file

Configure the `.env` file with the required information.

Here is the format of the `.env` file in need of values for the required environment variables:

```
# Environment variables for the Coordinator Machine
NODE_ID_AGENT_1=<NODE_ID_FOR_MACHINE_3_IN_AGENT_COLLECTION>
NODE_ID_NVIDIA_AGENT=<NODE_ID_FOR_MACHINE_3_IN_AGENT_COLLECTION>
NODE_ID_AGENT_3=<NODE_ID_FOR_MACHINE_3_IN_AGENT_COLLECTION>
NODE_ID_AGENT_4=<NODE_ID_FOR_MACHINE_4_IN_AGENT_COLLECTION>

NODE_ID_COORDINATOR=<NODE_ID_FOR_COORDINATOR_MACHINE>

MODEL_URL=https://huggingface.co/lmstudio-community/gemma-1.1-2b-it-GGUF/resolve/main/gemma-1.1-2b-it-Q8_0.gguf?download=true
HOST_IP_ADDRESS=<IP_ADDRESS_OF_COORDINATOR_MACHINE>
CLIENT_ID=<YOUR_CLIENT_ID>
DEVELOPER_ID_TOKEN=<YOUR_DEVELOPER_ID>
API_KEY=1234
AGENT_COLLECTION_NAME=multi-agent-collection
```

Here is an example of a properly configured `.env` for the Coordinator Machine for this scenario:

```
# Environment variables for the Coordinator Machine
NODE_ID_AGENT_1=192.168.86.41
NODE_ID_NVIDIA_AGENT=192.168.86.45
NODE_ID_AGENT_3=192.168.86.35
NODE_ID_AGENT_4=192.168.86.48

NODE_ID_COORDINATOR=192.186.86.21

MODEL_URL=https://huggingface.co/lmstudio-community/gemma-1.1-2b-it-GGUF/resolve/main/gemma-1.1-2b-it-Q8_0.gguf?download=true
HOST_IP_ADDRESS=192.186.86.21
CLIENT_ID=a5efxxxx-1fce-469a-xxxx-3827xxxxa759
DEVELOPER_ID_TOKEN=eyJhbGcixxxxxxxxxxxIsInR5cCI6IkpXVCIsImtpZCI6Ik80d0NjU0FFMkxkX1VTR3ZSNjdmU18yQlNuZGhuYjFxb2YyY2trUlAyVE0ifQ.eyJzdWIiOiIyOTcyMTc0NjAxOTE2NTE4NDxxxxxxxxxxxxWwiOiIyOTcyMTc0NjAxOTE2NTE4NDAwQGV4YW1wbGUuY29tIiwiYXVkIjoiYTVlZmUzY2ItMWZjZS00NjlhLWI4YWYtMzgyNzljODdhNzU5IiwiZXhwIjoxNzI2ODY5MDQ4LCJpYXQiOjE3MjQyNzcwNDgsImlzcyI6Imh0dHBzOi8vZGV2Y29uc29sZS1taWQubWltaWsuY29tIn0.YjEgCWTy0SpAP8pJwBG5P3ph2Z4mrCoexxxxxxxxxxxU8JhgLckim0vx2K-247nfnXyVx4orDR5ig8zBbnM0eGoizYVCvIxSsSD-UwuJoDNj3M1QTqsrzB__vlyzh8KRT6n5biTa4TT7ciUFHnTKiGYSdkMqomCc2muDrsnE9xG47g34qpLbnuKW3ZQJlcvkyeCxuVgD4TwNef_q4jlS22xhcCSvLaSLxP4M-xxxxxxxxxxxxxJpk2WNQ2DW-4CVnTMs6zZwBQcBtctE5o9WW8jdUofqs_o8aDVBJv89TW3nkdcLSiCSnAobw9SqoZginG9m1rejNqCr-pmAPLKIc-7u0Q
API_KEY=1234
AGENT_COLLECTION_NAME=multi-agent-collection
```

## Step 3: Execute the commands in setup.http

The file `setup.http` contains the commands for creating the Agent Collection that includes the Agent and Nvidia Machines created in previous scenarios along with the new Agent Machines created in this scenario.

Under Visual Studio Code, execute the code commands in `./coordinator-machine/setup.http`


# Getting an Instance of the User Console Up and running

Getting the User Console up and running is a two-step process. First, you need to configure the `sitedata.json` file with the necessary runtime information. Then you need to start the User Console web server.

## Step 1: Configuring the sitedata.js file

Set the IP address of the Coordinator Machine in the file named `./user-console/sitedata.js`. This information is stored in JSON format as follows:

---

```
config = {
  "API_KEY": "1234",
  "CONTROLLER_IP_ADDRESS": <IP_ADDRESS_OF_COORDINATOR_MACHINE>>
  "AGENT_COLLECTION_NAME": "standard-node-nvidia-collection"
};
```

Here is an example of a properly configured `sitedata.js` file.

---

```
config = {
  "API_KEY": "1234",
  "CONTROLLER_IP_ADDRESS": "192.168.86.21",
  "AGENT_COLLECTION_NAME": "standard-node-nvidia-collection"
};
```

Once the `sitedata.js` file has been configured, you're ready to start the web server.

## Step 2: Running the User Console web server

In a terminal window, navigate to  `03-multi-agent-architecture/user-console` directory and start the web server by executing the following command:



---

```
python3 -m http.server 8005
```

**NOTE:** Although the default port number on which the User Console runs is `8000`, in this case, we're going to have the web server listen on port `8005` to avoid any collision with the User Console web server started in the previous scenarios.