# MCRS SFL 验证规格书 v12.1 — FINAL CANONICAL（图形序贯化与类型封口）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / FINAL CANONICAL`
版本：`v12.1`（以 v12.0 为基做增补与修正、非压缩性重写；完全自包含单文件、零回引；替代 v1-v12.0。第十三轮外部审查 20 条红线全部核实成立、零驳回，其中三处为 v12 压缩重写造成的内容回归——设计方承认"全文重写制造回归"的模式并改用增量修订）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文 + RESOLVED_CONFIG + §13 环境产生逐日完全相同输出。`D+k` 均为交易日。

---

## 0. 终局条款、识别边界与生命周期治理

**三层条件识别边界**：最终科学结论限定于——供应商本体稳定期、风险集匹配共同支持域内、且该测量制度的安慰剂装置已被证明在 ±3bp 等效边界内的条件下，给定供应商实际输出的题材本体，协调相变是否携带未来收益信息。本体反事实形成不可识别；漂移可能与强叙事相关（信息性删失限制永久写入判词）；漂移期 Episode 隔离分层。

**科学死亡线（全条件复述）**："在本体稳定期、安慰剂装置被证明在 ±3bp 等效边界内、且具有风险集共同支持的点火事件中，题材协调相变未能在点火后 0-4 或 5-14 交易日窗口向题材全体成员产生 ≥10bp 的平均或中心收益扩散"——由四个科学经济节点在影子数据上全部 Economically FAIL（**序贯兼容上界** < MES，§9）触发。

**生命周期双预算**：regime ≤3；α 预算 0.03/0.015/0.005；β 预算 0.015/0.0075/0.0025；第 2 个 INCONCLUSIVE regime 关线；全部 regime 共同披露；meta 须预登记。**时钟**：ResearchClock（正式影子累计）≤6 年；WallClock（自快照库启动）≤8 年硬上限；四时钟（Research/Wall/ActiveShadow/PausedRunIn）进 OC；**OC 时间指标 = P(3 年/5 年/8 年内判决)，分别自快照库启动、正式影子启动、ActiveShadow 累计三个原点报告**（10 年指标废除——与 8 年墙钟冲突）。

**判决语义**：四分法判词；四人群分层；DEV/OOS-B = 工程与方向性证据；终审只认 self_collected；H-Z1 = 项目资源指标。
签署人：________ 日期：________

## 1. 图形序贯经济假设图（v12.1 核心修订）

### 1.1 节点、权重与转移（继承 v12 并补全）
```
节点（正式经济零假设 H_i: θ_i ≤ MES_i）与初始权重（×α_r）:
  L-mean 0.5 | I-mean 0.3 | L-ctr 0.1 | I-ctr 0.1；Z2b/P1a/Z3 初始 0
初始转移矩阵 g: L-mean→{Z2b .4, P1a .4, L-ctr .2}；I-mean→{Z2b .4, P1a .4, I-ctr .2}
  L-ctr→{Z2b .5, P1a .5}；I-ctr→{Z2b .5, P1a .5}；Z2b→{Z3 1}；P1a→{Z3 1}；Z3→∅
Bretz 更新（拒绝 j 后）: α_i ← α_i + α_j·g_ji；g_ik ← (g_ik+g_ij·g_jk)/(1−g_ij·g_ji)（分母 0 → 0）
```

