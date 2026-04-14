# Bright Data MCP + Dify 实战：Amazon 商品数据采集工作流
基于 Bright Data MCP 与 Dify 搭建的 Amazon 商品信息一键采集工作流，输入商品 URL / ASIN，自动输出结构化 JSON 数据。

---

## 项目说明
本文配套实战项目，实现：
- Amazon 商品详情页数据采集
- LLM 自动解析标题、价格、评分、评论数、卖点等关键字段
- 输出标准结构化 JSON 与可读摘要
- 零代码维护、无视反爬、稳定采集

适用人群：跨境电商数据工程师、AI 开发者、选品分析师、Python 开发者

---

## 前置准备
1. 注册 Bright Data 账号（含 $10 免费试用额度）  
   👉 注册地址：https://brightdata.com/your-affiliate-link
2. 注册/部署 Dify（云端或本地均可）  
   👉 Dify 官网：https://dify.ai
3. 获取 Bright Data MCP API Key
4. 在 Dify 中配置好可用的 LLM 模型

---

## 快速开始
### 1. 下载工作流模板
文件：`workflow_amazon_product_scraper.yml`

### 2. 导入 Dify
1. 打开 Dify 工作台 →工作室 →创建应用 →导入DSL文件  
2. 选择 ` workflow_amazon_price_monitor.yml` 导入

### 3. 关键配置（必须做，否则无法运行）
1. **配置 Bright Data MCP 工具**
   - 导入后如果原 `web_data_amazon_product` 节点不可用
   - 更改该节点 → 重新添加你自己的 Bright Data MCP 工具
   - 重新配置输入变量：传入 Amazon URL
2. **切换 LLM 模型**
   - 进入 LLM 解析节点
   - 切换为**你自己已配置的模型**
   - 默认模板使用作者的模型，无法直接运行
3. **填入你的 API Key**
   - 在 MCP 配置中替换：YOUR_BRIGHTDATA_API_KEY

### 4. 运行工作流
1. 输入 Amazon 商品详情页 URL
2. 点击运行
3. 自动输出结构化 JSON 结果

---

## 输出字段示例
```json
{
"platform/平台": "Amazon",
"product_name/商品名称": "Instant Pot Duo Plus 9-in-1 Multicooker, Pressure Cooker, Slow Cook, Rice Maker, Steamer, Sauté, Yogurt, Warmer & Sterilizer, Includes App with Over 800 Recipes, Stainless Steel, 6 Quarts",
"asin/商品ASIN": "B01NBKTPTS",
"brand/品牌": "Instant Pot",
"current_price/当前售价": 139.99,
"original_price/划线原价": 139.99,
"currency/货币类型": "USD",
"stock_status/库存状态": "In Stock",
"rating/评分": 4.7,
"review_count/评价总数": 52402,
"sales_volume/近一月销量": 8000,
"rank/类目排名": 2,
"seller/卖家名称": "Amazon.com",
"is_official/是否官方自营": true,
"is_prime/是否支持Prime": true,
"delivery/配送信息": "FREE delivery Saturday, April 18;Or Prime members get FREE delivery Overnight 7 AM - 11 AM. Order within 6 hrs 24 mins. Join Prime",
"return_policy/退换政策": "FREE 30-day refund/replacement",
"product_url/商品链接": "https://www.amazon.com/Instant-Pot-Plus-60-Programmable/dp/B01NBKTPTS?th=1&psc=1&language=en_US&currency=USD"
}
```
工作流架构
输入 URL → Bright Data MCP 采集 → LLM 结构化解析 → 输出 JSON

常见问题

Q1：导入后 MCP 节点置灰报错？

A：MCP 唯一标识 /和名称不一致与模板的不一致，对应不上，更改原节点，重新添加你自己的 Bright Data MCP 并配置变量。

Q2：LLM 节点报错？

A：切换为你自己在 Dify 中配置好的模型，如果编辑Q1后，LLM节点也需要重新选择一下输入变量(选择json)。

Q3：采集失败 / 被限制？

A：检查 Bright Data API Key 是否正确、额度是否有效。
