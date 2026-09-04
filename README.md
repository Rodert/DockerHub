# DockerHub

![Docker Hub 首页](assets/docker-hub-homepage.png)

Docker Hub 官方地址：[https://hub.docker.com/](https://hub.docker.com/)

2026 年 9 月 Docker 国内可用资源整理：Docker 工具下载与 Docker Hub 镜像地址。

## 菜单

- [Docker 工具下载](#docker-工具下载)
- [Docker 镜像](#docker-镜像)

## Docker 工具下载

仅收录官方提供、可免费使用的 Docker 工具与文档。

| 工具 | 适用系统 | 下载或安装说明 |
| --- | --- | --- |
| Docker Engine | Linux | [官方安装文档](https://docs.docker.com/engine/install/) |
| Docker Compose Plugin | Linux | [官方安装文档](https://docs.docker.com/compose/install/linux/) |
| Docker CLI 静态二进制包 | Linux | [官方下载说明](https://docs.docker.com/engine/install/binaries/) |

## Docker 镜像

以下为可用于拉取 Docker Hub 镜像的公共地址。已排除付费、推广、内网限定、需令牌或已失效的服务；地址会随网络环境变化，请优先选择可用项并合理使用。

| 服务 | 镜像地址 | 使用示例 |
| --- | --- | --- |
| 1Panel 镜像 | `docker.1panel.live` | `docker pull docker.1panel.live/library/nginx:latest` |
| 毫秒镜像 | `docker.1ms.run` | `docker pull docker.1ms.run/library/nginx:latest` |
| Docker Proxy | `dockerproxy.net` | `docker pull dockerproxy.net/library/nginx:latest` |
| Docker Proxy | `dockerproxy.link` | `docker pull dockerproxy.link/library/nginx:latest` |
| DaoCloud 公共镜像 | `docker.m.daocloud.io` | `docker pull docker.m.daocloud.io/library/nginx:latest` |
| 简行镜像 | `docker.jiaxin.site` | `docker pull docker.jiaxin.site/library/nginx:latest` |

> 官方镜像需要带上 `library` 命名空间，例如 `library/nginx`；个人或组织镜像则使用实际命名空间，例如 `username/image:tag`。

### 配置示例

Linux 上可创建或编辑 `/etc/docker/daemon.json`，填入一个或多个镜像地址：

```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://dockerproxy.net",
    "https://dockerproxy.link"
  ]
}
```

保存后重启 Docker：

```sh
sudo systemctl daemon-reload
sudo systemctl restart docker
```

使用以下命令验证拉取是否正常：

```sh
docker pull nginx:latest
```

### Windows 与 macOS 配置

Windows 和 macOS 使用 Docker Desktop 时，打开 **Settings**，进入 **Docker Engine**，将上述 JSON 合并到配置中，点击 **Apply & Restart** 保存并重启 Docker。完成后同样可执行以下命令验证：

```sh
docker pull nginx:latest
```

## 共同维护

欢迎大家提交好用的 Docker 镜像，也欢迎反馈失效地址，共同维护这一生态。我会持续维护并定期更新镜像项目。

由于一些原因，国内访问 Docker 镜像目前存在困难。本仓库将作为 DockerHub 的灯塔持续维护，且用且珍惜。

## 推荐

以下内容为本站推荐，后续可能会补充其他推荐站点。

- [ChatGPT 充值站点](https://chatgptopenplus.com/)
