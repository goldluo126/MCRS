# MCRS SFL 验证规格书 v7.1 — CANONICAL CLOSURE（自包含终版候选）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / CANONICAL`
版本：`v7.1`（全文自包含、零继承引用；替代 v1-v7.0，旧版条款未在本文出现即失效。第六轮外部审查 20 条红线全部核实成立、零驳回；本版性质 = canonical closure：不引入任何新因子与新经济假设，只封口编译歧义、零模型完整性、Gate 规则、组合账本与分法庭推断）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文件 MUST 产生逐日完全相同的信号、配对、交易与判词。

---

## 0. 终局条款与判决语义（运行前 MUST 由用户签署）

> 本实验（SFL v7.1）是 MCRS 日频研究线的最终实验。
> - **科学死亡线（措辞收窄）**：影子数据上 H-Z2a1 与 H-Z2a2 **均** Economically FAIL 于 MES_sci=10bp 时，死亡的命题是——**"题材协调相变能够向供应商题材全体成员产生 ≥10bp（10 日）的平均或中心收益扩散"**。该判词 MUST NOT 外推为稀疏核心传播、尾部效应、波动/成交效应或条件载体效应的死亡；
> - **项目线**：各法庭经济 MES（§9）。"效应存在但低于经济门槛" = 科学成立、项目关闭，两种判词分开书写；
> - 第四法庭 = 日线无自冲击 VWAP 执行代理法庭：非 Economically PASS = 关线强理由（非"任何执行不可能"的证明）；PASS 唯一出口 = 晋级 L1，禁称"已验证可交易"；
> - 范围声明：第二/四法庭验证**成熟题材本体的协调再激活**；H-Z2 估计量为 **matched-sample effect**（条件于已形成配对的效应，非无条件总体 ATT）；
> - 序贯法庭 append-only；提前判决仅限 Economically PASS；OOS-A 原封退库；DEV = internal pilot 永不并入最终 CI。
> 签署人：________ 日期：________

## 1. 研究对象与 Gatekeeping

**研究对象（冻结措辞）**：在某供应商已建立的题材本体中，一个此前协调休眠的题材，相对于**同日仍处风险集中的题材**，发生集中涨停相变后是否具有未来收益信息（风险集条件命题，非"客观题材发现"）。

**Gatekeeping 树（v7.1 修订）**：
```
Gate0-F（过滤器装置安慰剂，锁 Gate1）: P3 ∧ P4 通过
    通过线（冻结）: 伪事件效应点估计 |d| < 0.1 且 95% CI 含 0（P3、P4 各自满足）
Gate0-Z（载体装置安慰剂，仅锁 Gate3 的 H-Z3）: P1 机器合成数据自检通过
    （P1 的经验零分布本身是 H-Z3 的推断引擎，不再重复设"通过线"）
P2: 纯诊断，不构成任何 Gate
 → Gate1: H-Z2a1（均值, local α=0.04, 单侧）
    未达 Economically PASS → 解锁 H-Z2a2（鲁棒中心位置, local α=0.01, 单侧）
    [科学死亡 = a1 与 a2 均 Econ-FAIL@10bp（影子终期）]
 → Gate2（H-Z2a 任一 Statistically Positive 后解锁）:
    主假设 H-Z2b（α=0.025）与 H-P1a（α=0.025）——Bonferroni local 分配
    H-Z2c 降为描述性（无 alpha、不产生正式 PASS）
 → Gate3（H-Z2b 或 H-P1a 任一 Statistically Positive 后解锁）:
    主假设 H-Z3（α=0.05）；H-Z3b/H-Z4/H-Z6/H-P1b 描述性
 → Gate4: H-Z1（α=0.05）
下层失败不上溯；同 Gate 并列主张以 local alpha 吸收；描述性项禁用 PASS/FAIL 词汇。
```

