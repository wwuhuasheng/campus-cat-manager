# 📝 校园流浪猫管理系统 API 契约 v2.0

**核心原则**：前后端所有字段名必须严格一致（建议使用小写下划线 `snake_case`），严禁擅自修改。

## 1. 核心数据模型 (Data Model)

所有关于猫咪的信息必须包含以下五个维度：

| 字段名 (Field) | 类型 (Type) | 说明 (Description) | 示例 (Example) |
| --- | --- | --- | --- |
| `nickname` | string | 猫咪昵称 | "大黄" |
| `location` | string | 活动位置（最后目击点） | "图书馆北门" |
| `health_status` | string | 健康状况 | "良好 / 需绝育 / 皮肤病" |
| `risk_level` | int | 风险等级 (0:温顺, 1:警惕, 2:应激/咬人) | 0 |
| `register_time` | string | 登记时间 (ISO 8601格式) | "2026-03-08T18:30:00Z" |

---

## 2. 接口契约 (API Endpoints)

### 🟢 接口 A：获取猫咪全量列表

* **URL**: `GET /api/cats`
* **功能**: 前端打开首页时，拉取所有已登记的猫咪。
* **后端返回 (JSON)**:
```json
[
  {
    "nickname": "大黄",
    "location": "图书馆",
    "health_status": "健康",
    "risk_level": 0,
    "register_time": "2026-03-08T10:00:00Z"
  },
  {
    "nickname": "刀疤",
    "location": "后勤处",
    "health_status": "左眼受伤",
    "risk_level": 2,
    "register_time": "2026-03-08T11:20:00Z"
  }
]

```



### 🔵 接口 B：登记/上报新猫咪

* **URL**: `POST /api/cats`
* **功能**: 用户在 Flutter 填写完表单后提交。
* **前端发送 (JSON)**:
```json
{
  "nickname": "小黑",
  "location": "宿舍5栋",
  "health_status": "健康",
  "risk_level": 1
}

```


* **后端返回**: `{ "code": 200, "msg": "登记成功" }`

---

## 3. 给三位组员的特别说明

### 👤 组员 A (Flutter 前端)

* **任务**：在 Flutter 中定义一个 `Cat` 类，字段要和上面的模型一模一样。
* **重点**：当 `risk_level` 为 `2` 时，前端界面必须用 **醒目的红色** 标注“应激/危险”，提醒同学不要随意抚摸。
* **时间处理**：提交时如果不传 `register_time`，则由后端自动生成。

### 👤 组员 B (Go 后端)

* **任务**：在 Go 中定义 `Cat` 结构体（Struct），并加上 JSON 标签。
```go
type Cat struct {
    Nickname     string `json:"nickname"`
    Location     string `json:"location"`
    HealthStatus string `json:"health_status"`
    RiskLevel    int    `json:"risk_level"`
    RegisterTime string `json:"register_time"`
}

```


* **重点**：务必开启 **CORS（跨域）** 允许组员 A 的访问。

