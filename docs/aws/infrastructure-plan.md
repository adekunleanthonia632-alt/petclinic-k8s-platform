# GPM-10: AWS Infrastructure Deployment Plan

## Phase-by-Phase Deployment Plan

### Phase 1 — Terraform Infrastructure (15-20 minutes)
cd petclinic-k8s-platform/terraform
terraform init -backend-config=backend.hcl
terraform plan -out=tfplan
terraform apply tfplan
Creates: VPC, EKS cluster, ECR repos, RDS MySQL

### Phase 2 — Connect kubectl
aws eks update-kubeconfig --region us-east-1 --name petclinic-eks
kubectl get nodes
Expected: 2 nodes in Ready state

### Phase 3 — Install cluster components
helm install external-secrets external-secrets/external-secrets \
  --namespace external-secrets --create-namespace

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  --namespace kube-system --set clusterName=petclinic-eks

kubectl apply -n argocd -f \
  https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

### Phase 4 — Deploy ArgoCD manifests
kubectl apply -f argocd/secret-store.yml
kubectl apply -f argocd/external-secret.yml
kubectl apply -f argocd/application.yml
kubectl apply -f argocd/ingress.yml

### Phase 5 — Verify deployment
kubectl get pods -n petclinic
kubectl get ingress -n petclinic
curl https://eta-oko.com

## Cost per session
Running cost: approximately $0.22/hour
ALWAYS run terraform destroy after every session

## Rollback plan
If deployment fails: terraform destroy -auto-approve
Re-run from Phase 1 with corrected configuration
