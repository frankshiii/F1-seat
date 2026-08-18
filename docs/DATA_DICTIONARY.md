# 数据字典

[简体中文](DATA_DICTIONARY.md) · [English](DATA_DICTIONARY.en.md)

## 赛道文件

- `circuit.geometry.points`：中心线 `[x, y]` 数组，遥测坐标通常为分米。
- `circuit.corners`：弯角编号、显示标签、中心坐标和沿圈位置。
- `circuit.map_features.pit_lane`：正赛车辆实际走过的维修区轨迹。
- `circuit.map_features.drs_zones`：从 DRS 状态与位置样本推导的区段。
- `overtakes[].s`：超车发生位置的沿圈弧长。
- `incidents[].turn`：赛控消息明确提及的弯角；无明确位置时不会伪造坐标。
- `speed_profile`：360 个沿圈分箱的平均速度与 P95。
- `coverage`：纳入年份、场次和归一化方法。

## 观赛区域文件

- `schema_version`：当前为 `1.0.0`。
- `coordinate_system`：坐标类型、单位和配准方法。
- `sources`：本文档可引用的来源清单。
- `grandstands[].geometry`：区域多边形及几何来源 ID。
- `grandstands[].position`：中心点、沿圈位置及距赛道距离。
- `grandstands[].view`：可见弯角估算、方法、屏幕和说明。
- `grandstands[].features`：顶棚、座位形式和无障碍状态。
- `grandstands[].provenance`：逐字段来源 ID。
- `grandstands[].confidence`：几何、名称、顶棚和视野的 0–1 置信度。
- `grandstands[].validity`：适用赛季与最近核实日期。
- `grandstands[].extensions.zone_type`：`grandstand`、`general_admission`、`hospitality`、
  `fan_zone` 或 `unknown`。

## 解释规则

- `unknown` 表示未核实，不表示否定。
- `provisional` 表示可用于预览，但不能当作精确测绘。
- 距离单位以当前文档的 `coordinate_system.units` 为准。
- 名称相同的多个多边形可能属于同一看台的分段，消费者可按名称和邻近关系合并。