| ID | 假设 | 判决量 | MES | 身份 |
|---|---|---|---|---|
| H-Z2a1 | 全成员均值扩散 | 配对差（matched-sample） | 10bp/10 日 | Gate1 主 |
| H-Z2a2 | 鲁棒中心位置扩散（成员中位数——非"广度"） | 配对差 | 10bp | Gate1 回退 |
| H-Z2b | 可投资扩散 | 容量子集配对差 | 50bp | Gate2 主 |
| H-P1a | 纯确认政策价值 | 组合级 C−I spread | 年化 1% | Gate2 主 |
| H-Z2c | 超行业协调 | supported 子集 | — | 描述性 |
| H-Z3 | ZJ 排序 | 同池配对差 | 20bp | Gate3 主 |
| H-Z3b/Z4/Z6/P1b | 约束栈 / vs RS / 退出 / 系统政策 | — | — | 描述性 |
| H-Z1 | 端到端（VWAP 代理） | vs 动态暴露基准 | 年化 3% | Gate4 主 |
| H-T1/2/3, Z5, Z7, V1 | 分解与诊断 | — | — | 报告义务 |

## 2. 数据层

### 2.1 主源选定（机械评分卡）
```
SOURCE_SELECTION_SCORECARD（冻结）:
资格线（全部满足才入围）:
  a) 提供带 trade_date 的每日历史成分快照
  b) 连续覆盖 ≥ 3 自然年，快照缺失日率 ≤ 2%
  c) 题材 ID 年度稳定率 ≥ 95%（谱系调整后）
评分（依序判定，先高者胜）:
  1) 覆盖年数多者胜
  2) 落入成分数 [8,100] 带内的题材占比高者胜
  3) 仍并列 → 冻结偏好序: KPL > DC > THS（叙事标注语义优先）
```
主源 = 评分卡胜者；第二源 = 次名（原生复现，不映射）；THS 若未入围仅作交叉校验。普查报告 `CONCEPT_DATA_CENSUS.md` 逐项给出证据。

### 2.2 题材宇宙与排除表（正文冻结）
- 合格题材：成分数 ∈[8,100]；
- **排除正则（完整清单，冻结）**：名称匹配 `融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌` 者剔除；清单开跑前人类目检一次并哈希入库；
- **ConceptCluster**：每日以 Members_{D−1} 计算 Jaccard，complete-linkage（簇内任意两概念 >0.5）；
- **canonical_id 机械规则（冻结）**：merge → 继承 first_seen 最早的 parent canonical_id，同日并列取字典序最小；split → 与旧簇成分 Jaccard 最大的 child 继承，并列取字典序最小，其余 child 新建；多对多按先 merge 后 split 顺序处理；lineage 表（cluster_id/effective_date/parent/child/merge/split/canonical_id）append-only；
- 左截断：主源起始后 120 交易日内首现题材标 left_censored 禁入 new_concept；谱系 Jaccard>0.7（仅 ≤D 数据）。

### 2.3 快照库、双成员集、时钟 PIT
- 每交易日收盘后快照全部可得源，append-only + 抓取时间戳；
- 点火检测集 = Members_{D−1}；Episode 冻结基集 = Members_{D0−1}；MembershipExpansion 逐日记录（H-V1：新增 vs 基集成员收益差、动态 vs 冻结信号差）；
- 时钟 PIT：D 日 22:00 前已抓取且未依赖修订方可用于 D+1；发布时刻不可考字段（原因文本等）回测按 D+2 可用；违反 = 装置失败。

### 2.4 行情数据与合格宇宙
- 个股日线/复权/涨跌停（stk_limit 查表；pre-2019 回退 pct_chg≥+9.8%∧close==high）；封板 close_raw≥up_limit；触板 high_raw≥up_limit；
- **合格宇宙（冻结）**：上市 ≥60 交易日 ∧ 非 ST ∧ 非停牌 ∧ 非退市整理。**全部信号量（层构造、LU 计数、置换 donor、题材成员计数）只在合格宇宙上计算**——新股涨停不进 LU，也不进 donor 集；
- 特征缺失处置：20 日波动/动量需 ≥15 个有效日否则该股当日退出分层（记 feature_missing）；股性：历史 ≥250 日用 250 日窗，60-249 日用扩展窗（标 expanding_propensity）；
- 数据质量闸门（单位锚定、完整性、涨停价抽核 20 样本、覆盖率 ≥98%）失败 → GATE_FAILED.flag 阻断下游。

## 3. 状态变量与日度零模型

### 3.1 三对象与 minP 族校准（v7.1 修订：统一尺度）