### 1.2 图形序贯化（修复固定图 × 序贯的类型错误）
```
每节点信息时钟: 科学/Z2b/Z3 = 事件钟（锁定配对数）；P1a/H-Z1 = 日历钟（20 日块数）
中期分析时点（冻结）: 各节点在自身信息比例 {1/3, 2/3, 1.0} 开庭；
  SMD 整体检查失败 → 该次开庭永久取消（不顺延、不补开）
α-spending: 各节点在其当前 local α 下采用仿真校准的 OBF 型 spending
  （边界由 §10 边界仿真在完整图机制下联合产出并冻结）
**转入 α 使用规则（冻结）**: 节点 j 被拒绝、α 转入节点 i 时——
  (a) 已花费 α 不退还；(b) 转入 α **仅可用于转入时点之后的信息增量**
  （spending 曲线自转入时点起以"旧已花费 + 新增预算"重新铺设，
   禁止对已开庭数据追溯重算拒绝）；
  (c) 节点 i 的信息目标按冻结公式以当前累计 α 重算: n_i = n_table(α_current, MES_i, σ̂_blind)
   （n_table 由盲化 SSD 预生成为 α 网格 × 假设的查找表）
n_target 双目标（冻结）: n_i = max( n_PASS(α_path_min), n_FAIL(β_r) )
  α_path_min = 该节点在全部图路径中可能获得的最小非零 α（保守基线）；
  收到更多 α 时按 (c) 动态下调剩余需求
repeated p 值: 各次开庭输出与当前边界兼容的 repeated p（由边界仿真同套机制产出）
```

### 1.3 节点 full-pass 与业务护栏（修复双状态机）
```
full-pass(i) = 统计拒绝（repeated p ≤ 当前边界）∧ 预登记护栏通过:
  P1a 护栏: MDD_C−MDD_I ≤ 2pp ∧ CVaR_C 不劣（点估计）
  Z2b 护栏: capacity_liquidation_failure 事件占 T 臂比例 ≤ 20%
  科学节点: 无附加护栏
仅 full-pass 传播 α 并解锁下游 Gate；统计拒绝但护栏失败 → 节点标 guard_failed，
  其 α **退役不回收**（保守，防失败节点向下游输血）；判词如实分开书写
终期判决: 各已解锁节点达自身信息目标即终判；
  TerminalDate = 已解锁节点预计完成日之最大（受 §0 时钟封顶）；
  未解锁节点（如 Z3 从未解锁）不拖延上游判决；到时未达标者 INCONCLUSIVE
FAIL 侧: economic-FAIL 需**序贯兼容单侧上界**（§9.3）< MES，水平 1−β_r
```

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
资格线：带 trade_date 每日历史成分；覆盖 ≥3 年、缺失日率 ≤2%；ID 年度稳定率 ≥95%。评分：覆盖年数 → [8,100] 带内占比 → KPL>DC>THS。第二源原生复现；THS 交叉校验。`vendor_reconstructed_history` / `self_collected` 标签；终审只认后者。

