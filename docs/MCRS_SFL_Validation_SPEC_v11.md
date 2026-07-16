# MCRS SFL 验证规格书 v11.0 — FINAL CANONICAL（全文物理展开，零回引）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / FINAL CANONICAL`
版本：`v11.0`（替代 v1-v10 全部版本；本文未出现的条款一律失效；**本文不含任何对旧版本的引用**。第十一轮外部审查 18 条红线 + 附带论点全部核实成立、零驳回，含 ThemeDistance 恒等退化与 canonical 声明第三次不达标两处设计方自认错误）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文 + RESOLVED_CONFIG + §13 环境产生逐日完全相同输出。`D+k` 均为交易日。

---

## 0. 终局条款、识别边界与生命周期治理

**三层条件识别边界**：最终科学结论限定于——供应商本体稳定期（未触发 regime reset）、风险集匹配共同支持域内、安慰剂装置可执行的条件下，**给定供应商实际输出的题材本体**，协调相变是否携带未来收益信息。本体的反事实形成不可识别；本体漂移可能与强叙事相关（信息性删失——稳定期条件可能系统性排除叙事创新阶段，此限制永久写入判词）；漂移期 Episode 隔离分层报告。

**科学死亡线**：影子数据上四判定（Immediate/Landmark × 均值/中心）全部 Economically FAIL 于 MES_sci=10bp → 死亡命题："在本体稳定期、风险集共同支持域内的点火事件中，题材协调相变未能在点火后 0-4 或 5-14 交易日窗口向题材全体成员产生 ≥10bp 的平均或中心收益扩散"。

**生命周期治理（v11 修订：统计预算化）**：正式 measurement regime ≤3 个；**生命周期 alpha 预算：regime 1 = 0.03、regime 2 = 0.015、regime 3 = 0.005**（各 regime 的假设图初始权重按该预算缩放）；第 2 个 INCONCLUSIVE regime → 强制关线；全部 regime 结果共同披露；meta-analysis 须预登记；禁"SFL 整体已验证"表述。**项目总年限：自首个正式影子日起 ≤6 个日历年**，到期未判决 = 项目 INCONCLUSIVE 关线。

**判决语义**：四分法判词；false-death β=0.025（FAIL 需单侧 97.5% 上界 < MES）；四人群分层；DEV/OOS-B = 工程与方向性证据；终审只认 self_collected；H-Z1 = 项目资源指标（决策函数 §7.4，含预登记唯一延长规则，**无自由裁量否决**）。
签署人：________ 日期：________

## 1. 假设图（图形化多重检验，强 FWER 构造）

采用 Bretz 型图形化程序。设本 regime 预算 α_r（regime 1 = 0.03）。

```
节点与初始权重（×α_r）:
  L-mean 0.5 | I-mean 0.3 | L-ctr 0.1 | I-ctr 0.1
转移矩阵（拒绝后权重去向）:
  L-mean → {Z2b 0.4, P1a 0.4, L-ctr 0.2}
  I-mean → {Z2b 0.4, P1a 0.4, I-ctr 0.2}
  L-ctr  → {Z2b 0.5, P1a 0.5}
  I-ctr  → {Z2b 0.5, P1a 0.5}
  Z2b → {Z3 1.0} | P1a → {Z3 1.0} | Z3 终端
零假设类型: 各节点 positive-null（θ≤0，图内检验）；economic-PASS（CI 下界>MES）与
  economic-FAIL（上界<MES, β=0.025）在节点图外按四分法判词判定，不占图 α
H-Z1: 非推断节点（§7.4 决策函数）
强 FWER 验证义务: OC 仿真 MUST 覆盖混合真假配置（至少: 全 null；全真；仅 L-mean 真；
  仅 I-mean 真；L-mean+Z2b 真其余 null；中心真均值假；单个 Gate2 真），
  每配置验证 FWER ≤ α_r
```
estimand 一览：Immediate = Close_D0→Close_{D0+4}；Landmark = Close_{D0+4}→Close_{D0+14}（全基集科学 MTM）；Z2b = 容量子集可执行 P&L（§7.1）；P1a = 组合政策 spread；**Z3 = Top2Mean − RestOfPoolMean**（v11 修订：纯排序命题，池规模不变；MES 20bp 施加于此差值；池平均政策版降描述性）；各假设独立 n_target（含 n_Z3），未达判 INCONCLUSIVE。

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
资格线：带 trade_date 每日历史成分；连续覆盖 ≥3 年、缺失日率 ≤2%；ID 年度稳定率 ≥95%（谱系调整）。评分依序：覆盖年数 → 成分数 ∈[8,100] 带内题材占比 → 偏好序 KPL>DC>THS。第二源 = 次名原生复现（不映射）；THS 交叉校验。标签：`vendor_reconstructed_history=true`（工程/方向性）；`self_collected=true`（唯一终审资格）。