```
分层（合格宇宙，逐日）: 交易板块 × 流通市值三分位 × 20日波动三分位
  × 20日动量三分位 × 股性三分位；层最小 8 只；粗化序（冻结）: ①并动量 ②并波动 ③并股性 ④并市值；板块永不合并
置换: 保留当日各层真实涨停股数，层内重排涨停标签
  B_random = 2000 条随机置换；p 值 = (1 + r) / (B_random + 1)，
  其中 r = #{随机置换统计量 ≥ 观测值}；identity 由分子分母的 +1 承担，
  MUST NOT 另行加入置换集（off-by-one 唯一化）；N_total = 2001
(1) p_marg(c,D): 题材 c 的边际置换尾概率（以 LU 计数为统计量的精确置换尾）
    —— 全体题材统一尺度，无学生化/精确混用，退化分布自然得 p≈1
(2) p_FWER(c,D): Westfall-Young **minP** ——
    对每次置换 b，以秩法得全部休眠题材的 p_{c,b}；m_b = min_c p_{c,b}；
    p_FWER(c) = (1 + #{ m_b ≤ p_marg_obs(c) }) / (B_random + 1)
(3) CoordinationState(c,D) = −log10( p_marg(c,D) ) —— 全部合格题材每日计算，
    专用于 DORMANT 历史，不受当日族结构影响
点火条件: LU_real ≥ 2 ∧ p_FWER ≤ α_day（α_day 由 §5 冻结）
```
- **两阶段 Monte Carlo（冻结）**：全部候选先 B_random=2000；若 p̂_FWER ∈ [α_day/3, 3α_day] → **无条件**升至 B_random=20000 重算并以后者判决；程序级错误率由 §5 路径仿真端到端吸收（仿真运行同一两阶段流程）；seed = hash(trade_date, source_version, spec_version)；
- 证据边界措辞（冻结）：本装置严格校准**全局零假设下的日度扫描错误**；事件级强 FWER 依赖 subset pivotality 类条件，仅作近似解释，判词禁用"强 FWER 证明"；
- 分层诊断义务：日有效层数、中位层规模、粗化率、degenerate 记录。

### 3.2 行业条件口径
每点火事件加算 ThemeShock|Industry（分层 = 申万一级行业 × 市值三分位，其余维度先按粗化树合并；行业内层不足 8 只 → `industry_condition_uninformative`）；三态标签：p_cond≤0.10 → `industry_residual_supported`；>0.10 且检验有效 → `not_supported`；层稀 → `uninformative`。H-Z2a 判全部事件；"超行业协调"宣称走 H-Z2c（描述性）。

## 4. Episode 状态机

### 4.1 状态与生命周期（v7.1 补终点定义）
```
DORMANT（协调休眠）: 过去 20 交易日 CoordinationState ≥ 2 的天数 ≤ 1 ∧ Crowd 条件:
  题材份额分位历史 ≥120 日 → 自史分位 < 0.80
  60–119 日 → 扩展窗分位 < 0.80（标 crowd_expanding）
  < 60 日 → 当日横截面分位（全部合格题材中）< 0.80（标 crowd_xsec）
  三级 fallback 事件分层报告，MUST NOT 静默合并（新题材无宽松入口）
IGNITION: DORMANT 次日起 LU_real≥2 ∧ p_FWER≤α_day；同簇同日多概念 → p_marg 最小者胜
  （并列取题材 ID 字典序小）；EpisodeID=(canonical_id@D0, D0) 即刻锁定，基集=Members_{D0−1}
CONFIRMATION（landmark，D0+4 收盘统一裁决）: 见 §4.2
生命周期终点（冻结）:
  确认失败 → SignalEpisodeEnd = D0+4
  确认成功 → SignalEpisodeEnd = D0+10（固定，与主持有期一致）
  冷却 20 交易日自 SignalEpisodeEnd+1 起算（按 canonical_id）
  TradingPositionEnd 独立（EXIT-3C 变体可延至 60 日，不延长 Episode 身份）
  CAR(1..60) 为观察窗，不影响任何身份
```

