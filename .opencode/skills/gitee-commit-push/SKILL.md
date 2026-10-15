---
name: gitee-commit-push
description: 提交项目到 Gitee。当用户要求"提交项目"、"push 到 Gitee"、"推送到码云"或提到仓库 https://gitee.com/sun-housekeeping/1001sjz 时使用。执行 git add、commit 并 push 到指定远程仓库。
---

# 提交项目到 Gitee

将当前项目使用 git commit 提交，并 push 到远程仓库 `https://gitee.com/sun-housekeeping/1001sjz`。

## 执行步骤

1. **检查是否为 git 仓库**（在项目根目录执行）：

   ```
   git rev-parse --is-inside-work-tree
   ```

   如果不是仓库，先初始化：

   ```
   git init
   ```

2. **检查并设置远程仓库**：

   ```
   git remote -v
   ```

   - 如果没有 remote，添加：

     ```
     git remote add origin https://gitee.com/sun-housekeeping/1001sjz.git
     ```

   - 如果已有 remote 但 URL 不是 `https://gitee.com/sun-housekeeping/1001sjz.git`，先告知用户确认，再执行：

     ```
     git remote set-url origin https://gitee.com/sun-housekeeping/1001sjz.git
     ```

3. **暂存所有更改**：

   ```
   git add -A
   ```

4. **检查是否有更改可提交**：

   ```
   git status
   ```

   - 若无更改（nothing to commit），跳到第 6 步直接尝试 push。
   - 若用户在调用时提供了提交信息，使用该信息；否则根据本次改动内容生成一句简洁的中文提交信息（例如：`更新页面样式`、`新增 8-1 练习页面`）。

5. **提交**：

   ```
   git commit -m "<提交信息>"
   ```

6. **确认默认分支名并推送**：

   ```
   git branch --show-current
   ```

   - 若没有分支（新仓库首次提交后可能仍在 master/main 的裸状态），使用：

     ```
     git push -u origin HEAD
     ```

   - 若有分支（如 `master` 或 `main`）：

     ```
     git push -u origin master
     ```

     （将 `master` 替换为实际分支名。）

## 注意事项

- push 使用 HTTPS，首次推送或凭证过期时可能提示输入 Gitee 用户名和密码（或私人令牌）。如果命令因认证失败而卡住或报错，告知用户需要在终端手动完成认证，不要在日志或代码中记录任何密码/令牌。
- 若 push 被拒绝（远程已有提交），不要使用 `--force`；先执行 `git pull --rebase origin <分支名>`，解决冲突后（如有冲突，向用户询问）再重新 push。
- 全部命令都在当前项目根目录（工作目录）下执行，不要切换目录。
