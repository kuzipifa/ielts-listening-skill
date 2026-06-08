# Frontend Data Boundary

这个文档定义公开前端第一版需要的数据范围。目标是先确定产品表面，再定向脱敏，而不是先清理全部私人内容。

## 第一版页面

1. Dashboard
   - 今日任务
   - 22:00 截止状态
   - 完成率
   - 最近成绩
   - 错题数量
   - 抽查通过率

2. 提交作业
   - 今日任务勾选
   - 拼写自测结果
   - 今日反思
   - 生成标准 Skill 输入文本

3. Chat
   - 发送用户消息
   - 展示 Noah / 听力老师回复
   - 后续接入 LLM 和 Skill 上下文

4. 错题库
   - 错因分布
   - 错题列表
   - 抽查状态

5. 周计划
   - 周内每日任务
   - 核心任务标记
   - 完成状态

## 公开仓库可保留

- `SKILL.md` 的通用模板版本
- `persona/persona.template.md`
- `references/` 中不含私人关系和真实经历的通用教学规则
- `data.example/` 或 `app` 内 demo 数据
- 前端代码
- 启动说明

## 不公开

- `persona/persona.md`
- `data/`
- 真实每日作业
- 真实错题原句和个人 take-away
- 真实关系状态、diary、奖惩记录
- API key 和本地环境变量

当前 `.gitignore` 已忽略 `persona/persona.md` 和 `data/`。后续如果新增真实运行目录，建议继续忽略：

```gitignore
private/
.env
.env.local
```

## 建议 API 合约

```text
GET  /api/dashboard
GET  /api/plan/today
GET  /api/errors/summary
POST /api/homework/preview
POST /api/homework/submit
POST /api/chat
```

第一阶段可以继续使用 Markdown 作为本地存储。API 层负责把 Markdown 解析成前端需要的结构，并把表单内容追加写回对应文件。

## 脱敏策略

先脱敏会进入公开产品表面的字段：

- 用户姓名改为 `Learner`
- 具体日期改为相对训练日，如 `Day 1`
- 真实成绩可保留为 demo 曲线，但不要保留完整历史上下文
- 错题原句改为自造示例句
- Noah 人设改为可配置的 `coach persona`，不要公开私人关系设定

私人版本通过运行时配置加载真实 `persona/` 和 `data/`，公开版本默认加载 demo 数据。