### 4.2 确认（landmark；成员按冻结基集；全部剔除最高连板链本股）
```
成员分类: ClosedLimitMember（收盘封板）| TouchedOnlyMember（仅触板）|
          StrongResidualMember（收盘 ≥ +5% 未封板）
CONFIRM = [ 新增 ClosedLimitMember（相对 D0 封板集）≥ 1 ]
        ∧ [ Distinct(ClosedLimit ∪ StrongResidual) ≥ 2 ]      # 纯 TouchedOnly 不得确认
        ∧ [ 扩散: Age1..4 任一日 p_marg ≤ 0.10 且当日有新增封板成员
            或 晋级: MaxBoard 抬升 ∧ 连板链起点 ≥ D0−1 ]
        ∧ [ BombRate(Age1..4 合并, 触板 ≥3 时) ≤ 0.5 ]
成立 → 入场 D0+5；失败 → 夭折点火全量入库
```

### 4.3 EpisodeType 与检测滞后诊断（阈值冻结）
- new_concept（首现 ≤120 日，剔 left_censored）/ reactivation，分别报告；
- **DetectionLag 诊断（冻结定义）**：PriceShockDay = D0−60..D0−1 内首个 |日收益| ≥ 2×滚动 20 日 σ 的日；AmountShockDay = 首个 成交额 ≥ 2×自身 20 日均值 的日；DetectionLagProxy = D0 − min(两者)；成熟度三分类：`coordination_early`（PreIgnitionCAR20 < +10% ∧ D0 价格 120 日分位 < 0.7）/ `fully_mature`（CAR20 ≥ +25% 或分位 ≥ 0.9）/ 其余 `price_advanced_but_coordination_new`。仅诊断，不改触发。

## 5. 年度错误预算：路径级零模型（v7.1 修订：完整路径）

```
预算: 全局零假设下 UCB_95( E[假 Episode 数/年] ) ≤ 2      # 置信上界口径
生成器（冻结）:
  在 donor 层内以 20 交易日为块（随机块起点、circular），
  在可比股票间**联合置换完整路径向量**:
    { raw return, high/close/涨跌停状态, amount, turnover, 停牌/ST 状态 }
  ——整段搬移、保持轨迹内部一致性；MUST NOT 只换涨停标签而留收益/成交额在原股票
  donor 资格（冻结 caliper）: 同交易板块 ∧ 同市值三分位 ∧ 同股性三分位
    ∧ 块起点 20 日波动同三分位 ∧ 块起点 20 日动量同三分位   # 与日度五维分层对齐
零模型语义（冻结措辞）: 保留市场逐日情绪、行业共同冲击、个股连板序列与时间依赖，
  消除【题材成员身份 ↔ 协调轨迹】的特异对齐（"保留题材热度聚集"表述废除）
校准流程: 合成年数由目标精度定（初始 ≥400，UCB 半宽 ≤0.3 为准），对每条合成年
  运行完整装置（DORMANT→两阶段 minP IGNITION→landmark CONFIRMATION→冷却→簇去重）；
  α 搜索: 网格 {0.2%,0.4%,0.6%,0.8%,1.2%} 线性插值，多解取最严；
块长敏感性: 主 20 日，{10,40} 敏感性；跨块连板链在块边界截断（按块内计，处置留痕）
漏斗输出义务（至最终交易层）: 假点火 → 假确认（分扩散/晋级支）→ 假可投资事件
  → 假 ZJ 交易 → 假实际成交，全链每年期望数
```

## 6. 载体 ZJ 与第二法庭展开

- 容量：ADV20 ≥ 3.33 亿（AUM 2 亿 ÷12 ÷5%）∧ 流通市值 ≥50 亿；纯度主资格 D0−1 在籍 ≥20 日；参与（基集口径 D0→D0+4 超额>0 ∧ 换手 ≥1.2×20 日均值）；护栏（D0+4 非涨停 ∧ Episode 涨停 ≤1 ∧ 累涨<40%）；可买（D0+5 非开盘涨停/停牌 ∧ GapLimitRatio ≤0.70）；排序 EventAmountShock = mean(Amount[D0..D0+4])/mean(Amount[D0−20..D0−1])，取前 2，替补至第 4，单标的半仓；
- **第二法庭完全展开（冻结）**：
  - B 臂：池 ∈{3,4} 精确枚举全部 2-组合；池 ≥5 → 200 次无放回抽 2-组合，seed=hash(episode_id,'B')；
  - C0 池 = 容量 ∧ 可交易（无纯度/参与/护栏），同 EventAmountShock 排序取 2；
  - N 臂：RS20 = 个股 20 日收益 − 题材基集等权 20 日收益（题材相对口径），池内前 2；
  - B/C0/N 与 T_ZJ 使用**完全相同**的 D0+5 可买性、替补、半仓规则；
  - estimand = 事件级配对差之均值，lineage 聚类 bootstrap（§9）；
  - common support：H-Z3/Z4 限"完整池 ≥3 且可执行"事件集；H-Z3b 限"完整池 ≥2 ∧ C0 池 ≥2"；池不足题材属性必报。