### 2.2 题材宇宙与聚类（全文）
- 合格题材：成分 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`（开跑前目检+哈希）；
- **确定性聚类算法（全文）**：每日以 Members_{D−1} 计算全部题材对 Jaccard；候选对 = J>0.5，按 (J 降序, 题材ID对字典序) 排序依次处理：双方未入簇 → 建新簇 {x,y}；一方在簇 S → 当且仅当另一方与 S 全体成员 J>0.5 才并入；双方异簇 S1,S2 → 当且仅当 S1∪S2 任意两两 J>0.5 才合并；其余跳过；未入簇者单簇；
- canonical_id：merge 继承 first_seen 最早 parent（同日并列取 ID 字典序小）；split 由与旧簇 Jaccard 最大 child 继承（并列同规则），其余 child 新建；lineage 表（cluster_id/effective_date/parent/child/merge/split/canonical_id）append-only；Episode 创建即锁定点火时 canonical_id 与基集；
- 左截断：主源起始后 120 交易日首现题材禁入 new_concept；谱系：消失/新现概念 J>0.7 = 同谱系（仅 ≤D 数据）。

### 2.3 快照库、双成员集、时钟 PIT
每交易日收盘后快照全部源（append-only + 抓取时间戳）；点火检测集 = Members_{D−1}；Episode 基集 = Members_{D0−1}；MembershipExpansion 逐日记录（H-V1 诊断：新增 vs 基集成员收益差、动态 vs 冻结成员信号差）；时钟 PIT：D 日 22:00 前抓取且未依赖修订方可用于 D+1；发布时刻不可考字段（原因文本等）回测按 D+2；违反 = 装置失败。

### 2.4 行情、合格宇宙与市场状态
合格宇宙 = 上市 ≥60 交易日 ∧ 非 ST ∧ 非停牌 ∧ 非退市整理；全部信号量仅在合格宇宙上计算；封板 = close_raw≥up_limit、触板 = high_raw≥up_limit（pre-2019 回退：pct_chg≥+9.8% ∧ close_raw==high_raw）；20 日特征需 ≥15 有效日否则当日退出分层（feature_missing）；股性 = 250 日涨停次数分位（60-249 日扩展窗标 expanding）；质量闸门（单位锚定 / 完整性 / 涨停价抽核 20 样本 / 覆盖率 ≥98%）失败 → GATE_FAILED.flag 阻断下游。
**日度市场状态（唯一定义）**：STATE_D = UP iff HS300 收盘_D ≥ MA200(HS300)_D，否则 DOWN。年度状态（仅生成器年资格）：HS300 年收益 ≥0 为 UP 年。

### 2.5 本体漂移治理 v3（固定基线）
- 硬漂移（即停）：schema 破坏性变更 / ID 体系重置 / 发布时间越过 22:00 截止；
- 统计漂移：监控{题材总数、平均成员数、日变更率、ID 生灭率、改名率}；**基线 = 本 regime Run-in Stage-B 期间形成的固定 Phase-I 基线（正式影子期间不更新）**；触发 = EWMA（λ=0.2）越过冻结控制限且连续两个月；控制限由 OC 校准至稳定期 ARL ≥24 个月；近零分母双阈值（绝对 ≥5/月 ∧ 相对 ≥30%）；滚动 6 月统计仅作描述性趋势；
- 触发处置：暂停 → regime_id 递增 → 重新 Run-in → 重校准 → 按 §0 生命周期治理；漂移期 Episode quarantine 分层；
- **定期盲化 null 审计（v11 修订：全窗重放）**：每 125 交易日执行一次，但每次审计 = 携带 120 日 warm-up 状态的**完整 250 日滚动窗重放** ×200 条（成熟后窗口重叠推进）；t-UCB 对照校准预算 ×1.5 容差（双预算齐查）；一次越界挂旗、连续两次暂停；UP/DOWN 分报；审计误暂停率由 OC 校准（稳定期 5 年 ≤10%）。禁止任何"半窗 ×2"年化。

## 3. 日度零模型（minP，全文）

```
分层: 板块 × 流通市值3 × 20日波动3 × 20日动量3 × 股性3；层最小 8；
  粗化序: ①并动量 ②并波动 ③并股性 ④并市值；板块永不合并
置换: 保留当日各层真实涨停股数，层内 Fisher-Yates 重排标签；
  子流 seed = SHA-256(trade_date‖source_version‖spec_version‖b)（UTF-8、canonical 拼接）；
  不同 b 允许重复配置；各层独立打乱后拼接为全局 permutation
  B_random = 2000；任一候选 p̂_FWER ∈ [α_day/3, 3α_day] → 当日全族追加 18000 至 20000
  （前 2000 行与统计量不可变）
