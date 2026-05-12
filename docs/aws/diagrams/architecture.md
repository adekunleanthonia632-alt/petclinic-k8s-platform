# GPM-161: AWS Deployment Architecture Diagram

## Production Architecture

Internet
    |
    | HTTPS 443
    v
+------------------------------------------+
|     AWS Application Load Balancer        |
|     eta-oko.com                          |
|     ACM SSL certificate (auto-renewing)  |
+------------------+-----------------------+
                   |
                   | HTTP 8080
                   v
+------------------------------------------+
|     Amazon EKS Cluster (us-east-1)       |
|     Namespace: petclinic                 |
|                                          |
|     config-server      (8888)            |
|     discovery-server   (8761)            |
|     api-gateway        (8080)            |
|     customers-service  (8081) --> RDS    |
|     vets-service       (8083) --> RDS    |
|     visits-service     (8082) --> RDS    |
|     admin-server       (9090)            |
|     genai-service      (8084)            |
|                                          |
|     Namespace: monitoring                |
|     Prometheus, Grafana, Zipkin          |
|                                          |
|     Namespace: argocd                    |
|     Namespace: external-secrets          |
+------------------------------------------+
         |                    |
         v                    v
+----------------+   +------------------+
| Amazon RDS     |   | AWS Secrets      |
| MySQL 8.0      |   | Manager          |
| db.t3.micro    |   | DB credentials   |
+----------------+   +------------------+

## ECR Registry
8 repositories: config-server, discovery-server, api-gateway,
customers-service, vets-service, visits-service, admin-server, genai-service

## Route 53
A Record: eta-oko.com -> ALB DNS name

## CI/CD Flow
Developer push -> GitHub Actions -> Build -> ECR
ECR tag update -> platform repo -> ArgoCD detects -> deploys to EKS
