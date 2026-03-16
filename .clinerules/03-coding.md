# 编码规范

## Python（后端）

### 基本规范
- 遵循 PEP 8 和项目已有的 flake8 配置
- 类型注解必须完整（函数参数和返回值）
- 使用 f-string 而非 format() 或 % 格式化
- 异步函数使用 async/await，避免回调地狱
- 错误处理：捕获具体异常类型，不要裸 except

### 代码风格
- 参考已有代码风格，保持一致
- 单个文件不超过 300 行，超过则考虑拆分
- 函数不超过 50 行，超过则考虑提取子函数
- 变量命名要有描述性，避免单字母变量（循环变量除外）

### 导入顺序
```python
# 1. 标准库
import os
import sys

# 2. 第三方库
import pytest
from fastapi import FastAPI

# 3. 本地模块
from copaw.agents import react_agent
from copaw.config import settings
```

## TypeScript（前端）

### 基本规范
- 严格模式（strict: true）
- 函数式 React 组件 + Hooks
- 使用项目已有的 ESLint 配置
- API 类型定义放在 `console/src/api/types/`

### 代码风格
- 组件文件名使用 PascalCase（如 `UserProfile.tsx`）
- 工具函数文件名使用 camelCase（如 `formatDate.ts`）
- 每个 React 组件一个文件
- Props 必须定义类型接口

### 示例
```typescript
// Good
interface UserCardProps {
  name: string;
  avatar?: string;
}

export function UserCard({ name, avatar }: UserCardProps) {
  return (
    <div className="user-card">
      <span>{name}</span>
    </div>
  );
}
```

## 通用原则

### 命名
- 变量/函数：使用描述性名称，避免缩写
- 常量：UPPER_SNAKE_CASE
- 类名：PascalCase
- 私有成员：_underscore_prefix

### 注释
- 只在"为什么"不明显时才写注释
- 不要解释"是什么"（代码应该自解释）
- 不要留 TODO 注释，要么做要么删除
- 函数文档用 docstring（Python）或 JSDoc（TypeScript）

### 代码组织
- 相关代码放在一起
- 避免循环依赖
- 保持单一职责原则