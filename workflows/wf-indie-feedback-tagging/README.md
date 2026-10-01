# 情绪与优先级打标

> 情绪识别 → 需求强度打分 → 流失风险标记

工作流 `wf-indie-feedback-tagging`　·　归属 用户反馈聚合分析师　·　触发 事件（聚类后）　·　
复杂度 S　·　阶段 P1

## 调用链

- `评论情绪识别`（review-sentiment-tag）
- `需求强度打分`（demand-intensity-score）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 用户反馈聚合分析师 的「情绪与优先级打标」：<你的输入>
```
