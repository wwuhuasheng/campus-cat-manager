# 校园流浪猫项目 API 契约 v1.0

### 1. 猫咪信息模型
- name: string (名字)
- status: int (0:健康, 1:需救助)
- location: string (出现地点)

### 2. 获取猫咪列表接口
- URL: `GET /api/cats`
- 返回格式: `[{"name": "大黄", "status": 0, "location": "图书馆"}]`

### 3. 提交新猫咪接口
- URL: `POST /api/cats`
- 参数: 同上模型
