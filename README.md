# 西安观鸟图鉴

160种鸟类参考图鉴，附真实照片、识别特点、介绍、月份、生境与易混淆提示。支持18处观鸟地筛选，单文件离线使用。

![图鉴预览](docs/preview.png)

## 使用

下载仓库后，用浏览器打开根目录的 **`index.html`**。无需安装依赖；约15 MB，图片和资料已嵌入。

1. 在 **“我在这里”** 选择观鸟地点。
2. 选择月份，查看当前条件下本图鉴收录的候选鸟。
3. 如只希望查看资料曾明确提及的鸟，勾选 **“仅看有地点记录的鸟”**。
4. 点击图片放大，或选择2—3种并排对照；已见标记可在本机保存并导出CSV。

地点包含新渭沙、沣河文教园段、沣东沣河生态景区、沣渭、昆明池、丰庆、兴庆宫、大明宫、汉城湖、环城公园、曲江池、樊川、浐灞国家湿地公园、灞河西岸滨河公园、雁鸣湖、桃花潭、世博园广运潭、西安湖。

**地点记录与推定分开显示：** 有地点记录只代表资料曾提及；按生境推定的候选不是现场确证，也不表示一定可见。少见鸟只在有地点资料支持时纳入该地列表。月份为寻找窗口，全部列表仅覆盖本图鉴已有160种，不是全西安或单个地点的穷尽名录。

## 构建

需要 Python 3.10+ 和 Pillow。构建完全使用仓库内的图片与元数据，不需要联网抓取资料。

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python scripts/build_guide.py
```

Windows 中使用 `.venv\Scripts\activate` 激活环境。

构建生成 `index.html`、`data/guide.json` 和 `图片来源与许可.md`。修改界面请编辑 `scripts/template.html`，不要直接修改生成的 `index.html`。

## 验证

```sh
python scripts/validate_data.py
npm install
npx playwright install chromium
npm test
```

浏览器检查覆盖18个地点、已记载筛选、地点与月份交集、地点记忆、快速筛选、搜索、重置、手机宽度及离线请求。可通过 `CHROMIUM_EXECUTABLE_PATH` 指定已有Chromium。

## 维护数据

| 文件 | 用途 |
|---|---|
| `data/species.tsv` | 名录、月份、生境及学习顺序 |
| `data/descriptions.tsv` | 中文识别特点、介绍和混淆提示 |
| `data/places.json` | 地点信息、候选生境组合、逐种记录和来源 |
| `data/sources/` | 物种页面元信息与逐图许可 |
| `data/gbif_facets.json` | 区域记录检索快照；不作为精确公园记录 |
| `assets/` | 160张参考照片 |
| `scripts/places.py` | 地点数据校验与编译 |

`places.json` 中的 `profiles` 为人工整理的生境候选集合；`records` 必须附地点级来源，不可由生境匹配自动升级而来。新增鸟类应同时维护名录、中文描述、照片与许可信息。

## 来源与许可

所有参考照片来自 Wikimedia Commons，逐张作者和许可见 [图片来源与许可](图片来源与许可.md)。照片不默认拍摄于西安，部分为圈养参考个体。

资料使用管理机构发布、公开观鸟记录和逐种物种参考。图片各自适用原始许可，不可将它们统一声明为本项目原创；详细范围见 [第三方资料说明](THIRD_PARTY.md)。代码尚未选择额外开源许可证。

完整操作和资料说明见 [使用说明](docs/使用说明.md)。
