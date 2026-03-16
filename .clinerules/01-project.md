# CoPaw 项目概况

## 项目简介
CoPaw 是一个 AI 编码 Agent，支持多通道交互（CLI、Web、Slack 等），具备技能系统、记忆管理和 MCP 工具扩展能力。

## 技术栈

### 后端
- **语言**: Python 3.10+
- **框架**: FastAPI
- **Agent 核心**: LangGraph (ReAct Agent 架构)
- **LLM**: 支持多种模型（通过 routing_chat_model.py 路由）
- **测试**: pytest

### 前端
- **框架**: React + TypeScript
- **构建工具**: Vite
- **位置**: console/ 目录

### 部署
- Docker + Supervisor

## 项目结构

```
CoPaw/
├── src/copaw/
│   ├── agents/           # Agent 核心逻辑
│   │   ├── skills/       # 技能系统
│   │   ├── tools/        # 工具定义
│   │   ├── memory/       # 记忆管理
│   │   ├── prompts/      # 提示词模板
│   │   └── react_agent.py # 核心 Agent 实现
│   ├── app/              # Web 应用
│   │   ├── routers/      # API 路由
│   │   ├── channels/      # 通道（CLI、Web、Slack）
│   │   ├── approval/      # 审批机制
│   │   └── mcp/           # MCP 服务器
│   ├── cli/              # 命令行界面
│   └── config/           # 配置管理
├── console/              # 前端控制台
│   └── src/
├── tests/                # 测试
│   ├── unit/             # 单元测试
│   └── integrated/       # 集成测试
├── docs/                 # 文档
└── pyproject.toml        # Python 项目配置
```

## 关键文件
- `pyproject.toml` — Python 依赖和项目配置
- `console/package.json` — 前端依赖
- `src/copaw/agents/prompt.py` — Agent 提示词
- `src/copaw/agents/react_agent.py` — 核心 Agent 逻辑
- `src/copaw/agents/routing_chat_model.py` — 模型路由

## 开发命令
```bash
# 安装依赖
uv sync

# 运行测试
python -m pytest tests/ -v

# 运行 lint
flake8 src/

# 启动 CLI
python -m copaw

# 启动 Web
python -m copaw.app