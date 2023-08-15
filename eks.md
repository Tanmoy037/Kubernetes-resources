**To Create Eks cluster using Eksctl**
```eksctl create cluster --name game-deploy --region ap-south-1 --fargate ```

**For using Kubectl**
```aws eks update-kubeconfig --name game-deploy --region ap-south-1```

**To create new fargate profile(namespace)**

```
eksctl create fargateprofile \
    --cluster game-deploy \ 
    --region ap-south-1 \
    --name alb-sample-app \
    --namespace game-2048
```
       
