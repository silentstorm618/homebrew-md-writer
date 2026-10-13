# homebrew-tap

MD Writer 的 Homebrew tap 仓库。

## 安装

```bash
brew tap silentstorm618/md-writer
brew install --cask md-writer
```

## 为什么走 Homebrew 而不是直接下载 dmg

MD Writer 目前未加入 Apple Developer Program，产物无法签名公证。
直接下载 dmg 双击会被 Gatekeeper 拦下（提示「已损坏，无法打开」——
文件其实完好，只是没有票据）。

Homebrew 安装时会自动清除 `com.apple.quarantine` 扩展属性，
因此用户装完可以直接打开，无需右键或执行 `xattr` 命令。

等项目完成签名公证后，这个 tap 依然是最省事的升级渠道：

```bash
brew upgrade --cask md-writer
```

## 这个仓库怎么来的

`Casks/md-writer.rb` 里的 `version` 与 `sha256` 由主仓库
（`md-writer`）的 GitHub Actions 在发版时自动改写并推送，
不需要手动维护。

| 字段 | 更新时机 |
| --- | --- |
| `version` | push tag（`v*`）时同步为 tag 版本号 |
| `sha256` | 自动读取新产出的 `.pkg` 摘要 |

需要的 secret：`TAP_GITHUB_TOKEN`（有本仓库写权限的 PAT，`public_repo` 权限即可）。

## 本地校验

```bash
brew audit --cask --strict ./Casks/md-writer.rb
brew style ./Casks/md-writer.rb
```

发布前建议跑一遍 `brew audit`，它会检查 url 可达性、sha256 是否匹配、
cask 结构是否合规。
