# 🧬 Boss Distill

**Put Your Boss "Into" AI — Make Decision Logic Reusable**

> Have you ever felt like this — your colleague's proposal passes in one try, but yours gets rejected eight times? Your boss always asks those same questions during reviews, but you can never predict which one they'll ask this time?

**It's not that you're not capable — it's that you haven't understood your boss's "operating system".**

📺 **Demo Video**: [![Watch Demo Video](https://img.shields.io/badge/Watch-Demo-00d9ff?style=for-the-badge)](https://zylucifer-2020.github.io/createBoss/demo.html)

Boss Distill does one simple thing: extract your boss's decision-making logic from your daily interactions with them — and package it into a reusable Skill that you can call on anytime.

[![Version](https://img.shields.io/badge/version-3.0.0-orange)](./meta.json)
[![License](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)
[![Platform](https://img.shields.io/badge/platform-CodeBuddy-blue)](https://codebuddy.cn)
[![GitHub Stars](https://img.shields.io/github/stars/zylucifer-2020/createBoss?style=social)](https://github.com/zylucifer-2020/createBoss)

---

## 📋 Table of Contents

- [✨ Features](#-features)
- [🚀 Quick Start](#-quick-start)
- [📖 Core Features](#-core-features)
  - [🔨 Distillation: From Materials to Skill](#-distillation-from-materials-to-skill)
  - [🎯 Three Independent Skill Entrypoints](#-three-independent-skill-entrypoints)
  - [✏️ Correction & Incremental Update](#️-correction--incremental-update)
  - [🧬 Self-Evolution Mechanism](#️-self-evolution-mechanism)
  - [🛡️ Edge Case Handling](#️-edge-case-handling)
- [📁 File Structure](#-file-structure)
- [💡 Use Cases](#-use-cases)
- [❓ FAQ](#-faq)
- [🤝 Contributing](#-contributing)
- [📝 Changelog](#-changelog)

---

## 🙏 Acknowledgments & References

This project was inspired by and references the following excellent projects:

| Project | GitHub | Reference |
|---------|--------|-----------|
| **boss-skills** | [vogtsw/boss-skills](https://github.com/vogtsw/boss-skills) | Boss distillation approach |
| **nuwa-skill** | [alchaincyf/nuwa-skill](https://github.com/alchaincyf/nuwa-skill) | Skill distillation framework |
| **darwin-skill** | [alchaincyf/darwin-skill](https://github.com/alchaincyf/darwin-skill) | Self-evolution mechanism |

Special thanks to the authors of these projects for their open-source contributions, which made this project possible.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Smart Distillation** | Extract boss's decision logic from chat logs/meeting notes/emails/annotations |
| **Three-Part Extraction** | Judgment (decision logic) + Management (upward management) + Persona (communication style) |
| **Self-Evolution** | Learns during use, becomes more accurate over time |
| **Incremental Update** | When boss has new tendencies, one-click supplement without starting over |
| **Smart Parsing** | Auto-parse WeChat/Feishu/email/generic text, multiple formats supported |
| **Version Control** | Auto-backup on every update, rollback anytime |

---

## 🚀 Quick Start

### Method 1: Copy Prompt to AI Agent (Recommended)

Copy the following prompt and send it to OpenClaw, hermes, Claude Code, or other AI agent:

```markdown
Please use the create-boss skill (https://github.com/zylucifer-2020/createBoss)
to help me distill my boss.

Steps:
1. First read SKILL.md to understand how to use the skill
2. Run the skill and follow the process to guide me through boss distillation
3. Save the generated Boss Skill to the bosses/ directory

My materials: [Paste chat logs/meeting notes/emails here]
```

### Method 2: Git Clone Local Install

```bash
# 1. Clone repository
git clone https://github.com/zylucifer-2020/createBoss.git
cd createBoss/create-boss

# 2. View files
ls -la

# 3. Copy SKILL.md content to your AI agent/CodeBuddy
# 4. Follow the distillation process in SKILL.md
```

### Supported Data Sources

| Source | Format | Auto-Parse |
|--------|--------|:----------:|
| WeChat Chat Logs | txt / html / csv | ✅ `wechat_parser.py` |
| Feishu Messages | JSON / txt / copied text | ✅ `feishu_parser.py` |
| Emails | .eml / .mbox | ✅ `email_parser.py` |
| Meeting Notes / Docs | txt / md | ✅ `generic_chat_parser.py` |
| Direct Paste | Any text | ✅ No tool needed |

> 💡 **The more raw, the better** — Chat logs are better than meeting notes, meeting notes are better than summaries. Boss's exact words are the most valuable signal.

---

## 📖 Core Features

### 🔨 Distillation: From Materials to Skill

**Core Logic**: Extract not "what the boss said", but "how the boss thinks".

Boss Distill extracts the boss's implicit operating system and assembles it into three parts:

#### Part A — Judgment (Decision Logic)

How does he evaluate projects, proposals, and people?

```markdown
### Rule: Business Ownership First
- Standard: No business department willing to lead = fake demand
- Quote: "Don't do it yet. Wait for the business department to take the lead."
- Application: When evaluating new projects, first check if business is willing to invest resources
- Counter-example: Projects with only tech team enthusiasm get rejected
```

#### Part B — Management (Upward Management)

How should you communicate with him?

```markdown
### Rule: Report Risks with Solutions
- ✅ "Delay is 3 days, plan to catch up via X method, need Y resources"
- ❌ "Progress might be delayed" (reporting only problems without solutions gets questioned)
- Checklist: When reporting risk, must include [Problem] [Impact] [Solution] [Support Needed]
```

#### Part C — Persona (Communication Style)

How would he say it?

```markdown
### Dialogue Example
Subordinate: "We want to build an AI assistant that can help customers..."
Boss: "Wait. Did the business department ask for this? Have you calculated the ROI?"

### Minefields
- ❌ "This is important but..." (making excuses)
- ❌ Only reporting problems without solutions (will be asked "What's your suggestion?")
```

#### Running Logic

```
Received Question → Persona checks tone → Judgment evaluates → Management provides action → Output in boss's style
```

---

### 🎯 Three Independent Skill Entrypoints

Each Boss Skill automatically generates 4 entrypoints:

| Command | Purpose |
|---------|---------|
| `/{slug}` | Call complete Skill |
| `/{slug}-judgment` | Only boss's decision logic |
| `/{slug}-management` | Only upward management suggestions |
| `/{slug}-persona` | Only boss's communication style |

---

### ✏️ Correction & Incremental Update

#### Correction Anytime

```
You: "He wouldn't say it that way, he's more direct"
→ Correct Persona communication style, re-verify

You: "He wouldn't look at this first, he looks at ROI first"
→ Correct Judgment priority, re-verify
```

Corrections automatically re-run scenario simulations to ensure correctness.

#### Incremental Update

```
Update wang-zong's skill, he said some new things in the meeting recently
```

- Keep original high-confidence conclusions
- New evidence supplements details and edge cases
- Conflicting old/new conclusions handled by rules (support comparison)
- Output three patches: judgment_patch / management_patch / persona_patch

---

### 🧬 Self-Evolution Mechanism

> **Core Philosophy**: Boss's style isn't static, neither should the Boss Skill be. Let the Skill learn continuously during use.

#### How It Works

```
You interact with Skill
  → Each interaction automatically collects signals (new quotes/corrections/scenarios/confirmations)
  → Signals accumulate to threshold, auto-trigger evolution
  → New rules added / old rules corrected / conflicts tagged
  → Evolution report attached at the end of output
```

#### Signal Collection

| What You Say | Skill Auto-Does |
|-------------|-----------------|
| "He wouldn't say it that way, he's more direct" | Records correction signal, modifies Persona after 3 corrections |
| "Boss said 'look at ROI first' in today's meeting" | Records new quote, extracts new Judgment rule after 5 quotes |
| "Yes, that's exactly how he is" | Confirms existing rule, increases confidence |
| Describe a new decision scenario | Records new scenario, supplements uncovered situations |

#### Evolution Report Example

```
📋 Boss Skill Evolution Report (wang-zong v2 → v3)

  🆕 Added: Judgment「When cross-team collaboration, he first checks who's leading」(preliminary observation)
  ✏️ Corrected: Persona「He wouldn't say 'let me think about it', he'd say 'no' directly」(based on 3 corrections)
  ✅ Confirmed: Management「Report risks with solutions」(3 confirmations)
  ⚠️ Conflict: Judgment says "cares about ROI", but new quotes show "cares more about strategic positioning"
```

#### Safety Boundaries

| Protection | Description |
|-----------|-------------|
| New rules marked "preliminary observation" | Must be verified ≥3 times to be officially confirmed |
| Core rules not easily changed | Layer 0 and rules with ≥5 quote supports need ≥3 direct contradictions |
| Auto-backup before evolution | Archived to `versions/`, rollback anytime |
| Evolution can be disabled | Set `"auto_evolve": false` in meta.json |

---

### 🛡️ Edge Case Handling

We carefully considered various exceptional situations:

| Scenario | Handling |
|----------|----------|
| Insufficient materials (<5) | Clearly state, extract only 2-3 most reliable patterns, mark others as "insufficient material" |
| Tool parsing failure | Auto-fallback to direct text analysis |
| Materials contain sensitive info | Proactively remind about data masking, 3-level masking supported |
| Materials too large (>1MB) | Process in batches, split by time or topic |
| User exits mid-process | Auto-save progress, resume next time |
| Old/new conclusion conflicts | Handle by support comparison rules, don't overwrite arbitrarily |

---

## 📁 File Structure

### create-boss Repository Structure

```
createBoss/
├── README.md                              # This file
├── README_en.md                          # English version
├── LICENSE                               # MIT License
└── create-boss/                         # Skill main directory
    ├── SKILL.md                          # Distillation process (core entry)
    ├── meta.json                          # Metadata
    ├── requirements.txt                   # Python dependencies
    ├── references/
    │   ├── skill-template.md              # Boss Skill template (with self-evolution)
    │   ├── extraction-framework.md       # Extraction framework
    │   └── prompts/                      # Prompt templates
    └── tools/                             # Utility scripts
        ├── skill_writer.py               # Skill management
        ├── version_manager.py            # Version control
        ├── wechat_parser.py              # WeChat parser
        ├── feishu_parser.py              # Feishu parser
        ├── email_parser.py               # Email parser
        └── generic_chat_parser.py        # Generic text parser
```

### Generated Boss Skill Structure

```
bosses/{slug}/                              # e.g., bosses/wang-zong/
├── SKILL.md                    # Complete version (with rules + self-evolution)
├── judgment.md                 # Part A: Decision logic
├── management.md               # Part B: Upward management
├── persona.md                  # Part C: Communication style
├── *_skill.md                 # Three independent Skills
├── meta.json                   # Metadata (with evolution stats)
├── evolution/                   # 🧬 Self-evolution
│   ├── signals.jsonl          # Evolution signal collection
│   └── evolution-log.jsonl     # Evolution history
├── versions/                   # Version archives
└── knowledge/                  # Raw materials
```

---

## 💡 Use Cases

| Scenario | What to Do with Boss Skill |
|----------|---------------------------|
| 📋 **Pre-review rehearsal** | Let Skill simulate boss reviewing proposal, find gaps in advance |
| 📝 **Report writing** | Write according to boss's preferred format and logic |
| 💰 **Resource/priority negotiation** | Know which rhetoric works best with him |
| ⚠️ **Delivering bad news** | Practice how to report risks without being scolded |
| 🧑‍💻 **New employee onboarding** | Understand boss's style in 3 days instead of 6 months |
| 🔄 **Boss's style changed** | Incremental update, don't start from scratch |
| 📈 **Quarterly review prep** | Know what metrics boss cares about, organize materials by his logic |
| 🎯 **Cross-team collaboration** | Predict how boss will decide in cross-team projects |

---

## ❓ FAQ

**Q: Does my boss know I'm doing this?**
> That's your call. Using it for personal learning (understanding decision patterns) is usually fine. Using it to simulate boss for external communication requires caution.

**Q: What if I don't have enough materials?**
> With fewer than 5 interaction records, extract only 2-3 most reliable patterns, mark others as "insufficient material". A 60-point real Skill > a 90-point fabricated Skill.

**Q: Can I distill myself?**
> Yes. But be aware of self-perception bias — you may overestimate certain traits and ignore blind spots. Supplement with feedback from colleagues.

**Q: How to manage multiple bosses?**
> Each boss gets a separate Skill, stored in `bosses/{slug}/` directory, no interference.

**Q: Is my data safe?**
> All materials are saved locally in `knowledge/` directory, never uploaded to any server. You can also set data masking anytime.

**Q: Will the Skill become outdated?**
> The self-evolution mechanism ensures the Skill learns continuously during use. You can also manually trigger incremental updates.

---

## 🤝 Contributing

Contributions welcome! Please submit Issues and Pull Requests.

### Development Setup

```bash
# Clone repository
git clone https://github.com/zylucifer-2020/createBoss.git
cd createBoss/create-boss

# Install dependencies
pip install -r requirements.txt
```

### Commit Conventions

| Prefix | Description |
|--------|-------------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation |
| `refactor:` | Code refactoring |
| `test:` | Tests |
| `perf:` | Performance |

---

## 📝 Changelog

### v3.0.0 (2026-04-17)
- ✨ **New Self-Evolution Mechanism**: Skill learns continuously during use
- 🆕 Evolution signal collection (new quotes/corrections/scenarios/confirmations)
- 🆕 Evolution trigger conditions (3 corrections/5 new quotes/7 days + 3 signals)
- 🆕 Safety boundaries (new rule marking/core rule protection/auto-backup)
- 🆕 Auto-generated evolution reports

### v2.0.0 (2026-04-16)
- ✨ Edge case handling
- ✨ Checkpoint design reinforcement
- ✨ Complete output examples for all three parts

### v1.0.0 (2026-04-15)
- 🎉 Initial release
- ✨ Distillation process
- ✨ Three-part extraction framework

---

## 📜 License

MIT License - See [LICENSE](./LICENSE)

---

## 📬 Contact

- 📧 Email: zylucifer2020@163.com
- 🐛 Bug Report: [GitHub Issues](https://github.com/zylucifer-2020/createBoss/issues)
- 💡 Feature Request: [GitHub Discussions](https://github.com/zylucifer-2020/createBoss/discussions)
- ⭐ Star: [GitHub Repository](https://github.com/zylucifer-2020/createBoss)

---

<div align="center">

**If this project helps you, feel free to ⭐ Star!**

</div>
