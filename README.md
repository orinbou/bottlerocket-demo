# bottlerocket-demo
Bottlerocket demo for EKS

---

Bottlerocketは、
AWSが独自開発したコンテナ化されたワークロード（※EKS、ECSなど）を実行するために特別に設計された、軽量で安全な LinuxベースのオープンソースOSです。
AMIとして提供されるので、コンテナを実行するワーカーノード（ホストOS）として利用します

![demo](./assets/bottlerocket.png)

https://github.com/bottlerocket-os/bottlerocket

---

## デモの流れ
* EKSクラスタ構築
* デモアプリをデプロイ
* デモアプリへアクセス
* EKSクラスタ削除（後始末）

---
# デモを行う

## EKSクラスタ構築
EKSクラスタを構築する。
```
eksctl create cluster -f eks-cluster/cluster.yaml
```
実行結果（※正常に終了）
```
[ℹ]  eksctl version 0.34.0
[ℹ]  using region us-west-2
[ℹ]  setting availability zones to [us-west-2d us-west-2b us-west-2a]
[ℹ]  subnets for us-west-2d - public:192.168.0.0/19 private:192.168.96.0/19
[ℹ]  subnets for us-west-2b - public:192.168.32.0/19 private:192.168.128.0/19
[ℹ]  subnets for us-west-2a - public:192.168.64.0/19 private:192.168.160.0/19
[ℹ]  using Kubernetes version 1.18
[ℹ]  creating EKS cluster "bottlerocket-demo" in "us-west-2" region with managed nodes
[ℹ]  1 nodegroup (bottlerocket-demo-ng) was included (based on the include/exclude rules)
[ℹ]  will create a CloudFormation stack for cluster itself and 0 nodegroup stack(s)
[ℹ]  will create a CloudFormation stack for cluster itself and 1 managed nodegroup stack(s)
[ℹ]  if you encounter any issues, check CloudFormation console or try 'eksctl utils describe-stacks --region=us-west-2 --cluster=bottlerocket-demo'
[ℹ]  CloudWatch logging will not be enabled for cluster "bottlerocket-demo" in "us-west-2"
[ℹ]  you can enable it with 'eksctl utils update-cluster-logging --enable-types={SPECIFY-YOUR-LOG-TYPES-HERE (e.g. all)} --region=us-west-2 --cluster=bottlerocket-demo'
[ℹ]  Kubernetes API endpoint access will use default of {publicAccess=true, privateAccess=false} for cluster "bottlerocket-demo" in "us-west-2"
[ℹ]  2 sequential tasks: { create cluster control plane "bottlerocket-demo", 3 sequential sub-tasks: { no tasks, create addons, create managed nodegroup "bottlerocket-demo-ng" } }
[ℹ]  building cluster stack "eksctl-bottlerocket-demo-cluster"
[ℹ]  deploying stack "eksctl-bottlerocket-demo-cluster"
[ℹ]  building managed nodegroup stack "eksctl-bottlerocket-demo-nodegroup-bottlerocket-demo-ng"
[ℹ]  deploying stack "eksctl-bottlerocket-demo-nodegroup-bottlerocket-demo-ng"
[ℹ]  waiting for the control plane availability...
[✔]  saved kubeconfig as "C:\\Users\\xxxxxx.xxxxxx/.kube/config"
[ℹ]  no tasks
[✔]  all EKS cluster resources for "bottlerocket-demo" have been created
[ℹ]  nodegroup "bottlerocket-demo-ng" has 3 node(s)
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  waiting for at least 1 node(s) to become ready in "bottlerocket-demo-ng"
[ℹ]  nodegroup "bottlerocket-demo-ng" has 3 node(s)
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  node "ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal" is ready
[ℹ]  kubectl command should work with "C:\\Users\\xxxxxx.xxxxxx/.kube/config", try 'kubectl get nodes'
[✔]  EKS cluster "bottlerocket-demo" in "us-west-2" region is ready
```
構築したEKSクラスタを確認する。
```
kubectl get nodes

NAME                                            STATUS   ROLES    AGE   VERSION
ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal   Ready    <none>   77s   v1.18.9-eks-d1db3c
ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal   Ready    <none>   93s   v1.18.9-eks-d1db3c
ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal   Ready    <none>   95s   v1.18.9-eks-d1db3c
```
全ノードが Ready になっていればOKです。

