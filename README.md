# Dev Container

这是 taicode-labs 组织的基础开发容器镜像，提供统一的开发环境。

## 镜像特性

- **基础系统**: Ubuntu 22.04
- **默认 Shell**: Zsh + Oh My Zsh
- **开发工具**:
  - Git
  - Curl
  - NVM (Node Version Manager)
  - Node.js 22 (默认版本)

## 使用方法

### 拉取镜像

```bash
docker pull ghcr.io/taicode-labs/dev-container:latest
```

### 运行容器

```bash
docker run -it --rm \
  -v $(pwd):/workspace \
  -v ~/.ssh:/root/.ssh:ro \
  ghcr.io/taicode-labs/dev-container:latest
```

### 使用特定版本

```bash
docker pull ghcr.io/taicode-labs/dev-container:v1.0.0
```

## 开发说明

### 本地构建

```bash
docker build -t dev-container .
```

### 本地测试

```bash
docker run -it --rm -v $(pwd):/workspace dev-container
```

## 发布流程

1. 创建新的 Git tag（例如：`v1.0.0`）
2. 推送 tag 到 GitHub
3. 创建 GitHub Release
4. GitHub Actions 会自动构建并推送镜像到 GitHub Container Registry

```bash
git tag v1.0.0
git push origin v1.0.0
```

## 镜像版本说明

- `latest`: 最新稳定版本
- `vX.Y.Z`: 特定版本标签
- `main`: 主分支最新构建（开发版本）

## 许可证

MIT License
