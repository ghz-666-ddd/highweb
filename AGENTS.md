# AGENTS.md

## Overview
Student practice repo for a "高级网页设计" (Advanced Web Design) course. Flat collection of standalone HTML/CSS exercise files — no build system, package manager, framework, tests, or CI.

## Structure
- `index.html` — hub page linking all exercises; self-contained (inline `<style>`).
- Numbered files (`1.html`, `2-2.html`, `3-1.html`, …) are individual class exercises; the prefix tracks lesson/session number.
- Filenames may contain Chinese characters and spaces (e.g. `5-1 层叠与继承.html`); always quote paths in shell commands.
- `css.css` — tiny shared stylesheet used by some exercises; most pages use inline styles instead.
- Newer `11-x` exercises (`11-1.html`, `11-2.html`) are saved in this repo root per user instruction — confirm the target path if a prompt doesn't specify one (an earlier run used `D:\HighInternetDesign\新建文件夹\`).

## Conventions
- All pages: `<!DOCTYPE html>`, `<html lang="zh-CN">`, UTF-8 charset, Chinese UI text.
- Naming (required): all CSS class names, IDs, and JS variables start with `gaohaozhe_` (e.g. `.gaohaozhe_card`, `#gaohaozhe_nav`, `gaohaozhe_count`). Existing exercise files predate this rule — apply the prefix whenever you add or edit such names, and keep renames consistent within a file. (Earlier rules used `yuan_` / `lvmohan_`; treat those names in old logs/files as legacy.)
- Styling is mostly inline `<style>` blocks per page; prefer that pattern when adding or editing an exercise.
- Visual style (see `index.html`): CSS custom properties on `:root`, rounded cards, gradient backgrounds, `"Microsoft YaHei"` font stack.
- Keep pages self-contained so each file opens directly in a browser via file:// — no dev server needed.
- New HTML files (required): after creating a page, add a hyperlinked card for it in the `index.html` `.grid` section, following the existing pattern (`<a class="card" href="./文件名.html"><span class="tag">作品 N</span><h3>文件名</h3><p>中文简介</p></a>`); keep card order by lesson number.

## Commands
- No install/build/test/lint commands exist. Open any `.html` file in a browser to verify.
- If adding tooling later, prefer zero-dependency approaches (plain HTML/CSS) to match the repo's scope.

## Prompt logging (required)
- Before executing any user prompt, append an entry to `gaohaozhe_prompt.md` — never rewrite or truncate that file.
- Each entry contains: timestamp, model used (e.g. `opencode/mimo-v2.6-flash-free`), and the verbatim prompt text.
- Log the prompt first, then do the work; this applies to every session.
- `yuan_prompt.md` / `lvmohan_prompt.md` are legacy logs from earlier naming rules — leave them intact.

## Gotchas
- No lockfile, README, or CI — do not assume npm/Node tooling is available.
- Do not restructure or rename existing exercise files; the index page and course numbering depend on exact filenames.
