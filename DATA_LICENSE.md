# 数据来源与许可

[简体中文](DATA_LICENSE.md) · [English](DATA_LICENSE.en.md)

本仓库没有覆盖全部数据的统一许可证。许可证按来源层适用；单个 JSON 中的 `sources` 和
`provenance` 字段用于标明具体记录或字段的来源。本说明不是法律意见。

## OpenF1 衍生数据

赛道中心线、超车、赛控事件、速度分布、pit lane 与 DRS 数据由 OpenF1 数据计算，依据
[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 发布：必须署名、仅限
非商业用途，发布改编数据时须采用相同许可证并说明修改。

- 来源：https://openf1.org/
- 上游许可证：https://github.com/br-g/openf1/blob/main/LICENSE

## OpenStreetMap 数据

标记为 `osm` 的看台/建筑几何为 © OpenStreetMap contributors，依据
[ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/) 提供。公开使用衍生数据库时须
满足署名、Share-Alike 和可获取机器可读数据库等要求。

## 项目原创标注与 production 配准结果

标记为 `official-map-annotation` 的原始区域标注由项目维护者参考公开的官方场地图，
经 AI 辅助提取和人工修正、命名、复核形成。对于维护者有权许可、且尚未混入其他来源的
独立原创标注部分，依据
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 提供；请署名 `F1 Seat Data contributors`
并链接本仓库，同时注明是否修改。

`data/viewing-zones/*.json` 发布的是 production 坐标：多边形已经配准到 OpenF1 中心线，
`position.track_s`、距赛道距离和部分视野弯角也由该中心线计算；另有部分记录使用 OSM
几何。因此这些 production 文件是**混合许可数据**：

- OpenF1 配准及其衍生字段继续适用 CC BY-NC-SA 4.0；
- `osm` 几何继续适用 ODbL 1.0；
- CC BY 4.0 只覆盖维护者有权许可的独立原创标注贡献，不覆盖整个 JSON。

此授权不覆盖官方地图原图、标识、商标或项目无权许可的第三方内容。官方原图、截图和 PDF
不在本仓库发布；标注也不应被描述为官方测绘或认证。

## 官方事实参考

官方票务页、场地图和观赛指南只用于核实名称、清单、顶棚、屏幕、区域类型及近似位置。
本仓库发布结构化事实和项目标注，不授予第三方原始页面、图片或文字的权利。

## 复用清单

1. 查看文件内的 `sources`、`provenance`、`confidence` 和 `validity`。
2. 保留 OpenF1、OpenStreetMap 及项目标注署名；按 `provenance` 判断字段许可。
3. 不要把 OpenF1 衍生数据用于商业用途。
4. 不要把 `unknown` 当作否定事实，或把 provisional 数据宣传为精确测绘。
5. 不要把整个 `data/viewing-zones/` 目录标成 CC BY 4.0；组合数据时继续保留各层许可。
