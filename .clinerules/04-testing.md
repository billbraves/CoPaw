# 测试规范（TDD）

## 铁律

**没有失败的测试，不写生产代码。**

如果你先写了代码再补测试？删掉代码，从测试重新开始。不保留、不参考、不"调整"。

## Red-Green-Refactor 循环

### 🔴 RED — 先写测试

1. 一个测试只测一个行为
2. 测试名要清晰描述期望行为
3. 用真实代码，避免不必要的 mock

```python
# 示例：测试重试逻辑
@pytest.mark.asyncio
async def test_retry_operation_retries_3_times_on_failure():
    """重试失败操作应该重试3次"""
    attempts = 0

    async def failing_operation():
        nonlocal attempts
        attempts += 1
        if attempts < 3:
            raise ValueError("temporary error")
        return "success"

    result = await retry_operation(failing_operation, max_retries=3)

    assert result == "success"
    assert attempts == 3
```

### 运行测试，确认失败

```bash
python -m pytest tests/path/to/test.py -v
```

**必须看到测试失败**，且失败原因是功能缺失（不是语法错误或其他问题）。

如果测试意外通过，说明：
- 测试写得有问题
- 功能已经存在
- 测试没有真正验证期望的行为

### 🟢 GREEN — 写最少代码

1. 只写刚好让测试通过的代码
2. 不要提前优化
3. 不要加额外功能（YAGNI）
4. 不要过度设计

```python
# 最小实现（刚好让测试通过）
async def retry_operation(func, max_retries=3):
    for i in range(max_retries):
        try:
            return await func()
        except Exception as e:
            if i == max_retries - 1:
                raise e
```

### 运行测试，确认通过

```bash
python -m pytest tests/ -v
```

确认：
- 新测试通过 ✅
- 所有旧测试也通过 ✅

### 🔵 REFACTOR — 清理代码

1. 去除重复
2. 改善命名
3. 提取函数/常量
4. 简化逻辑

**重构期间测试必须保持绿色。**

每次重构后运行测试，确保没有破坏功能。

## 测试位置

| 类型 | 位置 | 命名 |
|------|------|------|
| 单元测试 | `tests/unit/` | `test_<模块名>.py` |
| 集成测试 | `tests/integrated/` | `test_<功能名>.py` |

## 测试命名规范

```python
# 格式：test_<被测功能>_<场景>_<期望结果>
def test_parse_config_with_valid_file_returns_config():
    pass

def test_parse_config_with_missing_file_raises_error():
    pass

def test_retry_operation_with_timeout_raises_timeout_error():
    pass
```

## 测试结构（AAA 模式）

```python
def test_feature_scenario_expected_result():
    # Arrange（准备）
    input_data = "test input"
    expected = "expected output"

    # Act（执行）
    result = function_under_test(input_data)

    # Assert（断言）
    assert result == expected
```

## 例外情况（需用户确认）

以下情况可以不写测试：
- 纯配置文件修改
- 一次性迁移脚本
- UI 样式微调
- 文档更新

## 禁止行为

- ❌ 先写代码，后补测试
- ❌ 为了让测试通过而修改测试（除非测试本身有 bug）
- ❌ 跳过 RED 阶段，不确认测试失败
- ❌ 在 REFACTOR 阶段添加新功能
- ❌ 使用大量 mock 导致测试失去意义