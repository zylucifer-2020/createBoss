# 🧬 Boss蒸馏

**把老板"装进"AI，让决策逻辑可复用**

> 你有没有过这种感觉——同一个方案，同事汇报一次过，你改了八版还是被打回？老板评审时总问那几个问题，但你永远猜不准这次会问哪个？

**不是你不行，是你没读懂老板的"操作系统"。**

📺 **宣传视频**：[![点击查看宣传视频](https://img.shields.io/badge/Watch-Demo-00d9ff?style=for-the-badge)](https://zylucifer-2020.github.io/createBoss/demo.html)

Boss蒸馏做的事情很简单：从你和老板的日常交互中，提炼出他的一套决策逻辑——然后装进一个Skill里，随时可以调用。

[![Version](https://img.shields.io/badge/version-3.0.0-orange)](./meta.json)
[![License](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![Platform](https://img.shields.io/badge/platform-CodeBuddy-blue)](https://codebuddy.cn)
[![GitHub Stars](https://img.shields.io/github/stars/zylucifer-2020/createBoss?style=social)](https://github.com/zylucifer-2020/createBoss)

---

## 📋 目录

- [✨ 功能概览](#-功能概览)
- [🚀 快速开始](#-快速开始)
- [📖 核心功能详解](#-核心功能详解)
  - [🔨 蒸馏：从素材到Skill](#-蒸馏从素材到skill)
  - [🎯 三个独立Skill入口](#-三个独立skill入口)
  - [✏️ 纠正与增量更新](#️-纠正与增量更新)
  - [🧬 自进化机制](#️-自进化机制)
  - [🛡️ 边界条件处理](#️-边界条件处理)
- [📁 文件结构](#-文件结构)
- [💡 适用场景](#-适用场景)
- [❓ FAQ](#-faq)
- [🤝 贡献指南](#-贡献指南)
- [📝 更新日志](#-更新日志)

---

## 🙏 致谢与参考

本项目在开发过程中参考了以下优秀项目的设计思路：

| 项目 | GitHub | 参考内容 |
|------|--------|---------|
| **boss-skills** | [vogtsw/boss-skills](https://github.com/vogtsw/boss-skills) | Boss蒸馏思路 |
| **nuwa-skill** | [alchaincyf/nuwa-skill](https://github.com/alchaincyf/nuwa-skill) | Skill蒸馏框架 |
| **darwin-skill** | [alchaincyf/darwin-skill](https://github.com/alchaincyf/darwin-skill) | 自我进化机制 |

感谢以上项目的作者开源分享，让这个项目得以站在巨人的肩膀上。

---

## ✨ 功能概览

| 核心功能 | 说明 |
|---------|------|
| **智能蒸馏** | 从聊天记录/会议纪要/邮件/批注中提炼老板的决策逻辑 |
| **三部分提取** | Judgment（评判逻辑）+ Management（向上管理）+ Persona（表达风格） |
| **自进化** | 使用过程中自动学习，越用越准 |
| **增量更新** | 老板有了新动向，一键补充，不用从头开始 |
| **智能解析** | 自动解析微信/飞书/邮件/通用文本，支持多种格式 |
| **版本管理** | 每次更新自动备份，随时可回滚 |

---

## 🚀 快速开始

### 方式一：复制提示语给智能体（推荐）

复制以下提示语，发送给CodeBuddy或其他AI智能体：

```markdown
请使用 create-boss 技能（https://github.com/zylucifer-2020/createBoss）
来帮我蒸馏我的老板。

操作步骤：
1. 先阅读 SKILL.md 了解技能用法
2. 运行该技能，按照流程引导我完成老板蒸馏
3. 将生成的 Boss Skill 保存到 bosses/ 目录下

我提供的素材：[在这里粘贴聊天记录/会议纪要/邮件等]
```

### 方式二：Git Clone本地安装

```bash
# 1. 克隆仓库
git clone https://github.com/zylucifer-2020/createBoss.git
cd createBoss/create-boss

# 2. 查看文件结构
ls -la

# 3. 将 SKILL.md 内容复制到你的智能体/CodeBuddy中使用
# 4. 按照SKILL.md中的流程执行蒸馏
```

### 开始蒸馏

准备好素材后，运行以下命令开始蒸馏：

```
帮我蒸馏我的老板，这是我跟他的聊天记录：
[粘贴微信聊天 / 飞书导出 / 会议纪要 / 邮件 / 批注]
```

蒸馏流程：
```
Step 1: 扔素材过来（支持多种格式）
Step 2: 确认3个问题（都可以跳过）
Step 3: 自动生成完整Skill + 3个独立调用入口
```

### 支持的数据源

| 来源 | 格式 | 自动解析 |
|------|------|:--------:|
| 微信聊天记录 | txt / html / csv | ✅ `wechat_parser.py` |
| 飞书消息 | JSON / txt / 复制文本 | ✅ `feishu_parser.py` |
| 邮件 | .eml / .mbox | ✅ `email_parser.py` |
| 会议纪要 / 文档 | txt / md | ✅ `generic_chat_parser.py` |
| 直接粘贴 | 任意文本 | ✅ 无需工具 |

> 💡 **素材越原始越好**——聊天记录比会议纪要好，会议纪要比事后总结好。老板原话才是最有价值的信号。

---

## 📖 核心功能详解

### 🔨 蒸馏：从素材到Skill

**核心逻辑**：提炼的不是"老板说了什么"，而是"老板怎么看问题"。

Boss蒸馏把老板的隐含操作系统提取出来，组装成三部分：

#### Part A — Judgment（评判逻辑）

他怎么评判项目、方案、人？

```markdown
### 规则：业务牵头优先
- 标准：没有业务部门愿意牵头 = 假需求
- 原话：「先别做，等业务部门来牵头再说」
- 应用：评估新项目时，先看是否有业务方主动提需求
- 反面：只有技术团队自嗨的项目会被否掉
```

#### Part B — Management（向上管理）

你应该怎么跟他沟通？

```markdown
### 规则：报风险必须带方案
- ✅ 「进度延迟3天，计划通过X方式追回，需要Y资源」
- ❌ 「进度可能延迟」（只报问题不带方案会被质疑）
- Checklist：报风险时必须包含 [问题] [影响] [方案] [需要的支持]
```

#### Part C — Persona（表达风格）

他会怎么说？

```markdown
### 对话体
下属：「我们想做一个AI助手...」
老板：「等一下，业务部门提这个需求了吗？ROI算过吗？」

### 雷区
- ❌ 「这个很重要但是……」（在找借口）
- ❌ 只提问题不带方案（会被质问「你的建议呢？」）
```

#### 运行逻辑

```
收到问题 → Persona 判断语气 → Judgment 评项目 → Management 给行动建议 → 用老板风格输出
```

---

### 🎯 三个独立Skill入口

每个Boss Skill自动生成4个调用入口：

| 命令 | 干什么 |
|------|--------|
| `/{slug}` | 调用完整Skill |
| `/{slug}-judgment` | 只看老板的评判逻辑 |
| `/{slug}-management` | 只看向上管理建议 |
| `/{slug}-persona` | 只看老板的表达风格 |

这样你可以根据需要调用不同部分，不需要每次都跑完整流程。

---

### ✏️ 纠正与增量更新

#### 随时纠正

```
你：他不会这么说，他更直接
→ 修正 Persona 表达风格，重新验证

你：他不会先看这个，他先看ROI
→ 修正 Judgment 优先级，重新验证
```

纠正后自动重新跑场景模拟，确保改对了。

#### 增量更新

```
更新一下王总的skill，他最近开会说了一些新东西
```

- 保留原有高置信结论
- 新证据补充细节和边界条件
- 新旧冲突时按规则处理（支撑度对比）
- 输出三块patch：judgment_patch / management_patch / persona_patch

---

### 🧬 自进化机制

> **核心理念**：老板的风格不是一成不变的，Boss Skill也不应该是。让Skill在使用中持续学习。

#### 工作原理

```
你和Skill对话
  → 每次交互自动采集信号（新原话/纠正/新场景/确认）
  → 信号积累到阈值，自动触发进化
  → 新规则补充 / 旧规则修正 / 矛盾标记
  → 输出末尾附上进化报告
```

#### 信号采集

| 你说了什么 | Skill自动做了什么 |
|-----------|-----------------|
| "他不会这么说，他更直接" | 记录纠正信号，积累到3条后修正Persona |
| "今天开会老板说了一句'先看ROI'" | 记录新原话，积累到5条后提炼新Judgment规则 |
| "对，他就是这样的" | 确认现有规则，增加置信度 |
| 描述了一个新的决策场景 | 记录新场景，补充Skill未覆盖的情况 |

#### 进化报告示例

```
📋 Boss Skill 自进化报告（王总 v2 → v3）

  🆕 新增：Judgment「跨部门协作时他会先看谁牵头」（初步观察）
  ✏️ 修正：Persona「他不会说"考虑一下"，而是直接说"不行"」（基于3次纠正）
  ✅ 确认：Management「报风险必须带方案」（3次确认）
  ⚠️ 矛盾：Judgment说"看重ROI"，但新原话显示"更看重战略卡位"
```

#### 安全边界

| 保护机制 | 说明 |
|---------|------|
| 新规则标注"初步观察" | 必须≥3次验证才正式确认 |
| 核心规则不轻易改 | Layer 0和≥5次原话支撑的规则需≥3次直接矛盾 |
| 进化前自动备份 | 归档到 `versions/`，可随时回滚 |
| 可关闭自进化 | 在meta.json中设置 `"auto_evolve": false` |

---

### 🛡️ 边界条件处理

我们认真考虑了各种异常情况：

| 场景 | 处理方式 |
|------|---------|
| 素材不足（<5条） | 明确告知，只提取2-3个最可靠模式，其余标注"素材不足" |
| 工具解析失败 | 自动fallback到直接文本分析 |
| 素材含敏感信息 | 主动提醒脱敏，支持3级脱敏策略 |
| 素材过大（>1MB） | 分批处理，按时间或主题拆分 |
| 用户中途退出 | 自动保存进度，下次可恢复 |
| 新旧结论冲突 | 按支撑度对比规则处理，不随意覆盖 |

---

## 📁 文件结构

### create-boss 仓库结构

```
createBoss/
├── README.md                              # 你在这里
├── LICENSE                                # MIT开源协议
└── create-boss/                          # Skill主目录
    ├── SKILL.md                          # 蒸馏流程（核心入口）
    ├── meta.json                          # 元数据
    ├── requirements.txt                   # Python依赖
    ├── references/
    │   ├── skill-template.md              # Boss Skill标准模板（含自进化模块）
    │   ├── extraction-framework.md       # 提取框架和验证方法论
    │   └── prompts/                       # 提示词模板
    │       ├── intake.md                  # 基础信息录入
    │       ├── judgment_analyzer.md      # Judgment分析
    │       ├── judgment_builder.md        # Judgment生成
    │       ├── management_analyzer.md    # Management分析
    │       ├── management_builder.md      # Management生成
    │       ├── persona_analyzer.md        # Persona分析
    │       ├── persona_builder.md         # Persona生成
    │       ├── correction_handler.md     # 纠正处理
    │       └── merger.md                  # 增量合并
    └── tools/                            # 工具脚本
        ├── skill_writer.py               # Skill写入与管理
        ├── version_manager.py            # 版本管理
        ├── wechat_parser.py              # 微信解析
        ├── feishu_parser.py              # 飞书解析
        ├── email_parser.py               # 邮件解析
        └── generic_chat_parser.py        # 通用文本解析
```

### 生成的Boss Skill结构

```
bosses/{slug}/                              # 如 bosses/wang-zong/
├── SKILL.md                    # 完整组合版（含运行规则+自进化模块）
├── judgment.md                 # Part A: 项目评判逻辑
├── management.md               # Part B: 向上管理建议
├── persona.md                   # Part C: 表达与行为风格
├── judgment_skill.md           # Part A 独立Skill
├── management_skill.md         # Part B 独立Skill
├── persona_skill.md            # Part C 独立Skill
├── meta.json                    # 元数据（含进化统计）
├── evolution/                   # 🧬 自进化模块
│   ├── signals.jsonl           # 进化信号采集
│   └── evolution-log.jsonl     # 进化历史
├── versions/                    # 版本归档（每次更新自动备份）
└── knowledge/                   # 原始素材
    ├── chats/
    ├── docs/
    ├── emails/
    └── meetings/
```

---

## 💡 适用场景

| 场景 | 用Boss Skill做什么 |
|------|------------------|
| 📋 **评审前预演** | 让Skill模拟老板审方案，提前查漏补缺 |
| 📝 **汇报材料打磨** | 按老板认可的格式和逻辑写 |
| 💰 **争资源/争优先级** | 知道什么话术最能打动他 |
| ⚠️ **报坏消息** | 练习怎么向上报风险才不会被骂 |
| 🧑‍💻 **新人快速适应** | 3天搞懂老板风格，不用踩半年坑 |
| 🔄 **老板风格变了** | 增量更新，不用从头蒸馏 |
| 📈 **季度总结准备** | 了解老板关心什么指标，按他的逻辑组织材料 |
| 🎯 **跨部门协作** | 预判老板在跨团队项目中会怎么决策 |

---

## ❓ FAQ

**Q: 老板知道我在做这个吗？**
> 你自己的判断。用于个人学习（理解决策模式）通常没问题，用于模拟老板对外沟通需要谨慎。

**Q: 素材太少怎么办？**
> 少于5条交互记录时，只提取2-3个最可靠的模式，其余标注"素材不足"。60分的真实Skill > 90分的编造Skill。

**Q: 可以蒸馏自己吗？**
> 可以。但注意自我认知偏差——你可能高估某些特质、忽略盲点，建议补充身边人的评价。

**Q: 多个老板怎么管理？**
> 每个老板单独生成一个Skill，放在 `bosses/{slug}/` 目录下，互不干扰。

**Q: 数据安全吗？**
> 所有素材都保存在本地 `knowledge/` 目录，不会上传到任何服务器。你也可以随时设置脱敏。

**Q: Skill会过时吗？**
> 有自进化机制，Skill会在使用中持续学习。也可以随时手动增量更新。

---

## 🤝 贡献指南

欢迎提交Issue和Pull Request！

### 开发环境

```bash
# 克隆仓库
git clone https://github.com/zylucifer-2020/createBoss.git
cd createBoss/create-boss

# 安装依赖
pip install -r requirements.txt
```

### 项目结构

- `SKILL.md` — Skill主流程定义
- `references/` — 提示词模板和分析框架
- `tools/` — 解析和管理工具

### 提交规范

- `feat:` 新功能
- `fix:` Bug修复
- `docs:` 文档更新
- `refactor:` 代码重构
- `test:` 测试相关

---

## 📝 更新日志

### v3.0.0 (2026-04-17)
- ✨ **新增自进化机制**：Skill在使用中持续学习，越用越准
- 🆕 进化信号采集（新原话/纠正/场景/确认）
- 🆕 进化触发条件（3条纠正/5条新原话/7天+3条信号）
- 🆕 安全边界（新规则标注/核心规则保护/自动备份）
- 🆕 进化报告自动生成

### v2.0.0 (2026-04-16)
- ✨ 补充边界条件处理
- ✨ 强化检查点设计
- ✨ 补充三部分完整输出示例

### v1.0.0 (2026-04-15)
- 🎉 初始版本
- ✨ 蒸馏流程
- ✨ 三部分提取框架

---

## 📜 License

MIT License - 详见 [LICENSE](./LICENSE)

---

## 📬 联系方式

- 📧 邮箱：zylucifer2020@163.com
- 🐛 Bug报告：[GitHub Issues](https://github.com/zylucifer-2020/createBoss/issues)
- 💡 功能建议：[GitHub Discussions](https://github.com/zylucifer-2020/createBoss/discussions)
- ⭐ 欢迎Star：[GitHub Repository](https://github.com/zylucifer-2020/createBoss)

---

<div align="center">

**如果这个项目对你有帮助，欢迎 ⭐ Star！**

</div>
