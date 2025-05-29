#  IPFS Pallet Storage Logger
This Python application logs the UserProfile and MinerProfile storage items from the IPFSPallet on a Substrate-based blockchain every 5 blocks. It uses the substrateinterface library to interact with the blockchain and logs the results to both the console and a file.
Prerequisites

Python: Version 3.8 or higher
Substrate Node: Access to a running Substrate node with the IPFSPallet pallet, accessible via WebSocket (e.g., wss://rpc.hippius.network)

pip: Python package manager

Git: Optional, for cloning the repository (if applicable)

#  Setup Instructions
## 1. Clone the Repository (Optional)
If the code is hosted in a repository, clone it to your local machine:

git clone <repository-url>

cd <repository-directory>

Alternatively, save the provided main.py file to a directory of your choice.
## 2. Set Up a Python Virtual Environment
Create and activate a virtual environment to manage dependencies:
On macOS/Linux:

python3 -m venv venv

source venv/bin/activate

On Windows:

python -m venv venv

venv\Scripts\activate

## 3. Install Required Packages
Install the substrate-interface library, which is used to interact with the Substrate node:

pip install substrate-interface

This will install the substrateinterface package and its dependencies.
## 4. Configure the Application
Edit the main.py file to set the WebSocket URL of your Substrate node:

Open main.py in a text editor.
Locate the main() function at the bottom of the file.

Update the ws_url variable to point to your Substrate node's WebSocket endpoint. For example:ws_url = "ws://your-node:9944"

## 5. Run the Application
With the virtual environment activated, run the script:

python main.py

# Run App With Kubernetes

minikube start

eval $(minikube docker-env)

docker build -t profile-pinner:latest .

kubectl apply -f ipfs-pvc.yaml

kubectl apply -f ipfs-deployment.yaml

kubectl apply -f ipfs-service.yaml

kubectl apply -f profile-pinner-deployment.yaml
