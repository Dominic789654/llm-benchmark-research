# AGENTS.md - LLM Benchmark Research Guide

> 本文档用于指导 AI Agent 更新和维护中国 LLM 对比报告
> 项目: llm-benchmark-research
> 创建时间: 2026-02-17

---

## 🎯 项目目标

维护一份准确、及时、全面的中国五大旗舰 LLM（Seed/Qwen/Kimi/GLM/MiniMax）对比报告

---

## 📚 信息源清单（按优先级排序）

### P0 - 必须检查（官方一手信息）

| 厂商 | 官方文档/API | 发布渠道 | 检查频率 |
|-----|-------------|---------|---------|
| **阿里云/Qwen** | https://help.aliyun.com/zh/model-studio/getting-started/what-is-model-studio | 阿里云百炼、Qwen官方博客 | 每月 |
| **Moonshot/Kimi** | https://platform.moonshot.cn/docs | 官方API文档、技术博客 | 每月 |
| **智谱AI/GLM** | https://open.bigmodel.cn/dev/api | 官方API文档、GLM技术报告 | 每月 |
| **MiniMax** | https://platform.minimaxi.com/document/Announcement | 开发者平台公告 | 每月 |
| **ByteDance/Seed** | Seed 官方发布（主要通过新闻）| 官方发布会、技术博客 | 每季度 |

**关键信息提取**:
- 上下文窗口变化（Token 数）
- 价格调整（输入/输出价格每百万 tokens）
- 新模型版本发布（如 Qwen4.0, Kimi 3.0）
- 新能力（多模态、工具调用、思考模式）
- 参数规模（总参数/激活参数）

### P1 - 权威第三方基准（必须引用）

| 基准平台 | URL | 检查频率 | 重点指标 |
|---------|-----|---------|---------|
| **Artificial Analysis** | https://artificialanalysis.ai | 每月 | Intelligence Index、价格性能比 |
| **SuperCLUE** | https://www.superclue.ai | 每季度 | 中文能力总分及细分 |
| **OpenCompass** | https://opencompass.org.cn | 每月 | C-Eval、CMMLU、GAOKAO |
| **LMSYS Arena** | https://chat.lmsys.org | 每月 | ELO 排名、人类偏好 |
| **SWE-Bench** | https://www.swebench.com | 每季度 | 代码能力（注意官方 vs 独立测试差异） |

### P2 - 独立验证（重要参考）

| 来源 | 说明 | 检查频率 |
|-----|------|---------|
| **SWE-rebench** | GitHub 独立复现测试 | 每季度 |
| **GitHub 社区** | 实际使用反馈、issue讨论 | 每月 |
| **Twitter/X 技术博主** | 一线工程师反馈 | 每周 |
| **AI Discord/论坛** | 开发者社区讨论 | 每月 |

### P3 - 竞品对比（国际基准）

| 模型 | 参考来源 |
|-----|---------|
| GPT-4/5 | OpenAI 官方、LMSYS Arena |
| Claude | Anthropic 官方、Artificial Analysis |
| Gemini | Google 官方、LMSYS Arena |

---

## ⚠️ 关键注意事项

### 1. 数据可信度分级

```
🟢 可信
├── 官方 API 文档中的技术规格
├── 第三方独立测试（SWE-rebench 等）
└── 开源可复现的评测代码

🟡 需谨慎
├── 厂商官方 benchmark 宣称（可能选优）
├── 未公开测试方法的评测
└── 早期内测版本数据

🔴 存疑
├── 与独立测试差距 >30% 的官方数据
├── 未说明测试条件的性能数据
└── 训练数据可能污染的 benchmark
```

### 2. 常见陷阱

#### 上下文窗口陷阱
- **宣传值 vs 实际值**: 厂商可能宣称 1M，但实际有效利用可能更低
- **价格陷阱**: 长上下文通常价格更高（如 Qwen3.5 1M 价格是 128K 的 5 倍）
- **模式差异**: 思考模式 vs 非思考模式可能有不同上下文限制

#### 性能数据陷阱
- **SWE-Bench 虚高**: MiniMax 官方 80.2% vs 独立 39.6%，差距巨大
- **Cherry Picking**: 厂商可能只公布表现好的 benchmark
- **版本混淆**: 开源版 vs API 版性能可能有差异

#### 价格陷阱
- **单位不一致**: 有些按 tokens，有些按字符
- **阶梯定价**: 注意长文本的价格跳变点
- **隐藏费用**: 多模态输入可能按不同规则计费

### 3. 必须标注的数据

所有以下数据必须注明来源和日期：
- [ ] 价格数据（带货币单位和生效日期）
- [ ] 性能百分比（区分官方/独立测试）
- [ ] 上下文窗口（区分总长度和有效利用）
- [ ] 排名数据（注明是哪个榜单）

