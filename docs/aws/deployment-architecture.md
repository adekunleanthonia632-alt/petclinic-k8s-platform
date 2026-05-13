# GPM-151: AWS Deployment Architecture Selection

## Selected Architecture: EKS + RDS + ALB

## Why EKS was selected
- Managed Kubernetes — AWS handles control plane
- Auto-scaling node groups
- Native integration with ECR, ALB, Secrets Manager
- Industry standard for microservices deployment
- Supports GitOps with ArgoCD

## Why RDS MySQL was selected
- Managed database — no admin overhead
- Automatic backups
- High availability option available
- MySQL 8.0 compatible with Spring PetClinic
- db.t3.micro sufficient for demo workloads

## Why ALB was selected
- Native Kubernetes ingress via AWS Load Balancer Controller
- SSL termination (ACM certificate)
- HTTP to HTTPS automatic redirect
- Health checks for pods

## Architecture decisions
| Decision | Choice | Reason |
|----------|--------|--------|
| Kubernetes version | 1.32 | Latest stable supported by EKS |
| Node type | t3.small | Cost-effective for demo |
| Node count | 2 (min 1, max 3) | Balance of availability and cost |
| Database | RDS MySQL 8.0 | Managed, compatible with app |
| Networking | Public subnets only | No NAT gateway cost |
| SSL | ACM free certificate | Auto-renewing |
| GitOps | ArgoCD | Industry standard |
| Secrets | Secrets Manager + ESO | Security best practice |
