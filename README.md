# F1 Seat Data

[简体中文](README.md) · [English](README.en.md)

面向 F1 赛道地图、观赛区域比较和数据研究的开放数据仓库。这里发布结构化数据，不包含
`F1-track` 私有产品的前端、推荐算法、标注工具、生产管线或部署配置。

当前快照覆盖 2026 赛历 22 站，包括：

- 赛道中心线、弯角、pit lane 与 DRS 区域
- 2023 年起已完赛正赛的定位超车、赛会事件和 360 段速度分布
- 看台、GA、Club / Hospitality 与其他观赛区域几何
- 逐字段来源、置信度、适用赛季和核实状态

当前数据包含 600 条原始观赛区域记录和 12,050 次定位超车。Madring 尚未举办首场 F1
正赛，因此使用明确标记为 provisional 的赛前轮廓，不提供伪造热力数据。

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

## 快速使用

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

本仓库没有覆盖所有文件的单一许可证：OpenF1 衍生数据、OSM 几何和项目原创标注分别
适用不同条款。复用前请阅读 [DATA_LICENSE.md](DATA_LICENSE.md) 和每个看台文档的
`sources` / `provenance` 字段。

## 贡献

请通过 Issue 报告错误，并提供赛道、适用赛季、字段、建议值和可核实来源。不要上传官方
地图原图、票务 PDF、卫星截图或其他无再分发权的材料。详见
[CONTRIBUTING.md](CONTRIBUTING.md)。

F1 Seat Data 是独立的非商业车迷数据项目，与 Formula 1、FIA、各大奖赛主办方、赛道、
票务平台、OpenF1 或 OpenStreetMap 没有隶属、赞助或背书关系。
