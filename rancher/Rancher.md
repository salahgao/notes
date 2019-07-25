# Rancher

Rancher是一套容器管理平台，它可以帮助组织在生产环境中轻松快捷的部署和管理容器。 Rancher可以轻松地管理各种环境的Kubernetes，满足IT需求并为DevOps团队提供支持。

## Docker Install

```
https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-convenience-script
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo systemctl start docker
sudo docker run hello-world
```

## 手动快速入门

[手动快速入门](https://rancher.com/docs/rancher/v2.x/en/quick-start-guide/deployment/quickstart-manual-setup/)

安装的时候 Rancher会占用80、443端口，nginx-ingress-controller也会占用80、443默认会报错。测试使用两个节点，nginx-ingress-controller部署在非Rancher的节点。

## 使用Ingress快速入门工作量
[使用Ingress快速入门工作量](https://rancher.com/docs/rancher/v2.x/en/quick-start-guide/workload/quickstart-deploy-workload-ingress/)

## NodePort快速入门的工作量
[NodePort快速入门的工作量](https://rancher.com/docs/rancher/v2.x/en/quick-start-guide/workload/quickstart-deploy-workload-nodeport/)

## 参考

https://rancher.com/docs/rancher/v2.x/en/

https://www.cnrancher.com/docs/