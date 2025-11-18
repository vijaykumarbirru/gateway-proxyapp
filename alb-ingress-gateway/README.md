# ALB + NGINX Ingress Helm Chart
This chart installs AWS ALB Ingress Controller and NGINX Ingress Controller together.

## Installation
```bash
helm install alb-nginx alb-nginx-ingress/
```
Deploy in gateway vpc

References
https://aws.amazon.com/blogs/opensource/kubernetes-ingress-aws-alb-ingress-controller/

https://docs.aws.amazon.com/eks/latest/userguide/lbc-manifest.html
kubectl apply \
--validate=false \
-f https://github.com/jetstack/cert-manager/releases/download/v1.13.5/cert-manager.yaml