---

## 🔄 更新流程

### 定期检查清单

#### 每月检查
```bash
# 1. 检查官方文档更新
- [ ] 阿里云百炼 Qwen 文档
- [ ] Moonshot 平台更新日志
- [ ] 智谱 Open 平台公告
- [ ] MiniMax 平台公告

# 2. 检查第三方基准
- [ ] Artificial Analysis Intelligence Index
- [ ] LMSYS Arena 排名变化
- [ ] OpenCompass 榜单

# 3. 社区动态
- [ ] Twitter/X 技术讨论
- [ ] GitHub 相关项目更新
```

#### 每季度深度检查
```bash
# 1. 价格全面对比
- [ ] 所有厂商最新定价
- [ ] 与国际模型价格对比

# 2. 性能基准
- [ ] SuperCLUE 新报告
- [ ] SWE-Bench / SWE-rebench 更新
- [ ] 新发布的独立测试

# 3. 新模型发布
- [ ] 是否有新 flagship 模型
- [ ] 现有模型重大版本更新
```

### 更新报告步骤

1. **发现变更** → 记录在 TODO
2. **多源验证** → 至少 2 个独立来源确认
3. **更新数据** → 修改 benchmark_comparison_report.md
4. **更新日期** → 修改报告日期和版本历史
5. **提交变更** → `git commit -m "data: update xxx for [model]"`
6. **推送仓库** → `git push origin main`

---

## 🔍 搜索关键词模板

### 查找官方更新
```
[厂商] [模型名] 发布 更新 2026
[厂商] [模型名] 价格调整
[厂商] [模型名] 上下文窗口
[厂商] [模型名] API 更新
```

### 查找评测数据
```
[模型名] benchmark 2026
[模型名] SWE-Bench
[模型名] SuperCLUE
[模型名] 评测对比
```

### 查找独立测试
```
[模型名] 实测
[模型名] 对比测试
[模型名] GitHub
SWE-rebench [模型名]
```

---

## 📊 数据维护检查表

### 模型基础信息
- [ ] 参数规模（总参数 / 激活参数）
- [ ] 上下文窗口（总长度 / 有效长度）
- [ ] 支持模态（文本 / 图像 / 视频 / 音频）
- [ ] 架构特点（MoE、Attention 机制等）

### 价格信息
- [ ] 输入价格（分档位：0-128K, 128K-256K, 256K-1M）
- [ ] 输出价格
- [ ] 货币单位（人民币/美元）
- [ ] 生效日期

### 性能数据
- [ ] 综合智能（Artificial Analysis Index）
- [ ] 代码能力（SWE-Bench，区分官方/独立）
- [ ] 中文能力（SuperCLUE）
- [ ] 知识能力（C-Eval, CMMLU）
- [ ] 多模态能力（MathVision等）

---

## 🚨 特殊情况处理

### 发现数据冲突
1. 记录冲突来源（A 说 X，B 说 Y）
2. 优先采信独立第三方测试
3. 在报告中注明数据来源和差异

### 厂商发布新模型
1. 判断是否替换现有 flagship
2. 更新模型概览表格
3. 添加版本历史说明
4. 保留旧数据作为参考（如有必要）

### 发现数据造假/严重偏差
1. 在报告中添加 ⚠️ 警示标注
2. 引用独立测试作为对比
3. 不删除官方数据，但明确标注可信度

---

## 📝 报告格式规范

### 价格格式
```markdown
| 模型 | 输入价格 | 输出价格 |
|-----|---------|---------|
| Model-X | ¥0.8/百万 tokens | ¥4.8/百万 tokens |
```

### 性能数据格式
```markdown
| 模型 | 得分 | 来源 | 日期 |
|-----|-----|------|-----|
| Model-X | 80.2% | 官方 | 2026-01 |
| Model-X | 39.6% | SWE-rebench 独立测试 | 2026-01 |
```

### 警示标注
```markdown
> **⚠️ 关键发现**: [发现内容]
```

---

## 🗂️ 相关资源

### 国内 AI 聚合平台
- 模型价格对比: https://www.aiservice.comparison
- AI 产品榜: https://www.aicpb.com

### 国际参考
- The LLM Index: https://llm-index.com
- LLM Pricing: https://llm-price.com

---

## 🤖 Agent 自我检查

每次更新前问自己：
1. [ ] 这个数据有来源吗？
2. [ ] 来源可靠吗（官方/独立第三方）？
3. [ ] 数据是最新的吗？
4. [ ] 有潜在的利益冲突吗？
5. [ ] 价格数据包含货币单位了吗？
6. [ ] 性能数据区分官方/独立测试了吗？

---

*本文档应与 benchmark_comparison_report.md 一起维护更新*
