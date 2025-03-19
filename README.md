# Kubernetes Voting App Microservices

This repository contains Kubernetes YAML configurations for a microservices-based voting application.

## Architecture Overview

The application consists of multiple microservices running in separate pods, each with a specific role:

- **Frontend**: Two frontend pods (`voting-app` and `result-app`), each exposed via a NodePort service.
- **Backend**: A worker pod (`worker`) that processes votes and communicates with the database.
- **Database**: PostgreSQL (`postgres`) for storing votes.
- **Cache**: Redis (`redis`) for temporary vote storage.

## Architecture Flow

```plaintext
                     +--------------------+
                     |  User Interaction  |
                     +--------------------+
                               |
          +--------------------------------------+
          |          Frontend Services         |
          +--------------------------------------+
          | 1. voting-app  (Python)            |
          | 2. result-app  (JavaScript)        |
          +--------------------------------------+
                     |       |
         (NodePort)  |       |  (NodePort)
                     v       v
          +-------------------------+
          |  Voting-App Pod (Python) |
          +-------------------------+
                     |
                     v
          +-----------------+
          |  Redis Pod      |
          |  (In-memory DB) |
          +-----------------+
                     |
                     v
          +-----------------+
          |  Worker Pod     |
          |  (Processing)   |
          +-----------------+
                     |
                     v
          +-----------------+
          |  Postgres Pod   |
          |  (Database)     |
          +-----------------+
                     |
                     v
          +----------------------------+
          |  Result-App Pod (JavaScript)|
          +----------------------------+
```
## Setup Instructions

1. **Clone the repository:**
   ```sh
   git clone https://github.com/sakshiexe/voting-app.git
   cd voting-app
   ```
   
2. **Deploy the application on Kubernetes:**
```sh
kubectl apply -f k8s/
```

3.**Verify that all pods are running:**
```sh
kubectl get pods
```

4.**Access the frontend:**
```sh
minikube service frontend --url
```

## Deployment

To redeploy changes, update the YAML files and apply them again:
```sh
kubectl apply -f k8s/
```

## Testing the Application

- **Access the frontend using the LoadBalancer or NodePort.**
- **Submit votes through the UI.**
- **Check the results processed by the Worker and stored in PostgreSQL.**

## Conclusion

This project demonstrates a basic microservices architecture using Kubernetes. It showcases service orchestration with a frontend, backend, Redis caching, PostgreSQL database, and a worker for data processing.






