# GitLab CI/CD with Docker & AWS EC2

This repository demonstrates an automated **CI/CD pipeline** for a Node.js application using:

* **GitLab CI/CD** for pipeline automation
* **Docker** for containerizing the application
* **GitLab Container Registry** for storing Docker images
* **AWS EC2** for deploying and running the application

## CI/CD Workflow

```mermaid
flowchart LR
    A[Developer] -->|Git Push| B[GitLab Repository]

    B --> C[GitLab CI/CD Pipeline]

    C --> D[Test]
    D -->|npm test| E{Tests Passed?}

    E -->|No| F[Pipeline Failed]
    E -->|Yes| G[Build Docker Image]

    G --> H[Push Image to<br/>GitLab Container Registry]

    H --> I[Deploy]

    I -->|SSH| J[AWS EC2]

    J --> K[Pull New Docker Image]
    K --> L[Stop Old Container]
    L --> M[Run New Container]

    M --> N[Application Running<br/>Port 80 → 3000]
```

## Pipeline

The CI/CD pipeline consists of three main stages:

**Test → Build → Deploy**

* **Test:** Install dependencies and run automated tests for the Node.js application.
* **Build:** Build a Docker image and push it to the GitLab Container Registry.
* **Deploy:** GitLab CI/CD connects to the AWS EC2 instance via SSH, pulls the latest Docker image, stops the old container, and starts a new container.

When new code is pushed to the repository, the pipeline automatically validates the application. Changes pushed to the main branch are then built into a new Docker image and deployed to AWS EC2.



----
test1
----
