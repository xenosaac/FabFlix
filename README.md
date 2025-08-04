# FabFlix


- #### Names:
   IZ，Junxiong Huang


- #### Collaborations and Work Distribution:
IZ led the project end-to-end:

- Developed the Java backend, including API endpoints, servlet logic, and integration.
- Managed the database setup, schema design, data population, and query optimization.
- Handled Tomcat debugging, configuration, and performance tuning.
- Provisioned and configured the AWS Kubernetes cluster, including IAM policies and access settings.
- Deployed Fabflix to K8s, refactored it into a multi-service architecture, and managed scaling.
- Designed and implemented the frontend UI/UX, including HTML, CSS, and JavaScript components.
- Built and containerized the Fabflix application using Docker.


Junxiong Huang contributed to supporting tasks, including:

- Writing configuration and deployment documentation.
- Performing smoke tests and logging results.
- Producing and editing the final video presentation.



1. This example application allows you to log in, see a movie by Eddie Murphy and leave comments.
2. In branch `Docker`, you will see how this application is turned into a docker image and deployed to AWS using Docker
3. In branch `Kubernetes`, you will see how this application is modified to be deployed using Kubernetes pods
4. In branch `Multi-Service`, you will see how this application is modified to a multi-service architecture.

## This README.md file is used for the Multi-Service branch

## Project Overview

FabFlix is a web application that allows users to browse movies, search for films, view details, and manage shopping carts. It demonstrates a full-stack development with Java backend, MySQL database, and frontend technologies.

## Architecture

The application is built with a multi-service architecture:

- **Login Service**: Handles user authentication using JWT.
- **Movies Service**: Manages movie browsing, search, and related functionality.

We use JSON Web Tokens (JWT) for stateless authentication and Maven profiles for building separate WAR files for each service.

### JSON Web Token (JWT)

We use JWT to handle user sessions across services. Utility classes manage JWT generation and validation.

### Maven Profiles

Maven profiles allow compiling different parts of the project into separate WAR files for each service.

## Building the Project

- Compile different parts:
  ```
  mvn package -P login
  mvn package -P movies
  ```

- Build Docker images:
  ```
  docker build -f Dockerfile.login -t yourusername/fabflix-login:latest .
  docker build -f Dockerfile.movies -t yourusername/fabflix-movies:latest .
  ```

- Push to Docker Hub:
  ```
  docker push yourusername/fabflix-login:latest
  docker push yourusername/fabflix-movies:latest
  ```

## Deployment on Kubernetes

### Prerequisites

- AWS Kubernetes cluster
- Docker Hub account
- MySQL Helm chart installed

### Deployment Steps

1. Deploy services:
   ```
   kubectl apply -f fabflix-multi.yaml
   ```

2. Deploy Ingress:
   ```
   kubectl apply -f ingress-multi.yaml
   ```

3. Access the application via the Ingress URL.

## Troubleshooting

- **Pods in PENDING state**
   ```bash
   kubectl describe pod <POD_NAME>
   ```
   Check the pod events to identify resource constraints or other issues.

- **Database Connection Issues**
   - Verify database credentials in context.xml
   - Check if MySQL service is running
   - Ensure database schema is properly imported

- **404 Errors**
   - Check WAR file structure
   - Verify Ingress path configuration
   - Check application context paths in Tomcat

- **Scaling Services**
   ```bash
   kubectl scale deployment fabflix-movies --replicas=3
   ```

- **Viewing All Resources**
   ```bash
   kubectl get all
   ```

## Technologies Used

- Java Servlets
- MySQL
- Docker
- Kubernetes
- JWT for authentication
- Maven for build management


</rewritten_file>