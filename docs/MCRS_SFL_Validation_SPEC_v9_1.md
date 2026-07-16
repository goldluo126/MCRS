# MCRS SFL 验证规格书 v9.1 — FINAL CANONICAL（单文件全展开）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / FINAL CANONICAL`
版本：`v9.1`（**完全自包含单文件**，替代 v1-v9.0 全部版本；本文未出现的旧条款一律失效。第九轮外部审查 18 条红线全部核实成立、零驳回，含设计方自认的 Run-in 统计逻辑错误与 canonical 自相矛盾）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文件 + RESOLVED_CONFIG + 冻结环境（§13）产生逐日完全相同的信号、配对、交易与判词。全部 `D+k` 为交易日偏移。

---

## 0. 终局条款、识别边界与判决语义（签署对象 = §12 联合哈希包）

**永久识别边界（冻结声明）**：本实验可识别的命题是——**给定供应商实际输出的题材本体，协调相变是否携带未来收益信息**（条件于本体的命题）。供应商本体在反事实市场中如何形成，不可识别；"三种 alpha 完全分离"的表述废除，改为"供应商识别效应隔离诊断 + 条件本体下的协调/载体效应检验"。

**科学死亡线（含 matched-support 限制）**：影子数据上四判定（Immediate 均值/中心、Landmark 均值/中心）全部 Economically FAIL 于 MES_sci=10bp 时，死亡命题 = "**在风险集匹配共同支持域内的**点火事件中，题材协调相变未能在点火后 0-4 日或 5-14 日窗口向供应商题材全体成员产生 ≥10bp 的平均或中心收益扩散"。out-of-support 事件（无法匹配的极端相变）明示不在本判决范围内；"不可因果识别"与"没有效应"分开书写。

**判决语义**：false-PASS 按 local α；false-death β=0.025（FAIL 需单侧 97.5% 上界 < MES）；四分法判词（Statistically Positive / Economically PASS / Economically FAIL / INCONCLUSIVE）；四人群（signal/matched/confirmed/executed）分层报告禁跨层外推；**DEV 与 OOS-B 正式身份 = 工程与方向性证据**（"法庭"措辞废除）；终审只认 self_collected 数据；H-Z1 为**项目资源决策指标**（非科学推断，不入 FWER 家族）；RESOLVED_CONFIG 必含分情景 Operating Characteristics 表（§10.4）供知情决策。
签署人：________ 日期：________

## 1. 假设层级与 Gatekeeping

```
Gate0-F（锁 Gate1）: P3 ∧ P4 对四个科学 endpoint 分别等效性通过（§8）
Gate0-Z（锁 H-Z3）: B 臂机器合成自检
 → Gate1（科学法庭）: H-Z2I-L-a1 Landmark 均值（α=0.025）→ 未达 Econ-PASS 解锁 L-a2 中心（α=0.005）
                     H-Z2I-I-a1 Immediate 均值（α=0.015）→ 同规则解锁 I-a2（α=0.005）
 → Gate2（四判定任一 Statistically Positive 解锁）: H-Z2b（α=0.025）/ H-P1a（α=0.025）
    描述性: H-Z2C（确认后条件效应+选择警告）、H-Z2c（行业）
 → Gate3（H-Z2b 或 H-P1a 任一 Econ-PASS 解锁）: H-Z3（α=0.05，Gate3+ 唯一正式检验）
    描述性: H-Z3b/Z4/Z6/P1b
 → Gate4（同 Gate3 解锁条件）: H-Z1 = 项目资源决策指标（报 CI 与 ≥3% 与否；无正式推断 PASS，
    不占 alpha——消除 sibling multiplicity）
序贯提前判决（仅 Econ-PASS）限 Gate1/2 主假设；Gate3 只终期；下游策略自影子第一天机械运行
并加密封存，Gate 解锁后启封未被查看的数据；此机制进 OC 仿真。
```

