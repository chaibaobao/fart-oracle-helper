# 屁者先知 · 秘密身份判定器

手机优先的纯静态实体桌游辅助工具。没有后端、依赖、账号、外部字体或遥测。只登记出局阵营并在每轮结束时判定胜负。

## 文件与运行

- `index.html`：入口与隐私说明
- `style.css`：电梯控制面板样式，320px 起适配及减少动画设置
- `script.js`：规则、交互及 localStorage 存档
- `test.cjs`：使用 Node 内置断言的规则测试
- `README.md`：使用与部署指南

可直接打开 index.html 试用；推荐在 HTTP/HTTPS 环境运行以获得稳定的 localStorage 行为。例如本目录执行 `python -m http.server 8080` 后打开 http://localhost:8080。测试执行 `node test.cjs`。

## 使用与隐私

初始化 5–10 人及屁者人数。出局者独自登记，确认提交后清除选择界面。公共页只显示总人数、累计出局及回合，不显示分阵营数据。所有原因的出局都登记；每轮可登记零人或多人，只有点击“结束本轮 · 检查胜负”才判定。第八轮按存活人数判定，平局提示查看实体规则书。双方全出局属于未定义冲突，会要求核实并撤销，而不会编造赢家。

撤销仅限本轮未结算记录，结算后锁定，防止通过反复结算反推身份。重开须二次确认。身份选择不进入 URL 或浏览器历史；刷新、返回及切换应用清除临时选择并遮挡，未提交的选择不保存。保存失败会显示错误且不宣布登记成功。存档损坏不会自动覆盖。

这是界面防窥，不是设备级加密。调试工具可读取本地存档，操作系统截图和应用切换预览也不在网页控制范围内。仅在同一设备同一浏览器单标签使用，勿让其他人查看私密登记错误提示。数据不上传，但 GitHub Pages 正常提供网页资源。清除站点数据会丢失进度。不同协议、浏览器或域名的存档不共享。

## GitHub Pages 部署

仓库：https://github.com/chaibaobao/fart-oracle-helper

源文件位于 main 分支根目录。启用发布：

1. 仓库 Settings → Pages → Build and deployment → Source 选择 Deploy from a branch。
2. Branch 选择 main，文件夹选择 / (root)，点击 Save。
3. 等待 Actions 中 Pages 构建成功，打开 Pages 设置给出的 HTTPS 地址。
4. 预期地址为 https://chaibaobao.github.io/fart-oracle-helper/ 。源代码提交不代表网站已上线，请以 Pages 发布状态为准。
5. 手机 Safari/Chrome 打开链接，确认资源和交互。所有资源使用相对路径。

GitHub 官方操作说明：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

后续可告诉 Codex：“修改 chaibaobao/fart-oracle-helper 的……并提交更新”。授权连接访问该仓库后可继续维护；合并至 main 后 Pages 自动重新发布，无需自定义 Actions。测试后刷新手机页面获取更新。也可将本目录拖入 Netlify 静态站点部署，但正式目标是 GitHub Pages。

## 验证记录与手机验收

已通过 Node 规则测试 A 两名屁者出局、B 两名非屁者出局继续、C 第八轮人数判定/平局、D 无人出局、E 登记不自动结算、G 两阵营超额拒绝，以及序列化恢复、全员出局冲突与撤销计数。语法检查通过。

尚未实机浏览器验证：F 刷新恢复 localStorage；H 返回/刷新/应用切换后不出现上一位身份、撤销/重开/终局保密；320/375/430px 布局与触屏交互；线上资源与 HTTPS。序列化测试不等于浏览器持久化实测。登记两种身份后应得到完全相同的成功界面；重复快速点击不得重复登记；刷新身份选择页不得自动提交；取消重开应保留进度。不得将本地测试结果表述为正式上线或手机实测成功。

## 精简交互更新

公共页只保留登记、结束本轮两个主要按钮，撤销与重开收进“更多操作”。身份选择和确认合并在同一屏，可直接改选；确认后立即遮挡。取消登记直接返回公共页。结束本轮一次点击完成结算，按钮短暂禁用以防双击跳过回合。保留交接遮挡、提交确认及重开确认。旧存档兼容。
