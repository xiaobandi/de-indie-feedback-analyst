# 多渠道反馈采集

> 邮件/应用商店/Discord/社群/问卷抓取 → 统一入库

工作流 `wf-indie-feedback-aggregate`　·　归属 用户反馈聚合分析师　·　触发 定时（每日）　·　
复杂度 M　·　阶段 P1

## 调用链

- `数据对接`（data-ingest-adapter）

## 文档

- [`WORKFLOW.md`](WORKFLOW.md) — 完整编排、闸门、降级与验收标准
- [`tests/cases.yaml`](tests/cases.yaml) — 端到端 / 闸门 / 降级用例

## 一句话试用

```text
帮我跑 用户反馈聚合分析师 的「多渠道反馈采集」：<你的输入>
```