---

## デモアプリをデプロイ
下記のGitリポジトリにあるデモアプリをデプロイします。（※ここは省略）

* Sock Shop :   
https://github.com/orinbou/microservices-demo.git
```
kubectl apply -f https://github.com/orinbou/microservices-demo/blob/master/deploy/kubernetes/complete-demo.yaml


```

---

## デモアプリへアクセス
デモアプリ（Sock Shop）画面へアクセスするためのURLを確認する。
```
kubectl get svc front-end -n sock-shop

NAME        TYPE           CLUSTER-IP        EXTERNAL-IP                                     PORT(S)        AGE
front-end   LoadBalancer   xxx.xxx.xxx.xxx   yyyyyy-1234567890.us-west-2.elb.amazonaws.com   80:30001/TCP   7m46s
```
Webブラウザでデモアプリ（Sock Shop）画面へアクセスする。  
http://yyyyyy-1234567890.us-west-2.elb.amazonaws.com/
![demo](./assets/demo12.png)

コマンド（kubectl）でデモアプリのk8sリソース（Pod）の状態を確認する。
```
kubectl get pod -n sock-shop

NAME                            READY   STATUS    RESTARTS   AGE
carts-7bbbd7779d-gd5xl          1/1     Running   0          16m
carts-db-84b777d9c-wd8g4        1/1     Running   0          16m
catalogue-8684f655d9-m2gqh      1/1     Running   0          16m
catalogue-db-5579f7f4cb-vhhcb   1/1     Running   0          16m
front-end-6f5fc69d6-kzr4r       1/1     Running   0          16m
orders-7ccf68495-mq4d7          1/1     Running   0          16m
orders-db-77c46b9c85-8trt8      1/1     Running   0          16m
payment-74976d749f-bsn5h        1/1     Running   0          16m
queue-master-799b6b57d5-t2jrq   1/1     Running   0          16m
rabbitmq-8458d7d4c-qwc8s        1/1     Running   0          16m
shipping-5c89f4886c-vvjdb       1/1     Running   0          16m
user-d6c48f668-6zm97            1/1     Running   0          16m
user-db-5cdfd6d44b-mnbbf        1/1     Running   0          16m
```

コマンド（kubectl）でデモアプリのk8sリソース（Pod）の詳細を確認する。
```
kubectl describe pod carts-7bbbd7779d-gd5xl -n sock-shop
```
実行結果
```
Name:         carts-7bbbd7779d-gd5xl
Namespace:    sock-shop
Priority:     0
Node:         ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal/xxx-xxx-xxx-xxx
Start Time:   Sat, 19 Dec 2020 23:14:23 +0900
Labels:       name=carts
              pod-template-hash=7bbbd7779d
Annotations:  kubernetes.io/psp: eks.privileged
Status:       Running
IP:           xxx-xxx-xxx-xxx
IPs:
  IP:           xxx-xxx-xxx-xxx
Controlled By:  ReplicaSet/carts-7bbbd7779d
Containers:
  carts:
    Container ID:   docker://508c46d3567754e57b68d73e13020d2242217c5e2c9c96bcda55e65042832378
    Image:          weaveworksdemos/carts:0.4.8
    Image ID:       docker-pullable://weaveworksdemos/carts@sha256:434d2f5a6e0e8beef1f253fe96f45b8437a703125fc003434c5282ecf8969a4f
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Sat, 19 Dec 2020 23:14:35 +0900
    Ready:          True
    Restart Count:  0
    Environment:
      ZIPKIN:     zipkin.jaeger.svc.cluster.local
      JAVA_OPTS:  -Xms64m -Xmx128m -XX:PermSize=32m -XX:MaxPermSize=64m -XX:+UseG1GC -Djava.security.egd=file:/dev/urandom
    Mounts:
      /tmp from tmp-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-wzp98 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  tmp-volume:
    Type:       EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:     Memory
    SizeLimit:  <unset>
  default-token-wzp98:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-wzp98
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  beta.kubernetes.io/os=linux
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age   From                                                   Message
  ----    ------     ----  ----                                                   -------
  Normal  Scheduled  27m   default-scheduler                                      Successfully assigned sock-shop/carts-7bbbd7779d-gd5xl to ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal
  Normal  Pulling    27m   kubelet, ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal  Pulling image "weaveworksdemos/carts:0.4.8"
  Normal  Pulled     27m   kubelet, ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal  Successfully pulled image "weaveworksdemos/carts:0.4.8"
  Normal  Created    27m   kubelet, ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal  Created container carts
  Normal  Started    27m   kubelet, ip-xxx-xxx-xxx-xxx.us-west-2.compute.internal  Started container carts
```