统计对象（(B+1)×C 矩阵，b=0 为观测行；S[b,c] = LU_{c,b}）:
  p[b,c] = #{ b'∈{0..B}: S[b',c] ≥ S[b,c] } / (B+1)      # 全行含自身取秩，≥ 计并列
  p_marg(c,D) = p[0,c]（Monte Carlo permutation tail probability，禁称"精确"）
  m_b = min_c p[b,c]（b=1..B）
  p_FWER(c,D) = (1 + #{ b: m_b ≤ p[0,c] }) / (B_random + 1)
  CoordinationState(c,D) = −log10 p_marg（全部合格题材每日计算，专用休眠历史）
点火: LU_real ≥ 2 ∧ p_FWER ≤ α_day
证据边界: 严格校准全局零假设下的日度扫描错误；事件级强 FWER 仅近似
行业条件口径: ThemeShock|Industry（申万一级×市值3 分层，其余按粗化序合并；层<8 →
  industry_condition_uninformative）；三态标签（p_cond≤0.10 supported / >0.10 not_supported /
  层稀 uninformative）；"超行业协调"宣称走 H-Z2c（描述性）
```

## 4. Episode 状态机与分解诊断（全文）

### 4.1 状态与时间轴
```
DORMANT: 过去 20 日 CoordinationState≥2 天数 ≤1 ∧ Crowd 三级 fallback <0.80
  （题材成交额占全市场份额 20 日平滑的分位：历史 ≥120 日自史 / 60-119 扩展窗[crowd_expanding]
   / <60 当日横截面[crowd_xsec]；三级分层报告禁静默合并）
IGNITION: DORMANT 次日起 LU_real≥2 ∧ p_FWER≤α_day；同簇同日取 p_marg 最小（并列 ID 序）；
  EpisodeID=(canonical_id@D0, D0) 锁定；基集 = Members_{D0−1}
CONFIRMATION（landmark D0+4 收盘，全量基于基集）:
  p_base_marg(Episode,D) = 基集成员按当日 PIT 特征定位当日全市场分层、复用当日置换矩阵
    的边际尾概率；身份冻结、可交易状态动态；不可交易成员当日不进 LU 分子；
    可交易基集 <8 → 当日不可检验
  成员分类（剔最高连板链本股）: ClosedLimit（收盘封板）/ TouchedOnly（仅触板）/
    StrongResidual（收盘 ≥+5% 未封板）
  CONFIRM = [新增 ClosedLimit ≥1] ∧ [Distinct(CL∪SR) ≥2] ∧
    [扩散: Age1..4 任一日 p_base_marg≤0.10 且有新增封板成员
     或 晋级: MaxBoard 抬升 ∧ 连板链起点 ≥D0−1] ∧ [BombRate(Age1..4, 触板≥3) ≤0.5]
时间轴: 入场执行 D0+5（=持有日 1）｜退出信号 D0+14 收盘｜退出执行 D0+15
  SignalEpisodeEnd: 成 D0+14 / 败 D0+4；冷却 20 日自次日（canonical_id）；CAR(1..60) 纯观察窗
DetectionLag: D0 − 最近正向激活段起点（激活日 = 日收益 ≥+2×20 日 σ，段间隔 ≤5 日；
  成交同构 ≥2×20 日均额）；负向冲击（≤−2σ）另记；
  成熟度: coordination_early（PreIgnitionCAR20<+10% ∧ 价格 120 日分位<0.7）/
  fully_mature（≥+25% 或 ≥0.9）/ 其余 price_advanced
EpisodeType: new_concept（首现 ≤120 日，剔左截断）/ reactivation，分别报告
```

### 4.2 E 系列分解诊断（全文）
```
E1（点火信息）: 全部 Ignition（含夭折）vs 匹配对照（伪时钟），入场 D0+1 收盘（科学口径），
  D0+4 与 D0+14 双窗；estimand = 题材级起始等权买入持有组合收益的配对差均值
E2（确认筛选, landmark）: D0+4 收盘分类 confirmed/failed；两组统一自 D0+5 起测
  Close_{D0+4}→Close_{D0+9}/Close_{D0+14}；描述性 + post-ignition selection 警告
E3（延迟成本, 双口径）: 口径 1 = Close_{D0}→Close_{D0+4}（纯延迟收益）；
  口径 2 = [Close_{D0}→Close_{D0+14}] − [Close_{D0+4}→Close_{D0+14}]
  （v11 更名: **共同终点财富机会成本** —— 数学上 = r₁(1+r₂)，非纯延迟）
均为诊断义务，无通过线，全部用科学 MTM（§7.1）
```

## 5. 条件本体零模型（轨迹运输 v3）

**零假设**：条件于已观察供应商成员路径，价格协调轨迹与题材身份无特异对齐。禁称"完整 DGP"。

```
路径向量（两 primitive + 派生，修复过约束）:
  运输 { Open/PrevClose, High/PrevClose, Low/PrevClose, Close/PrevClose,
        VWAP/PrevClose, Volume/ADVVol_pre, 停牌旗标 }
  派生: Amount = Volume × VWAP（不独立运输 Amount——修复三比率恒等冲突）
涨跌停投影（冻结七步序）:
  ①以 recipient 基线重建未约束 OHLCV+VWAP ②截断 Open、Close 于板块涨跌停界
  ③High=max(High,Open,Close)、Low=min(Low,Open,Close) 后再截断于界
  ④VWAP 投影至 [Low,High] ⑤Amount=Volume×VWAP 重算 ⑥重判涨停/触板/一字
  ⑦记录 projection_distance（各字段相对调整量 L1 和）；>5% → 该 donor 块不可用（记录并
   入 unswapped 类诊断——防止极端 donor 经截断人工制造涨停）
运输算法（修复退化目标与大数技巧）:
  节点 = 层内全部股票；合格边 = 同 donor 层 ∧ 块起点无共同合格题材标签；self-edge 允许
  **严格分阶段优化（禁大数惩罚）**:
    阶段 1: 最大基数匹配于合格边 → 最小 self-edge 数 S*
    阶段 2: 约束 self-edge 数 = S*，最小化 Σ FeatureDistance（v11 修订: 第二目标 =
      **市场特征距离** = 标准化欧氏(市值, 20日波动, 20日动量, 股性, ADV)，
      量化 ×10^6 int64——ThemeDistance 因合格边 Jaccard 恒 0 而恒 1，已删除）
    阶段 3: 在阶段 2 最优解集内，按 recipient ID 升序逐个固定其可行且保持最优的最小 ID
      donor（迭代固定法）→ 字典序唯一解
  self-edge 中选者 = unswapped（原路径归自己，不再作他人 donor——保证完美置换）；
  溢出检查义务: 全部整数成本和 < 2^62
  unswapped 闸门: 总体 ≤20% ∧ 题材度前 20% 股票 ≤ 总体 1.5×（条件表必报）
donor 层 = 板块×市值3×股性3×申万一级行业×块起点波动3×块起点动量3；层 ≥8；
  粗化序 ①并动量 ②并波动 ③并股性 ④并市值（行业与板块永不合并）；块 = 20 日
  （敏感性 10/40、随机起点、circular；跨块连板链按块内计留痕）
验证套件（生成器验证年上，容差冻结）: 日涨停数 KS≤0.05；连板 P50/90/99 相对误差 ≤10%；
  ADV 中位/P90 ≤10%；行业相关 ||Δ||_F/N ≤0.05；全市场日总成交额 KS≤0.05、自相关误差 ≤0.10；
  题材份额 KS≤0.05；CrowdPctl KS≤0.05；行业同日涨停数 KS≤0.10；行业共同触板 KS≤0.10；
  行业涨停 HHI 相对 ≤15%；行业上尾共现率相对 ≤15%；行业成交冲击共放大率相对 ≤15%；
  牛熊年分别达标；任一失败 → GENERATOR_FAIL → 历史校准禁用、仅 live null replay
四阶段分离: 真实年按状态资格分割（开发/验证集各含 ≥1 UP 年 ∧ ≥1 DOWN 年，
  不满足禁用历史校准）；合成年对半 → α 校准 / α 验证
α 选择: 校准半产出候选网格与 nuisance；验证半对 K 网格 × 双预算 = 2K 族做
  simultaneous UCB（Bonferroni 1−0.05/(2K)），取同时满足双预算的最大 α；无解上报；禁插值
双预算: UCB(E[假确认触发/年]) ≤2（t 上界，绝对半宽 ≤0.3）；
  UCB(E[FalseCapitalDays/年]) ≤40（bootstrap 分位上界，相对半宽 ≤15%）
  FalseCapitalDays = Σ_t MV(假仓)_t / (NAV_t/6)（满槽日 1、半仓 0.5）
漏斗输出: 假点火→假确认→假可投资→假 ZJ 交易→假成交→FalseCapitalDays
```

## 6. 载体 ZJ 与第二法庭（全文）

- 容量：ADV20@D0 ≥3.33 亿（AUM 2 亿 ÷12 ÷5%）∧ 流通市值@D0 ≥50 亿；纯度主资格 = D0−1 在籍 ≥20 交易日（文本/跨源仅排序分层与诊断，时钟 PIT 约束下回测 D+2 可用）；
- 参与：个股前复权复合收益 −基集等权复合收益（D0..D0+4）>0 ∧ mean(换手 D0..D0+4) ≥1.2×mean(D0−20..D0−1)；护栏：D0+4 收盘非涨停 ∧ Episode 涨停 ≤1 ∧ 累涨 <40%；
- 可买（D0+5）：非开盘涨停/停牌 ∧ GapLimitRatio=(Open_{D0+5}/Close_{D0+4}−1)/UpLimitPct ≤0.70；排序 = EventAmountShock = mean(Amount[D0..D0+4])/mean(Amount[D0−20..D0−1])，前 2（替补至 4、单标的半仓、空池记 zj_pool_empty）；
- **H-Z3（v11 修订 estimand）**：`Top2Mean − RestOfPoolMean`（同一 D0+5 可买池；D0+5 VWAP→D0+14 收盘）——纯排序命题、池规模不变；MES=20bp；池平均政策口径（Top2 − PoolEW）降为描述性；池 <4（rest 不足 2 只）→ 事件跳出 H-Z3；
- C0 池 = 容量∧可交易（D0+4 判定+D0+5 可买），同排序（H-Z3b 描述性）；N = 池内 RS20（个股 −基集等权，截止 D0+4）前 2（H-Z4 描述性）；common support 各自冻结；n_Z3 独立、不足判 INCONCLUSIVE；范围声明：第二/四法庭为成熟本体再激活法庭。

## 7. 四级法庭（全文）

### 7.1 第一法庭
- **匹配（分阶段最优，修复大数技巧）**：每 D0 处理集 vs 风险集（同日 DORMANT 未点火合格题材）；阶段 1 最大匹配数 → 阶段 2 固定后最小总距离 → 阶段 3 迭代固定法字典序唯一；协变量（成分数/前 20 日题材收益/成交份额/主板占比 @[D0−20,D0−1]）按 pre-assignment 风险集（含即将点火者）标准化（样本 SD、不 winsorize、零方差剔除后 √d 重归一）；距离量化 ×10⁶ int64（溢出检查）；卡尺 = 总标准化距离 ≤1.0；Jaccard<0.2；个股重叠 ≤20%；同日无放回、跨日可复用；unmatched → out-of-support registry（p_FWER/规模/年龄/LU/状态属性对比必报）；
- **SMD 审计（十变量全列）**：匹配 4 项 + 流通市值、20 日波动、股性、题材年龄、20 日换手、标签泛化度；全部 |SMD|≤0.10 一次生成整体判定；序贯节点失败该次永久跳过；
- **fallback tree（全文，为全部合法修复）**：unmatched>30% → 卡尺 1.0→1.5（一次）→ 仍超 → MATCH_INFEASIBLE 上报；ZJ 池达标占比<30% → H-Z3 预判 INCONCLUSIVE（禁调阈值）；年均 Episode ∉[10,150] → 上报停止；SMD 整体失败 → 上报（禁迭代删对）；逾越 = 版本升级；
- **科学口径**：前复权 close-to-close；成员级零删除（停牌延最后有效价；退市三级：①窗口内实际清算/换股价 ②最后成交价延续 ③事后结算价仅稳健性回填；stale 占比与退市贡献必报）；题材组合 = 起始等权买入持有不再平衡；均值 estimand = 组合收益配对差之均值；中心 estimand = 题材内成员中位数 → 配对差 → 均值；双窗（Immediate/Landmark）；Switching 主 ITT（对照日后点火不改身份）/ 副 per-protocol（删失）；判词 = matched-sample、共同支持域限定；
- **H-Z2b（v11 修订：真实货币 + 完整清算）**：事件预算 **B_e = AUM/6 = 3333.33 万元**（AUM=2 亿冻结）、事件内等权；D0+5 起逐日买入 FillAmount=min(剩余单, 5%×当日人民币成交额)，D0+7 截止未成部分永久现金；D0+15 起逐日卖出（同参与率、顺延滚动），**清算期限 D0+20**，到期未卖持仓按收盘 ×(1−2% haircut) 计值；R_e=(终现金+终持仓值−B_e)/B_e；含买 12.5bp/卖 17.5bp（印花税 PIT）；命名"容量子集可执行筛选效应"（清算规则下成立）。

### 7.2 政策比较（全文）
```
InstrumentSet（I/C 同一候选身份，D0 冻结）: EpisodeBaseSet ∩ ADV20@D0≥1亿 ∩ 非ST/停牌@D0
  ∩ 上市≥60日；事件内等权
Policy I: 买全部 Ignition，D0+1→信号 D0+10 收盘→执行 D0+11
Policy C: 仅买 CONFIRM=true，D0+5→D0+14→D0+15；夭折全程现金
账本: OrderBudget=min(CurrentNAV/6, 可用现金)；<半额拒绝（rejected_by_cash）；禁融资；
  Gross≤CurrentNAV；单股 ≤CurrentNAV/12；同日订单先按股票净额化；买入仅用日初现金；
  卖出所得次日可用；现金收益 0；共享持仓先到先得、后到留现金、退出不补入、
  退出信号归持有事件；优先级 = 题材 ID 字典序；无抢占；拒绝不补入；空池释放名额
判决（H-P1a）: CI_lower[年化R(C)−年化R(I)] > 1%（§9 stationary bootstrap）
  护栏: MDD 差 ≤2pp ∧ CVaR 不劣（点估计）；资本口径与投入调整口径双报
描述性: H-P1b（C 于 D0+4 重建 ZJ）、M-I/M-C 伪政策、DiD
```

### 7.3 第三法庭（全文）
Breadth(c,D)=|{基集可交易成员: close_qfq>MA20}|/|基集可交易成员|；ThemeRS20 = 基集起始等权 20 日收益 −HS300 同期；StockExcess20 = 个股 20 日前复权收益 −基集等权同期。EXIT-3C：Leg A（入场 ≤10 日 Breadth<0.30 全退）>B2（Breadth≤入场后峰值 −0.20 ∧ ThemeRS20<0 余退）>B1（Crowd>0.90 减半一次）>C（入场日起第 60 日兜底）；D 收盘判定 D+1 VWAP 执行（5% 参与顺延）；V-STOP（StockExcess20<−15% 单股退）；vs 固定 10 日主退出同一入场流完整组合对比（描述性；推断块长 60）。

### 7.4 第四法庭（全文）
成交：买零成交 iff high==low==涨停价、卖 iff ==跌停价；其余 Fill=min(净额单, 5%×日成交额)；同股订单先合并；VWAP=amount×10/vol；滑点 = Decision-to-VWAP slippage（禁称 IS 分解）；容量情景 1/3/5%；对照 = 动态暴露基准 R_dyn=Exposure_t（日初口径）×R_capacity+(1−Exposure)×0，capacity 指数 = 全 A 容量可交易（ADV≥1 亿、非 ST/停牌）等权**月度再平衡**（月末定成分、次月首日 VWAP 调仓、停牌持有）、同成本模型毛/净双口径；判决量 = 252×mean(日 spread)（CAGR 差仅经济报告）；判词 = "超过动态投入比例匹配的容量指数"；两因子（市场/规模）归因附加。
**H-Z1 决策函数（v11 修订：删自由裁量）**：晋级 L1 = 点估计 ≥3% ∧ 80% CI 下界>0 ∧ MDD 差 ≤5pp；关线 = 点估计<0 ∨ 95% 上界<3%；INCONCLUSIVE → **预登记唯一延长规则**：当且仅当点估计 ≥2% ∧ 80% 下界>−1% 时自动延长 125 交易日**一次**，延长期满按同函数终判（无二次延长、无人工否决）；其余 INCONCLUSIVE 即关线。

## 8. 安慰剂（全文）

- **P3（ITT 化 + 算法化）**：伪处理日从同日风险集抽取，匹配六协变量（DORMANT 历史、日度市场状态、Crowd 分位、题材规模、前 20 日收益、当日全市场涨停数三分位）；匹配机器与主法庭同（分阶段指派、当日风险集标准化、卡尺 1.0、同日无放回）；**主口径 ITT：伪日后发生真实 Ignition 不删失**（与 H-Z2 主 Switching 一致——修复删掉困难伪事件的偏差）；per-protocol 删失版降副口径；Gate0 以 ITT 版判定；
- P4：簇独立循环位移避开全部 Episode 窗口 ∧ 伪窗口涨停数分位差 ≤1 三分位（无合法位移剔除记录，>30% 上报）；
- 双层重采样：外层 500 次（canonical 簇 × 20 日块）bootstrap、内层每样本 1 轮伪化；
- **通过线**：d = Mean(配对差)/SD(配对差)（SD 用**原样本固定值**，四 endpoint 各自）；**SD<5bp → d 口径不可检验，该 endpoint 仅用绝对等效**；四 endpoint 各自外层 95% CI ⊂ [−0.1,+0.1]d ∧ [−10bp,+10bp]，全部通过才开 Gate1；Gate0 通过率进 OC。

## 9. 分法庭主推断（全文展开）

```
H-Z2 族: matched-sample 配对差；两向交叉重采样 bootstrap ——
  外层每次: 从 lineage 簇集合有放回抽 m 个簇（m=原簇数），从 20 日入场块集合有放回抽 k 块
  （k=原块数）；保留"其簇与其块均被抽中"的配对（含重复计数 = 抽中次数之积）；
  空交集 → 重抽（≤100 次，仍空记 degenerate_resample 并跳过该次）；B=5000；
  CI = percentile；单侧下界 = 分布 α 分位；任一维簇数 <10 → 该假设 INCONCLUSIVE 标记
H-P1a / H-Z1 / H-Z6: 日历 spread；stationary bootstrap（几何块长，均值 20；H-Z6 均值 60）；
  B=5000；percentile CI；稳健性 = Newey-West（带宽 = max(2×持有期, Andrews 自动)）
H-Z3: 事件级配对差（Top2−Rest）；lineage 簇 bootstrap（簇为重采样单位）；B=5000
共同: seed = SHA-256('inference'‖hypothesis_id‖spec_version)；块际残余重叠为已知局限
  （40 日块敏感性夹逼）；状态覆盖 n≥10 ∧ ≥15%；频率闸门 [10,150]/年
```

## 10. 序贯法庭与 OC

双时钟（事件钟 = 锁定配对数；日历钟 = 全部非重叠 20 日块）；分 estimand 边界世界（均值/中心/可投资/组合/**Z3 排序世界**各产 n_target 与边界；中心世界用对称位移使 Median=10bp）；终期 = Gate1/2 主假设 n_target 最大；未达自身 n_target 判 INCONCLUSIVE；提前判仅 Gate1/2 Econ-PASS；封存-启封（下游自影子首日机械运行加密封存，解锁后启封未见数据）；SMD 跳过；**OC 必含**：全生命周期机制（Gate0 阻断、drift 误报、审计误暂停、run-in 重执行、α 重配置、regime 重启与生命周期预算、状态覆盖等待）+ 效应五情景 + **混合真假配置族（§1 清单）验证各 regime FWER ≤ α_r** + **P(3/5/10 年内判决)**。

## 11. Prospective Run-in v4（两段制，修复本体样本谬误）

```
Stage-E（工程迁移，≥60 交易日）: 校验数据发布时间、schema、成员日变更率
  （Wilson 区间，半宽 ≤ max(0.5pp, 0.25×p̂)）、donor 可行率与匹配覆盖率
  （Wilson，半宽 ≤10pp，于 live null 世界评估）、日度/60 日窗 null trigger rate
  —— 真实信号数量 MUST NOT 进入任何停止条件（输入白名单断言）
Stage-B（年度预算确认，累计 ≥250 交易日 self-collected）:
  在**真实 250 日本体路径**上跑 live null replay ≥200 条置换重放 →
  确认年度双预算（t-UCB）→ 形成 drift Phase-I 固定基线 →
  **正式影子自 Stage-B 完成且 RESOLVED_CONFIG 确认之日起算**
  诚实限制（写入判词）: 200 条重放消除的是 Monte Carlo 误差，非本体抽样误差——
  预算确认条件于该 250 日本体年；年度审计（§2.5）持续复核
偏差处置: 越带 → 预登记规则重校准 α → 全链重跑（校准→可行性→n_target→边界→Gate0→
  OC/ExpectedYears→新哈希包→重签→影子重新起算）
```

## 12. 冻结流程

```
1. 快照普查+快照库启动【无条件立即】
2. 全引擎+合成自检（含: 分阶段指派唯一性断言[同输入两次求解同输出]、置换完备断言
   [每路径恰用一次]、投影七步序断言、两 primitive 派生断言、P3 ITT 断言、
   run-in 停止函数白名单断言、假设图权重守恒断言[Σ权重≤1]）
3. 历史条件零模型（状态资格线满足时）→ provisional α/config
4. 盲化设计可行性审计（§7.1 fallback tree）→ 5. 盲化 SSD（全部 n_target 含 n_Z3）
6. 分 estimand 边界世界 + OC（§10 全机制 + 混合配置 FWER 验证）
7. Run-in Stage-E → Stage-B（§11）→ 确认或重校准
8. RESOLVED_CONFIG（hypothesis graph YAML + OC 表 + ExpectedYears + Phase-I 基线）联合哈希
9. ★ 签署 → FREEZE TAG → 10. 解锁经验安慰剂与 DEV/OOS-B 探索读数
11. 正式影子（self_collected、append-only、双时钟、封存-启封、drift gate、250 日窗审计）
    → §0 判决（regime 预算 α_r；项目总年限 6 年）
```

## 13. 可复现性环境（冻结）
SHA-256 / UTF-8 / canonical JSON（键排序无空白）/ PCG64DXSM / little-endian int64 / IEEE-754 float64 / 稳定 mergesort（并列 ID 序）/ 固定并行归约序 / int64 溢出运行时断言。联合哈希包 = {SPEC 全文, RESOLVED_CONFIG.yaml, 代码 commit, requirements.lock, 容器镜像摘要, BLAS 版本, 数据 schema 版本, measurement_regime_id, 生成器验证报告, Phase-I 基线}。

## 14. 冻结参数总表（索引）

| 域 | 值 |
|---|---|
| 生命周期 | regime ≤3（α 预算 0.03/0.015/0.005）；第 2 个 INCONCLUSIVE 关线；项目 ≤6 年 |
| 假设图 | §1 初始权重与转移矩阵；混合配置 FWER 验证义务 |
| 运输 | 分阶段（min self-edge → min 特征距离 → 字典序迭代固定）；特征距离五维 ×10⁶ int64；投影七步 + 5% 容差；两 primitive；unswapped ≤20% ∧ 高题材度 ≤1.5× |
| Run-in | Stage-E ≥60 日（白名单精度条件）；Stage-B ≥250 日 self-collected 后开庭；Wilson 区间；max(0.5pp, 25%) 双阈值 |
| 漂移/审计 | Phase-I 固定基线；EWMA λ=0.2 连续两月 ARL≥24 月；审计 = 120 日 warm-up + 250 日全窗重放 ×200，容差 ×1.5，连续两次暂停 |
| H-Z2b | B_e=AUM/6=3333 万；买至 D0+7；清算至 D0+20；haircut 2% |
| H-Z3 | Top2Mean−RestOfPoolMean；MES 20bp；池 ≥4；n_Z3 独立 |
| H-Z1 | 决策函数 + 唯一自动延长（125 日一次，条件冻结）；总年限内 |
| P3 | ITT 主口径；六协变量分阶段指派；d 之 SD<5bp 降绝对等效 |
| 推断 | §9 全文（交叉重采样细则、B=5000、percentile、簇 <10 INCONCLUSIVE） |
| E3 | 口径 2 更名共同终点财富机会成本 |
| 其余 | §2-§8 正文即冻结值 |

## 15. 给验证 Agent 的交代要点
1. 本文件为唯一真相源（**零回引**——发现任何"沿旧版"式缺口即停止上报，那是规格 bug）；
2. 强制单测：§12 步骤 2 全列 + minP 秩矩阵 vs 暴力枚举、时间轴断言、B 臂（Top2−Rest）代数断言、H-Z2b 人民币参与率约束生效断言（构造 ADV 小于订单的样例）、Gate0 SD 地板断言；
3. 全部登记簿（四人群/out-of-support/漏斗/unswapped 条件表/regime 日志/quarantine/contaminated/degenerate_resample）入库；
4. 闸门 flag 阻断；影子期改规则 = 作废。

---

## 附录 A：第十一轮审查十八红线 → v11 落点
1 全文展开 → 全文（零回引）｜2 ThemeDistance 退化 → §5（特征距离替代）｜3 大数技巧废除 → §5/§7.1（分阶段+迭代固定）｜4 两 primitive → §5｜5 投影七步 → §5｜6 Run-in 两段制（60 日工程/250 日预算）→ §11｜7 双阈值+Wilson → §11｜8 Phase-I 固定基线 → §2.5｜9 审计全窗重放 → §2.5｜10 假设图权重/转移/混合配置 → §1/§10｜11 生命周期 α 预算 → §0｜12 匹配分阶段化 → §7.1｜13 H-Z2b 真实货币 → §7.1｜14 清算期限+haircut → §7.1｜15 P3 ITT → §8｜16 P3 算法化 → §8｜17 d 之 SD 地板 → §8｜18 H-Z3 改 Top2−Rest → §6（+E3 更名 §4.2、H-Z1 延长规则 §7.4、推断展开 §9、混合配置 OC §10）

## 附录 B：留痕
1. **自认错误两处**：ThemeDistance 恒等退化（约束与目标用同一被约束为常数的变量——第二优化目标是数学幻觉）；canonical 单文件声明第三次未达标（v9、v9.1、v10 均含回引）——本版全文物理展开；
2. Stage-B 250 日要求 = 正式影子开庭推迟约一年：这是"60 日本体不能凭 Monte Carlo 变成 200 个本体年"的诚实代价；期间 DEV/OOS-B 探索与工程完善照常进行；
3. H-Z3 改纯排序命题：损失"政策增益"直读性（由描述性池平均口径保留），换取效应尺度与池规模解耦；
4. H-Z1 唯一自动延长规则：以客观条件（点估计 ≥2% ∧ 80% 下界>−1%）替代人工否决——预承诺完整性优先于治理灵活性。

*登记时间：2026-07-16。冻结对象：全文。变更 = v11.x = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
