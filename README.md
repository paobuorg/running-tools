# 跑地图 · 跑步工具

[English](README.en.md) · 中文

本仓库保存 `tools.paobu.org` 使用的工具说明、输入输出契约、公式假设、来源与算例。它是纯内容仓库，不包含站点组件、浏览器计算代码、`package.json`、`node_modules` 或构建产物；工具实现位于 `site-tools`。

## 当前状态

- 八项工具：配速、分段、跑走结合、比赛预测、轨迹查看、格式转换、轨迹简化、路线参数比较，每项都有中文与英文说明。
- 八项工具已于 2026-10-27 完成 **AI 辅助编辑审阅**并发布（`published`，每项双语 `approve` 记录与匹配 digest）。审阅者是 `runmap-editorial`，明确标注为 AI 辅助，不是独立专业审阅；真实设备性能仍待验证。
- 二十个独立算例保存在 `data/cases/`，覆盖三种配速模式、负分段、跑走截断、Riegel 预测、轨迹高程与简化偏移等边界。
- 唯一作者/审阅身份是 `runmap-editorial`：「RunMap editorial desk (AI-assisted draft and review)」，没有个人资质声明；审阅记录为 AI 辅助编辑审阅，不是专业审阅。
- 项目没有远程仓库、公开 Issue 地址或已部署网站。

## 工具与口径

| 工具 | 版本 | 口径摘要 |
|---|---|---|
| 配速 `pace` | 1.1.0 | 距离-时间、距离-配速、时间-配速三种模式；支持公里与英里；恰好两个正数输入 |
| 分段 `splits` | 1.1.0 | 等配速或负分段；默认前后半程差 2%，限制 0–10%；秒数按最大余数法分配，总和必须等于输入总时间 |
| 跑走结合 `run-walk` | 1.0.0 | 按循环数或总时长排程；总时长模式在边界截断并标记；总时长上限 7 天，循环模式上限 1000 个循环 |
| 比赛预测 `race-predict` | 1.0.0 | Riegel 公式，指数固定 1.06；已知与目标距离限制在 5000–42195 米；不用于越野或超马 |
| 轨迹查看 `track-view` | 1.0.0 | GPX 或 GeoJSON 线几何；WGS84 测地距离；高程不足时报告未知，不以 0 补齐 |
| 格式转换 `track-convert` | 1.0.0 | GPX 与 GeoJSON 互换；只接受线几何；移除时间、设备与人员元数据 |
| 轨迹简化 `track-simplify` | 1.0.0 | 逐段 Ramer–Douglas–Peucker；容差 1–100 米；各段不连接，保留首尾点与原始坐标 |
| 路线参数比较 `route-compare` | 1.0.0 | 仅比较 2–4 条已发布路线；逐字段展示距离、爬升口径、路面与技术性；缺失即未知，不做排名 |

公式的完整描述、限制与舍入规则保存在各 `data/entities/{slug}.json` 的 `formulaDescription`、`assumptions` 与 `rounding` 字段；正文只解释用途和限制。规范版本随实体记录，修改计算口径必须提升 `specVersion` 并同步算例。

## 目录

```text
data/entities/{slug}.json          工具契约、公式说明、假设、舍入与来源引用
data/cases/{caseId}.json           独立算例：输入、期望输出与边界说明
data/sources/{sourceId}.json       标准、论文与公共指南来源
data/contributors/{personId}.json  公开作者与审阅者身份
data/reviews/{slug}.{locale}.json  通过审阅后记录内容摘要与决定
content/zh-CN/{slug}.md            中文说明与 frontmatter
content/en/{slug}.md               英文说明与 frontmatter
assets/                            可复用的小型素材
```

实体 ID 形如 `tool:pace`，slug 使用小写英文短横线。中英文通过 `entityId` 配对，计算规范只保存在 `data/entities/` 一处。正文不使用 MDX、内联脚本或动态 import。

## 浏览器端边界

实现位于 `site-tools`，按以下边界运行：

- 轨迹文件在浏览器本地读取，不上传、不写入分析日志，也不进入仓库。
- 单文件最多 20,000,000 字节、200,000 个坐标点；超限直接拒绝，不截断后继续。
- 解析与几何计算在 Worker 中执行；超过 10 秒显示可取消提示，超过 30 秒终止，不提供不完整下载。
- 拒绝 DTD、外部实体、非线几何、无效坐标与非有限数值。
- 轨迹距离是 WGS84 测地距离，属于信息性结果，不是经认证的赛道丈量。
- 转换会重新序列化几何，输出不会与原文件逐字节相同；缺少高程时保持缺失。
- 简化容差在局部投影平面内计算，与输出的 WGS84 距离变化分开报告。

## 本地使用

内容由 `site-tools` 构建时读取。六个工程位于同一父目录时路径自动解析；也可用 `TOOLS_CONTENT_DIR` 覆盖，或用 `PAOBU_REPOS_DIR` 指定父目录。本仓库没有安装或构建命令。

构建会校验双语配对、工具契约、算例引用、来源、许可、审阅日期与内容摘要。搜索索引由网站构建生成，不是第二份说明。

## 许可与纠错

- 新写说明与算例：CC BY 4.0，署名「跑地图 RunMap」。
- 引用的标准、论文与指南保留各自权利，只按来源条件引用。
- 网站代码：MIT，位于三个 `site-*` 仓库。

托管仓库建立后，请通过 Issue 或 Pull Request 指出具体公式、算例或来源问题。当前没有公开 Issue 地址，不提供虚构邮箱。贡献流程见 [CONTRIBUTING.md](CONTRIBUTING.md)。

最后核对日期：2026-10-27。
