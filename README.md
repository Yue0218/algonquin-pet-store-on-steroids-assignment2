# CST-8915 Assignment 2 

## **1. Updated Application Architecture**
![updated_architecture_diagram](./assets/updated_architecture_diagram.png)

---
## **2. Application and Architecture Explanation**
The **Best Buy App** must include the following components:  

| Service              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Store-Front**      | Customer-facing app for browsing and placing orders.              |
| **Store-Admin**      | Employee-facing app for managing products and viewing orders .     |
| **Order-Service**    | Handles order creation and sends data to the managed order queue via Azure Service Bus.          | 
| **Product-Service**  | Handles CRUD operations for product data.                          |
| **Makeline-Service** | Processes and completes orders by reading from the order queue.       |
| **AI-Service**       | Uses GPT-4 and DALL-E models to generates product descriptions and images.    |
| **Database**         | MongoDB for persisting order and product data.                            |

---
## **3. Deployment Instructions**
- Step-by-step instructions to deploy the application in a Kubernetes cluster.

### Step 1: Clone the Best Buy Repository

To begin, clone the [**Best Buy (On Steroids)**](https://github.com/Yue0218/algonquin-pet-store-on-steroids-assignment2) repository, which contains all necessary deployment files.

### Step 2: Set Up the AKS Cluster
Create an AKS cluster with two worker nodes for this exercise.

1. **Log in to Azure Portal:**
   - Go to [https://portal.azure.com](https://portal.azure.com) and log in with your Azure account.

2. **Create a Resource Group:**
   - In the Azure Portal, search for **Resource Groups** in the search bar.
   - Click **Create** and fill in the following:
     - **Resource group name**: `AlgonquinPetStoreRG`
     - **Region**: `Canada`.
   - Click **Review + Create** and then **Create**.

3. **Create an AKS Cluster:**
   - In the search bar, type **Kubernetes services** and click on it.
   - Click **Create** and select **Kubernetes cluster**
   - In the `Basics` tap fill in the following details:
     - **Subscription**: Select your subscription.
     - **Resource group**: Choose `AlgonquinPetStoreRG`.
     - **Cluster preset configuration**: Choose `Dev/Test`.
     - **Kubernetes cluster name**: `AlgonquinPetStoreCluster`.
     - **Region**: Same as your resource group (e.g., `Canada`).
     - **Availability zones**: `None`.
     - **AKS pricing tier**: `Free`.
     - **Kubernetes version**: `Default`.
     - **Automatic upgrade**: `Disabled`.
     - **Automatic upgrade scheduler**: `No schedule`.
     - **Node security channel type**: `None`.
     - **Security channel scheduler**: `No schedule`.
     - **Authentication and Authorization**: `Local accounts with Kubernetes RBAC`.
   - In the `Node pools` tap fill in the following details:
     - Select **agentpool**. Optionally change its name to `masterpool`. This nodes will have the controlplane.
        - Set **node size** to `D2as_v4`.
        - **Scale method**: `Manual`
        - **Node count**: `1`
        - Click `update`
     - Click on **Add node pool**:
        - **Node pool name**: `workerspool`.
        - **Mode**: `User` 
        - Set **node size** to `D2as_v4`.
        - **Scale method**: `Manual`
        - **Node count**: `2`
        - Click `add`
   - Click **Review + Create**, and then **Create**. The deployment will take a few minutes.

4. **Connect to the AKS Cluster:**
   - Once the AKS cluster is deployed, navigate to the cluster in the Azure Portal.
   - In the overview page, click on **Connect**. 
   - Select **Azure CLI** tap. You will need Azure CLI. If you don't have it: [**Install Azure CLI**](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
   - Login to your azure account using the following command:
      ```
      az login
      ```
   - Set the cluster subscription using the command shown in the portal (it will look something like this):
      ```
      az account set --subscription 'subscribtion-id'
      ```

   - Copy the command shown in the portal for configuring `kubectl` (it will look something like this):
     ```
     az aks get-credentials --resource-group AlgonquinPetStoreRG --name AlgonquinPetStoreCluster
     ```

   - Verify Cluster Access:
      - Test your connection to the AKS cluster by listing all nodes:
        ```
        kubectl get nodes
        ```
        You should see details of the nodes in your AKS cluster if the connection is successful.
---

### Step 3: Deploy the Best Buy Application

1. **Apply the YAML file to the AKS cluster:**
   - In this step, use the K8s deployment YAML files provided in **Deployment Files** folder.
   - Open the terminal and navigate to the file directory.
   - Run the following command to apply the YAML configuration and deploy the application to AKS:
      ```
      kubectl apply -f order-service-deployment.yaml
      kubectl apply -f product-service-deployment.yaml
      kubectl apply -f makeline-service-deployment.yaml
      kubectl apply -f store-front-deployment.yaml
      kubectl apply -f store-admin-deployment.yaml
      kubectl apply -f ai-service-deployment.yaml
      kubectl apply -f mongodb-deployment.yaml
      kubectl apply -f rabbitmq-deployment.yaml
      ```

2. **Verify the deployment:**
   - After the command executes, verify that the pods are running by using the following command:
     ```bash
     kubectl get pods
     ```

3. **Check services:**
   - Confirm that all services are up and running:
     ```bash
     kubectl get services
     ```

4. **Access the Store Front Application:**
   - The **Store Front** service is configured as a LoadBalancer, which exposes the application to the internet.
   - In the Azure Portal, go to **Kubernetes Services** > **AlgonquinPetStoreCluster** > **Services and ingresses**.
   - Locate the **store-front** service, and note the **EXTERNAL-IP** address.
   - Open the store-front application in your browser:
     ```
       http://<EXTERNAL-IP>
     ```
---

## 4. Table of Microservice Repositories
A table listing each microservice repository and its GitHub link.
| Service              | Repository Link                                   |
|----------------------|---------------------------------------------------|
| Store-Front          | [Store-Front GitHub Link](https://github.com/Yue0218/store-front-Assignment2)          |
| Store-Admin          | [Store-Admin GitHub Link](https://github.com/Yue0218/store-admin-Assignment2)          |
| Order-Service        | [Order-Service GitHub Link](https://github.com/Yue0218/order-service-Assignment2)        |
| Product-Service      | [Product-Service GitHub Link](https://github.com/Yue0218/product-service-Assignment2)      |
| Makeline-Service     | [Makeline-Service GitHub Link](https://github.com/Yue0218/makeline-service-Assignment2)     |
| AI-Service           | [AI-Service GitHub Link](https://github.com/Yue0218/ai-service-Assignment2)           |

## 5. Table of Docker Images
A table listing all Docker images you created, including their names and links to their Docker Hub repositories.
| Service             | Docker Image Link                                           |
|----------------------|------------------------------------------------------------|
| Store-Front          | [Store-Front Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/store-front-assignment2/general)          |
| Store-Admin          | [Store-Admin Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/store-admin-assignment2/general)          |
| Order-Service        | [Order-Service Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/order-service-assignment2/general)        |
| Product-Service      | [Product-Service Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/product-service-assignment2/general)      |
| Makeline-Service     | [Makeline-Service Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/makeline-service-assignment2/general)     |
| AI-Service           | [AI-Service Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/ai-service-assignment2/general)           |
| Virtual-Customer     | [Virtual-Customer Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/virtual-customer-assignment2/general)     |
| Virtual-Worker       | [Virtual-Worker Docker Hub Link](https://hub.docker.com/repository/docker/gaoyue218/virtual-worker-assignment2/general)       |

---

### **Issues or limitations**

I could not figure out how the service bus works, so I did the bonus task of creating CI/CD workflow instead.

---
## **6. Demo Video**  
A 5-minute max demo video showcasing the following:  
- The application in action after deployment to AKS cluster.  
- AI-generated product descriptions and images.  
- Integration with the managed order queue service.  

**Youtube Link: https://youtu.be/pJxgIYE3C9U**
---
