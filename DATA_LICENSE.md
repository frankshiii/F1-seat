# 数据来源与许可

[简体中文](DATA_LICENSE.md) | [English](DATA_LICENSE.en.md)

本说明适用于仓库中的数据文件和由管线生成的发布产物。它不是法律意见，也不替代任何
上游许可证或服务条款。

## 数据整体按 CC BY-NC-SA 4.0 发布

**本仓库发布的数据集（`web/data/*.json` 及由其导出的公开数据）整体依据
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 提供，见
[LICENSE-DATA](LICENSE-DATA)。**

之所以是这一条而不是更宽松的许可：比赛动作、速度剖面、赛道中心线以及所有基于中心线
计算的 `track_s`、距离和视野字段，都是 OpenF1 的衍生物，而 OpenF1 采用
CC BY-NC-SA 4.0。其 ShareAlike 条款要求衍生物以相同许可分发——这与是否商用无关，
是分发行为本身触发的义务。把最严格的一条覆盖全部，是唯一能一次性满足它的做法。

两点必须同时理解：

1. **项目代码仍是 [MIT](LICENSE)。** 代码可商用不等于数据可商用。
2. **数据许可不能突破上游。** 下面的分层说明用于告诉你每一类数据的上游是谁、
   额外背着什么义务（例如 89 个看台名称同时受 ODbL 约束）。CC BY-NC-SA 4.0 是
   项目对自己有权许可的部分所作的授权，不构成对上游权利的再授权。

项目自身原创、且未与其他来源混合的标注内容，作者另行同意时可按更宽松条件使用；
但一份完整的生产 JSON 是混合来源文档，**不得整体标称为 CC BY 4.0**。

## 来源分层

### 比赛动作、遥测衍生指标与赛道中心线

超车、位置、速度和赛控事件来自 OpenF1；正式赛道中心线也由多位车手的 OpenF1
`location` 轨迹重采样、取中位数和平滑生成。Pit lane 轨迹与 DRS 开启区同样由 OpenF1
`pit / car_data / location` 联合推导。本项目再计算弯角定位、过滤结果与聚合指标。
OpenF1 仓库公开的许可证为 **CC BY-NC-SA 4.0**。本项目因此仅按非商业粉丝项目分发相关
衍生数据，并保留 OpenF1 署名。商业使用、再授权或对 API 输出许可范围存在疑问时，必须
先向 OpenF1 确认。

- 来源：https://openf1.org/
- 许可证：https://github.com/br-g/openf1/blob/main/LICENSE

### OpenStreetMap 看台名称（仅名称，不再包含几何）

**几何层面已不含任何 OpenStreetMap 数据。** 全部 600 个观赛区域的多边形现在来自
项目自有标注（`official-map-annotation` 557 个、`official-map` 21 个）与 MIT 许可的
`bacinger/f1-circuits` 派生估算（22 个）。管线不再调用 Overpass API。

仍受 ODbL 约束的只剩**部分看台名称**：89 个区域的名称最初取自 OSM 的 `name` 标签，
分布为 monza 39、barcelona 17、silverstone 16、spielberg 9、shanghai 6、spa 1、hungaroring 1。

这个边界是**数据自描述**的：凡 `provenance.name` 包含 `"osm"` 的记录，其名称字段
© OpenStreetMap contributors，依据 **ODbL 1.0** 提供；其余字段不受此约束。
只使用几何、位置、超车热度等字段而不使用这些名称的下游用户，不触及 ODbL。

这些名称尚未逐条独立核实，其中已知有与官方地图标签矛盾的条目（例如某站的
`Tribuna C` 与 `Tribuna G` 疑似互换，`Tribuna E` 对应的官方标签为 `F`），
即**部分 OSM 名称可能本身就是错的**。用官方地图或票务页核实并替换这些名称，
是当前最有价值的社区贡献之一，见 CONTRIBUTING。核实完成后这一节将被整体删除。

- 来源及署名要求：https://www.openstreetmap.org/copyright
- 许可证：https://opendatacommons.org/licenses/odbl/1-0/

