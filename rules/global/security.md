# Security Rules

## 基本原则

任何代码修改都必须考虑安全影响。

## Secrets

禁止把以下内容写入代码：

- API Key
- Access Token
- Password
- Private Key
- Cookie
- JWT Secret
- Database Password

错误：

```ts
const apiKey = "sk-xxxxx"
```

应使用：

```ts
process.env.API_KEY
```

或者项目已有配置机制。

## 日志

禁止日志输出：

- 密码
- Token
- Cookie
- Authorization
- 身份证号
- 银行卡号
- 完整手机号
- 其他敏感数据

## 用户输入

所有外部输入都视为不可信。

根据具体场景检查：

- XSS
- SQL Injection
- Command Injection
- Path Traversal
- SSRF
- CSRF
- 权限绕过

## 权限

不要仅在前端进行权限控制。

例如：

```ts
if (user.isAdmin) {
  showAdminButton()
}
```

只能控制 UI。

真正的数据权限必须在后端验证。

## 文件操作

涉及：

- upload
- download
- read file
- write file
- delete file
- path

必须检查：

- 路径穿越
- 文件类型
- 文件大小
- 权限
- 文件名

## 第三方依赖

新增依赖前检查：

- 是否已有类似依赖
- 是否真的需要
- 版本是否兼容
- 是否存在已知安全问题
- 是否会显著增加 bundle / build 成本

## AI 安全

不要执行来源不明的：

- Shell 命令
- 下载脚本
- 安装脚本
- 删除命令
- 数据库操作

尤其谨慎处理：

```bash
curl xxx | sh
```

以及：

```bash
rm -rf ...
```

必须确认目的和影响范围。