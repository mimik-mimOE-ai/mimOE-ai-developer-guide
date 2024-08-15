# Setting Up and Running an Agent Collection that includes an Nvidia Agent Machine

This scenario builds on the work done in the previous scenario [Setting Up and Running a Single Agent Collection](../01-single-agent-architecture/). This scenario is one in which there are two Agent Machines. One of the Agent Machines was created in the previous scenario. The new Agent Machine is an Orin Jetson Nano device that you will add to the mimik Service Mesh in this scenario. The figure below illustrates the physical architecture of this scenario.

![Nvidia Architecture](../images/nvidia-collection.png)

# What to have on hand

* An Nvidia Orin Jetson Nano or an Nvidia Orin Jetson Nano/AGX device running Ubuntu 22.04
* The Nvidia device need to have the latest version of edgeEngine specifically intended for Nvidia machines. The deployment `.tar` file is named, `mimOE-SE-linux-developer-ARM64-CUDA-v3.12.0.tar`. Download and installation instructions can be found on [the mimik Release Page here](https://github.com/mimik-mimOE/mimOE-SE-Linux/).
* Once edgeEngine is up and running the Nvidia device needs to have port 8083 exposed.

We assume that you have an actual Nvidia device on hand and that the device has Ubuntu 22.04 installed on it.

* To learn the details about how to get the **Nvidia Orin Jetson Nano** device setup and configured with Ubuntu 22.04 read the Nvidia document titled [Jetson Orin Nano Developer Kit Getting Started Guide](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit).
* To learn the details about how to get the **Nvidia Orin Jetson Nano/AGX** device setup and configured with Ubuntu 22.04, read the Nvidia document titled, [Getting Started with Jetson AGX Orin Developer Kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-agx-orin-devkit).

# What you'll be doing

Setting Up and Running an Agent Collection that includes an Nvidia Agent Machine is a three-part undertaking as follows:

* Adding the Nvidia Orin Jetson Nano device to the mimik Service Mesh and configuring it with an LLM
* Updating the Coordinator Machine with an additional Agent Collection that includes the Agent Machine created in the previous scenario along with the newly installed Nvidia device.
* Connecting the User Console to the Coordinator Machine via its `nodeId`.


To configure the Nvidia Agent Machine go [here](./nvidia-agent-machine/)

To update the Coordinator Machine go [here](./coordinator-machine/)

To set up an instance of the User Console go [here](./user-console/)