### 2.2 题材宇宙与聚类
合格题材成分 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`（目检+哈希）。聚类：每日 Members_{D−1} 全对 Jaccard；J>0.5 按 (J 降序, ID 对字典序) 依次 clique 校验处理；canonical_id merge 继承 first_seen 最早（并列 ID 小）、split 由最大 Jaccard 子簇继承；lineage append-only；Episode 锁定点火时身份；左截断 120 日；谱系 J>0.7。

### 2.3 快照库、双成员集、时钟 PIT
每日收盘后快照全部源（append-only+时间戳）；点火检测集 Members_{D−1}；基集 Members_{D0−1}；MembershipExpansion 日记；22:00 截止；文本类回测 D+2。

### 2.4 行情、canonical 单位、合格宇宙、市场状态与总回报账本
- **canonical 单位（v12.1 冻结，修复恒等式单位缺口）**：price = 元/股；volume = 股；amount = 元；turnover = 小数；market_cap = 元。全部源数据在摄入层一次性换算（Tushare daily：vol 手 ×100 → 股；amount 千元 ×1000 → 元；VWAP = amount/volume 元/股），下游禁止再出现原始单位；Amount = Volume × VWAP 在 canonical 单位下恒成立；
- 合格宇宙 = 上市 ≥60 日 ∧ 非 ST/停牌/退市整理；封板 close_raw≥up_limit、触板 high_raw≥up_limit（pre-2019 回退 pct_chg≥+9.8%∧close==high）；20 日特征 ≥15 有效日；股性 250 日（60-249 扩展窗）；质量闸门失败 flag 阻断；
- 日度状态 STATE_D = UP iff HS300≥MA200；年度状态仅生成器资格；
- 科学收益事实源：不可变 raw close + PIT 公司行动 total-return ledger；outcome ledger 哈希链锁定；禁依赖可重算前复权序列。

### 2.5 本体漂移治理与审计
硬漂移即停（schema 破坏/ID 重置/发布越 22:00）。统计漂移：五指标 EWMA（λ=0.2）+ **UP/DOWN 分状态 Phase-I 固定基线**（各状态基线取自 Stage-B 该状态日；某状态 <30 日 → 该状态基线推迟至正式影子首 30 个该状态日并标记 baseline_deferred——修复状态依赖误重启）+ 连续两月确认；正式要求 = P(稳定 regime 5 年误 reset) ≤10%（五指标联合 OC 校准；ARL 派生报告）；近零分母双阈值。**125 日审计（数值冻结，修复方法冲突）**：携带 120 日 warm-up 的 250 日滚动窗重放 ×200 条；**触发数 t-UCB(95%) ≤ 3.0；FalseCapitalDays bootstrap 分位 UCB(95%) ≤ 60**；一次越界挂旗、连续两次暂停；UP/DOWN 分报；误暂停 OC 校准（5 年 ≤10%）。

## 3. 日度零模型（minP；宇宙/家族分离）

```
**MarginalUniverse_D（v12.1 修复矛盾）** = 当日全部 native 合格题材
  —— (B+1)×C_M 矩阵在此宇宙上计算；p_marg 与 CoordinationState 对全部合格题材可得
**FWERFamily_D** = 以 D−1 信息判定为 DORMANT 的题材子集（当日涨停结果读取前冻结）
  —— m_b = min_{c∈FWERFamily} p[b,c]；p_FWER 仅对家族成员定义；Ignition 仅在家族内裁决
分层: 板块×市值3×波动3×动量3×股性3；层 ≥8；粗化序动量→波动→股性→市值；板块不并
置换: 保留当日各层真实涨停数、层内 Fisher-Yates；子流 = SHA-256(trade_date‖src‖spec‖b)；
  B=2000，临界带 [α/3,3α] 全族追加至 20000（前 2000 行不可变）
p[b,c] = #{b': S[b',c]≥S[b,c]}/(B+1)；p_marg=p[0,c]；p_FWER=(1+#{m_b≤p[0,c]})/(B_random+1)
CoordinationState = −log10 p_marg；点火: LU_real≥2 ∧ p_FWER≤α_day
行业条件口径三态标签（p_cond 0.10 线；层<8 uninformative）
```

## 4. Episode 状态机（公式全展开，修复符号缺口）

### 4.1 基础量公式（冻结）
```
CrowdPctl(c,D) = rank_pct( Share20(c,D) 在 c 自身历史 Share20 中 )
  Share20 = mean_{t∈[D-19,D]}( Σ_{i∈Members} Amount_i,t / Σ_{全市场合格} Amount_j,t )
  历史 ≥120 日自史分位；60-119 扩展窗[crowd_expanding]；<60 当日横截面[crowd_xsec]
MaxBoard(c,D) = max_{i∈成员} 连续封板天数（连续 = 无间断交易日均封板）
BombRate(c, 窗) = #{触板未封: high≥up_limit ∧ close<up_limit} / #{触板}（触板 ≥3 才定义）
成员分类（剔最高连板链本股）: ClosedLimit = close_raw≥up_limit；
  TouchedOnly = high_raw≥up_limit ∧ close_raw<up_limit；
  StrongResidual = 未触板 ∧ 当日收益 ≥ +5%
