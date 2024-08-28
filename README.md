<p align="center">
    <a href="#" target="_blank" rel="noopener">
        <img src="https://i.imgur.com/4ff4nUV.jpeg" alt="Certimate - Your Trusted SSL Automation Partner" />
    </a>
</p>

# Certimate

Certimate 是一个开源的 SSL 证书管理工具，具有以下特点：

1. 支持私有部署：部署方法简单，只需下载二进制文件并执行即可完成安装。
2. 数据安全：由于是私有部署，所有数据均存储在本地，不会保存在服务商的服务器上，确保数据的安全性。
3. 操作方便：通过简单的配置即可轻松申请 SSL 证书，并且在证书即将过期时自动续期，无需人工干预。

Certimate 旨在为用户提供一个安全、简便的 SSL 证书管理解决方案。

- [Certimate](#certimate)
  - [安装](#安装)
    - [二进制文件](#二进制文件)
    - [Docker 安装](#docker-安装)
    - [默认账号：](#默认账号)
  - [概念](#概念)
    - [域名](#域名)
    - [dns 服务商授权信息](#dns-服务商授权信息)
    - [部署服务商授权信息](#部署服务商授权信息)
  - [使用](#使用)
  - [许可证](#许可证)



## 安装

### 二进制文件

你可以直接从[Releases 页](https://github.com/usual2970/certimate/releases)下载预先编译好的二进制文件，解压后执行:

```bash
./certimate serve
```


### Docker 安装

```bash

git clone git@github.com:usual2970/certimate.git && cd certimate/docker && docker compose up -d

```

然后在浏览器中访问 http://127.0.0.1:8090 即可访问 Certimate 管理页面。

### 默认账号：

```bash
用户名：admin@certimate.fun
密码：1234567890
```

## 概念

Certimate 的工作流程如下：

1. 用户通过 Certimate 管理页面填写申请证书的信息，包括域名、dns 服务商的授权信息、以及要部署到的服务商的授权信息。
2. Certimate 向证书场商的 API 发起申请请求，获取 SSL 证书。
3. Certimate 存储证书信息，包括证书内容、私钥、证书有效期等，并在证书即将过期时自动续期。
4. Certimate 向服务商的 API 发起部署请求，将证书部署到服务商的服务器上。

这就涉及域名、dns 服务商的授权信息、部署服务商的授权信息等。

### 域名

就是要申请证书的域名。

### dns 服务商授权信息

给域名申请证书需要证明域名是你的，所以我们手动申请证书的时候一般需要在域名服务商的控制台解析记录中添加一个 TXT 记录。

Certimate 会自动添加一个 TXT 记录，你只需要在 Certimate 后台中填写你的域名服务商的授权信息即可。

比如你在阿里云购买的域名，授权信息如下：

```bash
accessKeyId: xxx
accessKeySecret: TOKEN
```

在腾讯云购买的域名，授权信息如下：

```bash
secretId: xxx
secretKey: TOKEN
```

### 部署服务商授权信息

Certimate 申请证书后，会自动将证书部署到你指定的目标上，比如阿里云 CDN 这时你需要填写阿里云的授权信息。Certimate 会根据你填写的授权信息及域名找到对应的 CDN 服务,并将证书部署到对应的 CDN 服务上。

部署服务商授权信息和 dns 服务商授权信息一致，区别在于 dns 服务商授权信息用于证明域名是你的，部署服务商授权信息用于提供证书部署的授权信息。

## 使用

![Alt text](usage.gif)

## 许可证

Certimate 采用 MIT 许可证，详情请查看 [LICENSE](LICENSE.md) 文件。