コマンド（kubectl）でデモアプリのk8sリソース（Pod）のログを確認する。
```
kubectl logs carts-7bbbd7779d-gd5xl -n sock-shop
```
実行結果
```
OpenJDK 64-Bit Server VM warning: ignoring option PermSize=32m; support was removed in 8.0
OpenJDK 64-Bit Server VM warning: ignoring option MaxPermSize=64m; support was removed in 8.0
2020-12-19 14:14:44.663  INFO [bootstrap,,,] 6 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@51521cc1: startup date [Sat Dec 19 14:14:44 GMT 2020]; root of context hierarchy
2020-12-19 14:14:49.155  INFO [bootstrap,,,] 6 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'configurationPropertiesRebinderAutoConfiguration' of type [class org.springframework.cloud.autoconfigure.ConfigurationPropertiesRebinderAutoConfiguration$$EnhancerBySpringCGLIB$$b894f39] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v1.4.4.RELEASE)

2020-12-19 14:14:51.754  INFO [carts,,,] 6 --- [           main] works.weave.socks.cart.CartApplication   : No active profile set, falling back to default profiles: default
2020-12-19 14:14:51.841  INFO [carts,,,] 6 --- [           main] ationConfigEmbeddedWebApplicationContext : Refreshing org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@649d209a: startup date [Sat Dec 19 14:14:51 GMT 2020]; parent: org.springframework.context.annotation.AnnotationConfigApplicationContext@51521cc1
2020-12-19 14:14:57.688  INFO [carts,,,] 6 --- [           main] o.s.b.f.s.DefaultListableBeanFactory     : Overriding bean definition for bean 'managementServletContext' with a different definition: replacing [Root bean: class [null]; scope=; abstract=false; lazyInit=false; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; factoryBeanName=org.springframework.boot.actuate.autoconfigure.EndpointWebMvcHypermediaManagementContextConfiguration; factoryMethodName=managementServletContext; initMethodName=null; destroyMethodName=(inferred); defined in class path resource [org/springframework/boot/actuate/autoconfigure/EndpointWebMvcHypermediaManagementContextConfiguration.class]] with [Root bean: class [null]; scope=; abstract=false; lazyInit=false; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; factoryBeanName=org.springframework.boot.actuate.autoconfigure.EndpointWebMvcAutoConfiguration; factoryMethodName=managementServletContext; initMethodName=null; destroyMethodName=(inferred); defined in class path resource [org/springframework/boot/actuate/autoconfigure/EndpointWebMvcAutoConfiguration.class]]
2020-12-19 14:14:58.715  WARN [carts,,,] 6 --- [           main] o.s.c.a.ConfigurationClassPostProcessor  : Cannot enhance @Configuration bean definition 'refreshScope' since its singleton instance has been created too early. The typical cause is a non-static @Bean method with a BeanDefinitionRegistryPostProcessor return type: Consider declaring such methods as 'static'.
2020-12-19 14:14:59.591  INFO [carts,,,] 6 --- [           main] o.s.cloud.context.scope.GenericScope     : BeanFactory id=5e44614a-7369-3438-a326-d1b2bda21648
2020-12-19 14:15:00.384  INFO [carts,,,] 6 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.cloud.sleuth.instrument.async.AsyncDefaultAutoConfiguration$DefaultAsyncConfigurerSupport' of type [class org.springframework.cloud.sleuth.instrument.async.AsyncDefaultAutoConfiguration$DefaultAsyncConfigurerSupport$$EnhancerBySpringCGLIB$$2cb0e9ff] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2020-12-19 14:15:01.693  INFO [carts,,,] 6 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.cloud.autoconfigure.ConfigurationPropertiesRebinderAutoConfiguration' of type [class org.springframework.cloud.autoconfigure.ConfigurationPropertiesRebinderAutoConfiguration$$EnhancerBySpringCGLIB$$b894f39] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2020-12-19 14:15:01.791  INFO [carts,,,] 6 --- [           main] trationDelegate$BeanPostProcessorChecker : Bean 'org.springframework.cloud.sleuth.instrument.web.TraceWebAutoConfiguration' of type [class org.springframework.cloud.sleuth.instrument.web.TraceWebAutoConfiguration$$EnhancerBySpringCGLIB$$ecb4cb09] is not eligible for getting processed by all BeanPostProcessors (for example: not eligible for auto-proxying)
2020-12-19 14:15:05.023  INFO [carts,,,] 6 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat initialized with port(s): 80 (http)
2020-12-19 14:15:05.075  INFO [carts,,,] 6 --- [           main] o.apache.catalina.core.StandardService   : Starting service Tomcat
2020-12-19 14:15:05.081  INFO [carts,,,] 6 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/8.5.11
2020-12-19 14:15:05.479  INFO [carts,,,] 6 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2020-12-19 14:15:05.487  INFO [carts,,,] 6 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 13646 ms
：（※以下省略）
```