p_base_marg(Episode,D) = #{b'∈{0..B}: S_base[b',·] ≥ S_base[0,·]}/(B+1)
  （S_base = 冻结基集成员在当日全市场置换矩阵下的封板计数；成员按当日 PIT 特征
   定位当日分层；不可交易成员不进分子；可交易基集 <8 → 当日不可检验）
```

### 4.2 状态机与时间轴
DORMANT（20 日 CoordinationState≥2 天数 ≤1 ∧ CrowdPctl<0.80）→ IGNITION（次日起 LU≥2∧p_FWER≤α_day；同簇取 p_marg 小；EpisodeID 锁定）→ CONFIRMATION（landmark D0+4：新增 ClosedLimit≥1 ∧ Distinct(CL∪SR)≥2 ∧ [扩散 p_base_marg≤0.10+新增封板 或 晋级 MaxBoard 抬升∧链起点≥D0−1] ∧ BombRate(Age1..4)≤0.5）→ 入场 D0+5、信号 D0+14、执行 D0+15；SignalEnd 成 14/败 4；冷却 20 日自次日；CAR(1..60) 观察窗。DetectionLag（最近正向激活段）与成熟度三分类、EpisodeType、E1/E2/E3（E3 口径 2 = 共同终点财富机会成本）沿 v12 §4 全文。

## 5. 条件本体零模型（候选边恢复 + 校准细节恢复）

```
**候选边（v12.1 恢复 v11 遗失的灵魂约束）**:
  candidate_edge(i←j) = 同 donor 层 ∧ **无共同合格题材标签（块起点，合格标签 = §2.2
  排除后的 [8,100] 带内题材）** ∧ i≠j ∧ 投影可行（预计算: 完整 20 日重建+七步投影，
  projection_distance>5% 删边）；self-edge 单独始终可行
donor 层 = 板块×市值3×股性3×申万一级行业×块起点波动3×动量3；层 ≥8；
  粗化序①动量②波动③股性④市值（行业/板块不并）；
  **全粗化后仍 <8（v12.1 冻结）→ 该层全体 self-edge、计入 unswapped、20% 闸门照常适用**
三阶段完美指派: ①指派空间内 min self-edge 数 ②固定 S* min Σ FeatureDistance
  （五维 {ln市值, 波动, 动量, 股性, lnADV额} donor 层当块起点标准化、样本 SD、
   零方差删维√d 重归一、等权、缺失退出资格、int64×10⁶）③ID 迭代固定唯一化
路径向量: {O/H/L/C/VWAP 相对 PrevClose, Volume/ADVVol_pre, 停牌旗标}；Amount 派生
块 20 日（敏感 10/40、随机起点 seed=SHA-256('block'‖year‖layer)、circular）；
  bijection；unswapped ≤20% ∧ 高题材度 ≤1.5×
验证套件 13 指标（沿 v12 §5 全文）；**GENERATOR_FAIL 处置（v12.1 修复）**:
  历史验证失败 → live 路线前置条件 = 同一 13 项套件在 Stage-B 250 日 self-collected
  数据上全部通过；不通过 → 年度零模型不可用 → 正式影子不能开（上报项目决策）
**α_day 校准（v12.1 恢复遗失细节）**: 网格 {0.2%, 0.4%, 0.6%, 0.8%, 1.2%}（K=5）；
  合成年 ≥400 对半分（校准 200 / 验证 200）；验证半 simultaneous UCB
  （Bonferroni 1−0.05/(2K)=1−0.005）取满足双预算的最大 α；无解 → 上报停止（禁插值）
双预算: UCB_t(E[假确认触发/年]) ≤2（半宽 ≤0.3）；UCB_boot(E[FalseCapitalDays/年]) ≤40
  （相对半宽 ≤15%）；**资本政策对象（v12.1 冻结）= Policy C 账本**（6 槽、确认触发驱动，
  §7.2 全规则）——"假仓"即假确认事件在该账本下的实际持仓
