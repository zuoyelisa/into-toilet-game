# 辰宝学上厕所 · Into käy vessassa

一个给 2.5 岁小朋友的互动小游戏，帮助孩子了解如厕的过程：想上厕所、脱裤子、坐上马桶、擦屁股、冲水、穿好裤子、洗手。整个过程只需要**点一点**，不需要识字，不用拖动，也没有对错、没有输赢和倒计时。

**Demo：** 打开 `index.html`，或者在支持 GitHub Pages 的仓库里访问已发布的网址。

---

## 游戏内容

| 步骤 | 中文 | Suomi |
|---|---|---|
| 1 | 我想拉粑粑！/ 我想尿尿！ | Minulla on kakkahätä! / Minulla on pissahätä! |
| 2 | 脱裤子。 | Housut alas. |
| 3 | 去马桶啦！ | Mennään vessaan! |
| 4 | 坐上马桶，嗯—— | Istutaan pöntölle, hmm… |
| 5 | 扑通！拉粑粑啦！ | Plumps! Kakka tuli! |
| 6 | 擦擦屁股。 | Pyyhitään pylly. |
| 7 | 冲水！粑粑拜拜！ | Huuhdellaan! Hei hei, kakka! |
| 8 | 穿好裤子。 | Housut ylös. |
| 9 | 洗洗手，搓泡泡。 | Pestään kädet saippualla. |
| 10 | 辰宝真棒！ | Hienoa, Into! |
| 彩蛋 | 小狗、小猫、大象轮流来上厕所 | Koira, kissa, norsu |

每个画面都有一个发光、带黄色虚线圈的东西，提示宝宝去点。点了就会有动画和声音，随后自动进入下一步。

**拉粑粑 / 尿尿**：开始页可以选择"拉粑粑"或"尿尿"，尿尿的流程里粑粑换成了一颗黄色的小水滴。

**擦擦屁股**：点墙上的卷纸，白色纸巾会软软地拉出来，飘到辰宝手里，擦两三下，再轻轻飘进马桶。下一步冲水时，纸巾跟着一起冲走。两个流程都有这一步。

---

## 语言

- 页面右上角有两个按钮：**妈妈 · 中文**和 **Isä · SUOMI**。
- 选择中文时，句子中的中文加粗、深色显示，芬兰语变细、变浅；选择芬兰语时则相反。
- 语音跟着语言切换：中文是女声，芬兰语是男声。
- 所有语音都已经内置在页面里，不需要联网。

---

## 怎么玩

1. 用手机、iPad 或电脑打开页面。
2. 点开始页的"拉粑粑"或"尿尿"。
3. 点画面中发光的东西（辰宝、马桶、冲水按钮、泡泡等）。
4. 点底部的句子可以再听一遍；点左右箭头可以翻页。
5. 彩蛋里点小狗、小猫或大象，它们会跳一下，并读出动物的名字。三只都点过后会出现"再来一次"按钮。

**适配：**
- 手机横屏：顶部一条细栏，画面占满剩下的高度，按钮在左右下角。
- 手机竖屏和 iPad 竖屏：画面填满屏幕，按焦点区域裁切，辰宝和马桶会更大。
- 电脑和 iPad 横屏：完整显示整个场景。

> 声音提示：iPhone 和 iPad 的侧边静音开关会影响声音，请确认没有开启静音。

---

## 文件说明

```
02.2-into-toilet game/
├── index.html   # 游戏本体（所有图片、动画、声音都内嵌在这一个文件里）
└── README.md    # 本说明
```

游戏是**单个 HTML 文件**，不需要安装任何东西，也不需要网络（字体除外，字体会从 Google Fonts 加载，没有网络时会使用系统字体）。

---

## 技术说明

- 图形全部是 SVG 矢量绘制，在任何分辨率下都清晰。
- 中文语音由 Matcha TTS 生成，并用语音识别检查过每一句的内容。
- 芬兰语语音由 Piper 模型（harri-medium）生成。

**新增句子时怎么配出一样的声音**（2026 年 10 月"擦擦屁股"这一步就是这样做的）：
- 中文：按 `CHINESE_VOICE_GENERATION.md`（在本地 `02-into-game` 文件夹里，不在这个仓库）的做法，Matcha `matcha-icefall-zh-baker` + Vocos，语速 0.9。"擦擦"要在词典里加 `擦擦 ca1 ca`（第二个字轻声），不然会被读成"擦哈"。
- 芬兰语：**不是** `FINNISH_VOICE_GENERATION.md`（同一个本地文件夹）里的 edge-tts（那是"辰宝的一天"用的，声音更高）。这个游戏用的是 sherpa-onnx 的 `vits-piper-fi_FI-harri-medium`，语速 0.9。裁静音和归一化的方式和中文一样，再用 ffmpeg 转成 24 kHz 单声道 48 kbps MP3。
- 在 Mac 上直接用 `pip install piper-tts` 会因为找不到发音数据而报错，所以改用 sherpa-onnx 打包好的版本。
- 没有使用任何外部图片、角色或版权素材；所有角色都是原创。
- 声音使用 `<audio>` 播放，无法播放时会切换到 Web Audio，最后才使用设备自带语音。

## 设计原则

- 只有正面、鼓励的话语，没有"不可以""脏"之类的说法。
- 点错也没有失败，只会出现相应的动画和声音。
- 按钮和点击区域较大，适合小手操作。
- 画面颜色柔和，不会有让孩子不舒服的声音或画面。

---

## 致谢

- 辰宝的形象、场景和动画：由家人设计并确认。
- 语音由 Matcha TTS 和 Piper 生成。

## LICENSE

* This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/) - [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/80x15.png)](https://creativecommons.org/licenses/by/4.0/)

