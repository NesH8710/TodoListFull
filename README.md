# TodoListFull

使用 Java Spring Boot 作為後端，Vue 3 + Tailwind CSS 作為前端的 TodoList 應用系統。支援待辦事項 CRUD、完成狀態切換與狀態管理。

---

## 後端
- Java 8
- Spring Boot
- Spring Security（JWT 認證）
- Spring Data JPA
- PostgreSQL
- Lombok

## 前端
- Vue 3 (Composition API)
- Tailwind CSS
- Vite 開發工具
- axios API

## 環境設定

### 建立資料庫

先於 PostgreSQL 建立一個資料庫（例如 `todolist_db`）：

```sql
CREATE DATABASE todolist_db;
```

## 預計實作
- 使用者註冊、登入
- JWT驗證
- pinia狀態管理