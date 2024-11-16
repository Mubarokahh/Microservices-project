# Voting Application with CI/CD(JENKINS),KUBERNETES. (GOLANG MICROSERVICE)
## Introduction
This repo consist of anmicroservice voting appliaction in GO.A multi branch repo with each branch representing a microservice.These branches include : 
REDIS BRANCH, POSTGRES BRANCH, VOTING-SERVICE BRANCH, WORKER-SERVICE BRANCH, RESULT-SERVICE BRANCH
This application allows uders to vote for either cinema or netflix, it processes the votes in real-time and also displays the results. The application architecture includes JENKINS as the CI/CD tool, Kubernetes for orchestration of the microservices, Helm for deployment management, Prometheus for metic scrapping and Grafana for visualization.

## REQUIRED TOOLS
The following tools are installed:
Go 1.18 or later
Redis for in-memory data storage
PostgreSQL for persistent vote storage
Docker for containerization
Jenkins for CI/CD pipeline automation
Kubernetes for container orchestration
Docker Desktop for local containerization
Kubernetes in Docker (KIND) for managing Kubernetes clusters
Helm for Kubernetes deployment management
Prometheus & Grafana for monitoring and alerting

## DataFlow of the application 
- User vote for either cinema or Netflix
- The votes are storedgit  in redis
- The background worker syncs vote from Redis to PostgreSQL
- The result service then reads the results from PostgreSQL and displays the result
- Postgres then scap metric and grafana does the visualization.








