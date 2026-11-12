# Temperature & Top P 联动可视化

纯 HTML / CSS / JavaScript 的交互可视化，无框架、无需 npm 安装。

## 功能

- 双模块纵向排布：Temperature 调整概率分布，Top P 限制候选范围。
- Temperature 改变时，Top P 条形图和“参与 / 排除”状态同步更新。
- Top P 改变时，重新计算候选集合，Temperature 概率分布保持当前值。
- Temperature 进度条全部为紫色 `#AAA4ED`。
- Top P 参与项为紫色 `#AAA4ED`，排除项为荧光色 `#EFFF83`。
- 两个滑块的圆形按钮均为紫色 `#AAA4ED`。
- 页面最大宽度 **900px**，居中且响应式；其余样式保持简洁。

## 文件

- `site/index.html`：完整网页（HTML、CSS、JavaScript 一体）。
- `.github/workflows/deploy.yml`：GitHub Pages 自动发布工作流。

## 本地预览

在项目根目录运行：

```bash
python3 -m http.server 8000 --directory site
```

浏览器打开 <http://localhost:8000>。

## GitHub Pages 发布

1. 将此项目提交到 GitHub 仓库的 `main` 分支。
2. 在仓库 **Settings → Pages → Build and deployment → Source** 中选择 **GitHub Actions**。
3. 推送 `main` 或从 **Actions → Deploy static site to GitHub Pages** 手动触发。
4. 发布成功后，到 **Settings → Pages** 查看访问地址。

提示：若 GitHub Pages 尚未启用，首次运行可能需要在 Settings 中开启；仓库和组织策略可能影响公开可见性。

## 算法解释

用五个示例词的初始概率 `[0.45, 0.30, 0.15, 0.07, 0.03]`。

温度调整：`p_i(T) = p_i^(1/T) / sum(p_j^(1/T))`。

Top P：按温度调整后的概率降序累加，保留达到阈值的最小集合。为教学可视化，不代表具体模型真实 Token 分布；这里将汉语词语视作示例项。
