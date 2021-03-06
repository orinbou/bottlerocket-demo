# bottlerocket-demo ð

Bottlerocket demo for EKS  

---

æ³¨æï¼
ãã®æé ã«ã¯ã eksctl ãã¼ã¸ã§ã³ 0.84.0 ä»¥éãå¿è¦ã§ãã  
è©³ç´°ã¯ä¸è¨ã® ãTo launch Bottlerocket nodes using eksctlã ããç¢ºèªãã ããã  
https://docs.aws.amazon.com/eks/latest/userguide/launch-node-bottlerocket.html
 
---

Bottlerocketã¯ã
AWSãç¬èªéçºããã³ã³ããåãããã¯ã¼ã¯ã­ã¼ãï¼â»EKSãECSãªã©ï¼ãå®è¡ããããã«ç¹å¥ã«è¨­è¨ããããè»½éã§å®å¨ãª Linuxãã¼ã¹ã®ãªã¼ãã³ã½ã¼ã¹OSã§ãã
AMIã¨ãã¦æä¾ãããã®ã§ãã³ã³ãããå®è¡ããã¯ã¼ã«ã¼ãã¼ãï¼ãã¹ãOSï¼ã¨ãã¦å©ç¨ãã¾ã

![Bottlerocketð](./assets/bottlerocket.png)

https://github.com/bottlerocket-os/bottlerocket

---

## ãã¢ã®æµã
* ð EKSã¯ã©ã¹ã¿æ§ç¯
* ð ãã¢ã¢ããªãããã­ã¤
* ð ãã¢ã¢ããªã¸ã¢ã¯ã»ã¹
* ð EKSã¯ã©ã¹ã¿åé¤ï¼å¾å§æ«ï¼

---
# ãã¢ãè¡ã

## ð EKSã¯ã©ã¹ã¿æ§ç¯
EKSã¯ã©ã¹ã¿ãæ§ç¯ããã
```
eksctl create cluster -f eks-cluster/cluster.yaml
```
å®è¡çµæï¼â»æ­£å¸¸ã«çµäºï¼
```
2022-02-23 03:34:13 [â¹]  eksctl version 0.84.0
2022-02-23 03:34:13 [â¹]  using region us-west-1
2022-02-23 03:34:13 [â¹]  setting availability zones to [us-west-1a us-west-1b]
2022-02-23 03:34:13 [â¹]  subnets for us-west-1a - public:192.168.0.0/19 private:192.168.64.0/19
2022-02-23 03:34:13 [â¹]  subnets for us-west-1b - public:192.168.32.0/19 private:192.168.96.0/19
2022-02-23 03:34:13 [â¹]  nodegroup "bottlerocket-demo-ng" will use "" [Bottlerocket/1.21]
2022-02-23 03:34:13 [â¹]  using Kubernetes version 1.21
2022-02-23 03:34:13 [â¹]  creating EKS cluster "bottlerocket-demo2" in "us-west-1" region with managed nodes
2022-02-23 03:34:13 [â¹]  1 nodegroup (bottlerocket-demo-ng) was included (based on the include/exclude rules)
2022-02-23 03:34:13 [â¹]  will create a CloudFormation stack for cluster itself and 0 nodegroup stack(s)
2022-02-23 03:34:13 [â¹]  will create a CloudFormation stack for cluster itself and 1 managed nodegroup stack(s)
2022-02-23 03:34:13 [â¹]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-west-1 --cluster=bottlerocket-demo2'
2022-02-23 03:34:13 [â¹]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "bottlerocket-demo2" in "us-west-1"
2022-02-23 03:34:13 [â¹]  CloudWatch logging will not be enabled for cluster "bottlerocket-demo2" in "us-west-1"
2022-02-23 03:34:13 [â¹]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-west-1 --cluster=bottlerocket-demo2'
2022-02-23 03:34:13 [â¹]  
2 sequential tasks: { create cluster control plane "bottlerocket-demo2", 
    2 sequential sub-tasks: { 
        wait for control plane to become ready,
        create managed nodegroup "bottlerocket-demo-ng",
    } 
}
2022-02-23 03:34:13 [â¹]  building cluster stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:34:14 [â¹]  deploying stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:34:44 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:35:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:36:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:37:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:38:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:39:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:40:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:41:15 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:42:15 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:43:15 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:44:15 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:45:15 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 03:47:16 [â¹]  building managed nodegroup stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:47:17 [â¹]  deploying stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:47:17 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:47:33 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:47:51 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:48:08 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:48:25 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:48:43 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:49:00 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:49:17 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:49:35 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:49:50 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:50:08 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:50:24 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:50:44 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 03:50:44 [â¹]  waiting for the control plane availability...
2022-02-23 03:50:44 [â]  saved kubeconfig as "/home/ec2-user/.kube/config"
2022-02-23 03:50:44 [â¹]  no tasks
2022-02-23 03:50:44 [â]  all EKS cluster resources for "bottlerocket-demo2" have been created
2022-02-23 03:50:44 [â¹]  nodegroup "bottlerocket-demo-ng" has 3 node(s)
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:44 [â¹]  waiting for at least 1 node(s) to become ready in "bottlerocket-demo-ng"
2022-02-23 03:50:44 [â¹]  nodegroup "bottlerocket-demo-ng" has 3 node(s)
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:44 [â¹]  node "ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal" is ready
2022-02-23 03:50:46 [â¹]  kubectl command should work with "/home/ec2-user/.kube/config", try 'kubectl get nodes'
2022-02-23 03:50:46 [â]  EKS cluster "bottlerocket-demo2" in "us-west-1" region is ready
```
æ§ç¯ããEKSã¯ã©ã¹ã¿ãç¢ºèªããã
```
kubectl get nodes

NAME                                            STATUS   ROLES    AGE     VERSION
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   6m34s   v1.21.9
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   6m34s   v1.21.9
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   6m26s   v1.21.9
```
å¨ãã¼ãï¼ðx3å°ï¼ã Ready ã«ãªã£ã¦ããã°OKã§ãã

