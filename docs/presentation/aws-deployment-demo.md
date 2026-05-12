# GPM-217: AWS Deployment Demo Section

## Demo Script — AWS Infrastructure

### Opening (30 seconds)
Show the live application at https://eta-oko.com
This is Spring PetClinic deployed on AWS EKS using GitOps.

### 1. Show the Infrastructure (2 minutes)
Open AWS Console -> EKS -> petclinic-eks cluster
Show: 2 running nodes (t3.small)
Show: kubectl get pods -n petclinic (all 8 running)
Show: kubectl get svc -n petclinic

### 2. Show the Terraform Code (2 minutes)
Open petclinic-k8s-platform/terraform/
Show main.tf -> 4 modules: vpc, eks, ecr, rds
Show modules/eks/main.tf -> EKS cluster and node group
Show modules/rds/main.tf -> RDS and Secrets Manager
Key point: Everything is code, nothing manual

### 3. Show the GitOps Pipeline (2 minutes)
Open ArgoCD UI
Show: petclinic application -> Synced and Healthy
Show: GitHub Actions -> recent successful run
Explain: push to main -> CI builds -> ECR push -> ArgoCD deploys

### 4. Show the Database (1 minute)
AWS Console -> RDS -> petclinic-mysql
Show: Running, Multi-AZ: No, instance: db.t3.micro
Show: Secrets Manager -> petclinic/database-credentials
Key point: Credentials never hardcoded

### 5. Show Monitoring (1 minute)
Open Grafana dashboard
Show: Spring Boot Observability dashboard
Show: Kubernetes cluster overview

### Closing (30 seconds)
Full production-grade deployment:
Terraform IaC -> EKS Kubernetes -> GitOps ArgoCD
Secrets Manager -> External Secrets -> Zero hardcoded credentials
GitHub Actions CI/CD -> ECR -> Automatic deployment

## Demo URLs
| URL | What to show |
|-----|-------------|
| https://eta-oko.com | Live application |
| ArgoCD LoadBalancer URL | GitOps dashboard |
| Grafana LoadBalancer URL | Monitoring |
| AWS Console EKS | Cluster and nodes |
| AWS Console RDS | Database |
| GitHub Actions | CI/CD pipeline runs |

## Key points to emphasise
- Infrastructure as Code (Terraform) — repeatable, version controlled
- GitOps (ArgoCD) — cluster state always matches repo state
- Zero secrets in code — Secrets Manager and ESO
- Fully automated CI/CD — zero manual deployments