| ID | estimand（§7 冻结公式） | 收益口径 | MES | 时钟 |
|---|---|---|---|---|
| H-Z2I-I-a1/a2 | 点火即时（均值/中心） | Close_D0→Close_{D0+4}，全基集 MTM | 10bp | 事件 |
| H-Z2I-L-a1/a2 | 点火 landmark（均值/中心） | Close_{D0+4}→Close_{D0+14}，全基集 MTM | 10bp | 事件 |
| H-Z2b | 容量子集**可执行筛选效应** | VWAP_{D0+5}→VWAP_{D0+15}，含成本与 5% 参与 | 50bp | 事件 |
| H-P1a | 纯确认政策 | 组合日历 spread | 年化 1% | 日历 |
| H-Z3 | ZJ 排序 vs 池等权 | D0+5 VWAP→D0+14 收盘 | 20bp | 事件 |
| H-Z1 | 端到端（资源指标） | 252×mean(日 spread) vs 动态基准 | 3%（参考线） | 日历 |

容量双阈值声明：ADV≥3.33 亿 = ZJ 系统容量门槛；ADV≥1 亿 = 题材篮子可投资阈值——两个"可承载"定义分别标注禁混用。

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
- 资格线：带 trade_date 的每日历史成分；连续覆盖 ≥3 年、快照缺失日率 ≤2%；题材 ID 年度稳定率 ≥95%（谱系调整）；
- 评分（依序）：覆盖年数 → [8,100] 带内题材占比 → 偏好序 KPL>DC>THS；第二源 = 次名原生复现；THS 交叉校验；
- 标签：供应商回溯历史 = `vendor_reconstructed_history=true`（仅工程/方向性用途）；自建快照 = `self_collected=true`（唯一终审资格）。

### 2.2 题材宇宙治理
- 合格题材：成分数 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`，开跑前目检+哈希；
- **确定性聚类**（每日，Members_{D−1}）：候选对 = Jaccard>0.5，按 (J 降序, ID 对字典序) 排序依次处理：双方未入簇→建簇；一方在簇→与簇全员 J>0.5 才并入；双方异簇→并簇需全对 >0.5；未入簇者单簇；
- canonical_id：merge 继承 first_seen 最早（并列取 ID 小）；split 由最大 Jaccard 子簇继承（并列同）；lineage 表 append-only；
- 左截断：主源起始后 120 交易日首现题材禁入 new_concept；谱系 Jaccard>0.7（仅 ≤D 数据）。

### 2.3 快照库、双成员集、时钟 PIT
每交易日收盘后快照全部源（append-only+抓取时间戳）；点火检测集 = Members_{D−1}；Episode 基集 = Members_{D0−1}；MembershipExpansion 日记（H-V1 诊断：新增 vs 基集成员收益差、动态 vs 冻结信号差）；时钟 PIT：D 日 22:00 前抓取且未依赖修订方可用于 D+1；原因文本类回测按 D+2；违反 = 装置失败。

### 2.4 行情与合格宇宙
合格宇宙 = 上市 ≥60 交易日 ∧ 非 ST ∧ 非停牌 ∧ 非退市整理；全部信号量仅在合格宇宙上计算；封板 = close_raw≥up_limit、触板 = high_raw≥up_limit（pre-2019 回退 pct_chg≥+9.8%∧close==high）；20 日特征需 ≥15 有效日否则当日退出分层；股性 = 过去 250 日涨停次数分位（60-249 日扩展窗标 expanding）；质量闸门（单位锚定/完整性/涨停价抽核 20/覆盖率 ≥98%）失败 → GATE_FAILED.flag 阻断。

### 2.5 本体漂移治理（v9.1 新增）
- **Ontology Drift Gate**（月度监控）：题材总数、平均成员数、日成员变更率、ID 生灭率、改名率、API 发布时间、schema hash；任一越过预登记断点（相对基线变化 >30% 或 schema 变更）→ 暂停正式影子 → 生成 `measurement_regime_id` → 重新 Run-in（§11）→ 重校准 → 预登记规则决定分层继续或重开正式样本；**不同测量制度下的 Episode 禁止合并**；
- **定期盲化 null 审计**：每 125 交易日，在已收集成员快照上执行 live null replay（§11.2，无收益方向），核对假触发预算；失配 → 暂停法庭、不改旧信号、升版本、新制度样本重启。

## 3. 日度零模型（minP）

### 3.1 分层与置换
```
分层: 板块 × 流通市值3 × 20日波动3 × 20日动量3 × 股性3；层 ≥8；
粗化序: ①并动量 ②并波动 ③并股性 ④并市值；板块永不合并
置换: 保留当日各层真实涨停数，层内 Fisher-Yates 重排标签；
  每 b 独立 PRNG 子流 substream = SHA256(trade_date‖source_ver‖spec_ver‖b)（UTF-8、canonical 拼接）
  不同 b 允许重复配置；各层独立打乱后拼接为全局 permutation
