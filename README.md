# VCC-Assignment1
# VirtualBox Microservice Deployment

# Overview
This project demonstrates how to create multiple Virtual Machines (VMs) using VirtualBox, configure networking between them and deploy a microservice-based application across the connected VMs.

# Architecture

VMServer1: Hosts the microservice (Node.js-based REST API) and runs the server.

VMServer2: Acts as a client that communicates with the microservice on VMServer1.

To clone the repository and navigate to the project directory:

git clone https://github.com/Riteshlmb/VCC-Assignment1.git

cd VCC-Assignment1

# **VirtualBox-Based Microservice Deployment Report**

## **1. Introduction**
This report details the process of creating multiple Virtual Machines (VMs) using VirtualBox, configuring a network between them and deploying a microservice-based application across the connected VMs.

## **2. VirtualBox Installation and VM Creation**

### **2.1 Installing VirtualBox**
1. Download VirtualBox from the https://www.virtualbox.org/.
2. Run the installer and follow the installation instructions for your operating system.

### **2.2 Creating Virtual Machines**
1. Open VirtualBox and click **New**.
2. Provide a name (e.g., VMServer1), select the OS type (Ubuntu/Linux) and allocate memory (used 2GB).
3. Create a virtual hard disk (15GB used).
4. Repeat the process to create **VMServer2**.

## **3. Network Configuration for VM Communication**
### **3.1 Configuring Network Settings**
1. Open VirtualBox, go to **File > Host Network Manager** and create a Host-Only Network.
2. Assign Dynamic IPs to VMs: `192.168.56.0`
   - VMServer1: `192.168.56.5`
   - VMServer2: `192.168.56.4`
3. In VirtualBox settings for each VM:
   - Go to **Network > Adapter 1**
   - Select **NAT Network** when you wish to connect the VMs with each other.
   - Select **NAT** when you wish to connect to the internet of the host machine (Used to execute all sudo commands for various intallations).

4. Restart VMs and check connectivity using:
   ```bash
   ping 192.168.56.4  # From VMServer1 to VMServer2
   ping 192.168.56.5  # From VMServer2 to VMServer1
   ```

## **4. Deploying a Microservice-Based Application**

### **4.1 Setting Up the Microservice**
We use a simple Node.js-based REST API.

1. Install Node.js on **VMServer1**:
   ```bash
   sudo apt update && sudo apt install -y nodejs npm
   ```
2. Create a project folder and initialize a Node.js project:
   ```bash
   mkdir microservice && cd microservice
   npm init -y
   ```
3. Install Express and create `server.js`:
   ```bash
   npm install express
   nano server.js
   ```
   Add the following code:
   ```javascript
   const express = require('express');
   const app = express();
   const port = 3000;

   app.get('/', (req, res) => {
       res.send('Microservice Running on VMServer1');
   });

   app.listen(port, () => {
       console.log(`Server running at http://0.0.0.0:${port}`);
   });
   ```
4. Run the microservice:
   ```bash
   node server.js
   ```

### **4.2 Accessing the Microservice from VMServer2**
1. On VMServer2, install `curl` if not available:
   ```bash
   sudo apt install -y curl
   ```
2. Access the microservice:
   ```bash
   curl http://192.168.56.101:3000/
   ```
   Expected output: `Microservice Running on VMServer1`

## **5. Testing and Validation**
- Confirm VM communication using `ping`.
- Ensure the service is accessible from VMServer2.
- Use a web browser to open `http://192.168.56.5:3000/`.

## **6. Architecture Design**
A simple network architecture using VirtualBox in the center and the connection between VMServer1 and VMServer2.

## **7. Conclusion**
This report demonstrated the creation of Virtual Machines using VirtualBox, network configuration for inter-VM communication and the deployment of a simple microservice.


