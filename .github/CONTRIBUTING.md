# 贡献指南

感谢你对 Boss蒸馏 的兴趣！欢迎提交 Issue 和 Pull Request。

## 开发环境

```bash
# 克隆仓库
git clone https://github.com/zylucifer-2020/createBoss.git
cd createBoss/create-boss

# 安装依赖
pip install -r requirements.txt
```

## 项目结构

```
create-boss/
├── SKILL.md              # Skill主流程定义（核心入口）
├── references/            # 提示词模板和分析框架
│   ├── skill-template.md
│   ├── extraction-framework.md
│   └── prompts/          # 各部分的提示词模板
└── tools/                # 解析和管理工具脚本
```

## 提交规范

请使用以下前缀：

| 前缀 | 说明 |
|------|------|
| `feat:` | 新功能 |
| `fix:` | Bug修复 |
| `docs:` | 文档更新 |
| `refactor:` | 代码重构（不影响功能） |
| `test:` | 测试相关 |
| `perf:` | 性能优化 |
| `style:` | 代码格式调整 |

### 示例

```
feat: 添加微信聊天记录解析器
fix: 修复素材不足时的提示文案
docs: 更新README添加安装说明
```

## Pull Request 流程

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交你的改动 (`git commit -m 'feat: 添加xxx'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 创建 Pull Request

## 问题反馈

- 🐛 Bug报告：[GitHub Issues](https://github.com/zylucifer-2020/createBoss/issues)
- 💡 功能建议：[GitHub Discussions](https://github.com/zylucifer-2020/createBoss/discussions)

## 测试

在提交前，请确保：

1. SKILL.md 语法正确
2. 新增功能有对应的提示词模板
3. README 文档已同步更新

---

再次感谢你的贡献！🎉
