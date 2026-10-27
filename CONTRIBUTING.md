# 贡献说明

本仓库只接收工具说明、契约、公式假设、来源与算例。计算实现、页面组件和浏览器读取逻辑在 `site-tools`；网站视觉与共享组件在 `site-www/packages/core`。修改公式时，内容与代码必须成对提交。

## 提交前

1. 确认工具 slug 与 `entityId` 唯一，并说明它解决的具体问题和不适用的场景。
2. 在 `formulaDescription` 写清输入、运算顺序、单位、边界与舍入；在 `assumptions` 逐条列出简化条件；不要只在正文里口头描述。
3. 为每个数值规则增加或更新 `data/cases/` 中的独立算例，写明输入、期望输出和边界意图。舍入、截断、单位换算与「未知」必须可复现。
4. 修改计算口径必须提升 `specVersion`，并同步 `site-tools` 实现与测试；不能只改说明或只改代码。
5. 中英文事实、限制和错误条件必须一致，不做单向补充。
6. 引用标准、论文或公共指南时记录 `sourceId`、URL 或 DOI、定位段与支持的结论；不编造来源、作者或实测。
7. 轨迹工具只能处理用户主动选择的本地文件；不设计上传、遥测或将文件内容写入日志的行为。

## 工具特定约束

- 配速：三种模式都只接受恰好两个正数输入；英里使用国际英里 1,609.344 米。
- 分段：负分段只改变前后半程时间分配，不做主观难度或名次预测；秒数总和必须等于输入总时间。
- 跑走结合：不根据时间推算距离，不评价训练适宜性；总时长模式必须标记被截断的段落。
- 比赛预测：指数固定为 1.06，距离限制 5000–42195 米；不得包装成完赛保证、概率或越野预测。
- 轨迹查看/转换/简化：只接受线几何，缺失高程保持未知；分段不连接；转换去除时间、设备与人员元数据。
- 路线参数比较：只比较已发布路线，缺失值显示未知，不生成安全、难度或适配性排名。没有已发布路线时页面应显示空状态，不填充样例数据。

## 审阅与状态

状态为 `draft`、`in-review`、`published`、`withdrawn`。`published` 需要两种语言都有作者与审阅者，并存在 `approve` 审阅记录；审阅摘要必须匹配当前内容。公式或算例改变后必须重新审阅。

## 校验

在 `site-tools` 运行：

```text
pnpm test:content
pnpm test
pnpm check
pnpm build
```

内容校验检查双语配对、工具契约、算例引用、来源、许可与审阅摘要。测试失败时修正内容或实现，不绕过检查。

---

# Contributing

This repository accepts tool documentation, contracts, formula assumptions, sources and cases only. The calculation implementation, page components and browser file handling live in `site-tools`; shared visual components live in `site-www/packages/core`. A formula change requires matching content and code changes.

Before submitting, confirm that the slug and `entityId` are unique and state both the problem the tool solves and the cases it does not cover. Put inputs, operation order, units, limits and rounding in `formulaDescription`, and list every simplification in `assumptions`. Add or update an independent case in `data/cases/` with inputs, expected output and boundary intent so rounding, truncation, unit conversion and “unknown” are reproducible. A changed calculation requires a higher `specVersion` plus matching implementation and tests; documentation-only or code-only changes are not accepted. Keep Chinese and English facts, constraints and error conditions consistent, cite a `sourceId`, URL or DOI for standards and papers, and never invent sources, authors or test results.

Tool-specific rules: pace accepts exactly two positive inputs and uses the international mile of 1,609.344 m; negative splits allocate time across halves without predicting difficulty or placing; run-walk never infers distance and marks truncated segments; race prediction keeps the 1.06 exponent and the 5000–42195 m range and is not a finish guarantee or trail predictor; track tools accept line geometry only, preserve missing elevation as unknown, never join segments and strip timestamps, device names and personal metadata; route comparison uses published routes only, shows missing values as unknown, produces no safety, difficulty or suitability ranking, and shows an empty state rather than sample data when no route is published.

New entities start as `draft`, move to `in-review` after bilingual, source and rights checks, and to `published` only with authors, reviewers and an `approve` review record in both languages whose digest matches the current content. After a formula or case change, run `pnpm test:content`, `pnpm test`, `pnpm check` and `pnpm build` in `site-tools`. Fix failures rather than bypassing them.