---

## EKSクラスタ削除（後始末）
最後にEKSクラスタを削除する。
```
eksctl delete cluster -f eks-cluster/cluster.yaml
```
実行結果（※正常に終了）
```
[ℹ]  eksctl version 0.34.0
[ℹ]  using region us-west-2
[ℹ]  deleting EKS cluster "bottlerocket-demo"
[ℹ]  deleted 0 Fargate profile(s)
[✔]  kubeconfig has been updated
[ℹ]  cleaning up AWS load balancers created by Kubernetes objects of Kind Service or Ingress
[ℹ]  2 sequential tasks: { delete nodegroup "bottlerocket-demo-ng", delete cluster control plane "bottlerocket-demo" [async] }
[ℹ]  will delete stack "eksctl-bottlerocket-demo-nodegroup-bottlerocket-demo-ng"
[ℹ]  waiting for stack "eksctl-bottlerocket-demo-nodegroup-bottlerocket-demo-ng" to get deleted
[ℹ]  will delete stack "eksctl-bottlerocket-demo-cluster"
[✔]  all cluster resources were deleted
```
※追記：  
AWSマネコンの CloudFormation > スタック で確認したところ削除に失敗（DELETE_FAILED）することがあるようです。  
その場合は、AWSマネコンから関連リソース（VPC, Subnetなど）を手動で削除してからスタックを削除してください。  

コマンド（eksctl）実行時にスタック削除結果を待機する場合は「--wait」オプションを使うと良さそうです。
```
eksctl delete cluster -f eks-cluster/cluster.yaml --wait
```

---

以上で、Bottlerocketのデモは終了です。お疲れ様でした<(_ _)>