ããå°ãè©³ããç¢ºèªãã¦ã¿ãã¨ã¯ã¼ã«ã¼ãã¼ãã® OS-IMAGE ãã  
ã¡ããã¨ ãBottlerocket OS 1.6.0 (aws-k8s-1.21)ã ã«ãªã£ã¦ãããã¨ãç¢ºèªã§ãã¾ãã
```
kubectl get nodes -o wide

NAME                                            STATUS   ROLES    AGE     VERSION   INTERNAL-IP      EXTERNAL-IP     OS-IMAGE                               KERNEL-VERSION   CONTAINER-RUNTIME
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   9m34s   v1.21.9   192.168.28.190   52.53.249.241   Bottlerocket OS 1.6.0 (aws-k8s-1.21)   5.10.93          containerd://1.5.9+bottlerocket
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   9m34s   v1.21.9   192.168.35.196   18.144.39.104   Bottlerocket OS 1.6.0 (aws-k8s-1.21)   5.10.93          containerd://1.5.9+bottlerocket
ip-xxx-xxx-xxx-xxx.us-west-1.compute.internal   Ready    <none>   9m26s   v1.21.9   192.168.48.243   13.56.178.164   Bottlerocket OS 1.6.0 (aws-k8s-1.21)   5.10.93          containerd://1.5.9+bottlerocket
```

---

## ð ãã¢ã¢ããªãããã­ã¤
ååç©ºéãä½æããã
```
kubectl create namespace sock-shop

namespace/sock-shop created
```
ãã¢ã¢ããªï¼Sock Shopï¼ãããã­ã¤ããã
```
kubectl apply -f microservices-demo/complete-demo.yaml

deployment.apps/carts-db created
service/carts-db created
deployment.apps/carts created
service/carts created
deployment.apps/catalogue-db created
service/catalogue-db created
deployment.apps/catalogue created
service/catalogue created
deployment.apps/front-end created
service/front-end created
deployment.apps/orders-db created
service/orders-db created
deployment.apps/orders created
service/orders created
deployment.apps/payment created
service/payment created
deployment.apps/queue-master created
service/queue-master created
deployment.apps/rabbitmq created
service/rabbitmq created
deployment.apps/shipping created
service/shipping created
deployment.apps/user-db created
service/user-db created
deployment.apps/user created
service/user created
```

