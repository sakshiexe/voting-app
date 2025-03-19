# Voting App Microservices on Kubernetes

This repository contains Kubernetes YAML configurations for a microservices-based voting application. The app consists of multiple components running as pods and services, including a frontend, backend, Redis, PostgreSQL, and a worker service.

## Tech Stack

- **Frontend:** HTML pages served from a pod
- **Backend:** Python-based API for handling votes
- **Database:** PostgreSQL for persisting votes
- **Cache:** Redis for temporary vote storage
- **Worker:** Handles vote processing and transfers data between Redis and PostgreSQL
- **Orchestration:** Kubernetes for containerized service management

## Architecture

```plaintext
+-------------+       +------------+       +----------+
|  Frontend   | ----> |  Backend   | ----> |  Worker  |
+-------------+       +------------+       +----------+
                                  |             |
                                  v             v
                           +-----------+   +-----------+
                           |   Redis   |   | Postgres  |
                           +-----------+   +-----------+

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