漏斗全表输出
```

## 6. 载体 ZJ 与第二法庭（公式全展开）

```
容量: ADV20@D0 ≥ 3.33e8 元 ∧ 流通市值@D0 ≥ 5e9 元
纯度: D0−1 在籍 ≥20 交易日；参与: [Π(1+r_i) − Π(1+r_基集等权)](D0..D0+4) > 0
  ∧ mean(turnover_i, D0..D0+4) ≥ 1.2 × mean(turnover_i, D0−20..D0−1)
护栏: D0+4 收盘非涨停 ∧ Episode 内封板次数 ≤1 ∧ Π(1+r_i)(D0..D0+4) − 1 < 40%
可买(D0+5): 非开盘涨停/停牌 ∧ GapLimitRatio = (Open_{D0+5}/Close_{D0+4} − 1)/UpLimitPct_{D0+5} ≤ 0.70
  （UpLimitPct 按板块 10%/20%/30%）
EventAmountShock_i = mean(Amount_i, D0..D0+4) / mean(Amount_i, D0−20..D0−1)；取前 2、
  替补至第 4、单标的半仓、池空记录
H-Z3: estimand = Top2Mean − RestOfPoolMean（D0+5 VWAP 买入→D0+14 收盘，
  含成本买 12.5bp/卖 17.5bp）；common support = 可买池 ≥4 的事件全体；MES 20bp；
  主推断 = 处理-对照 lineage 连通分量 × 20 日入场块两向 bootstrap；n_Z3 独立
**H-Z2b（v12.1 四定义补全）**:
  estimand = Mean( R_e(T) − R_e(A) ) —— 配对差（A = 匹配对照题材的容量篮子按同一
    执行引擎跑伪事件 P&L）
  成本 = 买 12.5bp / 卖 17.5bp（印花税 PIT: 2023-08-28 前卖 10bp）
  B_e = AUM/6 = 3333.33 万元（AUM=2e8 元冻结）；买入 D0+5..D0+7；清算 D0+15..D0+20
  haircut = max(2%, 10% × 残余市值 / **ADV20@D0+20**)、上限 20%
  **capacity failure 护栏 = capacity_liquidation_failure 占 T 臂事件 ≤20%**（§1.3 full-pass 条件）
描述性: 池平均政策口径、C0（容量池同排序）、N（池内 RS20 = 个股 20 日收益 − 基集等权
  20 日收益, 截止 D0+4, 前 2）
```

## 7. 四级法庭

### 7.1 第一法庭
匹配（分阶段最优 ①max 匹配数 ②min 总距离 ③ID 迭代固定；协变量 4 项 @[D0−20,D0−1] pre-assignment 风险集标准化；卡尺 1.0；Jaccard<0.2；个股重叠 ≤20%；同日无放回跨日可复用；unmatched → out-of-support registry）；SMD 十变量 ≤0.10 一次生成整体判定、序贯节点失败永久取消该次；fallback tree（unmatched>30%→卡尺 1.5 一次→MATCH_INFEASIBLE；ZJ 池<30%→H-Z3 预判 INCONCLUSIVE；频率 ∉[10,150]→停止；SMD 失败→上报）；科学口径（total-return ledger；成员零删除；退市三级；起始等权买入持有；均值 = 组合配对差均值；中心 = 成员中位数→配对差→均值；双窗；ITT 主/PP 副；判词全条件复述）。

### 7.2 政策比较（订单生命周期补全）
```
InstrumentSet（D0 冻结）= 基集 ∩ ADV20@D0≥1e8 ∩ 非ST/停牌@D0 ∩ 上市≥60日；事件内等权
Policy I: 全部 Ignition，D0+1 入场；Policy C: 仅 CONFIRM=true，D0+5 入场；夭折持现金
**订单生命周期（v12.1 冻结）**:
  event_budget 在接纳日锁定 = min(接纳日 NAV/6, 可用现金)（此后不随 NAV 重算）
  买入: 入场日起滚动执行（5% 参与），**买入截止 = 入场日+2**，未成部分永久现金
  卖出: 信号日次日起滚动执行，直至全部卖出（跌停/停牌顺延；无卖出截止）
  槽位: max_active_slots=6；部分成交占整槽；持仓（含顺延尾与 EXIT-3C 长仓）完全退出
    才释放；被拒事件不占槽；空池事件即时释放
  单股 ≤ CurrentNAV/12；受上限截断的剩余预算留现金；成本买 12.5bp/卖 17.5bp；
  同日净额化；买用日初现金；卖出所得次日可用；现金收益 0；优先级 = 题材 ID 序；无抢占
