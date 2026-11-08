# 更新记录

本项目按[语义化版本](https://semver.org/lang/zh-CN/)的思路管理版本。发布时应同步更新用户脚本元数据 `@version`、内部 `SCRIPT_VERSION`、面板页脚文本三处版本号——当前快照**三者并不一致**，详见下方已知问题。

早期开发记录不完整，以下从本次开源快照开始整理。本仓库是 **3.0.2 的独立快照**，与后续 3.4.x 系列不是同一条发布线。

## [3.0.2] - 2026-11-08（开源快照）

### 文档

- 首次整理 GitHub 开源说明：README、配置项参考、权限与第三方请求清单、隐私提示、安全政策、贡献指南、行为准则、Issue / PR 模板。
- 补充 MIT 许可证文件，并标注上游「超星满分助手」的衍生作品授权风险。
- 补充发布前检查清单（仓库链接、`@license` / `@homepage`、Raw 安装地址等占位项）。

### 本快照包含的功能（相对 3.0.1 的既有改动）

- 新增 `video.video-player`、`.video-container video` 等视频选择器。
- 章节目录改用海旗课程页实际的 `.section-item`，当前节按 `.active` 定位；无法定位当前节时只等待，不再回退点击第一节造成循环重播。
- 切换下一节时跳过 `.locked` / `.lock-icon` / `.unlock-time` 的锁定章节，并给出「后续章节处于锁定状态」提示。
- 切换前 `scrollIntoView`，并提示「已切换下一节，等待视频加载」。
- 版本号由 3.0.1 更新为 3.0.2（仅元数据与面板文本，内部常量未同步）。

### 已知问题（本次未修改代码，仅如实记录）

- `@version` 为 `3.0.2`、面板显示 `v3.0.2`，但内部 `SCRIPT_VERSION` 仍为 `3.0.0`；题库请求头 `v` 与 `<html data-manfen-initialized>` 发送的也是 `3.0.0`。
- 源码注释声称题库接口「全部 https」，但一之题库 `http://cx.icodef.com/wyn-nb?v=4` 仍为明文 HTTP。
- `debugger`、`notice`、`questionType`、`removeHtml`、`cl`、`_GM_info` 为未使用的死代码；`debugger` 开关实际无法启用。
- `minAccuracy` 在设置界面缺少数值校验；防回拽的原型改写安装后不还原。
- 题库返回内容以 `innerHTML` 渲染，未转义；详见 SECURITY.md。
- 无总开关、无验证码处理、无控制台诊断命令、无日志持久化、无 iframe 支持、无自动更新。

---

## 发布新版本时的检查项

1. 同步 `@version`、`SCRIPT_VERSION`、面板 `v3.x.x` 三处。
2. 更新 README 的「默认行为」「已知限制」「发布前检查清单」。
3. 若新增 `@match` / `@connect` / `@require` / `@grant`，同步更新 README 权限说明与安全政策。
4. 运行 `node --check ycust_manfen_haiqikeji.user.js`。
5. 在匹配页面验证视频、切换、答题、提交、面板与日志路径。
6. 确认提交内容不含真实题库令牌、Cookie 或个人课程数据。
