# 数据贡献指南

[简体中文](CONTRIBUTING.md) · [English](CONTRIBUTING.en.md)

> **本仓库的生成文件不接受直接 PR，但公开接受数据纠错 Issue。**
> 不需要会写代码、Git 或 JSON；维护者会把核实后的纠错整合进数据源并重新生成本仓库。

最快的参与方式：

1. [打开看台信息纠错表](https://github.com/frankshiii/F1-seat/issues/new?template=stand-correction.yml)。
2. 选择赛道和涉及的信息，填写适用赛季或现场日期。
3. 分别写出当前值、建议值和可核实的来源；不确定的地方直接标明。
4. 提交 Issue。维护者会核对、更新数据源并在后续镜像中发布。

整条赛道、新赛道或一批结构化数据请使用
[赛道数据提案表](https://github.com/frankshiii/F1-seat/issues/new?template=circuit-data.yml)。

当前最有价值的任务是核实数据中 `provenance.name` 含 `"osm"` 的 89 个看台名称，并提供当季
官方页面或注明日期的现场观察。

## 可接受贡献

- 看台/GA/Club 名称、别名、区域类型和适用赛季纠错
- 顶棚、屏幕、无障碍信息和现场观察
- 几何偏移、弯角编号或 pit lane / DRS 区段问题
- 来源失效、置信度或 provenance 修正

## 不接受内容

- 官方地图原图、票务 PDF、卫星截图或付费数据库导出
- 没有来源或适用赛季的批量猜测
- 直接修改生成文件、但无法说明数据变化原因的 PR

贡献者应只提交自己有权分享的内容。自动提取结果必须经过人工复核；未知事实保留
`unknown`，不要用推测补齐。
