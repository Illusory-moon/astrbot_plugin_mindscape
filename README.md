# 灵魂景观 Mindscape · AstrBot 插件

> **给你的 AstrBot 装上长期记忆、人格语气，和「真的可以什么都不说」的权利。**

这是 [bot-mindscape](https://github.com/Illusory-moon/bot-mindscape) 的 AstrBot 单文件整合插件。

<img src="assets/demo-2-memory.png" width="600" alt="三天前的事它还记着">

> **「说一件三天前令你印象最深的事」** —— 它答得上来，而且是**具体那一件事**。

---

## 它治什么

| 毛病 | 平时什么样 | 这一层怎么治 |
|---|---|---|
| **金鱼记忆** | 昨天的事今天就忘，反复问已经知道的东西 | 认知层：五层记忆装配 |
| **文字机器** | 说的话永远像客服模板 | 表达层：风格层 + 表情包调度 |
| **机械出戏** | 群里冒出 `LLM 响应错误: APITimeoutError` | 沉浸层：拦下来，绝不发出去 |
| **不叫不动** | 只会「收到消息 → 回一句」 | 唤醒层：自己会开口，也能真的闭嘴 |

## 安装

**方式一：插件市场**（推荐）

在 AstrBot 的插件市场里搜索「**灵魂景观**」或「**mindscape**」，点安装。

**方式二：手动**

```bash
cd AstrBot/data/plugins
git clone https://github.com/Illusory-moon/astrbot_plugin_mindscape.git
```

然后在 AstrBot 管理面板重启插件（或 `docker restart astrbot`）。

装好后启动日志里应该看到：

```
[mindscape] 插件已加载（7 个模块）
```

## 配置

⚠️ **这个插件不读 AstrBot 的插件配置页**，它的配置是独立文件：

```
~/.mindscape/config.yaml          # 可用环境变量 MINDSCAPE_CONFIG 改路径
```

为什么这么设计：同一份配置**既给插件用，也给命令行脚本用**，而且主仓库自带两个管理界面。

配置示例见主仓库 [`config/config.example.yaml`](https://github.com/Illusory-moon/bot-mindscape/blob/main/config/config.example.yaml)。
最小可用配置长这样：

```yaml
memory:
  max_chars: 2500              # 每轮注入的字数预算
  bots:
    - self_id: "你的botQQ"
      name: "bot名字"
      diary: "./data/bot-name.md"        # 记忆原文
      people: "./data/bot-name.people.md"
      rules:                            # 这个 bot 自己的行为约束
        - "被点名时必须回复"
```

## 哪些功能需要额外打补丁

**插件装完即可用的三层**：认知层、表达层、沉浸层（含「真的可以什么都不说」）。

**需要给 AstrBot 本体打补丁才能完整使用**：唤醒层的进阶策略 ——
「提到名字必回」「自主冒泡」「定向性判定」「每 bot 独立白名单」。
原因是这些判定发生在框架的**消息分发阶段**，比插件更早，插件钩子够不到。

补丁在主仓库 [`patches/`](https://github.com/Illusory-moon/bot-mindscape/tree/main/patches) 目录，附带自动安装脚本。
不打补丁也能正常用，只是唤醒策略退回 AstrBot 原生的「前缀 / @ 唤醒」。

## 更多截图

### 它自己会开口，也可以真的闭嘴

**没有任何人叫它。** 群里在闲聊，它挑了个没人注意的时间自己冒一句：

<img src="assets/demo-4-bubble.png" width="460" alt="自主冒泡">

### 它记得一个人

<img src="assets/demo-3-notes.png" width="500" alt="它记得一个人">

## 许可

MIT