## 7. 四级法庭

### 7.1 第一法庭：风险集匹配（v7.1 方法论升级）

**框架 = risk-set matching**：每个 D0，处理 = 当日点火题材；风险集 = 同日 DORMANT 且未点火的合格题材；
- 匹配：k=1、**同一 D0 风险集内无放回**；跨日期同一题材可再次作为对照（相关性由 lineage 聚类吸收）；协变量冻结于 D0−1（窗口 [D0−20,D0−1]）：成分数、题材收益、成交份额、主板占比；标准化欧氏距离、卡尺 1.0σ；约束：T-A 成分 Jaccard<0.2、处理/对照组合个股重叠 ≤20%；失配 → 事件退出（unmatched，>30% 警报）；
- **一次生成、整体判定**：审计协变量（匹配 4 项 + 市值/波动/涨停倾向/题材年龄/换手/标签泛化）任一 |SMD|>0.10 → MATCH_BALANCE_FAILED（禁止迭代删对）；
- Switching：主 ITT（对照日后点火不改身份）；副 per-protocol（对照点火日删失）；
- **Estimand 与判词（冻结）**：全部 H-Z2 效应 = **matched-sample 配对差**（条件于已形成配对；规避最近邻匹配下普通 bootstrap 的失效问题），判词禁用"总体无条件 ATT"表述；
- 组合与入场：H-Z2a1 = 基集可交易成员等权、H-Z2a2 = 成员收益中位数（**鲁棒中心位置**）、H-Z2b = 容量子集（ADV20_D0 ≥1 亿等 **D0 可得条件** + 各自入场日独立可买性）等权；T 与 A 均 D0+5 入场（A 用伪时钟），主持有 10 日（副 20 日），CAR(1..60) 必报；
- Gate1 解锁规则（冻结）：H-Z2a2 检验当且仅当 H-Z2a1 **未达 Economically PASS**；CI 构造：单侧 cluster bootstrap 百分位 CI，水平 = 1−local α；
- a-FAIL∧b-PASS 判词模板：先加验 Effect_investable−Effect_noninvestable 与匹配题材容量成员对照，才可定性；
- 分解诊断：E1（点火 vs 风险集未点火，D0+1 起）、E2（landmark：D0+4 分类，统一 D0+5 起测）、E3（延迟成本双口径）。

### 7.2 政策比较（组合账本冻结）

```
InstrumentSet（H-P1a）: 仅 D0 收盘可得信息 —— Members_{D0−1} ∩ ADV20_D0≥1亿
  ∩ 非ST/非停牌@D0 ∩ 上市≥60日；Policy I 于 D0+1、Policy C 于 D0+5
  各自独立施加执行日可买性（开盘涨停/停牌/GapLimit>0.70 剔除，不得反向删除对方标的）
组合账本（冻结）:
  事件预算 = 初始 NAV / 6（固定，不因事件不足放大）；事件内标的等权；
  同股同时属两个活跃 Episode → 最早事件持有，后到事件该股份额留现金（记 shared_position_reject）；
  单股总权重 ≤ 2 × 单事件单股预算；现金收益 = 0（冻结，保守）；
  部分成交剩余留现金；优先级 = 先到先得 → 同日 D0 p_FWER 升序 → 题材 ID 字典序；
  无抢占；拒绝事件记 rejected_by_capacity 不补入；空池即时释放名额
判决（H-P1a 主，Gate2 α=0.025）: CI_lower[年化R(C) − 年化R(I)] > 1%
  （日历时间组合 spread 直接估计，stationary bootstrap）
  护栏（点估计）: MDD_C−MDD_I ≤ 2pp ∧ CVaR 不劣
  双口径必报: 资本口径 R_C−R_I 与投入调整口径 (R_C−R_cash)/Exp_C − (R_I−R_cash)/Exp_I
H-P1b（描述性）: C 于 D0+4 重建 ZJ 的系统政策；M-I/M-C 伪政策与 DiD 必报
```

