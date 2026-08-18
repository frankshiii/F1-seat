# F1 Seat Data

[简体中文](README.md) · [English](README.en.md)

> ## 在线使用
>
> **[打开 F1 选座助手：f1.shiqiqian.com →](https://f1.shiqiqian.com)**
>
> 不需要安装，不提供购票；用于比较赛道动作数据、看台位置、类型、顶棚和视野信息。

面向 F1 赛道地图、观赛区域比较和数据研究的开放数据仓库，只发布结构化数据。

> **这是一个只读镜像。** 内容由源仓库 [F1-track](https://github.com/frankshiii/F1-track) 的
> `pipeline/export_open_data.py` 自动生成并推送，请**不要直接在本仓库提 PR**——
> 这里的改动会在下次同步时被覆盖。纠错和数据贡献请到源仓库提交，见下方“贡献”。

当前快照覆盖 2026 赛历 22 站，包括：

- 赛道中心线、弯角、pit lane 与 DRS 区域
- 2023 年起已完赛正赛的定位超车、赛会事件和 360 段速度分布
- 看台、GA、Club / Hospitality 与其他观赛区域几何
- 逐字段来源、置信度、适用赛季和核实状态

当前数据包含 600 条原始观赛区域记录和 12,050 次定位超车。Madring 尚未举办首场 F1
正赛，因此使用明确标记为 provisional 的赛前轮廓，不提供伪造热力数据。

## 在线版怎么用

1. 在“赛历”选择分站；下一场比赛会显示剩余天数。
2. 进入赛道后切换“超车 / 事故 / 速度”，地图只突出当前指标排名前 5 的弯角。
3. 桌面使用滚轮或按钮缩放并拖动地图；手机双指缩放，放大后单指平移。
4. 红色虚线表示 pit lane，绿色虚线表示 DRS；点击或悬停赛道可查看弯号和局部数据。
5. 按“看台 / GA / Club / 其他”筛选观赛区域，点看台查看类型、顶棚、视野、距离和置信度。
6. 将 2–3 个看台加入“对比”，再结合个人对超车、事故和顶棚的偏好判断。

地图是辅助决策工具，不包含实时票价、库存或具体座位排号。`unknown` 表示尚未核实。

## 目录

```text
data/
├── circuits/<slug>.json       # 赛道、弯角、动作记录、速度及地图功能
├── viewing-zones/<slug>.json  # 看台/GA/Club 几何与属性
└── index/
    ├── circuits.json          # 赛历及状态
    └── tracks-mini.json       # 轻量缩略路径与计数
schema/
├── circuit.schema.json
└── viewing-zones.schema.json
docs/
└── DATA_DICTIONARY.md
```

`slug` 是跨文件连接键，例如：

```text
data/circuits/suzuka.json
data/viewing-zones/suzuka.json
```

## 开发者怎么使用数据

JavaScript：

```js
const circuit = await fetch(
  "https://raw.githubusercontent.com/frankshiii/F1-seat/main/data/circuits/suzuka.json"
).then(response => response.json());

console.log(circuit.circuit.name, circuit.overtakes.length);
```

Python：

```python
import json
from pathlib import Path

circuit = json.loads(Path("data/circuits/suzuka.json").read_text())
zones = json.loads(Path("data/viewing-zones/suzuka.json").read_text())
print(circuit["circuit"]["name"], len(zones["grandstands"]))
```

## 坐标与精度

- 正式赛道与大部分观赛区域使用遥测笛卡尔坐标，单位为分米。
- `s` 表示从起终点开始的赛道弧长位置；不同文件应优先通过 `s` 对齐，不要假设 x/y
  是经纬度。
- `confidence`、`validity` 和 `coverage` 是数据的一部分，`unknown` 不等于“没有”。
- `official-map-annotation` 表示维护者参考官方场地图，经 AI 辅助提取和人工修正/复核形成
  的项目标注；它不是官方地图原图、官方测绘或官方认证。
- 原始官方地图、截图、PDF 和卫星底图不在本仓库发布。

完整字段解释见 [数据字典](docs/DATA_DICTIONARY.md)。

## 来源与许可

本数据集整体依据 **[CC BY-NC-SA 4.0](LICENSE-DATA)** 提供。

之所以带 NonCommercial：比赛动作、速度剖面、赛道中心线以及所有由中心线计算的字段都是
OpenF1 的衍生物，而 OpenF1 采用 CC BY-NC-SA 4.0，其 ShareAlike 条款由「分发」触发，
与是否商用无关。

一处额外义务：**89 个区域的看台名称**取自 OpenStreetMap，其名称字段另受 ODbL 约束。
边界是数据自描述的——`provenance.name` 含 `"osm"` 的记录才背这个义务。**几何不含任何
OSM 数据。** 只取几何、位置和超车热度而不使用这些名称的用途，完全不触及 ODbL。

复用前请读 [DATA_LICENSE.md](DATA_LICENSE.md) 和每个文档的 `sources` / `provenance` 字段。

## 贡献

请通过 Issue 报告错误，并提供赛道、适用赛季、字段、建议值和可核实来源。不要上传官方
地图原图、票务 PDF、卫星截图或其他无再分发权的材料。详见
[CONTRIBUTING.md](CONTRIBUTING.md)。

F1 Seat Data 是独立的非商业车迷数据项目，与 Formula 1、FIA、各大奖赛主办方、赛道、
票务平台、OpenF1 或 OpenStreetMap 没有隶属、赞助或背书关系。
