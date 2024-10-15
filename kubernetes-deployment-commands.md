# Kubernetes Deployment Commands

This document provides a list of common `kubectl` commands used for managing Kubernetes deployments.

```bash
# Create a Deployment
kubectl create -f deployment-definition.yml

# Get Deployments
kubectl get deployments

# Update a Deployment
kubectl apply -f deployment-definition.yml
kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1

# Check Deployment Status
kubectl rollout status deployment/myapp-deployment

# Check Deployment History
kubectl rollout history deployment/myapp-deployment

# Rollback a Deployment
kubectl rollout undo deployment/myapp-deployment
