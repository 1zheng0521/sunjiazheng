---
name: github-commit-push
description: '提交并推送当前项目到 GitHub。用户要求 git commit、push、发布本项目到 GitHub，或指定 GitHub 仓库时使用。'
---

# 提交并推送项目到 GitHub

将用户要求的项目更改安全地提交，并推送到指定的 GitHub 仓库。

## 执行步骤

1. 在项目根目录确认 Git 仓库、当前分支、工作区状态、远程地址和最近提交：

   ```sh
   git rev-parse --is-inside-work-tree
   git status --short
   git branch --show-current
   git remote -v
   git log -1 --oneline
   ```

2. 检查待提交的改动，确认提交范围符合用户要求。不要覆盖或丢弃用户改动；提交整个项目时，检查新文件是否属于项目内容，并留意凭证、密钥、本机配置和调试日志等不应公开的内容。

3. 确认目标仓库和分支。若用户指定仓库，使用其准确地址；不要仅为推送而擅自修改现有 remote。若目标不明确，先询问用户。提交前检查本地提交历史及远端状态。

4. 按用户要求暂存文件；提交整个项目时可使用：

   ```sh
   git add -A
   git status --short
   git diff --cached --check
   ```

   提交前再次核对暂存内容。提交说明简短、准确；没有用户指定时，根据实际改动拟定。

5. 创建提交并核实结果：

   ```sh
   git commit -m "<提交说明>"
   git status --short
   git log -1 --oneline
   ```

6. 推送到已确认的远端和分支：

   ```sh
   git push <remote> HEAD:<目标分支>
   ```

   首次推送且需要设置上游时，可使用 `git push -u <remote> HEAD:<目标分支>`。

7. 核实推送结果并向用户汇报提交哈希、目标仓库和分支。遇到认证、网络或证书错误时如实说明；不要在日志或代码中记录凭证，不要关闭 TLS 校验。若推送因远端存在未包含的提交而被拒绝，不要强制推送；先检查差异，再与用户确认如何整合。