### `circuit_alignment` SVG 与衍生观赛区域几何

20 条 2026 赛道当前使用本地 `circuit_alignment/*.svg` 中的赛道、看台、GA 和
Hospitality 轮廓生成发布几何。这些 SVG 由项目维护者依据公开的官方赛道/场地图，经 AI
辅助提取后逐站人工修正、命名和复核，是项目维护的**标注层**，不是第三方提供的 SVG 素材。

官方地图用于本地参考和事实核实；项目发布 SVG 标注坐标及其转换结果，不发布官方地图
原图、截图或 PDF，也不声称标注结果是官方测绘或官方认证。标注层与 OpenF1、OSM 等
混合来源数据仍应分别记录 provenance。维护者有权许可且未混入其他来源的独立原创标注
可采用 CC BY 4.0；映射到 OpenF1 中心线后的 production 坐标、`track_s`、距离和视野字段
继续适用 OpenF1 的 CC BY-NC-SA 4.0，`osm` 几何继续适用 ODbL。完整 production JSON
因此是混合许可数据，不能整体声明为 CC BY 4.0。

- 管线来源 ID：`official-map-annotation`
- 本地输入：`circuit_alignment/<slug>.svg`
- 标注方法：官方地图参考 + AI 辅助提取 + 人工修正与复核
- 生成命令：`npm run build:svg-production`
- 当前发布范围：20 站、557 条观赛区域几何（已剔除距赛道中心线超过 450 m 的离群区域）

### 弯角编号锚点

弯号及大致位置属于独立的标注层，存放在 `pipeline/data/corner_anchors.json`，以从起终点开始的
圈长比例表示，并在构建时投影到 OpenF1 中心线。已按官方图复核的站点记录对应来源；
`bootstrap_pending_review` 表示从项目旧版赛道标注迁移、尚未完成独立官方图复核。

- 当前正式中心线及其 x/y 坐标不调用或复制 MultiViewer circuits API；
- 迁移锚点只是小型弯号注释基线，不代表精确测绘或官方认证；
- 独立复核完成前，下游应保留其状态，不应将其宣传为官方数据；
- 贡献者应优先用当季官方赛道图提交修正，并更新来源和复核状态。

旧版迁移来源曾使用：https://multiviewer.app/

### 地理赛道轮廓

Madring 的赛前临时轮廓，以及管线用于地理配准的部分赛道轮廓，来自
`bacinger/f1-circuits`，依据 **MIT License** 提供。具体归属应保留在数据 provenance 中。

- 来源：https://github.com/bacinger/f1-circuits
- 仓库固定快照及上游许可：`pipeline/vendor/`

### 官方票务页、场地图和观赛指南

这些材料只用于核实看台清单、名称、顶棚、视野描述和近似位置。原始 PDF、图片、网页
截图和卫星底图不随仓库或网站发布。事实记录保存来源 URL、检索日期、适用赛季和置信度；
这不表示项目拥有原材料的版权或再分发权。

### 社区贡献事实

贡献者提交的现场观察、别名、核实状态和人工标注会记录来源与置信度。涉及照片或其他
可能受版权保护的材料时，贡献者必须拥有分享权限，并在提交中说明允许的用途。

## 给复用者的检查清单

在复制、再分发或部署数据前：

1. 查看每个文档的 `sources`、`provenance`、`confidence` 和 `validity`。
2. 保留 OpenF1、OpenStreetMap 及其他上游署名和许可证链接。
3. 不要把 `unknown` 解释为否定结论。
4. 不要把低置信度或 `provisional` 几何宣传为精确测绘数据。
5. 不要假设代码可商用就意味着捆绑数据也可商用。
6. 商业用途必须单独处理 OpenF1 的 NonCommercial 限制及其他上游权利。
7. `official-map-annotation` 表示项目维护者制作的标注，不是官方地图原图或官方认证；
   对外开放时只授予项目有权许可的标注内容，并与 OpenF1、OSM 等来源分层发布。
