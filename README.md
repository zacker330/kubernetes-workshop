1. 认识kubectl与k8s之间的关系
1. 认识Pod、创建Pod、进入Pod，查看Pod的日志
  ```bash
  kubectl apply -f 1.httpbin-pod.yaml
  # 列出default namespace的Pod
  kubectl get pod 
  # 查看Pod的事件
  kubectl describe pod httpbin
  # 查看日志，学习会错误日志
  kubectl logs -f httpbin
  # 再次查看日志
  kubectl logs -f httpbin -c httpbin-container
  # 将pod代理到本地
  kubectl port-forward httpbin 8080:80
  ```
1. 认识service、Endpoint
  ```bash
  # 创建service
  kubectl apply -f 2.httpbin-pod-service.yaml
  # 查看svc，认识endpoint
  kubectl describe svc httpbin-service
  # 将svc代理到本地
  kubectl port-forward svc/httpbin-service 8080:80
  ```
  最后，清理实验现场：
  ```yaml
  kubectl delete -f 1.httpbin-pod.yaml
  kubectl delete -f 2.httpbin-pod-service.yaml
  ```
1. 认识Deployment
  可以理解为Pod的控制器的一种类型
  ```bash
  kubectl apply -f 4.httpbin-deployment.yaml
  kubectl get pod
  # 查看其中一个pod
  kubectl describe pod httpbin-deployment-5d4c65bb96-67dz9
  # 修改4.httpbin-deployment.yaml文件，将replicas的值改成3后，执行 
  kubectl apply -f 4.httpbin-deployment.yaml
  #然后再看pod数量
  kubectl get pod
  # 这时，创建svc
  kubectl apply -f 2.httpbin-pod-service.yaml
  # 执行
  kubectl describe svc httpbin-service
  ```
  最后，清理实验现场：
  ```
  kubectl delete -f 2.httpbin-pod-service.yaml
  kubectl delete -f 4.httpbin-deployment.yaml
  ```

1. 认识Helm
  本质上就是一个k8s的manifest的模板引擎。
  1. 查看chart，了解chart与Helm的关系
  2. 查看values.yaml，了解values和chart的关系
  3. 我们是如何使用chart的
  4. 执行chart
    ```bash
    helm install httpbin ./5.http-bin-chart
    #查看chart生成的manifest
    kubectl get pod 
    kubectl get pod httpbin-http-bin-5976bf8c69-pxsrh -o yaml
    # 修改values中的resource配置，了解resource配置，再次执行部署
    helm upgrade --install httpbin ./5.http-bin-chart

    ```
  
  

