# 立绘图库 · xsd_gallery（命名说明）

面板立绘按 **拼音 id** 自动找图，**不用改代码**。但「一个角色有多张图」时，靠命名区分**阶段/场景**。

## 命名规则（2026-09-28 定）

```
<拼音>.jpg|png            主立绘（= 默认阶段 baseline）
<拼音>_2.jpg|png          同一阶段的第二张（随机加载时会和主图一起抽）
<拼音>_3.jpg|png          同一阶段的第三张
<拼音>_<阶段>.jpg|png     特定场景/阶段，例如 _bath_front、_bath_side、_bed、_battle
```

- **只有小写字母、数字、下划线**；绝不用中文名。
- **阶段后缀要和代码里的变体表对上**：面板脚本 `状态栏面板.js` 的 `XSD_VARIANTS` 里写着
  「拼音 → { 阶段名: [后缀…] }」。没登记的后缀**不会被加载**（宁可不显示，也不串阶段）。
- **随机加载只在同一阶段内抽**：例如叶红缨，
  `baseline` 组 = `yehongying`、`yehongying_2`（正常立绘，含饮酒那张）；
  `bath` 组 = `yehongying_bath_front`、`yehongying_bath_side`（沐浴，正/侧）。
  **站街场景绝不会抽到沐浴图**，反过来也一样。

## 当前收录

| 角色 | 拼音 id | 阶段组 | 文件 |
|---|---|---|---|
| 闻观语 | `wenguanyu` | baseline | `wenguanyu`、`wenguanyu_2` |
| 孤月 | `guyue` | baseline | `guyue`、`guyue_2` |
| 叶红缨 | `yehongying` | baseline | `yehongying`、`yehongying_2` |
| 叶红缨 | `yehongying` | bath | `yehongying_bath_front`、`yehongying_bath_side` |
| 楚灵夜 | `chulingye` | baseline | `chulingye`、`chulingye_2`、`chulingye_3` |

> 每张都同时有 **.png（原图，1.4–2.1 MB）** 与 **.jpg（96×128 面板小图，3.5–4.5 KB）**。
> 面板**只用 .jpg**（一次都不断 404）；.png 留着当大图源，点开放大时按需用。

## 找图顺序（找不到就降级，永不碎图）

1. `user/images/xsd_gallery/<id>.jpg` ← **面板首选**
2. 同目录 `.png`、`.webp`
3. `/user/images/xsd_gallery/…`（反代兼容）、`xsd_gallery/…`（public 目录部署）
4. catbox 云图（分享给别人时用；直链写在 `卡片脚本/状态栏面板.js` 的 `XSD_CLOUD` 锚点里）
5. **SVG 占位剪影**（按角色配色画的人形剪影 ＋ 名字）

## 放大与翻面

- **点面板上的立绘** ⇒ 开灯箱看大图；灯箱里可**左右翻面**（← → 键或按钮），翻的就是**同一阶段组**里的那几张。
- 每次渲染会从该阶段组里**抽一张**（用楼层号做种子 ⇒ 同一楼重绘不会跳图，换楼才换）。

## 换图 / 加图

- **换图**：同名覆盖即可，刷新就变。
- **加角色**：图按 `<拼音>.jpg|png` 丢进来，并把拼音 id 补进面板脚本的 `XSD_PINYIN`（唯一要改代码的地方）。
- **加同角色新阶段图**：按 `<拼音>_<阶段>.jpg|png` 命名，并在 `XSD_VARIANTS` 里登记该阶段的后缀。
- **分享给别人**：图传 catbox 拿直链 → 填进 `XSD_CLOUD` 锚点（可用 `_catbox_upload.mjs` 一键上传＋回填）。