### 7.3 第三法庭（完全展开）
- 定义：Breadth_c,D = 基集可交易成员中 close_qfq > MA20(close_qfq) 占比；ThemeRS20 = 基集等权 20 日收益 − 沪深300 同期；StockExcess20 = 个股 20 日收益 − 基集等权 20 日收益；
- EXIT-3C：Leg A（Age≤10 ∧ Breadth<0.30 → 全退）；B1（CrowdPctl>0.90 → 减半一次）；B2（Breadth ≤ Episode 峰值−0.20 ∧ ThemeRS20<0 → 余仓退）；C（60 日兜底）；优先级 A>B2>B1>C；V-STOP 变体（StockExcess20 <−15% 单股退）；
- **比较口径（冻结）**：与固定 10 日主退出在**同一入场流的完整组合模拟**中对比（资本占用、并发挤出、换手成本、更长暴露全部内生），日历时间差为主、事件级分解为辅（描述性，Gate3）。

### 7.4 第四法庭：日线无自冲击 VWAP 执行代理法庭
- **执行公式（冻结）**：VWAP = amount×10/vol（元/股，日线）；FillAmount = min(DesiredOrder, 0.05 × 当日成交额)；同股多订单先合并再检查 5%；一字日（high==low）零成交；涨停但有成交的日按公式参与（买入端 GapLimit 已在 D0+5 入场规则中约束）；卖出同 5% 上限，未完部分逐日滚动（跌停/停牌顺延），剩余仓位继续计收益；滑点命名 Decision-to-VWAP slippage；容量情景 1/3/5% 三档；
- **主对照（v7.1 修订）**：动态暴露匹配基准 R_dyn,t = Exposure_t × R_capacity,t + (1−Exposure_t) × R_cash,t（容量指数 = 全 A 容量可交易等权**月度再平衡**、与策略同一成本模型、毛/净双口径）；全投资容量指数与沪深300/现金为经济参照；A_sys（匹配题材伪时钟全管道）仅归因；
- H-Z1 判决：策略 vs R_dyn 的年化净 alpha，MES=3%（Gate4 α=0.05）。

## 8. 安慰剂与自检（通过线冻结）

**Freeze 前（合成自检）**：注入信号检出/无效拒出、未来字段哨兵、置换均匀性、minP vs 小样本暴力枚举逐位对照、landmark 断言、盲化白名单审计、匹配一次生成断言、路径生成器"连板序列保留 + 收益/成交额随轨迹整体搬移"断言。
**Freeze 后（经验安慰剂）**：
- P3：伪点火日从"DORMANT 且其后未点火"日抽取，跑全管道 → 通过线 |d|<0.1 ∧ CI 含 0；
- P4：每 canonical 簇独立循环位移避开全部 Episode 窗口 → 同一通过线；
- （P3∧P4 = Gate0-F，锁 Gate1）；
- P1：ZJ 池内排序置换（H-Z3 推断引擎，小池枚举；其合成自检 = Gate0-Z，锁 H-Z3）；
- P2：匹配对内触发置换 —— 仅诊断。

## 9. 分法庭主推断（v7.1 修订：废除"唯一主 CI"）

| 法庭/假设 | 主推断（唯一） | 稳健性 |
|---|---|---|
| H-Z2 族（a1/a2/b/c） | matched-sample 配对差 + 两向 cluster bootstrap（canonical lineage × 入场时间块 20 日） | 40 日块；stationary bootstrap |
| H-P1a / H-Z1 / H-Z6 | 日历时间 spread + stationary bootstrap（期望块长 20） | NW（lag=max(2×持有期, auto)） |
| H-Z3 / Z3b / Z4 | 事件级同池配对差 + lineage 聚类 bootstrap | 时间块加聚 |
- 时间块说明（留痕）：20 日块 = 2×主持有期，块际残余重叠仅影响 ≤1/20 邻界配对、幅度 ≤50% 窗口——以 40 日块敏感性夹逼；重叠图社区聚类因链式合并风险不作主口径；
- 四分法判词（全法庭统一）：Statistically Positive（单侧 CI_l>0）/ Economically PASS（CI_l>MES）/ Economically FAIL（CI_u<MES）/ INCONCLUSIVE；
- 状态覆盖：每市场状态独立簇 n≥10 ∧ 占比 ≥15%；频率闸门 [10,150]/年。