ã³ãã³ãï¼kubectlï¼ã§ãã¢ã¢ããªã®k8sãªã½ã¼ã¹ï¼Podï¼ã®ç¶æãç¢ºèªããã
```
kubectl get pod -n sock-shop

NAME                           READY   STATUS    RESTARTS   AGE
carts-7c9df6fdb4-x5rzm         1/1     Running   0          6m31s
carts-db-6c6c68b747-n2p9q      1/1     Running   0          6m31s
catalogue-7c6dcb64f7-spq6v     1/1     Running   0          6m31s
catalogue-db-96f6f6b4c-6nhl9   1/1     Running   0          6m31s
front-end-7b8bcd59cb-vkzbj     1/1     Running   0          6m31s
orders-c9994cff9-gnc9d         1/1     Running   0          6m30s
orders-db-659949975f-txdfz     1/1     Running   0          6m30s
payment-8576977df5-4n9cz       1/1     Running   0          6m30s
queue-master-bbb6c4b9d-cfsqv   1/1     Running   0          6m29s
rabbitmq-6d77f74dc-6wvwr       1/1     Running   0          6m29s
shipping-5d7c4f8bbf-tpksr      1/1     Running   0          6m29s
user-846f474c46-wdb8j          1/1     Running   0          6m28s
user-db-5f68d7b558-w97g9       1/1     Running   0          6m29s
```
å¨ã¦ã® Pod ã Running ã«ãªã£ã¦ããã°OKã§ãã

---

## ð ãã¢ã¢ããªã¸ã¢ã¯ã»ã¹
ãã¢ã¢ããªï¼Sock Shopï¼ç»é¢ã¸ã¢ã¯ã»ã¹ããããã®URLãç¢ºèªããã
```
kubectl get svc front-end -n sock-shop

NAME        TYPE           CLUSTER-IP        EXTERNAL-IP                                     PORT(S)        AGE
front-end   LoadBalancer   xxx.xxx.xxx.xxx   yyyyyy-1234567890.us-west-1.elb.amazonaws.com   80:30001/TCP   7m46s
```
Webãã©ã¦ã¶ã§ãã¢ã¢ããªï¼Sock Shopï¼ç»é¢ã¸ã¢ã¯ã»ã¹ããã  
http://yyyyyy-1234567890.us-west-1.elb.amazonaws.com/

![demo](./assets/front-end.png)

ã¡ããã¨ãã¢ã¢ããªï¼Sock Shopï¼ãåãã¦ã¾ãã­ã

---

## ð EKSã¯ã©ã¹ã¿åé¤ï¼å¾å§æ«ï¼
æå¾ã«EKSã¯ã©ã¹ã¿ãåé¤ããã
```
eksctl delete cluster -f eks-cluster/cluster.yaml --wait
```
å®è¡çµæï¼â»æ­£å¸¸ã«çµäºï¼
```
2022-02-23 12:07:58 [â¹]  eksctl version 0.84.0
2022-02-23 12:07:58 [â¹]  using region us-west-1
2022-02-23 12:07:58 [â¹]  deleting EKS cluster "bottlerocket-demo2"
2022-02-23 12:08:46 [â¹]  deleted 0 Fargate profile(s)
2022-02-23 12:08:46 [â]  kubeconfig has been updated
2022-02-23 12:08:46 [â¹]  cleaning up AWS load balancers created by Kubernetes objects of Kind Service or Ingress
2022-02-23 12:09:54 [â¹]  
2 sequential tasks: { delete nodegroup "bottlerocket-demo-ng", delete cluster control plane "bottlerocket-demo2" 
}
2022-02-23 12:09:54 [â¹]  will delete stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:09:54 [â¹]  waiting for stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng" to get deleted
2022-02-23 12:09:54 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:10:13 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:10:33 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:10:51 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:11:06 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:11:25 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:11:43 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:12:03 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:12:21 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:12:38 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-nodegroup-bottlerocket-demo-ng"
2022-02-23 12:12:39 [â¹]  will delete stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:12:39 [â¹]  waiting for stack "eksctl-bottlerocket-demo2-cluster" to get deleted
2022-02-23 12:12:39 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:12:55 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:13:14 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:13:34 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:13:51 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:14:06 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:14:26 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:14:42 [â¹]  waiting for CloudFormation stack "eksctl-bottlerocket-demo2-cluster"
2022-02-23 12:14:42 [â]  all cluster resources were deleted
```
â»è¿½è¨ï¼  
AWSããã³ã³ã® CloudFormation > ã¹ã¿ãã¯ ã§ç¢ºèªããã¨ããåé¤ã«å¤±æï¼DELETE_FAILEDï¼ãããã¨ãããããã§ãã  
ãã®å ´åã¯ãAWSããã³ã³ããé¢é£ãªã½ã¼ã¹ï¼VPC, Subnetãªã©ï¼ãæåã§åé¤ãã¦ããã¹ã¿ãã¯ãåé¤ãã¦ãã ããã  

---

ä»¥ä¸ã§ãBottlerocketã®ãã¢ã¯çµäºã§ãããç²ãæ§ã§ãã<(_ _)>
