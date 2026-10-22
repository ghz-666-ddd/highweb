---
name: git-commit-push
description: Handle git add commit push flow for this repo and push to Gitee remote. Use when the user asks to commit, push, 提交项目, git commit, or push 到 gitee. Do not use for branches other than master or remote setup unrelated to this repo.
---

# Git 提交推送流程（本仓库）

本仓库是「高级网页设计」课程练习的 git 仓库，远程仓库为
`https://gitee.com/gaohaozhe/ghz.git`（分支 `master`）。

## 前置检查

1. 先追加提示词日志（若本条提示词尚未记录）：向 `gaohaozhe_prompt.md` 末尾追加时间、模型、提示词原文，绝不覆盖。
2. 运行 `git status`、`git log --oneline -10`、`git remote -v` 了解现状。
   - 若 `git log` 报 "does not have any commits yet"，说明是首次提交，直接 `git add -A`。
   - 若 `git remote -v` 为空，添加远程：`git remote add origin https://gitee.com/gaohaozhe/ghz.git`

## 提交步骤

1. `git add -A`（或只 add 相关文件；不要提交无关的临时文件）
2. 提交信息用中文、简短一行，贴合仓库风格，例如：
   - `新增 11-2.html 3D 动画练习`
   - `更新 index.html 卡片链接`
3. 仅在用户明确要求时才 commit/push；不要 amend、不要 force push、不要改 git config。

## 推送

```powershell
git push -u origin master
```

- HTTPS 推送需要 Gitee 凭据；Windows 上通常由 Git Credential Manager 弹窗提示输入用户名/密码（用 Gitee 的私人令牌/密码）。
- 推送失败时先看报错：认证失败 → 提示用户配置凭据；`remote origin already exists` → 不要重复 add；无提交 → 先 commit。
- 首次推送成功后记录远程分支已建立，之后用 `git push` 即可。

## 验证

- `git status` 显示 working tree clean
- `git log --oneline -3` 显示提交
- `git remote -v` 显示 origin 指向 gitee 仓库