## 10. 序贯影子法庭（联合校准）

- Append-only 铁律：Episode、配对、簇身份、目标试验定义、统计权重、控制归属、交易账本一经形成永不重定义；
- 分析时钟 = 已锁定配对数；**n_target 分假设**：n_Z2a1 / n_Z2a2 / n_Z2b / n_P1a / n_Z1 由盲化 SSD 分别产出；影子终期 = Gate1/Gate2 主假设 n_target 之最大者；中期于该最大值的 1/3、2/3 配对数处；
- **边界联合仿真（冻结生成器）**：从盲化 pilot 配对残差按（簇 × 20 日时间块）重采样；**三个效应情景**：① 同质位移 θ=MES；② 稀疏混合（20% 事件承载 5×MES、80% 为零）；③ 状态依赖（牛市 +2×MES / 熊市 −MES 混合）；每条路径运行完整决策树（a1→a2 回退→Gate2 解锁→三个分析时点），校准整体 Type I / power / 期望样本量后冻结数值边界；提前判决仅限 Economically PASS，提前 FAIL 仅 non-binding futility，正式 FAIL 只在终期。

## 11. 冻结流程（顺序即依赖）

```
1. 快照普查（评分卡机械选主源）→ 快照库启动（时钟 PIT 字段）
2. 全引擎 + 合成数据工程自检（§8 前半）
3. 路径级零模型（§5 完整路径生成器）→ UCB 校准 α_day → Episode 生成规则冻结
4. 盲化设计可行性审计（Freeze 前，白名单输出，禁触收益方向）:
   unmatched 率 / SMD 分布 / ZJ 池≥3 占比 / 有效簇数 / 每状态事件数 / 数据完整率
   → 不可行处允许修复设计参数（留痕 Decisions），此时仍未见任何收益方向
5. 冻结前盲化样本量估计（白名单: 方差/ICC/事件频率/各 n_target）
6. 序贯边界联合仿真（§10 三情景）→ 边界冻结
7. ★ FREEZE TAG（sfl-v7.1-freeze）
8. 经验安慰剂（Gate0-F/Z）→ DEV 探索性读数（internal pilot 身份）→ OOS-B 一次
9. 影子运行（append-only 序贯法庭）→ 按 §0 判决
```

## 12. 冻结参数总表（canonical 全量）

| 域 | 参数 → 值 |
|---|---|
| 主源 | 评分卡 §2.1；偏好序 KPL>DC>THS |
| 宇宙 | 成分 [8,100]；排除正则 §2.2 全文；上市 ≥60 日；覆盖率 ≥98% |
| 聚类 | Jaccard>0.5 complete-linkage；canonical 继承规则 §2.2；左截断 120；谱系 0.7 |
| 分层 | 板块×市值3×波动3×动量3×股性3；层 ≥8；粗化序动量→波动→股性→市值；特征最少 15 有效日；股性扩展窗 ≥60 日 |
| 零模型 | B_random=2000（p=(1+r)/(B+1)，identity 唯一由 +1 承担）；临界带 [α/3,3α] 无条件升 20000；minP 族校准；seed=hash(date,src,ver) |
| 预算 | UCB95(E[V])≤2/年；α 网格 {0.2,0.4,0.6,0.8,1.2}%、插值取最严；合成年 ≥400 或 UCB 半宽 ≤0.3；donor caliper 五维（§5）；块 20（敏感 10/40、随机起点、circular） |
| 状态机 | DORMANT：CoordState≥2 天数 ≤1/20 日 ∧ Crowd 三级 fallback<0.80；点火 LU≥2 ∧ p_FWER≤α_day；确认 landmark D0+4（§4.2）；入场 D0+5；SignalEnd=D0+4/D0+10；冷却 20 日自 End+1 |
| ZJ | ADV≥3.33 亿 ∧ 市值 ≥50 亿；在籍 ≥20 日；参与/护栏 §6；GapLimit≤0.70；EventAmountShock 前 2 替补至 4 半仓；B/C0/N 规则 §6 |
| 匹配 | 风险集内 k=1 无放回（跨日可复用）；4 协变量@[D0−20,D0−1]；卡尺 1.0σ；Jaccard<0.2；重叠 ≤20%；SMD≤0.10 整体判定；matched-sample estimand |
| 政策 | InstrumentSet 仅 D0 信息；账本 §7.2（预算 NAV/6、同股先到先得、单股帽、现金收益 0） |
| 执行 | VWAP=amount×10/vol；Fill=min(单,5%×日成交额)；同股订单先合并；一字零成交；卖出滚动顺延；成本买 12.5bp/卖 17.5bp（印花税 PIT） |
| 退出 | 主固定 10 日（副 20）；EXIT-3C §7.3（组合级对比）；V-STOP −15% |
| 基准 | H-Z1 主对照 = 动态暴露匹配基准（容量指数月度再平衡+现金）；参照组固定 |
| 推断 | 分法庭主推断表 §9；MES：10bp 科学 / 50bp 一庭经济 / 20bp 二庭 / 1% 政策 / 3% 四庭；Gate local alpha §1 |
| 序贯 | 时钟=配对数；分假设 n_target；终期=Gate1/2 主假设最大 n；三效应情景边界；提前判仅 PASS |
| 诊断阈值 | DetectionLag：2σ 价格冲击 / 2× 均值成交冲击 / 成熟度三分类 §4.3 |

