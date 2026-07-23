---
name: catalyst-design
version: 1.0.2
license: MIT
homepage: https://github.com/ANDYPENG09/catalyst-design-skill
category: 学术研究
platforms:
  - WorkBuddy
  - Claude Code
  - Cursor
  - OpenClaw
  - Hermes
  - QClaw
  - ima
  - Codex
description: |-
  催化剂设计指导技能。基于分层、可追溯、可动态演进的方法论体系（融合 catalyst-search 检索文献、用户经 AI/skill 获取的资料及外部渠道），为用户提供催化剂组分选择、结构设计、合成策略与性能优化建议。可独立运行；也可与 catalyst-search 协作——消费其结构化文献输出（文献矩阵）以增强针对性，并将新证据回填方法论库。
  Catalyst design guidance skill. Based on a layered, traceable, and dynamically evolving methodology system (fusing catalyst-search retrieval results, user-acquired materials via AI/skills, and external channels), it provides advice on catalyst composition selection, structural design, synthesis strategy, and performance optimization. Runs standalone; also collaborates with catalyst-search — consuming its structured literature output (matrix) for sharper targeting and feeding new evidence back into the methodology base.
agent_created: true
---

# 催化剂设计指导 (Catalyst Design)

## 何时使用 | When to use
- 用户要"催化剂怎么设计 / 选什么组分 / 怎么优化性能 / 合成路线建议 / 催化剂配方 / 电催化剂设计 / 合成条件怎么选"
  - Users asking "how to design a catalyst / which composition to pick / how to optimize performance / synthesis-route advice / catalyst formulation / electrocatalyst design / how to choose synthesis conditions"
- 典型输入：设计目标（反应类型 + 材料体系/性能诉求），可选：catalyst-search 的文献检索结果
  - Typical input: design goal (reaction type + material system / performance need); optional: catalyst-search literature results
- 覆盖反应：HER / OER / ORR / PEMWE / 全解水 / 光催化 / 塑料升级回收等
  - Covers: HER / OER / ORR / PEMWE / overall water splitting / photocatalysis / plastic upcycling, etc.

## 何时不使用 | When NOT to use
- 纯文献检索任务 → 用 `catalyst-search`（本技能不重复检索）
  - Pure literature search → use `catalyst-search` (this skill does not re-search)
- 非催化领域的材料设计（如电池正极、半导体器件）→ 不适用
  - Non-catalysis material design (e.g., battery cathodes, semiconductor devices) → not applicable
- 仅需查一个具体 DOI / 论文全文 → 用 WebSearch/WebFetch 即可
  - Just looking up a specific DOI / full text → use WebSearch/WebFetch directly

## 前置条件 | Prerequisites
- 本技能自带知识库（`references/`）与模板（`templates/`），无需外部依赖即可运行
  - Ships with its own knowledge base (`references/`) and templates (`templates/`); runs with no external dependencies
- 可选：`WebSearch`/`WebFetch` 可用时，可补查特定规律的出处（非必需）
  - Optional: when `WebSearch`/`WebFetch` are available, may trace a specific rule's origin (not required)

## 输入接口 | Input interface
- **必填 | Required**：设计目标（含反应类型 + 材料体系或性能诉求）
  - Design goal (reaction type + material system or performance need)
- **可选 | Optional**：`catalyst-search` 的结构化文献输出（即 `literature_matrix.md` 格式的文献矩阵表 + 支撑结论 + 验证建议）
  - The structured literature output of `catalyst-search` (the `literature_matrix.md` table + supporting conclusions + validation suggestions)
  - 提供了文献 → 结合文献中的具体体系与指标，给出针对性建议并标注文献支撑
    - With literature → give targeted advice using its specific systems/metrics and cite the support
  - 未提供文献 → 基于内置设计方法论（见 `references/design_methodology.md`）给出通用建议
    - Without literature → give general advice from the built-in methodology (see `references/design_methodology.md`)

## 设计方法论体系（分层 · 多来源 · 可追溯 · 可演进） | Methodology system (layered · multi-source · traceable · evolvable)
> 方法论**持续融合多来源证据**，按四层体系组织，并可随新增文献动态更新。
> The methodology **continuously fuses multi-source evidence**, organized in four layers, and evolves dynamically with new literature.
> - 完整分层知识库 | Full layered knowledge base: `references/design_methodology.md`（每条带来源标签+置信度+更新日期 / each entry carries source tag + confidence + update date）
> - 动态更新机制 | Dynamic update mechanism: `references/methodology_update_protocol.md`
> - 可追溯条目台账 | Traceability registry: `references/methodology_registry.md`（编号→出处/DOI 逐级溯源 / trace by ID → source/DOI）

