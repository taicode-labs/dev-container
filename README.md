# Dev Container

这是 taicode-labs 组织的基础开发容器镜像，提供统一的开发环境。

## 主要用途

- **本地开发环境**: 配合 VS Code Dev Containers 插件使用，提供一致的开发环境
- **CI/CD 加速**: 预装常用工具和依赖，大幅减少 GitHub Actions 的构建时间和费用
- **团队协作**: 确保所有开发者使用相同的工具链版本，避免"在我机器上可以运行"的问题

## 镜像特性

- **基础系统**: Ubuntu 22.04
- **默认 Shell**: Zsh + Oh My Zsh
- **开发工具**:
  - Git
  - Curl
  - NVM (Node Version Manager)
  - Node.js 22 (默认版本)

## 使用方法

### 在项目中使用 Dev Container

在你的项目根目录创建 `.devcontainer/devcontainer.json`：

```json
{
  "name": "项目名称",
  "image": "ghcr.io/taicode-labs/dev-container:latest",
  "customizations": {
    "vscode": {
      "extensions": [
        "dbaeumer.vscode-eslint",
        "esbenp.prettier-vscode"
      ]
    }
  },
  "forwardPorts": [3000, 8080],
  "postCreateCommand": "npm install",
  "remoteUser": "root"
}
```

然后在 VS Code 中：

1. 安装 "Dev Containers" 插件
2. 按 `F1` 或 `Ctrl+Shift+P`
3. 选择 "Dev Containers: Reopen in Container"

### 直接使用 Docker 运行

拉取镜像：

```bash
docker pull ghcr.io/taicode-labs/dev-container:latest
```

运行容器：

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

## 在 CI/CD 中使用

### GitHub Actions 示例

使用此镜像可以显著减少 Actions 运行时间，因为无需每次都安装 Node.js、工具等依赖。

```yaml
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/taicode-labs/dev-container:latest
      credentials:
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Install dependencies
        run: npm install
      
      - name: Run tests
        run: npm test
      
      - name: Build
        run: npm run build
```

### 节省时间对比

- **不使用预构建镜像**: 每次 CI 运行需要 2-3 分钟安装 Node.js、工具等
- **使用此镜像**: 直接开始执行任务，节省 2-3 分钟/次

对于频繁运行的 CI/CD 流程，可以显著降低 GitHub Actions 使用时长和费用。

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
