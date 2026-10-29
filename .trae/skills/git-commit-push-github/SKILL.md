---
name: git-commit-push-github
description: 将本仓库提交并推送到 GitHub 远程仓库 https://github.com/ghz-666-ddd/highweb.git（分支 master）。用户说“提交到 GitHub”“push 到 github”“上传到 GitHub 仓库”时使用；只处理正常提交与推送，不做分支改造、不改 git config、不 force push。
---

# GitHub 提交推送流程（本仓库）

本仓库是「高级网页设计」课程练习的 git 仓库，GitHub 远程为
`git@github.com:ghz-666-ddd/highweb.git`（分支 `master`）。

Gitee 远程 `origin`（`https://gitee.com/gaohaozhe/ghz.git`）保持不变，GitHub 使用独立的
远程名 `github`，避免覆盖既有配置。

## 本机已确认的网络与认证条件

- `github.com:443`（HTTPS）在本机超时不可用，**不要用 https 地址推送**。
- `github.com:22` 也会被拦截，SSH 需走 **443 端口**：`ssh.github.com`。
- 已在本机 `~/.ssh/config` 配好：

```text
Host github.com
  HostName ssh.github.com
  User git
  Port 443
  IdentityFile ~/.ssh/id_ed25519_gitee
  IdentitiesOnly yes
```

- 能通过认证的私钥是 `~/.ssh/id_ed25519_gitee`（`id_rsa` 未被 GitHub 接受）。
- 可用 `ssh -T git@github.com` 自检，出现 `Hi ghz-666-ddd!` 即认证正常。

## 前置检查

1. 先把本次提示词追加到 `gaohaozhe_prompt.md` 末尾（时间、模型、提示词原文），只追加不覆盖。
2. 运行 `git status`、`git log --oneline -5`、`git remote -v` 了解现状。
3. 确认 GitHub 远程地址为 SSH 形式：

```powershell
git remote get-url github
```

若报 “No such remote”，则添加（已存在则跳过，不要重复 add）：

```powershell
git remote add github git@github.com:ghz-666-ddd/highweb.git
```

## 提交步骤

1. 只 add 本次相关文件（如 `15-1.html`、`index.html`、`gaohaozhe_prompt.md`），不要 `git add -A`
   把临时文件、截图、缓存一起提交。
2. `.trae/`、`.opencode/` 已在 `.gitignore` 中；若要提交其中的 skill 文件，需显式
   `git add -f .trae/skills/<skill名>/SKILL.md`。
3. 提交信息用中文、简短一行，贴合仓库风格，例如：
   - `新增 15-1.html 数 7 规则盒子页面`
   - `新增 GitHub 推送 skill`
4. 仓库已有的提交信息无统一前缀，不需要加 emoji 或英文前缀。
5. 只在用户明确要求时才 commit / push；不 amend、不 force push、不改 git config。

## 推送

```powershell
git push github master
```

- 首次推送可用 `git push -u github master` 建立对 `github/master` 的跟踪，之后直接 `git push github`。
- 若 GitHub 仓库已有内容，先 `git fetch github` 查看，失败时不要强行 force push。
- 推送失败先看报错：
  - `Permission denied (publickey)` → 检查 `~/.ssh/config` 的 Host github.com 是否走 443 与
    `id_ed25519_gitee`，并用 `ssh -T git@github.com` 自检。
  - `Failed to connect to github.com port 443` → 说明用成了 HTTPS 地址，改回 SSH 地址。
  - `non-fast-forward` / `rejected` → 报告冲突，让用户决定，禁止 force push。
  - 无提交 → 先 commit 再推送。

## 验证

- `git status` 显示 working tree clean（或只剩被忽略文件）
- `git log --oneline -3` 显示新提交
- `git remote -v` 同时显示 `origin`（Gitee）与 `github`（GitHub，SSH 地址）
- `git log github/master --oneline -1` 与本地提交一致（推送成功）
