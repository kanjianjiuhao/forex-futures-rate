# 外盘涨跌统计（网页版）

把原本跑在本机的外盘涨跌统计工具搬到云端：GitHub Actions 定时抓数据 → 存成 data.json → GitHub Pages 网页展示。手机、电脑打开网页即可看。

## 文件说明

| 文件 | 作用 |
|---|---|
| `fetch.py` | 抓数据：东财+新浪双源拉 24 个品种，算涨跌幅，写 `data.json` |
| `.github/workflows/fetch.yml` | 定时任务：北京时间 8:50 / 12:50 / 16:50 / 20:50 各跑一次 |
| `index.html` | 展示页：读 `data.json` 渲染表格，每 60 秒自动刷新 |
| `data.json` | 数据文件（首次运行后自动生成） |

## 部署步骤（一次性，约 5 分钟）

1. 登录 GitHub → 右上角 `+` → **New repository**
   - 仓库名随意（如 `wai-pan`），**必须选 Public（公开）**
   - 不要勾选初始化 README
2. 创建后，把本目录里这几个文件上传进去：
   - `fetch.py`、`index.html`
   - `.github/workflows/fetch.yml`（注意保留 `.github/workflows/` 这层目录结构）
3. 开 Pages：仓库 → **Settings → Pages**
   - Source 选 `Deploy from a branch`，分支选 `main`，目录选 `/ (root)`，保存
   - 等约 1 分钟，页面会显示你的网址：`https://<用户名>.github.io/<仓库名>/`
4. 首次跑数据：仓库 → **Actions** 标签页 → 左侧 `fetch` → **Run workflow** → 确认
   - 等它跑完（绿色 ✓），刷新你的网页网址，就能看到表格了

## 日常使用

- 网页数据由定时任务每天 4 次自动刷新（8:50 / 12:50 / 16:50 / 20:50）
- 想看最新：仓库 → Actions → `fetch` → **Run workflow** → 跑完刷新网页（约 1 分钟）

## 说明

- 定时任务每次只跑约 1 分钟，公开仓库不限额度，不用担心资源限制
- 数据来自东财+新浪公开接口，可能有延迟或缺失（缺失显示「—」，※ 表示双源偏差 >0.5%）
- 不构成投资建议
