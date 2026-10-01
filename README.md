# 用户反馈聚合分析师

> 把散落五个渠道的用户反馈变成每周一张决策表
>
> **4.4.4**　·　独立开发者　·　阶段 P1　·　
> 复杂度 M　·　¥49-99/月　·　定义卡 4.4.4

![架构](docs/images/architecture.svg)

**一句话**：已有活跃用户的所有产品型独立开发者

---

## 这个数字员工解决什么问题

把散落五个渠道的用户反馈变成每周一张决策表

| 项 | 内容 |
|---|---|
| 服务对象 | 已有活跃用户的所有产品型独立开发者 |
| 可量化目标 | 反馈覆盖率（已采集渠道/全渠道）100%；周报准时率；高优需求从提出到进路线图 ≤2 周 |
| 投入产出 | 月省约 25h ≈ ¥2000 vs 订阅，回报比 >20 倍 |
| 需求依据 | D02、D19 |
| 分发渠道 | GitHub、Coze扣子商店、Dify Marketplace |

## 30 秒上手

```bash
git clone <本仓库地址> && cd de-indie-feedback-analyst
pip install pyyaml
python3 tests/run.py            # 先跑一遍自检，确认环境与契约都对得上
```

试用（把 `<输入>` 换成本人真实材料）：

```text
请以「用户反馈聚合分析师」的身份，帮我跑「多渠道反馈采集」。
材料如下：<输入>
要求：只使用材料里出现过的数字，缺的写 <待填>；对外文案停在待确认状态。
```

详细接入见 [`docs/01-安装与接入.md`](docs/01-安装与接入.md)。

## 仓库结构

```text
de-indie-feedback-analyst/
├── employee.yaml          # 机器契约（能力清单 + 依赖锁）
├── dependencies.yaml      # 对 core 的外部依赖（含版本）
├── persona/               # 运行提示词 / 边界 / KPI
├── skills/                # 私有原子技能（4 个）
├── spec-bindings/         # 有意不公共化能力的本地绑定声明（1 个）
├── workflows/             # 本员工工作流（5 条）
├── kb/                    # 知识库 RAG 契约
├── connectors/            # 连接器绑定（只读为主，写操作人工确认）
├── docs/                  # 六类发布文档
└── tests/                 # 自动化多场景测试
```

## 私有原子技能（4）

| 技能 | slug | 复杂度 | 阶段 | 成熟度 |
|---|---|---|---|---|
| `更新日志自动生成` | `changelog-writer` | S | P2 | 契约完备 |
| `需求强度打分` | `demand-intensity-score` | S | P1 | 契约完备 |
| `反馈聚类` | `feedback-clustering` | S | P1 | 契约完备 |
| `路线图建议` | `roadmap-recommendation` | S | P2 | 契约完备 |

## 平台公共技能依赖（2）

| 技能 | slug | 全平台复用员工数 |
|---|---|---|
| `简报生成` | `brief-generator` | 10 |
| `评论情绪识别` | `review-sentiment-tag` | 5 |

> 这些技能来自 `agent-skills-core@1.0.0`，本仓库**只引用不复制**。

## Spec 绑定层（1）

| 能力 | slug | 契约位置 | 本仓落点 |
|---|---|---|---|
| `数据对接` | `data-ingest-adapter` | `agent-skills-core/specs/data-ingest-adapter.md` | `spec-bindings/data-ingest-adapter.md` |

> 这一族能力**有意不公共化**（与外部平台接口强绑定）。本仓不存正文，
> 只留本地绑定声明与连接器配置。

## 工作流（5）

| 工作流 | slug | 触发 | 阶段 | 调用技能数 |
|---|---|---|---|---|
| `多渠道反馈采集` | `wf-indie-feedback-aggregate` | 定时（每日） | P1 | 1 |
| `去重聚类` | `wf-indie-feedback-dedup` | 事件（采集后） | P1 | 1 |
| `情绪与优先级打标` | `wf-indie-feedback-tagging` | 事件（聚类后） | P1 | 2 |
| `周报生成` | `wf-indie-feedback-weekly` | 定时（每周一） | P1 | 1 |
| `路线图建议` | `wf-indie-feedback-roadmap` | 定时（每月） | P2 | 2 |

## 知识库与连接器

- 知识库语料：['历史反馈库', '产品路线图文档（RAG）']
- 连接器：LLM 推理 API、平台发布端点（Coze/Dify/WorkBuddy）

## 质量与验收

| 项 | 值 |
|---|---|
| 技能文件数 | 87 |
| 多场景用例数 | 248 |
| 用例通过 | 248 |
| 验收结论 | ✅ 通过 |

完整报告：[`docs/05-验收与测试.md`](docs/05-验收与测试.md)

## 许可

专有许可，详见 [`LICENSE`](LICENSE)。
