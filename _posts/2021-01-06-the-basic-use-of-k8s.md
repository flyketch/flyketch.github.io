## 部署简单的k8s 服务

### 部署业务应用

> 创建deploy.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  namespace: handsonlab
  labels:
    app: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      name: myapp
  template:
    metadata:
      labels:
        name: myapp
      namespace: handsonlab
    spec:
      containers:
        - name: myapp
          image: nginx:1.19.6
          ports:
            - containerPort: 8080

```

> 部署应用并查看结果信息

```
kubectl apply -f deploy.yaml

kebectl get pod -n handsonlab
```

### 部署服务

> 创建service.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
  namespace: handsonlab
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
  type: NodePort
  selector:
    name: myapp
```

> 部署服务并查看结果信息

```
kubectl apply -f service.yaml

kubectl get service -n handsonlab
```

### 配置 ingress 开放外部访问

> 创建ingress.yaml

```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myapp-ingress
  namespace: handsonlab
spec:
  rules:
    - http:
        paths:
          - path: /welcome
            backend:
              serviceName: myapp-service
              servicePort: 8080
```

> 部署ingress并查看结果信息

```
kubectl apply -f ingress.yaml

kubectl get ingress -n handsonlab
```

### 卸载资源

> 卸载ingress

```
kubectl delete ingress myapp-ingress -n handsonlab
```

> 卸载service

```
kubectl delete service myapp-service -n handsonlab
```

> 卸载deployment

```
kubectl delete deployment myapp-deployment -n handsonlab
```

### 查看卸载结果

```
kubectl get all -n handsonlab
```

