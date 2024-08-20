# Setting Up a Multiple Agent Machine Scenario

- [Setting Up a Multiple Agent Machine Scenario](#setting-up-a-multiple-agent-machine-scenario)
- [What You Need to Have On Hand](#what-you-need-to-have-on-hand)
- [What You'll be Doing](#what-youll-be-doing)
- [Configuring the Agent Machines](#configuring-the-agent-machines)
  - [Step 1: Create working directories for each Agent Machine](#step-1-create-working-directories-for-each-agent-machine)
  - [Step 2: Copy the contents of env.template into .env files in the working directories](#step-2-copy-the-contents-of-envtemplate-into-env-files-in-the-working-directories)
  - [Step 3: Configure the .env files](#step-3-configure-the-env-files)
  - [Step 4: Create the setup.http file for each Agent Machine's working directory](#step-4-create-the-setuphttp-file-for-each-agent-machines-working-directory)
  - [Step 5: Execute the setup.http files in the Agent Machine working directories](#step-5-execute-the-setuphttp-files-in-the-agent-machine-working-directories)
- [Configuring the new Agent Collection on the Coordinator Machine](#configuring-the-new-agent-collection-on-the-coordinator-machine)
  - [Step 1: Create the .env file](#step-1-create-the-env-file)
  - [Step 2: Configure the .env file](#step-2-configure-the-env-file)
  - [Step 3: Execute the commands in setup.http](#step-3-execute-the-commands-in-setuphttp)
- [Getting an Instance of the User Console Up and running](#getting-an-instance-of-the-user-console-up-and-running)
  - [Configuring the sitedata.js file](#configuring-the-sitedatajs-file)
  - [Running the User Console web server](#running-the-user-console-web-server)


The purpose of Scenario 3 is to demonstrate how to add Agent Machines to the mimik Service Mesh and then to modify the existing Coordinator Machine by adding a new Agent Collection that supports 4 Agent Machines.

These 4 Agent Machines are the Agent Machines created previously in Scenario 1 and 2, plus the two new Agent Machines you'll create in this scenario.

# What You Need to Have On Hand

This scenario requires that you have on hand two computers with AMD/Intel processors. Each computer needs to be running the latest version of edgeEngine.

# What You'll be Doing

In this scenario you will provision two Agent Machines using Visual Studio REST Client `setup.http` files. Then, you'll define a new Agent Collection on the existing Coordinator Machine. Finally, you'll create an instance of the User Console web server. You configure the User Console web server to work with the new Agent Collection. Once the User Console web server is configured, you'll be able to submit AI prompts to Coordinator Machine. The Coordinator Machine will return a result that include the response from each Agent Machine in the new Agent Collection. Also, the Coordinator Machine will return a unified response composed of the responses from each Agent Machine.

# Configuring the Agent Machines

Execute the following steps to get the 2 new Agent Machines up and running

## Step 1: Create working directories for each Agent Machine

You'll need to create working directories for each of the new Agent Machines. Execute the following command in a terminal window to create the working directories.

```
mkdir agent_machine_03 && mkdir agent_machine_04
```

## Step 2: Copy the contents of env.template into .env files in the working directories

The file named `env.template` contains the declaration of the environment variables that the Agent Machine `setup.http` files need. Execute the following command in a terminal window to copy the contents of the `env.template` into the `.env` file for one of the new Agent Machines.

```
cp ./agent-machines/env.template ./agent_machine_03/.env
```

Execute the following command in a terminal window to copy the contents of the `env.template` into the `.env` file for one of the other new Agent Machines.

```
cp ./agent-machines/env.template ./agent_machine_04/.env
```

## Step 3: Configure the .env files

Add the required values to the `.env` files in `agent_machine_03` and `agent_machine_04`

## Step 4: Create the setup.http file for each Agent Machine's working directory

The file `setup.template` has the structure and data that you'll copy into a `setup.http` file for each Agent Machine's working directory. You'll copy the contents of `setup.template` into a `setup.http` file in each Agent Machine's working directory.

In a terminal window, execute the following command to copy the contents of `setup.template` into the `setup.http` file for one of the new Agent Machines.

```
cp ./agent-machines/setup.template ./agent_machine_03/setup.http
```

In a terminal window, execute the following command to copy the contents of `setup.template` into the `setup.http` file for one of the other new Agent Machines.

```
cp ./agent-machines/setup.template ./agent_machine_04/setup.http
```

## Step 5: Execute the setup.http files in the Agent Machine working directories

Go to the `setup.http` file in the working directories for each of the new Agent Machines


# Configuring the new Agent Collection on the Coordinator Machine

## Step 1: Create the .env file

In a terminal window, execute the following command to copy the contents of the file `./coordinator-machine/env.template` into the file `./coordinator-machine/.env`.

```
cp ./coordinator-machine/env.template ./coordinator-machine/.env
```

## Step 2: Configure the .env file

Configure the `.env` file with the required information.

## Step 3: Execute the commands in setup.http

The file `setup.http` contains the commands for creating the Agent Collection that includes the Agent and Nvidia Machines created in previous scenarios along with the new Agent Machines created in this scenario.

Under Visual Studio Code, execute the code commands in `./coordinator-machine/setup.http`


# Getting an Instance of the User Console Up and running

Getting the User Console up and running is a two-step process. First, you need to configure the `sitedata.json` file with the necessary runtime information. Then you need to start the User Console web server.

## Configuring the sitedata.js file

Set the IP address of the Coordinator Machine and the name of the newly created Agent Collection in the file named `sitedata.js`. This information is stored in JSON format as follows:

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

## Running the User Console web server

In a terminal window, navigate to  `02-nvidia-architecture/user-console` directory and start the web server by executing the following command:


---

```
python3 -m http.server 8004
```

**NOTE:** Although the default port number on which the User Console runs is `8000`, in this case, we're going to have the web server listen on port `8004` to avoid any collision with the User Console web server started in the previous scenario.