# GitHub Actions 配置指南

## 步骤1：进入仓库设置

1. 访问您的Fork仓库：https://github.com/Singgle12332/daily_stock_analysis
2. 点击 `Settings` 标签
3. 左侧菜单选择 `Secrets and variables` → `Actions`
4. 点击 `New repository secret` 添加以下配置

## 步骤2：添加Secrets

### AI 模型配置（必填）

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `GEMINI_API_KEY` | `sk-AKkkdXloo6qvYRcD5HppTjPcWZUBaQA8rL6ynFdd6MQH64de` | Gemini API Key |
| `GEMINI_MODEL` | `gemini-3-flash-preview` | Gemini 模型名称 |
| `GEMINI_MODEL_FALLBACK` | `gemini-2.5-flash` | 备选模型 |
| `GEMINI_REQUEST_DELAY` | `3.0` | 请求延迟（秒）|

### OpenAI 兼容 API 配置（可选）

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `OPENAI_BASE_URL` | `https://elysiver.h-e.top` | API 地址 |
| `OPENAI_MODEL` | `Gemini-3-pro-view` | 模型名称 |

### 搜索引擎配置（推荐）

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `TAVILY_API_KEYS` | `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` | Tavily API Key |

### 邮件通知配置

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `EMAIL_SENDER` | `2839706793@qq.com` | 发件人邮箱 |
| `EMAIL_PASSWORD` | `bpvjpchsgyejdggb` | 邮箱授权码 |

### 自选股列表配置（必填）

| Secret 名称 | 值 | 说明 |
|------------|-----|------|
| `STOCK_LIST` | `300059,600030,600036,601318,300033,688981,002371,688041,002415,603501,300750,002594,300274,300124,601012,600519,000858,000333,600887,600809,300760,600276,603259,600436,300015,600893,000768,600760,600372,600150,002179,000733,600879,688122,600316,002371,688012,688072,688037,688082,600276,688235,002422,688180,688331,00700,03690,09988,01810,00883,00941,00388,01024,02015,02269` | 自选股代码列表 |

## 步骤3：启用GitHub Actions

1. 点击仓库的 `Actions` 标签
2. 点击 `I understand my workflows, go ahead and enable them`
3. 确认工作流已启用

## 步骤4：手动测试运行

1. 进入 `Actions` → `每日股票分析`
2. 点击 `Run workflow`
3. 选择运行模式：
   - `full` - 完整分析（股票+大盘）
   - `market-only` - 仅大盘复盘
   - `stocks-only` - 仅股票分析
4. 点击 `Run workflow`

## 步骤5：查看运行结果

1. 在 `Actions` 页面查看运行记录
2. 点击具体的运行记录查看日志
3. 查看生成的报告（如果有）

## 自动运行时间

默认配置为每个工作日 **18:00（北京时间）** 自动执行

如需修改时间，编辑 `.github/workflows/daily_analysis.yml` 文件中的 cron 表达式：

```yaml
schedule:
  - cron: '0 10 * * 1-5'  # UTC 10:00 = 北京时间 18:00
```

## 常见问题

### Q: 如何获取邮箱授权码？
A: 以QQ邮箱为例：
1. 登录QQ邮箱网页版
2. 设置 → 账户 → POP3/SMTP服务
3. 开启服务
4. 点击生成授权码
5. 复制授权码到 `EMAIL_PASSWORD`

### Q: 如何修改定时时间？
A: 编辑 `.github/workflows/daily_analysis.yml` 中的 cron 表达式：
- 北京时间 09:30 → `'30 1 * * 1-5'`
- 北京时间 15:00 → `'0 7 * * 1-5'`
- 北京时间 18:00 → `'0 10 * * 1-5'`

### Q: 如何添加更多通知渠道？
A: 可以同时配置多个Secrets：
- `WECHAT_WEBHOOK_URL` - 企业微信
- `FEISHU_WEBHOOK_URL` - 飞书
- `TELEGRAM_BOT_TOKEN` + `TELEGRAM_CHAT_ID` - Telegram

## 配置完成后的效果

- ✅ 每个工作日18:00自动运行分析
- ✅ 分析您的所有自选股
- ✅ 生成决策仪表盘
- ✅ 推送分析结果到邮箱
- ✅ 完全免费，无需服务器
