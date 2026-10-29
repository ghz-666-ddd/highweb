# AGENTS.md

## Overview
Student practice repo for a "高级网页设计" (Advanced Web Design) course. Flat collection of standalone HTML/CSS/JS exercise files — no build system, package manager, framework, tests, CI, third-party libraries, or CDN.

## Structure
- `index.html` — hub page linking all exercises; self-contained (inline `<style>`).
- Numbered files (`1.html`, `2-2.html`, `3-1.html`, …) are individual class exercises; the prefix tracks lesson/session number.
- Filenames may contain Chinese characters and spaces (e.g. `5-1 层叠与继承.html`); always quote paths in shell commands.
- `css.css` — tiny shared stylesheet used by some exercises; most pages use inline styles instead.
- `font/` — local iconfont 字体目录，图标样式文件（如 `iconfont.css`）和字体文件（`.woff2` / `.ttf` / `.eot`）存放于此。需要图标时从本地引用，禁止 CDN。
- Newer `11-x` exercises (`11-1.html`, `11-2.html`) are saved in this repo root per user instruction — confirm the target path if a prompt doesn't specify one (an earlier run used `D:\HighInternetDesign\新建文件夹\`).

## Conventions
- All pages: `<!DOCTYPE html>`, `<html lang="zh-CN">`, UTF-8 charset, Chinese UI text.
- Header comment (required): every `.html` file must include a comment immediately after `<!DOCTYPE html>` in this exact shape:
  ```html
  <!-- 姓名：高浩哲，日期：YYYY-MM-DD，功能：一句话说明本页用途 -->
  ```
- Naming (required): all CSS class names, IDs, JS variables, and CSS custom properties (`--*`) start with `ghz_` (e.g. `.ghz_card`, `#ghz_nav`, `ghz_count`, `--ghz_bg`). No bare generic names like `.container`, `.card`, `.header`. Legacy names from earlier rules (`gaohaozhe_`, `lvmohan_`, `yuan_`, `yl_`) must be renamed to `ghz_` whenever a file is touched.
- Tech stack (required): only native HTML / CSS / JavaScript allowed. **禁止**任何第三方库、框架、CDN 引入（包括但不限于 jQuery、Bootstrap、Vue/React、Tailwind、Font Awesome、unpkg、jsdelivr 等）。
- Icons (required): 需要图标时，优先使用 `font/iconfont.css` 中的本地 iconfont 类名（写法 `<i class="iconfont icon-xxx"></i>`）。只有 `font/` 目录不存在 iconfont 时才使用纯 CSS / emoji / SVG 内联替代，临时方案也要注明"待接入 iconfont"。绝对禁止在线字体 CDN 或图标库 CDN。
- Styling is mostly inline `<style>` blocks per page; prefer that pattern when adding or editing an exercise.
- Visual style (see `index.html`): CSS custom properties on `:root`, rounded cards, gradient backgrounds, `"Microsoft YaHei"` font stack.
- Keep pages self-contained so each file opens directly in a browser via file:// — no dev server needed.
- New HTML files (required): after creating a page, add a hyperlinked card for it in the `index.html` `.yl_grid` section, following the existing pattern (`<a class="yl_card" href="./文件名.html"><span class="yl_tag">作品 N</span><h3>文件名</h3><p>中文简介</p></a>`); keep card order by lesson number.

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
- `font/` 目录当前为空。要使用 iconfont 时先把 `iconfont.css` 和对应的 `.woff2` / `.ttf` / `.eot` 字体文件放进去，再在 HTML `<head>` 里用 `<link rel="stylesheet" href="./font/iconfont.css">` 引入。临时没放的话用 CSS/emoji 凑，但要写"待接入 iconfont"注释。
- 任何页面**不得**出现 `cdn.jsdelivr.net`、`unpkg.com`、`code.jquery.com`、`cdnjs.cloudflare.com` 等 CDN 域名，也不得 `<script src="...">` / `<link href="...">` 引用第三方资源。
