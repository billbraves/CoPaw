# Git 提交规范

## 提交信息格式

```
<type>(<scope>): <description>

[可选正文]
```

### 类型（type）

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | feat(agent): 添加记忆管理功能 |
| `fix` | Bug 修复 | fix(cli): 修复命令行参数解析错误 |
| `docs` | 文档更新 | docs: 更新 README 安装说明 |
| `refactor` | 重构（不改变功能） | refactor(skills): 简化技能注册逻辑 |
| `test` | 测试相关 | test(memory): 添加记忆检索单元测试 |
| `chore` | 杂项（构建、配置等） | chore: 更新依赖版本 |
| `style` | 代码格式（不影响逻辑） | style: 统一缩进为 4 空格 |
| `perf` | 性能优化 | perf(router): 优化路由匹配性能 |

### 范围（scope）

可选，表示影响的模块：
- `agent` — Agent 核心
- `skills` — 技能系统
- `tools` — 工具定义
- `memory` — 记忆管理
- `cli` — 命令行界面
- `app` — Web 应用
- `api` — API 路由
- `mcp` — MCP 服务器
- `console` — 前端控制台

### 示例

```
feat(skills): 添加代码审查技能

- 支持自动检测代码风格问题
- 支持检测潜在 bug
- 生成审查报告

Closes #123
```

```
fix(memory): 修复记忆检索时的空指针异常

在检索空记忆列表时会抛出 NullPointerException，
现在会正确返回空列表而不是抛出异常。
```

## 提交规则

### 原子性
- 每个提交只做一件事
- 每个原子任务一个 commit
- 不要把不相关的改动放在一起

### 提交前检查
- [ ] 所有测试通过
- [ ] 没有 lint 错误
- [ ] 代码格式符合项目规范
- [ ] 提交信息清晰描述了改动

### 语言
- 提交信息用英文
- 提交正文可以用中文或英文
- 保持项目已有风格一致

## 禁止行为

- ❌ 提交带有 `console.log`、`print` 等调试代码
- ❌ 提交带有 `TODO`、`FIXME` 等未完成标记
- ❌ 提交超大改动（应该拆分为多个原子提交）
- ❌ 提交信息模糊（如 "fix bug"、"update code"）
- ❌ 提交不相关的改动（如功能开发和配置修改混在一起）

## 分支命名

```
feature/xxx    # 新功能
fix/xxx        # Bug 修复
refactor/xxx   # 重构
docs/xxx       # 文档更新
```

## 工作流

1. 从 main 创建功能分支
2. 每个原子任务完成后 commit
3. 功能完成后创建 PR
4. 代码审查通过后合并
5. 删除功能分支