## **Project Requirements**  

### **1. Updated Application Architecture**
![updated_architecture_diagram](./assets/updated_architecture_diagram.png)

### **2. Application and Architecture Explanation**
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
### **3. Deployment Instructions**
- Step-by-step instructions to deploy the application in a Kubernetes cluster.

#### Step 1: Clone the Algonquin Pet Store Repository

To begin, clone the [**Algonquin Pet Store (On Steroids)**](https://github.com/ramymohamed10/algonquin-pet-store-on-steroids) repository, which contains all necessary deployment files.

 **Review the Deployment Files**:
   - Navigate to the `Deployment Files` folder
   - This folder contains YAML files for deploying all necessary Kubernetes resources, including services, deployments, StatefulSets, ConfigMaps, and Secrets.

#### Step 2: Set Up the AKS Cluster
Create an AKS cluster with two worker nodes for this exercise.


## Table of Microservice Repositories
A table listing each microservice repository and its GitHub link.
| Service              | Repository Link                                   |
|----------------------|---------------------------------------------------|
| Store-Front          | [Store-Front GitHub Link](https://github.com/Yue0218/store-front-Assignment2)          |
| Store-Admin          | [Store-Admin GitHub Link](https://github.com/Yue0218/store-admin-Assignment2)          |
| Order-Service        | [Order-Service GitHub Link](https://github.com/Yue0218/order-service-Assignment2)        |
| Product-Service      | [Product-Service GitHub Link](https://github.com/Yue0218/product-service-Assignment2)      |
| Makeline-Service     | [Makeline-Service GitHub Link](https://github.com/Yue0218/makeline-service-Assignment2)     |
| AI-Service           | [AI-Service GitHub Link](https://github.com/Yue0218/ai-service-Assignment2)           |
| MongoDB              | [MongoDB GitHub Link](https://github.com/docker-library/mongo)                     |
| Virtual-Customer     | [Virtual-Customer GitHub Link](https://github.com/Yue0218/virtual-customer-Assignment2)     |
| Virtual-Worker       | [Virtual-Worker GitHub Link](https://github.com/Yue0218/virtual-worker-Assignment2)       |

## Table of Docker Images
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

### **4. Demo Video**  
Record a **5-minute max demo video** showcasing the following:  
- The application in action after deployment to AKS cluster.  
- AI-generated product descriptions and images.  
- Integration with the managed order queue service.  

- https://youtu.be/pJxgIYE3C9U

---
