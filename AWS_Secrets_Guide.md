# AWS Secrets Configuration Guide for GitHub Actions

## Required GitHub Secrets
Add these secrets in your GitHub repository:

### 1. AWS_ROLE_TO_ASSUME
- **Value**: ARN of IAM role, e.g. `arn:aws:iam::123456789012:role/GitHubOIDCDeployRole`
- **Purpose**: Role assumed by GitHub Actions via OIDC.

### 2. AWS_REGION
- **Value**: AWS region, e.g. `us-east-1`

### 3. EKS_CLUSTER_NAME
- **Value**: Name of your EKS cluster, e.g. `my-eks-cluster`

---

## OIDC Setup for GitHub Actions
1. Create an IAM OIDC provider:
   - URL: `https://token.actions.githubusercontent.com`
2. Add trust policy to IAM role (see IAM_Trust_Policy.json).
3. Attach permissions policies:
   - AmazonEKSClusterPolicy
   - AmazonEKSWorkerNodePolicy
   - AmazonEC2ContainerRegistryFullAccess
   - AmazonEKS_CNI_Policy

---

## Workflow Reference
Your GitHub Actions workflow uses these secrets:
```yaml
with:
  role-to-assume: ${{ secrets.AWS_ROLE_TO_ASSUME }}
  aws-region: ${{ secrets.AWS_REGION }}
```
And updates kubeconfig:
```bash
aws eks update-kubeconfig --region ${{ secrets.AWS_REGION }} --name ${{ secrets.EKS_CLUSTER_NAME }}
```
