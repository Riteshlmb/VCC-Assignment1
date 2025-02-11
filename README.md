# VCC-Assignment1
# VirtualBox Microservice Deployment

# Overview

This project demonstrates how to create multiple Virtual Machines (VMs) using VirtualBox, configure networking between them, and deploy a microservice-based application across the connected VMs.

# Architecture

VMServer1: Hosts the microservice (Node.js-based REST API) and runs the server.

VMServer2: Acts as a client that communicates with the microservice on VMServer1.

Host-Only Network: Initially, use Nat Network to connects both VMs for internal communication.

# Prerequisites

VirtualBox installed

Ubuntu (or any Linux-based OS) installed on both VMs

Basic knowledge of networking and Linux commands

# Setup Instructions

## Step 1: VirtualBox VM Creation

Open VirtualBox and create two VMs:

VMServer1 (API server)

VMServer2 (Client)

Install Ubuntu on both VMs.

Assign at least 2GB RAM and 15GB storage.

## Step 2: Network Configuration

In VirtualBox, go to File > Host Network Manager and create a Host-Only Network.

Select a Nat Network for Local Communication & Nat to access the computers Internet to install various API etc

Assign Dynamic IPs:

192.168.56.X

Configure network adapter settings:

Go to Settings > Network

Set Adapter 1 to Nat Network

## Step 3: Deploy Microservice on VMServer1

Install Node.js:

sudo apt update && sudo apt install -y nodejs npm

Clone the repository and navigate to the project directory:

git clone https://github.com/Riteshlmb/VCC-Assignment1.git
cd VCC-Assignment1

Install dependencies and start the server:

npm install
node server.js

## Step 4: Access Microservice from VMServer2

On VMServer2, install curl if not installed:

sudo apt install -y curl

Test API connectivity:

curl http://192.168.56.5:3000/

Expected response: Microservice Running on VMServer1

# Testing and Validation

Verify connectivity with ping 192.168.56.5 from VMServer2.

Open http://192.168.56.5:3000/ in a browser.

Check logs on VMServer1 to confirm API requests.
