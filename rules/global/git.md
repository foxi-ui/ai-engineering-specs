# Git Rules

## 基本原则

每次修改前先检查：

```bash
git status
git branch --show-current
git diff
```

理解当前工作区状态后再修改。

## 不覆盖用户修改

如果工作区存在用户未提交修改：

- 不要覆盖
- 不要 reset
- 不要 checkout 用户修改
- 不要删除未知文件
- 不要自动 stash

除非用户明确要求。

## 修改范围

任务完成后检查：

```bash
git diff --stat
git diff
git diff --check
```

确认：

- 没有无关文件
- 没有调试代码
- 没有临时文件
- 没有意外格式化整个文件
- 没有意外修改 lock 文件
- 没有意外修改配置

## Commit

如果用户没有要求，不主动提交 commit。

如果用户要求提交：

1. 先运行验证
2. 检查 diff
3. 使用清晰的 commit message

推荐：

```text
feat: add xxx
fix: resolve xxx
refactor: simplify xxx
test: add xxx tests
docs: update xxx
chore: update xxx
```

## 禁止危险操作

未经明确要求禁止：

```bash
git reset --hard
git clean -fd
git checkout -- .
git restore .
git push --force
```

尤其不能使用这些命令清理用户已有修改。