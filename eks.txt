eksctl create cluster --name game-deploy --region ap-south-1 --fargate

aws eks update-kubeconfig --name game-deploy --region ap-south-1


```eksctl create fargateprofile \
    --cluster game-deploy \ 
    --region ap-south-1 \
    --name alb-sample-app \
    --namespace game-2048```         --- to create new fargate profile(namespace)
