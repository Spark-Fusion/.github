# Git 规范流程

本文档定义了燃点聚变组织的 Git 工作流程与规范，旨在确保团队协作的高效性和代码质量。

## 目录

- [分支管理](#分支管理)
- [提交规范](#提交规范)
- [代码审查](#代码审查)
- [发布流程](#发布流程)
- [常见问题](#常见问题)

## 分支管理

### 分支命名规范

- **主分支**：`main` 或 `master` - 生产环境代码，保持稳定
- **开发分支**：`develop` - 开发环境代码，集成最新功能
- **功能分支**：`feature/功能名称` - 新功能开发
- **修复分支**：`fix/问题描述` - Bug 修复
- **热修复分支**：`hotfix/问题描述` - 紧急生产问题修复
- **发布分支**：`release/版本号` - 版本发布准备

### 分支策略

1. **功能开发流程**
   ```
   main → develop → feature/xxx → develop → main
   ```

2. **Bug 修复流程**
   ```
   main → fix/xxx → develop → main
   ```

3. **紧急修复流程**
   ```
   main → hotfix/xxx → main (同时合并到 develop)
   ```

### 分支操作规范

- 从 `develop` 分支创建功能分支
- 功能完成后，通过 Pull Request 合并到 `develop`
- 定期同步 `develop` 分支的最新代码
- 删除已合并的分支，保持仓库整洁

## 提交规范

### 提交信息格式

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### 提交类型（type）

- `feat`: 新功能
- `fix`: Bug 修复
- `docs`: 文档更新
- `style`: 代码格式调整（不影响功能）
- `refactor`: 代码重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建过程或辅助工具的变动
- `ci`: CI/CD 相关

### 提交示例

```bash
# 新功能
git commit -m "feat(auth): 添加用户登录功能"

# Bug 修复
git commit -m "fix(api): 修复数据查询接口超时问题"

# 文档更新
git commit -m "docs(readme): 更新项目说明文档"

# 代码重构
git commit -m "refactor(utils): 重构工具函数模块"
```

### 提交规范要求

- 提交信息使用中文或英文，保持一致性
- 主题行不超过 50 个字符
- 主题行使用祈使语气（如：添加、修复、更新）
- 详细说明放在正文中，每行不超过 72 个字符
- 多个提交应逻辑清晰，避免大而全的提交

## 代码审查

### Pull Request 规范

1. **PR 标题格式**
   ```
   <type>(<scope>): <description>
   ```
   例如：`feat(user): 添加用户头像上传功能`

2. **PR 描述模板**
   ```markdown
   ## 变更说明
   - 描述本次变更的主要内容
   
   ## 相关 Issue
   - 关联的 Issue 编号
   
   ## 测试说明
   - 测试步骤和结果
   
   ## 截图（如适用）
   - 添加相关截图
   ```

3. **PR 要求**
   - 确保代码通过所有测试
   - 确保代码符合项目规范
   - 添加必要的测试用例
   - 更新相关文档
   - 至少需要一名团队成员审查通过

### 审查检查清单

- [ ] 代码符合项目编码规范
- [ ] 功能实现正确且完整
- [ ] 包含必要的测试用例
- [ ] 文档已更新
- [ ] 没有引入新的警告或错误
- [ ] 性能影响已考虑
- [ ] 安全性问题已检查

## 发布流程

### 版本号规范

遵循 [语义化版本](https://semver.org/lang/zh-CN/) 规范：`主版本号.次版本号.修订号`

- **主版本号**：不兼容的 API 修改
- **次版本号**：向下兼容的功能性新增
- **修订号**：向下兼容的问题修正

### 发布步骤

1. **创建发布分支**
   ```bash
   git checkout -b release/v1.0.0 develop
   ```

2. **更新版本号**
   - 更新 `package.json`、`CHANGELOG.md` 等文件
   - 提交版本更新

3. **测试验证**
   - 在发布分支上进行完整测试
   - 修复发现的问题

4. **合并到主分支**
   ```bash
   git checkout main
   git merge --no-ff release/v1.0.0
   git tag -a v1.0.0 -m "Release version 1.0.0"
   ```

5. **同步到开发分支**
   ```bash
   git checkout develop
   git merge --no-ff release/v1.0.0
   ```

6. **删除发布分支**
   ```bash
   git branch -d release/v1.0.0
   ```

## 常见问题

### Q: 如何撤销上一次提交？

**A:** 根据情况选择：

```bash
# 撤销提交但保留更改
git reset --soft HEAD~1

# 撤销提交并丢弃更改（谨慎使用）
git reset --hard HEAD~1
```

### Q: 如何修改上一次提交信息？

**A:**
```bash
git commit --amend -m "新的提交信息"
```

### Q: 如何合并多个提交？

**A:** 使用交互式 rebase：
```bash
git rebase -i HEAD~n  # n 为要合并的提交数量
```

### Q: 如何同步远程分支？

**A:**
```bash
# 获取远程更新
git fetch origin

# 合并远程分支
git merge origin/branch-name

# 或使用 rebase
git rebase origin/branch-name
```

### Q: 冲突如何解决？

**A:**
1. 先拉取最新代码：`git pull origin branch-name`
2. 解决冲突文件中的冲突标记
3. 添加解决后的文件：`git add .`
4. 完成合并：`git commit`

## 最佳实践

1. **频繁提交**：小步快跑，频繁提交代码
2. **清晰描述**：提交信息要清晰描述变更内容
3. **及时同步**：定期同步远程分支，避免冲突积累
4. **代码审查**：所有代码变更都应经过审查
5. **保持整洁**：及时删除已合并的分支
6. **备份重要变更**：重要功能开发前创建备份分支

---

*最后更新：2026年*