### 四层体系（Layered Framework）
- **L1 基础理论层 | L1 Theory**：为什么这样设计——构效关系、d 带中心/Sabatier、反应机理分型(AEM/LOM;Volmer-Heyrovsky)、活性-稳定性权衡、缺陷即活性、双功能协同
  - Why design this way — structure-property relations, d-band center/Sabatier, mechanism typing (AEM/LOM; Volmer-Heyrovsky), activity-stability trade-off, defects-as-activity, bifunctional synergy
- **L2 方法工具层 | L2 Methods & Tools**：用什么手段——合成方法库(SEA/低熔点掺杂/配体锚定/单源热解/Joule heating/模板/晶界工程…)、表征与计算工具(XRD/STEM/XPS/EXAFS/DFT/ML)、结构设计手段(尺寸/有序化/核壳/载体/单双原子)
  - What means to use — synthesis library (SEA/low-melting doping/ligand anchoring/single-source pyrolysis/Joule heating/templating/grain-boundary engineering…), characterization & computation (XRD/STEM/XPS/EXAFS/DFT/ML), structural design (size/ordering/core-shell/support/single-dual atoms)
- **L3 技术参数层 | L3 Parameters**：具体参数窗口——退火温度(450–1150 °C)、降温速率(慢冷≤2 °C/min)、气氛、粒径、掺杂量、组分配比、后处理
  - Concrete parameter windows — annealing temp (450–1150 °C), cooling rate (slow ≤2 °C/min), atmosphere, particle size, doping level, composition ratio, post-treatment
- **L4 实践验证层 | L4 Validation**：如何证明有效——RDE→MEA 分级评测、标准(TCASMES 400-2024/T/CRES 0030-2025)、各体系性能基准、有序度/稳定性/放大验证
  - How to prove it works — RDE→MEA tiered evaluation, standards (TCASMES 400-2024/T/CRES 0030-2025), per-system benchmarks, ordering/stability/scale-up validation

### 来源标签（可追溯性）| Source tags (traceability)
`[CS]` catalyst-search 检索文献(含 DOI) | `[AI]` 用户经 AI/skill 获取 | `[EXT]` 外部渠道(会议/专利/标准/内部数据) | `[EXP]` 经验推测(待验证)。置信度 ★~★★★。
`[CS]` catalyst-search retrieval (with DOI) | `[AI]` user-acquired via AI/skill | `[EXT]` external channel (conference/patent/standard/internal data) | `[EXP]` empirical guess (to verify). Confidence ★~★★★.
> 生成建议时须带出所引条目的来源标签，区分"文献已证实"与"经验推测"。
> When generating advice, surface the source tag of each cited entry; distinguish "literature-confirmed" from "empirical guess".

## 工作流 | Workflow
1. **解析输入 | Parse input**：提取设计目标（反应类型 / 体系 / 性能）；收集并区分多来源证据——catalyst-search 文献矩阵 `[CS]`、用户经 AI/skill 提供的资料 `[AI]`、外部渠道 `[EXT]`。输入不完整（缺反应类型或材料体系）时，先向用户澄清，不臆测。
   - Extract design goal; collect and tag multi-source evidence — catalyst-search matrix `[CS]`, user-provided `[AI]`, external `[EXT]`. If input is incomplete (missing reaction type or material system), ask the user to clarify first; do not guess.
2. **匹配规律（按四层）| Match rules (by layer)**：目标映射到 L1 理论(选机理方向)→ L2 方法工具(选合成/表征手段)→ L3 参数(定参数窗口)→ L4 验证(定评测路径)。
   - Map goal to L1 theory (mechanism direction) → L2 methods (synthesis/characterization) → L3 parameters (windows) → L4 validation (evaluation path).
3. **生成建议 | Generate advice**：输出组分选择 + 结构设计 + 合成策略 + 条件优化 + 验证建议；每条引用注明**来源标签**(及 DOI)与置信度，区分"文献已证实"与"经验推测"。
   - Output composition + structure + synthesis + conditions + validation; each citation notes **source tag** (and DOI) and confidence; distinguish confirmed vs guessed.
