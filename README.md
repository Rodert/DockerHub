# DockerHub 镜像集中营

![Docker 标志](assets/docker-logo-gallery.png)

Docker Hub 官方地址：[https://hub.docker.com/](https://hub.docker.com/)

GitHub Pages：[https://rodert.github.io/DockerHub/](https://rodert.github.io/DockerHub/)

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

## 各系统详细配置

下面的配置仅用于 Docker Hub 镜像拉取，不会修改镜像名称或容器启动参数。`registry-mirrors` 可以填写一个或多个地址，保存后建议使用 `docker info` 和 `docker pull` 验证。

### Windows（Docker Desktop）

1. 打开 Docker Desktop，点击右上角 **Settings**。
2. 进入 **Docker Engine**，在现有 JSON 中加入 `registry-mirrors` 配置。不要删除原有的其他配置项。
3. 点击 **Apply & Restart**，等待 Docker Desktop 重启完成。
4. 在 PowerShell 中验证：

```powershell
docker info
docker pull nginx:latest
```

Windows Docker Desktop 使用的是内部 Linux 虚拟机，通常不需要手动编辑 Windows 文件。若使用的是 Windows Server 上的 Docker Engine，可编辑 `C:\ProgramData\docker\config\daemon.json`，然后执行：

```powershell
Restart-Service docker
docker info
```

### macOS（Docker Desktop）

1. 打开 Docker Desktop，进入 **Settings** → **Docker Engine**。
2. 将 `registry-mirrors` 合并到右侧 JSON 配置中。
3. 点击 **Apply & Restart**，等待 Docker Desktop 完成重启。
4. 在 Terminal 中验证：

```sh
docker info
docker pull nginx:latest
```

macOS Docker Desktop 同样运行在内部 Linux 虚拟机中，一般不需要直接修改 macOS 本地文件。

### Linux（Docker Engine）

适用于 Ubuntu、Debian、CentOS、Rocky Linux 等使用 systemd 管理 Docker 的系统：

1. 创建 Docker 配置目录：

```sh
sudo mkdir -p /etc/docker
```

2. 编辑 `/etc/docker/daemon.json`，写入以下内容；如果文件已有配置，请合并 JSON 字段，不要重复添加第二个 `registry-mirrors`：

```json
{
  "registry-mirrors": [
    "https://docker.1ms.run",
    "https://dockerproxy.net",
    "https://dockerproxy.link"
  ]
}
```

3. 重新加载配置并重启 Docker：

```sh
sudo systemctl daemon-reload
sudo systemctl restart docker
```

4. 检查镜像地址是否已生效并测试拉取：

```sh
docker info
docker pull nginx:latest
```

如果 Docker 无法启动，先检查 JSON 格式和日志：

```sh
sudo systemctl status docker
sudo journalctl -u docker --no-pager -n 50
```

### Linux Rootless Docker

Rootless 模式不使用 `/etc/docker/daemon.json`，配置文件通常位于 `~/.config/docker/daemon.json`：

```sh
mkdir -p ~/.config/docker
```

写入同样的 `registry-mirrors` 配置后，重启当前用户的 Docker 服务：

```sh
systemctl --user restart docker
docker info
docker pull nginx:latest
```

## 共同维护

欢迎大家提交好用的 Docker 镜像，也欢迎反馈失效地址，共同维护这一生态。我会持续维护并定期更新镜像项目。

由于一些原因，国内访问 Docker 镜像目前存在困难。本仓库将作为 DockerHub 的灯塔持续维护，且用且珍惜。

## 推荐站点

- [ChatGPT 充值站点](https://chatgptopenplus.com/)
- [科学上网工具](https://tinyurl.com/network-saku)
