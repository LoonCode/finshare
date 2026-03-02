# 发布指南

本文档说明如何发布新版本到 PyPI。

## 前置条件

1. 在 GitHub 仓库中配置 `PYPI_API_TOKEN` secret
   - 访问 https://pypi.org/manage/account/token/ 创建 API token
   - 在 https://github.com/finvfamily/finshare/settings/secrets/actions 添加 secret

## 发布方式

### 方式 1: 手动触发（推荐）

访问 https://github.com/finvfamily/finshare/actions/workflows/publish.yml

点击 "Run workflow"，有三种选项：

#### 选项 A: 指定版本号
- **version**: 输入具体版本号，如 `0.1.2`
- **version_type**: 忽略此选项

#### 选项 B: 自动递增版本号
- **version**: 留空
- **version_type**: 选择递增类型
  - `patch`: 0.1.0 → 0.1.1（修复 bug）
  - `minor`: 0.1.0 → 0.2.0（新功能）
  - `major`: 0.1.0 → 1.0.0（重大变更）

#### 选项 C: 使用默认设置
- 两个选项都留空，默认执行 patch 递增

### 方式 2: 创建 Release

1. 访问 https://github.com/finvfamily/finshare/releases/new
2. 创建新 tag，格式：`v0.1.2`
3. 填写 Release 标题和说明
4. 点击 "Publish release"
5. 自动触发发布流程，使用 tag 中的版本号

## 发布流程

1. 读取当前版本号
2. 根据输入确定新版本号
3. 更新 `finshare/__version__.py`
4. 构建 Python 包
5. 上传到 PyPI
6. 提交版本号更新到 Git（仅手动触发时）

## 版本号规范

遵循 [语义化版本](https://semver.org/lang/zh-CN/)：

- **MAJOR**: 不兼容的 API 变更
- **MINOR**: 向下兼容的功能新增
- **PATCH**: 向下兼容的问题修正

## 示例

### 发布 bug 修复版本
```
当前版本: 0.1.0
操作: Run workflow → version 留空 → version_type 选 patch
结果: 0.1.1
```

### 发布新功能版本
```
当前版本: 0.1.1
操作: Run workflow → version 留空 → version_type 选 minor
结果: 0.2.0
```

### 发布指定版本
```
当前版本: 0.2.0
操作: Run workflow → version 输入 1.0.0 → version_type 忽略
结果: 1.0.0
```

## 验证发布

发布成功后：

1. 检查 PyPI: https://pypi.org/project/finshare/
2. 测试安装: `pip install finshare==新版本号`
3. 验证版本: `python -c "import finshare; print(finshare.__version__)"`

## 故障排查

### 认证失败
- 检查 `PYPI_API_TOKEN` secret 是否正确配置
- 确认 token 有上传权限

### 版本冲突
- PyPI 不允许重复上传相同版本
- 需要递增版本号重新发布

### 构建失败
- 检查 `pyproject.toml` 和 `setup.py` 配置
- 查看 Actions 日志获取详细错误信息