B_random = 2000；两阶段: 任一候选 p̂_FWER∈[α_day/3, 3α_day] → 当日全族追加 18000 至 20000
  （前 2000 行与统计量不可变）
```

### 3.2 统计对象
```
S[b,c] = LU_{c,b}（b=0 为观测行；(B+1)×C 矩阵）
p[b,c] = #{ b'∈{0..B}: S[b',c] ≥ S[b,c] } / (B+1)     # 全行含自身取秩，≥ 计并列
p_marg(c,D) = p[0,c]（Monte Carlo permutation tail probability）
m_b = min_c p[b,c]（b=1..B）
p_FWER(c,D) = (1 + #{ b: m_b ≤ p[0,c] }) / (B_random + 1)
CoordinationState(c,D) = −log10 p_marg（全部合格题材每日计算，专用休眠历史）
点火: LU_real ≥ 2 ∧ p_FWER ≤ α_day
```
证据边界：严格校准全局零假设下的日度扫描错误；事件级强 FWER 仅近似，判词禁用"强 FWER 证明"。行业条件口径：ThemeShock|Industry（申万一级×市值3 分层，其余粗化；层<8 → uninformative）；三态标签 supported/not_supported/uninformative（p_cond 0.10 线）。

## 4. Episode 状态机

```
DORMANT: 过去 20 日 CoordinationState≥2 天数 ≤1 ∧ Crowd 三级 fallback <0.80
  （≥120 日自史分位 / 60-119 扩展窗[crowd_expanding] / <60 横截面[crowd_xsec]；分层报告禁合并）
IGNITION: DORMANT 次日起 LU_real≥2 ∧ p_FWER≤α_day；同簇同日取 p_marg 最小（并列 ID 序）；
  EpisodeID=(canonical_id@D0, D0) 锁定；基集 = Members_{D0−1}
CONFIRMATION（landmark，D0+4 收盘统一裁决；全量基于基集）:
  p_base_marg(Episode,D): 身份冻结、可交易状态动态、成员按当日 PIT 特征定位当日全市场分层、
    复用当日置换矩阵；不可交易成员当日不进 LU 分子；可交易基集 <8 → 当日不可检验
  成员分类（剔最高连板链本股）: ClosedLimit（收盘封板）/ TouchedOnly（仅触板）/
    StrongResidual（收盘 ≥+5% 未封板）
  CONFIRM = [新增 ClosedLimit ≥1] ∧ [Distinct(ClosedLimit∪StrongResidual) ≥2]
          ∧ [扩散: Age1..4 任一日 p_base_marg≤0.10 且有新增封板成员
             或 晋级: MaxBoard 抬升 ∧ 连板链起点 ≥D0−1]
          ∧ [BombRate(Age1..4 合并, 触板≥3) ≤0.5]
时间轴（交易日）: 入场执行 D0+5（=持有日 1）｜退出信号 D0+14 收盘｜退出执行 D0+15
  SignalEpisodeEnd: 确认成功 D0+14 / 失败 D0+4；冷却 20 日自 End 次日（按 canonical_id）
  CAR(1..60) 自 D0+5 起纯观察窗；TradingPositionEnd 独立
诊断: DetectionLag = D0 − max(最近正向激活段起点)（激活日 = 日收益 ≥+2×20 日 σ，段间隔 ≤5 日；
  成交冲击同构 ≥2×20 日均额）；负向冲击单独记；成熟度三分类（CAR20 +10%/+25%、价格分位 0.7/0.9）
EpisodeType: new_concept（首现 ≤120 日，剔左截断）/ reactivation，分别报告
```

## 5. 条件本体零模型与年度错误预算（正式更名）

**零假设（冻结措辞）**：**条件于已观察到的供应商成员路径**，价格协调轨迹与题材身份无特异对齐。本装置 MUST NOT 称"完整数据生成过程"或"数据生成过程 closure"——供应商成员过程的反事实不可由价格置换识别（§0 永久边界）。

```
四阶段数据分离（状态资格线，修复奇偶分割缺陷）:
  生成器开发集与验证集各须含 ≥1 个 UP 状态年 ∧ ≥1 个 DOWN 状态年（HS300 年度涨跌定义）
  无法满足 → 历史年度校准禁用，α 只能由 live null replay（§11.2）产出
  合成年再对半 → α 校准合成年 / α 验证合成年
生成器: donor 层 = 板块×市值3×股性3×申万一级行业×块起点波动3×块起点动量3；
  donor 排斥: recipient 与 donor 在块起点无共同**合格题材**标签（排除正则命中的机械标签
    不计入重叠判断——修复可行性问题）
  受约束 bijection（冻结算法）: Hopcroft-Karp 最大基数匹配，目标字典序 =
    ①最大化成功交换股票数 ②最大化 recipient-donor 题材距离 ③ID 序；禁 self-match；
    无可行 donor → 保留原路径记 unswapped
  unswapped 闸门: 总体 ≤20% ∧ **题材度前 20% 股票的 unswapped 率 ≤ 总体 1.5 倍**
    （label-degree / 涨停倾向 / 市值条件 unswapped 率必报——修复选择性缺失）
  搬移 = 无量纲向量 { r_close, high/prev, low/prev, amount/ADV20_pre, turnover/mean_pre, 停牌旗标 }
    → recipient 基线重建 → 涨停/触板按 recipient 板块规则重判 → 全部机器输入递归重算
验证套件（生成器验证集上，容差冻结）: 日涨停数 KS≤0.05；连板 P50/P90/P99 相对误差 ≤10%；
  ADV 中位/P90 ≤10%；行业相关 ||Δ||_F/N ≤0.05；**全市场日总成交额分布 KS≤0.05 及其
  一阶自相关误差 ≤0.10；题材成交份额分布 KS≤0.05；CrowdPctl 分布 KS≤0.05**（修复总量不保）
  牛熊年分别达标；任一失败 → GENERATOR_FAIL
预算与 α 选择:
  主预算 UCB(E[假确认触发/年]) ≤2（t 上界，绝对半宽 ≤0.3）
  协预算 UCB(E[FalseCapitalDays/年]) ≤40（bootstrap 分位上界，相对半宽 ≤15%）
  FalseCapitalDays = Σ_t MarketValueOfFalsePositions_t / (NAV_t/6)（满槽日=1、半仓日=0.5）
  α 选择（修复验证集复用）: 在验证合成年上对全网格 K 点做 **simultaneous UCB**
    （Bonferroni 1−0.05/K），取同时满足双预算的**最大 α**；无解 → 上报（禁逐级回退复用）
漏斗输出: 假点火→假确认→假可投资→假 ZJ 交易→假成交→FalseCapitalDays
```

## 6. 载体 ZJ 与第二法庭

- 容量：ADV20@D0 ≥3.33 亿 ∧ 流通市值@D0 ≥50 亿；纯度主资格 = D0−1 在籍 ≥20 日（文本/跨源仅排序分层与诊断，受时钟 PIT 约束）；
- 参与：个股前复权复合收益 − 基集等权复合收益（D0..D0+4）>0 ∧ mean(换手 D0..D0+4) ≥1.2×mean(D0−20..D0−1)；
- 护栏：D0+4 收盘非涨停 ∧ Episode 内涨停 ≤1 ∧ Episode 累涨（前复权）<40%；
- 可买（D0+5）：非开盘涨停/停牌 ∧ GapLimitRatio=(Open_{D0+5}/Close_{D0+4}−1)/UpLimitPct_{D0+5} ≤0.70；
- 排序 = EventAmountShock = mean(Amount[D0..D0+4])/mean(Amount[D0−20..D0−1])，前 2（替补至 4、单标的半仓、池空记录）；
- **B 臂（解析化，修复枚举冗余）**：B = D0+5 可买池**等权平均收益**（数学上等于全部 2-组合等权平均）；H-Z3 命题 = "AmountShock 前 2 是否优于同一可买池的平均股票"；T 与 B 同池同口径（D0+5 VWAP→D0+14 收盘）；池=1 → 半仓；池=0 → 跳出；
- C0 = 容量∧可交易池（D0+4 判定+D0+5 可买）同排序；N = 池内 RS20（个股 20 日收益−基集等权，截止 D0+4）前 2；
- common support：H-Z3/Z4 限完整池 ≥3；H-Z3b 限双池 ≥2；池不足题材属性必报；范围声明：在籍 ≥20 日使新概念首月无 ZJ——第二/四法庭为成熟本体再激活法庭。

## 7. 四级法庭

### 7.1 第一法庭（风险集匹配；estimand 公式冻结）

- 匹配：每 D0 处理集 vs 风险集（同日 DORMANT 未点火合格题材）；目标字典序 ①最大匹配数 ②最小总距离 ③ID 序（dummy 节点+超额惩罚实现）；协变量（成分数/前 20 日题材收益/成交份额/主板占比，[D0−20,D0−1]）按 **pre-assignment 风险集**（含即将点火者）横截面标准化（样本标准差、不 winsorize、零方差剔除后按 √剩余维数重归一）；卡尺 = 总标准化距离 ≤1.0；约束 Jaccard<0.2、个股重叠 ≤20%；同日无放回、跨日可复用（lineage 聚类吸收）；unmatched → **out-of-support signal registry**（属性对比必报）；SMD≤0.10 一次生成整体判定；序贯节点失败 → 该次永久跳过；
- **科学收益口径（冻结公式）**：
```
成员级: r_i = 前复权收盘价比 − 1（分红送转已调整）；停牌沿最后有效前复权价；
  退市 = 最后成交价延续至窗口末（不删除、不记 −100%）；换股按比例接续新证券；
  任何成员零删除（缺失延最后价记 stale_price_flag）
均值 estimand: 每题材"起始等权、买入持有、不再平衡"组合收益 → 配对差（T−A）→ 对配对差取均值
中心 estimand（定义 A，冻结）: 每题材成员收益中位数 → 配对差 → 对配对差取均值
Immediate 窗 = Close_D0 → Close_{D0+4}；Landmark 窗 = Close_{D0+4} → Close_{D0+14}
```
- H-Z2b（**可执行筛选效应**，更名）：容量子集（ADV20@D0≥1 亿等 D0 条件）VWAP_{D0+5}→VWAP_{D0+15}，含买 12.5bp/卖 17.5bp 与 5% 参与顺延；
- 判词纪律：matched-sample、共同支持域限制、四人群、ITT 主/per-protocol 副、E1/E2（landmark）/E3 沿既有定义。

### 7.2 政策比较
Policy I（显式）：买**全部**点火（无论日后确认），D0+1 入场→D0+10 信号→D0+11 执行；Policy C（显式）：**仅买 CONFIRM=true**，D0+5→D0+14→D0+15，夭折持现金；InstrumentSet 仅 D0 信息；账本：OrderBudget=min(CurrentNAV/6, 可用现金)、<半额拒绝、禁融资、单股 ≤CurrentNAV/12、同日先净额化、买入仅用日初现金、卖出所得次日可用、现金收益 0、优先级 = 题材 ID 序、无抢占；判决 CI_lower[年化R(C)−R(I)]>1%（stationary bootstrap 块 20）+ 回撤/CVaR 护栏 + 资本/投入双口径。

### 7.3 第三法庭
EXIT-3C（Breadth<0.30@Age≤10 全退；Crowd>0.90 减半一次；Breadth≤峰值−0.20∧题材RS20<0 余退；60 日兜底；A>B2>B1>C；D 收盘判定 D+1 VWAP 执行；峰值自 D0+5；块长 60 推断）vs 固定 10 日，同一入场流完整组合对比（描述性）。

### 7.4 第四法庭（项目资源指标）
成交：买零成交 iff high==low==涨停价、卖 iff ==跌停价；Fill=min(净额单, 5%×日成交额)；Decision-to-VWAP slippage；容量 1/3/5% 三档；对照 = 动态暴露基准（Exposure 日初口径 × 容量指数[月末定成分、次月首日 VWAP 调仓、月内停牌持有] + 现金 0）；判决量 = 252×mean(日 spread)（CAGR 差仅经济报告）；判词 = "超过动态投入比例匹配的容量指数"；附两因子（市场/规模）风险调整回归归因（非生死线）；**H-Z1 报告 CI 与参考线 3%，不作正式推断 PASS**。

## 8. 安慰剂

- P3：伪点火日从"DORMANT 且其后未点火"日抽取；P4：簇独立循环位移避开全部 Episode 窗口且伪窗口全市场涨停数分位差 ≤1 三分位（无合法位移剔除记录，剔除率>30% 上报）；
- **双层重采样**：外层 500 次（canonical 簇 × 20 日时间块）联合 bootstrap；内层每样本一轮伪化；
- **通过线（四 endpoint 分别等效）**：对 Immediate/Landmark × 均值/中心四个 endpoint，各自外层分布 95% CI ⊂ [−0.1,+0.1]d ∧ [−10bp,+10bp]，**全部通过**才开 Gate1；Gate0 通过率/不可执行率/CI 宽度进 OC 仿真；
- P1 = B 臂引擎自检（Gate0-Z）；P2 = 诊断。

## 9. 分法庭主推断

| 假设 | 主推断 | 稳健性 |
|---|---|---|
| H-Z2 族 | matched-sample 配对差 + 交叉重采样两向 bootstrap（lineage × 20 日入场块，B=5000） | 40 日块；stationary |
| H-P1a / H-Z1 | 日历 spread + stationary bootstrap（块 20） | NW lag=max(2h,auto) |
| H-Z6 | 同上，块 60 | — |
| H-Z3 | 事件配对差 + lineage 聚类 bootstrap | 时间块加聚 |
块际残余重叠为已知局限（40 日块夹逼）；状态覆盖 n≥10 ∧ ≥15%；频率闸门 [10,150]/年。

## 10. 序贯影子法庭

- 双时钟：事件钟 = 锁定配对数；日历钟 = 自首 Episode 起全部非重叠 20 日块（**无暴露过滤**——现金日是政策价值组成部分）；
- 分 estimand 边界世界：均值世界（同质 10bp 与稀疏 20%×50bp，均值皆 10bp）；中心世界（对称位移使 Median=10bp——稀疏世界中位数为 0 不得用）；可投资世界（子集 50bp）；组合世界（Episode 流重排+账本重放注入年化 1%）；各自产出 n_target 与边界；
- 终期 = Gate1/2 主假设 n_target 最大值；未达自身 n_target 者判 INCONCLUSIVE；封存-启封、SMD 跳过、Gate0 阻断全部进 OC 仿真；
- **OC 表（RESOLVED_CONFIG 必含，分情景）**：{Null, MES, 2×MES, Sparse, State-dependent} × {P(PASS), P(FAIL), P(INCONCLUSIVE), 决策时间 P50, P90, 分状态覆盖时长}。

## 11. Prospective Run-in v2（修复本轮头号错误）

### 11.1 终止规则（精度制）
≥60 交易日 ∧ ≥20 个 Ignition ∧ ≥8 个 Confirmed Trigger ∧ 两市场状态均有观测（数值由盲化精度仿真确认为初始冻结值；run-in 不消耗正式样本，不足则延长）。

### 11.2 Live Null Replay（合法校验对象）
```
在 self-collected 成员快照上（固定真实每日本体路径）:
  对价格/涨停轨迹运行条件零模型（§5 生成器的 live 版）→ 重放完整状态机
  → E[null confirmed triggers | live membership]
用该量校验历史 α 的迁移性（预登记容差带）
**禁止**用真实市场的观测触发频率估计假阳性率——
  Observed = True + False，零模型只预测 False；
  用观测数调 α = 因真实信号出现而反向压制 alpha（v9 错误，本版废除）
可直接对实测校验的量（非信号污染）: 成员变更率、题材数量与规模分布、分层厚度、
  donor 可行率、匹配成功率、ZJ 池覆盖率、数据发布时间、schema
```

### 11.3 重配置依赖链（修复"只换 CONFIG"）
run-in 触发 α 或任何设计参数变更 → **全链重跑**：路径零模型校准 → 可行性审计 → 全部 n_target → 序贯边界 → Gate0 → **ExpectedYears 机械重算**（= n_target / live 有效事件年率，含 P50/P90/分状态/INCONCLUSIVE 概率）→ 新联合哈希包 → **用户重新签署** → 新 freeze tag → 正式影子自新签署日重新起算。

## 12. 冻结流程（治理顺序修复）

```
1. 快照普查+快照库启动【无条件立即】
2. 全引擎+合成自检（§8 前置自检、B 臂解析断言、科学口径无 VWAP 断言、净额化断言、
   bijection 确定性断言、label-degree 闸门断言）
3. 历史路径零模型（若状态资格线满足）→ provisional α 与 provisional config
4. 盲化设计可行性审计（fallback 树）→ 5. 盲化 SSD（分 estimand n_target）
6. 分 estimand 边界世界仿真 + OC 表
7. **Prospective Run-in（§11：终止规则 + live null replay）→ 确认或重校准**
8. RESOLVED_CONFIG 生成与联合哈希（§13 清单）→ 9. ★ 用户签署 → FREEZE TAG
10. **freeze 之后**才解锁经验安慰剂正式运行与 DEV/OOS-B 探索性读数（工程与方向性证据身份）
11. 正式影子（self_collected、append-only、双时钟、封存-启封、月度 drift gate、
    每 125 日盲化 null 审计）→ §0 判决
```

## 13. 可复现性环境（冻结）

```
hash = SHA-256；encoding = UTF-8；serialization = canonical JSON（键排序、无空白）
PRNG = PCG64DXSM；整数 = little-endian int64；浮点 = IEEE-754 float64
排序 = 稳定 mergesort（并列按 ID 字典序）；并行归约顺序固定
联合哈希包 = { 本 SPEC 全文, RESOLVED_CONFIG.yaml, 代码 commit, requirements.lock,
  容器镜像摘要, BLAS 版本, 数据源 schema 版本, measurement_regime_id, 生成器验证报告 }
```

## 14. 冻结参数总表（本文全部数值的索引）

| 域 | 值 |
|---|---|
| 宇宙 | 成分 [8,100]；上市 ≥60 日；排除正则 §2.2；覆盖率 ≥98% |
| 聚类 | J>0.5 确定性贪心 clique；canonical 继承 §2.2；左截断 120；谱系 0.7 |
| 零模型 | 五维层（≥8，粗化序冻结）；B 2000→全族 20000；minP 秩矩阵 §3.2；LU≥2 ∧ p_FWER≤α_day |
| 状态机 | 休眠 20 日 CoordState≥2 ≤1 天 ∧ Crowd<0.80 三级；确认 landmark §4；时间轴 D0+5/14/15；冷却 20 |
| 条件本体零模型 | donor 六维层+合格题材零重叠+HK 最大基数匹配；unswapped ≤20% ∧ 高题材度 ≤1.5×；验证套件 8 指标 §5；状态资格分割 |
| 预算 | UCB(假确认触发)≤2（t，半宽 0.3）；UCB(FalseCapitalDays)≤40（bootstrap，相对 15%）；simultaneous UCB 选最大 α |
| ZJ | ADV≥3.33 亿∧市值 ≥50 亿；在籍 ≥20 日；参与/护栏/GapLimit≤0.70；EventAmountShock 前 2；B=池等权 |
| 匹配 | 字典序目标；pre-assignment 标准化；卡尺 1.0；SMD≤0.10；同日无放回 |
| 科学口径 | 前复权 close-to-close；起始等权买入持有；中心=定义 A；退市延价零删除；双窗 §7.1 |
| H-Z2b | VWAP→VWAP 含成本参与（可执行筛选效应） |
| 政策/账本 | §7.2 全条款；单股 ≤NAV/12；卖出资金次日可用 |
| 推断 | §9 表；MES 10bp/50bp/20bp/1%/3%（H-Z1 参考线）；α 0.025/0.005/0.015/0.005/0.025/0.025/0.05；β_death 0.025 |
| 序贯 | 双时钟；分 estimand 世界；终期 max(n_target)；OC 五情景表 |
| Run-in | ≥60 日 ∧ ≥20 点火 ∧ ≥8 确认 ∧ 双状态；live null replay；全链重配置 |
| 漂移 | 月度 drift gate（断点 30%/schema）；125 日盲化 null 审计 |
| 环境 | §13 全清单 |

## 15. 给验证 Agent 的交代要点

1. 本文件为唯一真相源（零外部引用）；歧义即停；
2. 强制单测（在既有全部断言外新增）：live null replay 禁触真实触发数断言、simultaneous UCB 覆盖 K 网格断言、B 臂解析等价断言（池等权 == 全组合均值，数值验证）、四 endpoint 安慰剂断言、退市延价零删除断言、买入持有不再平衡断言、H-Z1 无正式 PASS 断言、drift gate 断点断言；
3. 四人群/登记簿/漏斗/unswapped 条件表/run-in 校验带/regime 日志全量入库；
4. 闸门 flag 阻断；影子期改规则 = 作废。

---

## 附录 A：第九轮审查十八红线 → v9.1 落点
1 单文件 canonical → 全文｜2 live null replay → §11.2｜3 run-in 精度终止 → §11.1｜4 全链重配置 → §11.3｜5 冻结顺序（run-in 先于 DEV/OOS 解锁）→ §12｜6 条件本体零模型更名 → §5/§0｜7 永久识别边界 → §0｜8 donor 排斥标签集+label-degree 闸门 → §5｜9 受约束 bijection 算法 → §5｜10 总量验证指标 → §5｜11 simultaneous UCB → §5｜12 双预算分别方法 → §5｜13 状态资格分割 → §5｜14 H-Z1 降项目指标 → §1/§7.4｜15 Gate0 四 endpoint → §8｜16 死亡判词共同支持域 → §0｜17 estimand 公式/公司行动/买入持有 → §7.1｜18 B 臂解析化+H-Z2b 可执行+FalseCapitalDays+drift gate+null 审计+环境冻结+OC 分情景 → §6/§7.1/§5/§2.5/§13/§10

## 附录 B：留痕
1. **自认错误两处**：Run-in 用观测信号数校验假信号零模型（v9 头号错误——会因真实行情出现而压制 alpha）；"零继承"声明与"沿 v8 四章"并存的自相矛盾；
2. H-Z1 采纳选择 B（降项目指标）而非 α 分割：与"第四法庭禁称 alpha、仅资源闸门"的既有哲学一致，且避免为一个非科学命题消耗科学 alpha；
3. B 臂解析化后 P1 安慰剂身份同步简化为引擎自检（解析式无抽样噪声可置换）；
4. run-in 初始数值（60/20/8）为冻结初值，最终由盲化精度仿真确认——确认属 §12 步骤 4-6 的一部分，非事后调整。

*登记时间：2026-07-16。冻结对象：全文。变更 = v9.2 = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
