# Namada 自助托管
该存储库有助于使用 Docker 快速启动具有 3 个验证器的本地版本的 namada 区块链.
这对于 Curios 用户和开发人员来说都是有帮助的.
有很多博客文章 [blog posts](https://mirror.xyz/0xe4e0B45aa2b06Df651337E3519ee6ccD81511Bf0/V8GPGi3XTf1WcL0nB2oGKo1T6X1cHfzfQCpj11tuUPI) 详细说明了如何安装和使用此代码.

### 要求
- Docker (或 Windows/Mac 上的 Docker Desktop) 
---

## 初始化设置

从示例文件创建 .env，并根据需要更改值
```shell
cp .env.sample .env
```
从 docker hub 拉取镜像或从头开始构建它。
要拉取图像，请执行以下操作：  
```shell
docker compose pull
```
或者，从 dockerfile 构建映像（需要更多时间并且需要大量 RAM） :

```shell
docker compose build
```

# 运行网络

启动区块链
```shell
docker compose up -d
```
第一次启动它需要 2-3 分钟来下载必要的文件并设置链。然后你就可以使用它  

#### 检查日志
```shell
docker compose logs -f 
```
#### 执行命令
执行到namada-1，例如
```shell
docker compose exec namada-1 bash
```

然后您可以在区块链上运行任何命令。例如：
```shell
namada --version
```
有关命令的更多信息，请查看官方文档 [official docs](https://docs.namada.net/users)

# Namada 接口和扩展

该堆栈附带一个名为的容器interface，该容器为 [official namada-interface](https://github.com/anoma/namada-interface)
提供服务.它还在启动期间构建 Namada 浏览器扩展.链ID自动设置为本地运行的 Namada 区块链.    
您可以通过该.env文件调整支持的环境变量.    
构建云需要很长时间才能完成，因此请耐心等待，在此期间您可以使用 CLI.    

## 使用界面
容器准备就绪后，您可以在浏览器中访问该界面，默认地址为 http://localhost:3000/

## 使用扩展
扩展文件可在 `extensions` 目录中访问.要安装 chrome 钱包扩展，请执行以下操作:    

I在 Chrome 中，选择“管理扩展”
单击切换开关以启用“开发人员模式”
单击“加载已解压”并指向 `extensions/chrome` 此项目中

**重要** 如果您重建 CHAIN_ID 更改，则应重新安装扩展    

# 拆除
删除所有内容
```shell
docker compose down -v
```

# 了解问题
- 用户界面不显示正确的帐户余额
- Interface Docker 镜像大小非常大，构建时间需要很长时间