## 13. 给验证 Agent 的交代要点

1. 本文件为唯一真相源；任何歧义 → 停止上报，禁止参考旧版补全；
2. 强制单测（新增粗体）：minP vs 暴力枚举、**off-by-one 断言（p 值分母 = B_random+1，identity 不在置换集内）**、CoordinationState 与 p_FWER 分离断言、landmark 断言、**路径生成器全向量搬移断言（涨停状态与收益/成交额 MUST 同轨迹移动）**、**canonical_id 继承规则断言（构造 merge/split 已知答案）**、风险集无放回断言、账本同股冲突断言、append-only 断言、盲化白名单审计；
3. 夭折点火/空池/unmatched/拒绝/共享持仓冲突全量入库；
4. 闸门失败 flag 阻断；影子期间改规则 = 作废。

---

## 附录 A：第六轮审查二十红线 → v7.1 落点
1 Gate0 拆分+通过线 → §1/§8｜2 minP 统一尺度 → §3.1｜3 off-by-one 唯一化 → §3.1｜4 全路径向量联合置换 → §5｜5 删"题材热度聚集" → §5｜6 UCB 校准+α 搜索冻结 → §5｜7 块长敏感性 → §5｜8 canonical 继承算法 → §2.2｜9 Episode 终点/冷却起点 → §4.1｜10 Crowd 三级 fallback → §4.1｜11 鲁棒中心更名+死亡判词收窄 → §0/§1/§7.1｜12 Gate1 解锁规则+CI 构造 → §7.1｜13 Gate 内 local alpha+描述性降格 → §1｜14 H-Z2c 最小冻结定义 → §3.2/§7.1｜15 评分卡+排除正则全文 → §2.1/2.2｜16 合格宇宙与缺失处置 → §2.4｜17 H-P1a 篮子仅 D0 信息 → §7.2｜18 组合账本 → §7.2｜19 分法庭主推断+matched-sample 判词+风险集匹配 → §9/§7.1｜20 盲化设计可行性审计前置 → §11

## 附录 B：设计权选择留痕（v7.1 增量）
1. **minP 而非"退化题材退出家族"**：统一尺度且不损失退化题材的信息（其 p≈1 自然无害），比排除法少一条特殊分支；
2. **时间块取 20 日（2×持有期）而非重叠图社区**：重叠图有链式合并风险且不可预先枚举；块际残余重叠以 40 日块敏感性夹逼，留痕；
3. **现金收益冻结为 0**：保守方向（低估 Policy C 与策略），避免引入无风险利率序列的新数据依赖；
4. **风险集匹配采纳**（审查 §二十八）：同日无放回、跨日可复用、lineage 聚类吸收——它同时解决了复用作用域（§二十七）与"全局无放回耗尽优质对照"两个问题，是本轮唯一的方法论升级且零新因子。

*登记时间：2026-07-16。冻结对象：全文。变更 = v7.2 = 新试验。§0 未签署、§11 步骤 1-6 未完成前不得 freeze。*
