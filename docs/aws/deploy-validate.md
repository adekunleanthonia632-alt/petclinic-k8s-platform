# GPM-158: Deploy and Validate PetClinic on AWS

## Validation Checklist

### Step 1 — Verify all pods are running
kubectl get pods -n petclinic

| Pod | Expected Status |
|-----|----------------|
| config-server | Running |
| discovery-server | Running |
| api-gateway | Running |
| customers-service | Running |
| vets-service | Running |
| visits-service | Running |
| admin-server | Running |
| genai-service | Running |

### Step 2 — Verify services
kubectl get svc -n petclinic

### Step 3 — Verify ingress
kubectl get ingress -n petclinic

### Step 4 — Verify application
curl -I https://eta-oko.com

### Step 5 — Verify database connection
kubectl logs deployment/customers-service -n petclinic | grep -i 'started'

### Step 6 — Verify Eureka registration
kubectl port-forward svc/discovery-server 8761:8761 -n petclinic

### Step 7 — Verify monitoring
kubectl get pods -n monitoring

## Common issues and fixes
| Issue | Cause | Fix |
|-------|-------|-----|
| Pod in CrashLoopBackOff | Config server not ready | Wait 2 minutes |
| ImagePullBackOff | ECR auth expired | Re-login to ECR |
| Database connection failed | RDS SG rule missing | Check SG allows 3306 from VPC |
| ALB not created | LB controller not installed | Reinstall aws-load-balancer-controller |
