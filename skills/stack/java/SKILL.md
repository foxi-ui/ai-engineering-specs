---
name: java
description: Java / Spring Boot 项目修改代码前的检查项：确认 Java 与 Spring Boot 版本及构建工具，保持 Controller → Service → Repository 分层，区分 Request DTO / Entity / Response VO，注意事务边界、N+1 与 SQL 注入，不随意升级 Maven 依赖
---

# Java Development Skill

## 开始前检查

确认：

```text
Java version
Maven / Gradle
Spring Boot version
Database
ORM
Architecture
```

例如：

```text
Java 8
Java 11
Java 17
Java 21
```

不要默认可以使用最新 Java API。

---

## Architecture

优先理解项目已有结构：

```text
Controller
↓
Service
↓
Repository / Mapper
↓
Database
```

不要在没有必要时改变架构。

---

## DTO / VO / Entity

职责明确：

```text
Request DTO
↓
Domain / Service
↓
Entity
↓
Response VO
```

避免直接把 Entity 当 API Response。

---

## Controller

Controller 主要负责：

- 参数接收
- 参数校验
- 调用 Service
- 返回结果

不要把大量业务逻辑写在 Controller。

---

## Service

Service 负责业务逻辑。

复杂事务明确：

```java
@Transactional
```

使用事务前确认事务边界。

---

## Database

检查：

- SQL Injection
- Transaction
- N+1
- Index
- Pagination
- Lock
- Connection Pool

---

## Exception

不要简单：

```java
catch (Exception e) {
    e.printStackTrace();
}
```

使用项目已有异常体系和日志体系。

---

## Dependency

修改 Maven 依赖前检查：

```text
pom.xml
dependencyManagement
parent
Spring Boot version
```

避免随意升级。

---

## 验证

根据项目：

```bash
./mvnw test
./mvnw verify
./mvnw package
```

或者使用项目已有脚本。