判决（P1a 节点）: 252×mean(r_C − r_I) 的序贯兼容下界 > 1%（§9）；
  full-pass 另需护栏（§1.3: MDD 差 ≤2pp ∧ CVaR 不劣）
```

### 7.3 第三法庭
沿 v12 §7.3 全文（Breadth/ThemeRS20/StockExcess20 公式、EXIT-3C 优先级与执行时钟、V-STOP、组合级对比、推断块 60）。

### 7.4 第四法庭
沿 v12 §7.4 全文（一字判定、净额化 5% 参与、Decision-to-VWAP slippage、容量 1/3/5%、动态暴露基准 + **容量指数成本模型 = 与策略同一成本（买 12.5bp/卖 17.5bp）月度调仓双口径**、判决量 252×mean、两因子归因、H-Z1 决策函数 + 唯一自动延长）。

## 8. 安慰剂

P3（同日风险集、精确匹配 {STATE_D, 涨停数三分位} + 连续 4 维 {dormant_high_count_20, CrowdPctl, ln 成员数, 前 20 日收益}、分阶段指派、ITT 主口径）；P4（簇独立循环位移避 Episode 窗 ∧ 活跃度匹配）；**双层重采样外层 ≥2000（v12.1 提升，修复 500 次撑不起 ±3bp 硬闸门）**、内层 1 轮伪化；通过线 = 四 endpoint 各自外层 95% CI ⊂ [−0.1,+0.1]d ∧ [−3bp,+3bp]；d=Mean/SD(配对差)（原样本固定 SD；SD<5bp 降绝对等效）；Gate0 通过率进 OC。

## 9. 分法庭主推断（p 值与序贯兼容界补全）

### 9.1 点估计与重采样
H-Z2 族/H-Z3：配对差 + 两向交叉重采样 bootstrap——**第一维 = 处理-对照 lineage 二部图连通分量（v12.1 修复控制复用依赖）**、第二维 = 20 日入场块；外层抽 m 分量 + k 块有放回、保留交集配对、空交集重抽 ≤100 次。H-P1a/H-Z1/H-Z6：日历 spread + stationary bootstrap（块 20；H-Z6 块 60）+ NW 稳健。

### 9.2 正式检验 p 值（v12.1 冻结，修复"只有 percentile CI"）
```
H_i: θ ≤ MES_i 的一侧移位零假设 bootstrap p 值:
  p_i = ( 1 + #{ b: θ̂*_b − θ̂ ≥ θ̂ − MES_i } ) / ( B + 1 )
  （以重采样分布在零边界 θ=MES 处中心化；与检验反演 CI 一致）
**自适应 B（修复 MC 分辨率）**: 最低 B ≥ 100/α_i（当前 local α）；阶梯 5k→20k→100k；
  p_i 的 Clopper-Pearson 95% 上界 ≤ 当前边界才允许拒绝；不可分辨 → 本次开庭不拒绝
repeated p 值: 由 §10 边界仿真同套机制对各开庭时点校准输出
```

### 9.3 序贯兼容 FAIL 上界（v12.1 冻结）
economic-FAIL 的单侧 1−β_r 上界采用 stagewise-ordering 序贯兼容构造：由 §10 边界仿真在"该节点未提前 PASS"的条件路径分布上校准终期上界临界值；普通固定样本 bootstrap 上界仅作描述性并列。

## 10. 序贯法庭与 OC

各节点自身信息比例 {1/3,2/3,1} 开庭（§1.2）；终期 = 分量条件（§1.3）；封存-启封；SMD 取消制。**边界仿真（联合产出）**：完整图机制（动态 α 转移 + 转入仅未来 + spending + repeated p + 序贯 FAIL 上界 + 护栏 + SMD 取消 + Gate0 阻断 + drift/审计/run-in/regime 全生命周期）在混合真假配置族（全 null/全真/各单真/灰区 θ∈(0,MES)×4/Gate2 半真/护栏失败配置）下逐配置验证 P(任一错误经济 full-pass) ≤ α_r ∧ P(错误死亡) ≤ β_r；效应五情景；四时钟分布；P(3/5/8 年判决) 三原点报告。

## 11. Prospective Run-in（两段制，精度规则修订）

```
Stage-E（≥60 交易日，可延长）: 校验发布时间、schema、成员日变更率、donor 可行率、
  匹配覆盖率、null trigger rate
  **精度方法（v12.1 修订）**: (10 日时间块 × canonical lineage) 双层 cluster bootstrap；
  **最低有效时间块数 ≥6（不足则 Stage-E 延长）**
  分指标停止阈值（95% CI 半宽）: 成员变更率 ≤ max(0.5pp, 0.25×p̂)；donor 可行率 ≤3pp；
  匹配覆盖率 ≤5pp；null trigger rate 按时间块估计（半宽 ≤ 0.5×点估计）
  真实信号数量 MUST NOT 进入停止条件（白名单断言）
Stage-B（累计 ≥250 交易日 self-collected）: 真实 250 日本体路径 live null replay ≥200 条 →
  **若历史 GENERATOR_FAIL: 13 项验证套件须在本段数据上全部通过，否则年度零模型不可用**
  → 确认双预算（触发 t-UCB / 资本日 bootstrap UCB，与 §5 逐字一致）→
  UP/DOWN 分状态 Phase-I 基线 → 正式影子自 Stage-B 完成 + RESOLVED_CONFIG 确认起算
偏差处置: 越带 → 预登记重校准 → 全链重跑 → 重签 → 影子重新起算
```

## 12. 冻结流程

```
1. 快照普查+快照库启动【无条件立即】
2. 引擎+合成自检（新增: MarginalUniverse/FWERFamily 分离断言、候选边题材零重叠断言、
   图形序贯转入 α 仅未来断言、canonical 单位断言[手/千元换算样例]、
   订单生命周期断言、p 值移位中心化断言、n_table 查找断言）
3. 历史条件零模型（状态资格线）→ provisional α/config
4. 盲化可行性审计 → 5. 盲化 SSD（n_table: α 网格 × 假设 × PASS/FAIL 双目标）
6. 边界仿真（§10 全项联合）→ 7. Run-in Stage-E → Stage-B
8. RESOLVED_CONFIG（图+更新算法+spending+n_table+OC 表+四时钟+Phase-I 分状态基线）联合哈希
9. ★ 签署 → FREEZE → 10. 解锁经验安慰剂与 DEV/OOS-B 探索
11. 正式影子 → §0 判决
```

## 13. 可复现性环境
SHA-256 / UTF-8 / canonical JSON / PCG64DXSM / little-endian int64 / IEEE-754 float64 / 稳定 mergesort（并列 ID 序）/ 固定归约序 / int64 溢出断言。联合哈希包 = {SPEC, RESOLVED_CONFIG, 代码 commit, requirements.lock, 镜像摘要, BLAS, schema 版本, regime_id, 生成器验证报告, Phase-I 分状态基线, outcome ledger 根哈希}。

## 14. 冻结参数总表（v12.1 增量索引）

| 域 | 值 |
|---|---|
| 图形序贯 | 信息比例 {1/3,2/3,1}；OBF 型仿真校准 spending；转入 α 仅未来增量；n_table 动态；n=max(n_PASS@α_min, n_FAIL@β_r)；SMD 失败该次取消 |
| full-pass | 统计拒绝 ∧ 护栏（P1a: MDD≤2pp∧CVaR；Z2b: 清算失败 ≤20%）；guard_failed α 退役 |
| 终期 | 分量条件；TerminalDate=已解锁节点完成日最大；未解锁不拖延 |
| minP | MarginalUniverse（全部合格）/ FWERFamily（D−1 DORMANT）分离 |
| 运输 | 候选边含题材零重叠（恢复）；层全粗化后<8 → 全 self-edge；α 网格 {0.2..1.2}% K=5、合成年 ≥400 对半 |
| 单位 | 元/股、股、元、小数、元（摄入层一次换算） |
| 生成器 | GENERATOR_FAIL → live 13 项套件通过才可用 |
| Run-in | 10 日块 ≥6；分指标阈值（3pp/5pp 等） |
| 审计 | 触发 t-UCB≤3.0；资本日 boot-UCB≤60 |
| 推断 | 移位零假设 bootstrap p；B≥100/α 自适应阶梯；序贯兼容 FAIL 上界；处理-对照连通分量聚类；Gate0 外层 ≥2000 |
| H-Z2b | 配对 estimand；成本；haircut ADV20@D0+20；失败率护栏 20% |
| 政策 | 订单生命周期（预算接纳日锁定、买入截止+2、槽位全规则） |
| OC | P(3/5/8 年) 三原点；灰区与护栏失败配置；资本政策对象 = Policy C 账本 |
| 基线 | 漂移 Phase-I 分 UP/DOWN 状态固定 |

## 15. 给验证 Agent 的交代要点
1. 唯一真相源（零回引，缺口即停）；2. §12 步骤 2 全部断言 + 既有断言集（minP vs 枚举、指派反例 S*=2、时间轴、B 臂代数、货币参与率、SD 地板、总回报账本不可变）；3. 全部登记簿入库；4. 闸门 flag 阻断；影子期改规则 = 作废。

---

## 附录 A：第十三轮审查二十红线 → v12.1 落点
1 图形序贯化 → §1.2｜2 中期时点冻结 → §1.2｜3 终期分量条件 → §1.3｜4 路径 n_target/n_table → §1.2｜5 序贯兼容 FAIL 界 → §9.3｜6 移位零假设 p 值 → §9.2｜7 自适应 B+MC 闸门 → §9.2/§8｜8 full-pass 护栏入图 → §1.3｜9 宇宙/家族分离 → §3｜10 候选边恢复 → §5｜11 层<8 处置 → §5｜12 canonical 单位 → §2.4｜13 α 网格恢复+资本政策对象 → §5｜14 GENERATOR_FAIL live 验证 → §5/§11｜15 Stage-E 块数与分指标阈值 → §11｜16 审计数值冻结 → §2.5｜17 连通分量聚类 → §9.1｜18 公式全展开 → §4/§6｜19 H-Z2b 四定义 → §6｜20 订单生命周期+OC 8 年 → §7.2/§0

## 附录 B：留痕
1. **模式级自认**：v12 的三处内容回归（候选边约束、α 网格、公式集）由压缩性全文重写造成——v9→v12 每次重写都在丢失旧版已修内容；自本版起改增量修订制，重写禁令写入交付纪律；
2. guard_failed 节点 α 退役不回收：保守方向（损失功效、不损失错误率）；
3. n_table 查找表制：以预生成表替代运行时重算，换取动态 α 下样本量规则的确定性；
4. Stage-E 最低 6 个 10 日块：60 日下限在低活跃期会自动延长——诚实的代价。

*登记时间：2026-07-16。冻结对象：全文。变更 = v12.2 = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
