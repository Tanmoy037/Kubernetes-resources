**To Create Eks cluster using Eksctl**

```eksctl create cluster --name game-deploy --region ap-south-1 --fargate ```

**For using Kubectl**

```aws eks update-kubeconfig --name game-deploy --region ap-south-1```

**To create new fargate profile**

```
eksctl create fargateprofile \
    --cluster game-deploy \ 
    --region ap-south-1 \
    --name alb-sample-app \
    --namespace game-2048
```

**commands to configure IAM OIDC provider**

```eksctl utils associate-iam-oidc-provider --cluster game-deploy --approve```

**Download IAM policy**

```curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json```
