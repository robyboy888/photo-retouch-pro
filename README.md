# Photo Retouch Pro

把 10 条常用照片精修指令，整理成一个能按需求选择模式、保留人物身份与自然细节的 Agent Skill。

**适用于已有照片的编辑，也可以只生成精修提示词。** 技能本身不带图像模型，不需要为编写提示词配置 API Key；实际修图由当前环境提供的图像编辑工具完成。

## 十类操作

| 编号 | 操作 | 核心要求 |
| --- | --- | --- |
| 01 | 专业精修 | 调整曝光色彩，保留肤质与身份 |
| 02 | 移除物体或人物 | 重建背景，处理对应投影和反射 |
| 03 | 替换背景 | 保留主体，匹配光影、透视与景深 |
| 04 | 增强并放大 | 核实尺寸，不杜撰模糊细节 |
| 05 | 更换服装 | 保留人物，正确处理面料与遮挡 |
| 06 | 扩展照片 | 延续画面，不用裁切和拉伸代替 |
| 07 | 改变时间 | 统一天空、阴影、反射与环境受光 |
| 08 | 修正闭眼 | 优先参考同一人的睁眼照片 |
| 09 | 修复衣服褶皱 | 清理明显折痕，保留自然受力褶皱 |
| 10 | 移除设计元素 | 清除指定文字等，保留邻近布局 |

## 安装到 Codex

把本仓库放入 `~/.codex/skills/photo-retouch-pro`。首次安装可以运行：

```sh
git clone https://github.com/robyboy888/photo-retouch-pro.git ~/.codex/skills/photo-retouch-pro
```

Windows PowerShell：

```powershell
git clone https://github.com/robyboy888/photo-retouch-pro.git "$HOME/.codex/skills/photo-retouch-pro"
```

如果目录已经存在，先检查其来源和本地改动，不要强行覆盖。启动新会话以刷新技能发现；未显示时重启客户端。

其他支持 `SKILL.md` 的工具可以读取相同入口；具体图像工具需要在对应环境中提供，未承诺各平台均已测试。

## 使用示例

附上照片，直接描述需求：

```text
用 $photo-retouch-pro 专业精修这张人像，改善光线，保留毛孔，不瘦脸。
```

```text
用 $photo-retouch-pro 移除左下角的路人，包括他的地面投影，其他人不变。
```

```text
用 $photo-retouch-pro 把背景换成明亮的书店，人物和服装不变。
```

```text
用 $photo-retouch-pro 把照片左右扩展到 16:9，保留原画面。
```

```text
用 $photo-retouch-pro 修复闭眼，第二张是同一个人的睁眼参考，只改第一张。
```

```text
只写提示词：使用 $photo-retouch-pro 把这张产品照片改为日落光线。
```

支持组合操作，例如“先去掉路人，再换成黄昏光线，最后增强清晰度”。不会自动执行所有十种操作。

## 能力边界

- **身份保留是编辑约束与检查重点，不是生成模型的零误差保证。**
- **8K 以实际文件像素为准。** 未指定尺寸时按长边 7680 像素且保留比例理解；是否能导出取决于工具。放大不代表恢复真实丢失细节。
- 要求未修改区域逐像素不变时，需要蒙版或与原图合成；单次生成不保证这一点。
- 闭眼照片没有显示真实眼部细节，无参考时只做合理补全并说明限制。
- 默认另存文件；图片不会因为技能发布在 GitHub 就自动上传到仓库。

## 文件

```text
SKILL.md                 编辑流程、保留规则和交付要求
references/modes.md      十种精修模板与检查要点
agents/openai.yaml       Codex 技能显示信息
```

本仓库只包含技能文字与元数据，没有捆绑模型、私人照片或商业 API。基于用户提供的十条精修指令整理增强。结构校验不等同于实际出图质量验证；本次发布未附实图测试案例。

## English

An agent skill for ten common photo edits with identity and detail preservation: natural retouching, removal, background replacement, enhancement, wardrobe changes, outpainting, time-of-day relighting, closed-eye correction, garment smoothing, and design cleanup. Use with an image-editing-capable agent. Prompt-only use is supported. No model or API credentials are bundled.

License: MIT.
