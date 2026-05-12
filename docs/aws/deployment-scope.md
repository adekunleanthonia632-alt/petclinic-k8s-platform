# GPM-149: AWS Deployment Scope Confirmation

## Confirmed with Greg (Technical Lead) and Sandra

## What is being deployed
Spring PetClinic Microservices — 8 services to AWS EKS

## AWS Account
Owner: Osenat Alonge (etaoko333)
Region: us-east-1 (N. Virginia)

## Infrastructure scope
| Resource | Details | Owner |
|----------|---------|-------|
| VPC | 10.0.0.0/16, 2 public subnets | Osenat/Terraform |
| EKS Cluster | petclinic-eks, K8s 1.32 | Osenat/Terraform |
| Node Group | 2x t3.small | Osenat/Terraform |
| ECR | 8 repositories | Osenat/Terraform |
| RDS MySQL | db.t3.micro, 20GB | Osenat/Terraform |
| ALB | internet-facing, SSL | Osenat/Helm |
| Route 53 | eta-oko.com | Osenat |
| ACM | SSL certificate | Osenat |

## What team members do NOT do
- No direct AWS console access for resource creation
- All infrastructure created via Terraform only
- All deployments via ArgoCD GitOps
- Secrets via AWS Secrets Manager + ESO only

## Greg and Sandra confirmation
Deployment scope confirmed: us-east-1, EKS + RDS + ECR + ALB
Team members contribute documentation and code reviews
Osenat applies infrastructure and manages AWS account
