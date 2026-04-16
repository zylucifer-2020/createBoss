# Boss蒸馏 · Create Boss Skill

> 将职场中老板的聊天记录、会议纪要、邮件、批注等材料"蒸馏"成可复用的 Skill，模拟老板的决策风格、沟通方式和管理逻辑。

## 这是什么？

你有没有想过——

- 老板评审项目时为什么总问那几个问题？
- 为什么有些方案一次过，有些改了八版还是不行？
- 为什么你觉得讲清楚了，老板还是不满意？
- 怎么报风险才不会被骂？怎么争资源才能批下来？

**答案藏在老板的日常交互里。** 会议中的追问、邮件的批注、审批时的措辞——这些才是真正的认知架构。

**Boss蒸馏**就是把这些日常交互提炼成一套可复用的决策Skill。安装后，你可以：

- 🔍 用老板的视角评审项目
- 📝 写出老板认可的文稿
- 🎯 做出更精准的向上汇报
- 🧠 理解老板的决策逻辑

## 核心理念

> **提炼的不是"老板说了什么"，而是"老板怎么看问题"。**

一个好的人物Skill是一套可运行的认知操作系统：

- 他用什么**判断标准**看项目？（Judgment）
- 你应该怎么**向上管理**？（Management）
- 他怎么**表达**？（Persona）

**关键区分**：捕捉的是HOW they think，不是WHAT they said。

## Skill的三部分结构

每个蒸馏出的Boss Skill由三部分组成：

| 部分 | 内容 | 独立调用 |
|------|------|---------|
| **Part A — Boss Judgment** | 他如何评判项目、方案、进度、风险、资源和人 | `/{slug}-judgment` |
| **Part B — Managing Up** | 你应如何向上同步、报风险、提方案、争资源、争优先级 | `/{slug}-management` |
| **Part C — Persona** | 他的表达风格、情绪逻辑、管理姿态、压力状态 | `/{slug}-persona` |

运行逻辑：

```
收到问题 → Persona 判断语气与姿态 → Judgment 评项目 → Management 给出向上管理动作 → 用老板的风格输出
```

## 支持的数据来源

| 来源 | 聊天记录 | 文档/批注 | 会议纪要 | 解析工具 | 备注 |
|------|:-------:|:---------:|:-------:|---------|------|
| 微信聊天记录 | ✅ | — | — | `wechat_parser.py` | 导出 txt/html/csv |
| 飞书消息导出 | ✅ | ✅ | ✅ | `feishu_parser.py` | JSON/txt/复制文本 |
| 邮件 `.eml` / `.mbox` | ✅ | ✅ | — | `email_parser.py` | 可提取邮件风格 |
| Markdown / 文本 | ✅ | ✅ | ✅ | `generic_chat_parser.py` | 会议纪要、项目复盘 |
| 直接粘贴文字 | ✅ | ✅ | ✅ | — | 复制会议记录等 |

## 使用方式

### 蒸馏你的老板

```
帮我蒸馏我的老板，这是我跟他的聊天记录：[粘贴内容]
```

或提供文件：

```
这是老板批注过的文档：[附件]
这些是会议纪要：[附件]
帮我创建一个老板的Skill
```

### 调用已创建的Skill

| 命令 | 说明 |
|------|------|
| `/{slug}` | 调用完整 Skill |
| `/{slug}-judgment` | 仅老板的项目评判逻辑 |
| `/{slug}-management` | 仅向上管理建议 |
| `/{slug}-persona` | 仅老板的说话与行为风格 |

### 管理命令

| 命令 | 说明 |
|------|------|
| 列出所有老板 | 运行 `tools/skill_writer.py --action list` |
| 删除老板 | 运行 `tools/skill_writer.py --action delete --slug {slug}` |
| 版本回滚 | 运行 `tools/version_manager.py --action rollback --slug {slug} --version {version}` |

## 蒸馏流程

```
基础信息录入 → 素材接收 → 三部分提取 → Skill构建 → 验证交付
```

1. **基础信息录入**：称呼、岗位、管理风格印象
2. **素材接收**：聊天记录、会议纪要、邮件、批注
3. **三部分提取**：Judgment + Management + Persona
4. **Skill构建**：生成完整Skill + 三个独立Skill
5. **验证交付**：场景模拟测试

## 纠正机制

使用过程中如果发现"老板不会这么说"，可以随时纠正：

- "他不会这么说" → 修正 Persona
- "他不会先看这个" → 修正 Judgment
- "他更在意的是xxx" → 修正对应部分

纠正会记录到 Persona 的 Correction 区，后续生成会自动参考。

## 文件结构

```
create-boss/
├── SKILL.md                              # 蒸馏流程和核心指引
├── meta.json                             # 元数据
├── README.md                             # 本文件
├── requirements.txt                      # Python依赖
├── references/
│   ├── skill-template.md                 # Boss Skill的标准模板和输出结构
│   ├── extraction-framework.md           # 提取框架和验证方法论
│   └── prompts/                          # 分析与生成的提示词模板
│       ├── intake.md                     # 基础信息录入
│       ├── judgment_analyzer.md          # Judgment分析提示词
│       ├── judgment_builder.md           # Judgment生成模板
│       ├── management_analyzer.md        # Management分析提示词
│       ├── management_builder.md         # Management生成模板
│       ├── persona_analyzer.md           # Persona分析提示词
│       ├── persona_builder.md            # Persona生成模板
│       ├── correction_handler.md         # 纠正处理规则
│       └── merger.md                     # 增量合并规则
└── tools/                                # 工具脚本
    ├── skill_writer.py                   # Skill文件写入与管理
    ├── version_manager.py               # 版本管理
    ├── wechat_parser.py                  # 微信聊天记录解析
    ├── feishu_parser.py                  # 飞书消息解析
    ├── email_parser.py                   # 邮件解析
    └── generic_chat_parser.py            # 通用文本解析
```

## 适用场景

- 项目评审前，先让 Skill 模拟老板会挑什么问题
- 周报/汇报前，先检查信息是不是老板关心的格式
- 资源申请前，先判断怎样说更容易拿到支持
- 出现延期/风险时，先练习怎么向上报坏消息
- 学习老板的管理风格与决策模式

## 质量原则

| 原则 | 说明 |
|------|------|
| **原话 > 总结** | 老板原话比你的解读更有价值 |
| **矛盾 > 和谐** | 发现矛盾保留矛盾，真实的人都有矛盾 |
| **行为 > 声明** | 老板做了什么比说了什么更重要 |
| **具体 > 抽象** | "他会追问ROI"比"他关注价值"有用得多 |
| **规则 > 标签** | "5分钟没结论就打断"比"雷厉风行"有用得多 |
| **诚实 > 完美** | 60分的真实Skill > 90分的编造Skill |

## 绝不做的事

- ❌ 编造老板没说过的话
- ❌ 美化老板的决策逻辑
- ❌ 忽略负面观察
- ❌ 在素材不足时强行生成完整画像
- ❌ 把通用管理道理包装成"老板的独特见解"
- ❌ 只给标签不给行为

## License

MIT
