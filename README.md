# cn-install

加速部分安装脚本访问，解决 GitHub 访问慢或无法访问的问题。

## opencode-install-mirror.sh

OpenCode 安装脚本的国内加速镜像版本。

原始脚本来源：[https://opencode.ai/install](https://opencode.ai/install)

### 与原版的区别

将所有 GitHub 相关 URL 替换为通过 `g.blfrp.cn` 代理访问：

| 原始地址 | 镜像地址 |
|---------|---------|
| `https://github.com/anomalyco/opencode/...` | `https://g.blfrp.cn/github.com/anomalyco/opencode/...` |
| `https://api.github.com/repos/anomalyco/opencode/...` | `https://g.blfrp.cn/api.github.com/repos/anomalyco/opencode/...` |

共替换 5 处 URL：
1. 最新版下载地址（`releases/latest/download/`）
2. 版本信息 API 地址（`api.github.com/repos/.../releases/latest`）
3. 指定版本下载地址（`releases/download/v.../`）
4. 版本验证地址（`releases/tag/v...`）
5. 可用版本信息地址（`releases`）

### 使用方法

**一键安装（推荐）：**

```bash
curl -fsSL https://g.blfrp.cn/raw.githubusercontent.com/Nikolay-Jiang/cn-install/main/opencode-install-mirror.sh | bash
```

安装指定版本：

```bash
curl -fsSL https://g.blfrp.cn/raw.githubusercontent.com/Nikolay-Jiang/cn-install/main/opencode-install-mirror.sh | bash -s -- --version 1.0.180
```

**本地运行：**

```bash
# 安装最新版
bash opencode-install-mirror.sh

# 安装指定版本
bash opencode-install-mirror.sh --version 1.0.180

# 查看帮助
bash opencode-install-mirror.sh --help
```

### 注意事项

- 此脚本仅替换了 GitHub 访问地址，其他逻辑与原版完全一致
- 代理服务 `g.blfrp.cn` 为第三方提供，可用性取决于代理服务本身
- 如遇代理不可用，可使用原版脚本：`curl -fsSL https://opencode.ai/install | bash`