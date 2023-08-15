eksctl create cluster --name game-deploy --region ap-south-1 --fargate

aws eks update-kubeconfig --name game-deploy --region ap-south-1

**To create new fargate profile(namespace)**
       