4. **动态回填（演进）| Dynamic backfill (evolve)**：若本次用到用户新提供的文献/结论产生了新规律，按 `references/methodology_update_protocol.md` 校验后回填 `design_methodology.md` 与 `methodology_registry.md`（含来源、DOI、置信、状态）。证据不足(仅 [EXP])的方向，主动建议调用 catalyst-search 补检以升级为 [CS]。
   - If new user literature yields new rules, validate per `methodology_update_protocol.md` then backfill both files (source, DOI, confidence, status). For under-evidenced (only [EXP]) directions, proactively suggest catalyst-search re-check to upgrade to [CS].
5. **输出 | Output**：按 `templates/design_proposal.md` 输出设计建议书；引用文献采用 GB/T 7714（格式见 catalyst-search 的 `templates/citation_gb7714.md`，本技能自带同名模板亦可）。
   - Output the design proposal per `templates/design_proposal.md`; cite in GB/T 7714 (see catalyst-search's `templates/citation_gb7714.md`, or this skill's own copy).

## 输出接口 | Output interface
- 设计建议书（组分 / 结构 / 合成 / 条件 / 验证），格式见 `templates/design_proposal.md`
  - Design proposal (composition / structure / synthesis / conditions / validation); format in `templates/design_proposal.md`
- 若引用文献，给出 GB/T 7714 引用，并标明"文献支撑"或"经验推测"
  - If citing literature, give GB/T 7714 citation and label "literature-supported" or "empirical guess"

## 与其他能力分工 | Division of labor
- 文献检索由 `catalyst-search` 负责；本技能不重复检索，仅消费其输出或基于内置知识给建议
  - Literature search is catalyst-search's job; this skill does not re-search, only consumes output or uses built-in knowledge
- 如需补查特定设计规律的出处，可用 WebSearch/WebFetch（可选，非必需）
  - To trace a specific rule's origin, WebSearch/WebFetch may be used (optional)

## 注意事项 | Notes
- 建议须有据（内置方法论或所提供文献），不凭空断言
  - Advice must be grounded (built-in methodology or supplied literature); no ungrounded claims
- 明确区分"文献已证实"与"经验推测"
  - Clearly distinguish "literature-confirmed" from "empirical guess"
- 设计建议须附带可执行的验证路径（表征/测试），便于用户复核
  - Advice must include an actionable validation path (characterization/testing) for user verification
- **安全与权限 | Safety & permissions**：本技能仅读取自带 `references/`、`templates/`；不执行系统命令、不写入用户文件、不发起除可选 WebSearch/WebFetch 外的网络请求；不收集或外传用户数据。
  - This skill only reads its own `references/` and `templates/`; runs no system commands, writes no user files, makes no network requests beyond optional WebSearch/WebFetch; collects or exfiltrates no user data.

## 示例 | Example
- **输入**：设计一个酸性 OER 催化剂，要求 η₁₀ < 200 mV、稳定 > 500 h
- **输出**：
  - 组分：Ru@IrOₓ 核壳（Ru 核活性高、IrOₓ 壳抗溶）`[CS]` ★★★
  - 结构：核壳界面电荷重分布，优化 Ru 的含氧中间体吸附 `[CS]` ★★★
  - 合成：Adams Fusion 制 IrOₓ 壳 + 还原沉积 Ru 核 `[CS]` ★★
  - 条件：退火 400–500 °C（过高致 Ru 溶入壳、过低有序度不足）`[EXP]` ★
  - 验证：RDE 测 η₁₀/Tafel；ICP-MS 监测 Ru/Ir 溶解；30k 圈 ADT `[CS]` ★★★
  - Input: design an acidic OER catalyst with η₁₀ < 200 mV, stability > 500 h
  - Output: composition Ru@IrOₓ core-shell / structure interfacial charge redistribution / synthesis Adams Fusion + reductive Ru deposition / conditions anneal 400–500 °C / validation RDE + ICP-MS + ADT; each tagged [CS]/[EXP] with confidence.

## 项目主页 | Project home
- **GitHub**：https://github.com/ANDYPENG09/catalyst-design-skill （源码、更新与 Issue 反馈 | source, updates & issues）
- **配套技能 | Companion**：https://github.com/ANDYPENG09/catalyst-search-skill （催化文献检索 | catalysis literature search）
