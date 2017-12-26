# auto-devops-demo
gitlab-ci 自动构建-部署-预览 demo

## 准备条件
* `gitlab-ce` 10.0.3+
* `gitlab docker runner` 9.5.0+
* `kubernetes` 1.7+
* `ingress-nginx` 0.9.0+
* `private registry` docker 私有仓库 https://registry.example.com


## 添加域名泛解析
假设你的域名为 `example.com`， `ingress` 服务地址为 `192.168.1.10`，添加一条泛解析记录：
```
*.example.com A 192.168.1.10
```
## 项目设置
在项目 Settings -> Integrations -> Kubernetes, 或 Admin Area -> Service Templates -> Kubernetes 中激活并设置 `KUBE_URL(API URL)`, `KUBE_CA_PEM(CA Certificate)`, `KUBE_TOKEN(Token)` 参数
## 修改 `.gitlab-ci.yml`
```
AUTO_DEVOPS_DOMAIN: example.com # 你的域名
CI_REGISTRY_IMAGE: registry.example.com/auto-devops-demo # 项目私有仓库地址
```
`可根据实际情况调整构建步骤`
## 运行
修改并提交代码，点击菜单 `CI/CD` -> `Environment` 即可看到自动构建-部署-预览效果。