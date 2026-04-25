## Snell 协议

Snell 协议是由 Surge 团队设计的一种轻量级、高效的加密代理协议，专注于提供安全、快速的网络传输服务。该协议通过简洁的设计和强大的加密技术提供高性能的网络服务。

### Snell v4 vs v5 对比

| 特性                | Snell v4 | Snell v5 |
|---------------------|----------|----------|
| 状态                | 稳定版   | 最新版   |
| 安全性              | ✅       | ✅       |
| QUIC Proxy          | ❌       | ✅       |
| Dynamic Record Sizing | ❌    | ✅       |
| 出口控制            | ❌       | ✅       |

### ShadowTLS

ShadowTLS 是一个轻量级的 TLS 伪装工具，能够有效规避 TLS 指纹检测。它通过模拟正常的 HTTPS 流量，提供更好的隐私保护和连接稳定性。

---

## 安装指南

### Snell 安装脚本

脚本提供跨平台安装支持，自动判断系统类型并完成配置。

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/anpplex/snell.sh/main/install.sh)"
```

### 多功能管理菜单（仅支持 Debian/Ubuntu）

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/anpplex/snell.sh/main/menu.sh)
```

### 按系统选择的安装方式

#### Debian/Ubuntu
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/anpplex/snell.sh/main/snell-debian.sh)
```

#### CentOS
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/anpplex/snell.sh/main/snell-centos.sh)
```

#### Alpine（推荐使用 Docker 安装）

##### 使用 Docker
```bash
docker run -d --name snell-server \
  --restart unless-stopped \
  --network host \
  -e SNELL_PORT=6160 \
  -e SNELL_PSK=your_psk \
  -e SNELL_VER=v5 \
  anpplex/snell-server:latest
```

##### 使用 Docker Compose
```yaml
services:
  snell:
    image: anpplex/snell-server:latest
    container_name: snell-server
    restart: unless-stopped
    network_mode: host
    environment:
      - SNELL_PORT=6160
      - SNELL_PSK=your_psk   # 自定义密钥
      - SNELL_VER=v5
    volumes:
      - ./snell-config:/etc/snell
```

##### 本地构建镜像
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/anpplex/snell.sh/main/snell-docker.sh)"
```

---

## 配置指南

以下是部分参考配置：

### Snell v4 配置示例
```bash
HK = snell, 1.2.3.4, 57891, psk = xxxxxxxxxxxx, version = 4, reuse = true, tfo = true
HK = snell, ::1, 57891, psk = xxxxxxxxxxxx, version = 4, reuse = true, tfo = true
```

### Snell v5 配置示例
```bash
HK = snell, 1.2.3.4, 57891, psk = xxxxxxxxxxxx, version = 5, reuse = true, tfo = true
HK = snell, ::1, 57891, psk = xxxxxxxxxxxx, version = 5, reuse = true, tfo = true
```

---