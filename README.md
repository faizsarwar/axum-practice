IPFS Pallet Storage Logger
Overview
The IPFS Pallet Storage Logger is a Python application that monitors and logs the UserProfile and MinerProfile storage items from the IPFSPallet on a Substrate-based blockchain. It queries the blockchain every 5 blocks using the substrateinterface library and logs the results to both the console and a file (pallet_storage.log). This tool is useful for tracking profile data changes on a Substrate node with the IPFS pallet.
Prerequisites

Python: Version 3.8 or higher
Substrate Node: Access to a running Substrate node with the IPFSPallet, accessible via WebSocket (e.g., wss://your-node:9944)
pip: Python package manager
Git: Optional, for cloning the repository
Kubernetes (optional, for deployment):
minikube for local Kubernetes clusters
kubectl for managing Kubernetes resources
Docker for building container images



Setup Instructions
1. Clone the Repository (Optional)
If the code is hosted in a repository, clone it to your local machine:
git clone <repository-url>
cd <repository-directory>

Alternatively, save the main.py file to a directory of your choice.
2. Set Up a Python Virtual Environment
Create and activate a virtual environment to manage dependencies:
On macOS/Linux:
python3 -m venv venv
source venv/bin/activate

On Windows:
python -m venv venv
venv\Scripts\activate

3. Install Required Packages
Install the substrate-interface library to interact with the Substrate node:
pip install substrate-interface

4. Configure the Application
Edit the main.py file to set the WebSocket URL of your Substrate node:

Open main.py in a text editor.
Locate the main() function.
Update the ws_url variable to your Substrate node's WebSocket endpoint, e.g.:

ws_url = "wss://your-node:9944"

5. Run the Application
With the virtual environment activated, run the script:
python main.py

The application will connect to the Substrate node, query storage items every 5 blocks, and log the results to pallet_storage.log and the console.
Deploying with Kubernetes
To deploy the application on a Kubernetes cluster (e.g., for production or scalable monitoring), follow these steps:
Prerequisites

Install minikube for a local Kubernetes cluster: Minikube Installation
Install kubectl: kubectl Installation
Install Docker: Docker Installation

Steps

Start minikube:

minikube start


Set up the Docker environment for minikube:

eval $(minikube docker-env)


Build the Docker image for the application:

docker build -t profile-pinner:latest .


Apply the Kubernetes configuration files (ensure you have ipfs-pvc.yaml, ipfs-deployment.yaml, ipfs-service.yaml, and profile-pinner-deployment.yaml):

kubectl apply -f ipfs-pvc.yaml
kubectl apply -f ipfs-deployment.yaml
kubectl apply -f ipfs-service.yaml
kubectl apply -f profile-pinner-deployment.yaml

Note: These YAML files define persistent volume claims, deployments, and services for the application. Ensure they are configured to match your Substrate node's WebSocket URL and other environment-specific settings. Contact the repository maintainer for these files if not provided.
Notes

Block Time: The application assumes a block time of ~6 seconds. To adjust the polling interval, modify the time.sleep() value in the main.py loop (e.g., time.sleep(30) for 30 seconds).
Log Rotation: Logs are stored in pallet_storage.log. For long-running instances, consider using a log rotation tool like logrotate on Linux or a Python library like logging.handlers.RotatingFileHandler. Example:
