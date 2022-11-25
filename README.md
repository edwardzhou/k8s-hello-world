# k8s 
环境准备

```
# 装配k8s配置文件
kubectl kustomize . > k8s.yaml

# 部署
kubectl apply -f k8s.yaml --namespace=demo-test

```

# 打开项目网关

在kubesphere管理界面，打开项目网关，获得http端口号，如 31665
的云主机的安全组中，把31665端口放开

http://<server-ip>:31665/



# 当前需要解决的问题

web browser(210.129.19.178) ----> [ ingress(10.233.107.21) --path route--> nginx --upstream--> hello-world-app ]


Ingress把请求转发给nginx时，并没有把客户端的ip(210.129.19.178)传递给后端的nginx，而是把自己的容器ip(10.233.107.21)传递给了nginx

页面展示

```
x-forwarded-for: ["127.0.0.6, 10.233.107.21"]

x-real-ip: ["10.233.107.21"]

```

期待展示的是

```
x-forwarded-for: ["127.0.0.6, 10.233.107.21, 210.129.19.178"]

x-real-ip: ["210.129.19.178"]

```


这个配置不知道该如何调整，才能正确的把客户端ip传递下去