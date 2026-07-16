# MCRS SFL 验证规格书 v13.0 — QUALIFIED CANDIDATE（审查宪法版）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / QUALIFIED CANDIDATE`
版本：`v13.0`（以 v12.1 为基的**增量修订**（非重写）；完全自包含单文件、零回引；替代 v1-v12.1。本版三项任务：①冻结合格标准为审查宪法（§-1）②关闭 C1 残余（图形序贯唯一算法，§1.2）③补 C5 十项表（§1.4）+ 验收协议（§16）与非阻断登记簿（§17）。C2/C3/C4 经核实已由 v12.1 关闭，本版确认保留）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文 + RESOLVED_CONFIG + §13 环境产生逐日完全相同的**正式输出**（定义见 §-1）。`D+k` 均为交易日。

---

## §-1 审查宪法（合格标准，冻结）

### 标准一：确定性可复现
相同冻结数据、配置、代码版本与执行环境下，两个独立 Agent 的**正式对象**必须完全一致：①每日股票与题材合格宇宙 ②ConceptCluster 与 canonical lineage ③p_marg/p_FWER 与点火裁决 ④Episode 状态、Confirmation、冷却 ⑤风险集匹配结果 ⑥ZJ 池、排序与交易候选 ⑦每笔订单/成交/持仓/现金/退出 ⑧每法庭样本集、统计量、CI ⑨Gate 状态与最终判词。底层浮点允许 |x_A−x_B|<1e−12 的预冻结误差，但不得改变任何排名、阈值比较、配对、交易、Gate 或判词。

### 标准二：正式判词受统计装置支持
每个正式 PASS/FAIL/科学死亡/项目晋级判词，必须与预注册的假设、样本、错误预算和停止规则一致。会改变正式结论的每个节点必须完整回答十项：Population / Estimand / Null / MES / Sample / Dependence / Multiplicity / Sequential rule / Decision rule / Failure state（§1.4）。

### 阻断类别与终止规则
- **A 类（确定性阻断）**：能证明存在两个合规实现依据本文产生不同正式输出；
- **B 类（统计判词阻断）**：能证明统计装置不支持某个正式判词（零假设与判词不一致 / 多重性未覆盖正式声明 / 序贯停止破坏 CI 含义 / 样本与判词人群不一致）；
- **终止规则**：A=0 ∧ B=0 → SPEC 立即 QUALIFIED / FREEZE APPROVED。此后新问题的准入门槛 = 提供以下至少一项：①具体输入反例证明输出分歧 ②具体真假配置证明超错误预算 ③具体路径证明检验对象与判词对象不一致。"理论上可更严谨/也许有更好方法"不构成阻断；
- **非阻断项处置**：登记为 KNOWN_LIMITATION / FUTURE_ENHANCEMENT / ROBUSTNESS_OPTION（§17），不得阻止实验启动；
- **验收程序**：§16 双 Agent 一致性测试（八哈希）+ 统计装置压力测试，两项通过即合格。

## 0. 终局条款、识别边界与生命周期治理

**三层条件识别边界**：最终科学结论限定于——供应商本体稳定期、风险集匹配共同支持域内、且该测量制度的安慰剂装置已被证明在 ±3bp 等效边界内的条件下，给定供应商实际输出的题材本体，协调相变是否携带未来收益信息。本体反事实形成不可识别；漂移可能与强叙事相关（信息性删失限制永久写入判词）；漂移期 Episode 隔离分层。

**科学死亡线（全条件复述）**："在本体稳定期、安慰剂装置被证明在 ±3bp 等效边界内、且具有风险集共同支持的点火事件中，题材协调相变未能在点火后 0-4 或 5-14 交易日窗口向题材全体成员产生 ≥10bp 的平均或中心收益扩散"——四个科学经济节点在影子数据上全部 Economically FAIL（序贯兼容上界 < MES）触发。

**生命周期双预算**：regime ≤3；α 预算 0.03/0.015/0.005；β 预算 0.015/0.0075/0.0025；第 2 个 INCONCLUSIVE regime 关线；全部 regime 共同披露；meta 须预登记。**时钟**：ResearchClock ≤6 年；WallClock（自快照库启动）≤8 年硬上限；四时钟进 OC；OC 时间指标 = P(3/5/8 年内判决) 三原点报告。

**判决语义**：四分法判词；四人群分层；DEV/OOS-B = 工程与方向性证据；终审只认 self_collected；H-Z1 = 项目资源指标。
签署人：________ 日期：________

## 1. 图形序贯经济假设图

### 1.1 节点、权重与转移
```
节点（H_i: θ_i ≤ MES_i）与初始权重（×α_r）: L-mean 0.5 | I-mean 0.3 | L-ctr 0.1 | I-ctr 0.1；
  Z2b/P1a/Z3 初始 0
初始转移 g: L-mean→{Z2b .4, P1a .4, L-ctr .2}；I-mean→{Z2b .4, P1a .4, I-ctr .2}
  L-ctr→{Z2b .5, P1a .5}；I-ctr→{Z2b .5, P1a .5}；Z2b→{Z3 1}；P1a→{Z3 1}；Z3→∅
Bretz 更新（拒绝 j）: α_i ← α_i + α_j·g_ji；g_ik ← (g_ik+g_ij·g_jk)/(1−g_ij·g_ji)（分母 0→0）
```

### 1.2 图形序贯唯一算法（v13 关闭 C1）
```
节点状态: State_i = ( α_granted, α_spent, I_done, look_schedule, boundary_table, status )
  status ∈ {locked, active, rejected_pending_guard, full_pass, guard_failed, retired}
α_spent 定义 = 在 H0(θ=MES_i) 下、按**已执行各次开庭的实际边界**计算的累计拒绝概率
  （由边界引擎在冻结种子下输出，确定性数值）
边界引擎（唯一算法载体，冻结代码+冻结种子 → 同输入同输出）:
  输入 (α_granted, α_spent, 剩余 look 信息比例表, MES_i, σ̂_blind, 时钟类型)
  输出 剩余各 look 的名义临界值 c_k（OBF 型形状），满足条件错误率口径:
    P_H0( 在剩余任一 look 拒绝 | 迄今未拒绝 ) = (α_granted − α_spent) / (1 − α_spent)
事件处理（全部事件按日终顺序执行；同日多事件按节点名字典序）:
E1 开庭(look k):
  SMD 整体检查失败 → 该 look 从 schedule 永久移除（不花费 α；边界引擎下次重生成时
    以"少一次开庭"处理）
  否则: 计算 repeated p（§9.2 移位零假设 bootstrap、自适应 B）；p ≤ c_k → status=
    rejected_pending_guard；α_spent 更新为含本次 look 的累计值
E2 收到转移 α（数量 δ）:
  α_granted += δ；调用边界引擎重生成剩余 look 边界（输入含更新后 α_granted 与既有
    α_spent）——**转入 α 仅经由"剩余 look 边界"生效，已执行 look 的裁决永不重算**；
  信息目标更新: n_target_i ← n_table(α_granted, MES_i, σ̂_blind)（仅影响未来排期）
E3 rejected_pending_guard → 护栏评估（§1.3）:
  通过 → full_pass：按 §1.1 更新式将 α_granted 全额传播（触发接收节点 E2）并解锁下游 Gate
  失败 → guard_failed：α 退役不传播（保守）
终期: 各已解锁节点达自身 n_target 即终判；TerminalDate = 已解锁节点预计完成日之最大
  （受 §0 时钟封顶）；未解锁节点不拖延上游；到时未达标 → INCONCLUSIVE
FAIL 侧: economic-FAIL = 序贯兼容单侧 1−β_r 上界（§9.3）< MES，仅终期判定
```

### 1.3 full-pass 护栏
P1a 护栏：MDD_C−MDD_I ≤2pp ∧ CVaR_C 不劣（点估计）。Z2b 护栏：capacity_liquidation_failure 占 T 臂事件 ≤20%。科学节点无附加护栏。仅 full_pass 传播 α 并解锁 Gate；guard_failed 的 α 退役。

### 1.4 正式节点十项表（v13 关闭 C5 汇总缺口）

| 项 | 科学四节点（L/I × mean/ctr） | Z2b | P1a | Z3 |
|---|---|---|---|---|
| Population | 本体稳定期 ∧ 安慰剂等效 ∧ 风险集共同支持域内的全部 Ignition（含夭折；signal→matched 人群） | 同左 ∧ 容量子集非空 | 同左（组合层全体日历日） | 同左 ∧ D0+5 可买池 ≥4 |
| Estimand | matched-sample 配对差均值：mean = 题材起始等权买入持有组合收益差；ctr = 题材内成员中位数收益差；窗 I=Close_D0→D0+4、L=Close_{D0+4}→D0+14（total-return ledger） | Mean(R_e(T)−R_e(A))：事件预算现金流 P&L 配对差（§6） | 252×mean(r_C−r_I)：日历组合 spread | Top2Mean−RestOfPoolMean（D0+5 VWAP→D0+14 收盘，含成本） |
| Null | θ ≤ 10bp | θ ≤ 50bp | θ ≤ 1%（年化） | θ ≤ 20bp |
| MES | 10bp/窗 | 50bp/事件 | 年化 1% | 20bp/事件 |
| Sample | 影子期锁定配对（事件钟）；unmatched 入 out-of-support registry 不入样 | 同左（可买池非空事件） | 影子期全部非重叠 20 日块（日历钟） | 可买池 ≥4 的事件 |
| Dependence | 处理-对照 lineage 连通分量 × 20 日入场块两向 bootstrap | 同左 | stationary bootstrap（块 20）+NW 稳健 | 同科学节点 |
| Multiplicity | §1.1 图初始权重 ×α_r；生命周期 α/β 预算（§0） | 图节点（初始 0，经转移获得） | 同左 | 同左（Gate3 后） |
| Sequential | 信息比例 {1/3,2/3,1} 开庭；§1.2 算法；提前判仅 PASS；SMD 失败该次取消 | 同左 | 同左 | 同左 |
| Decision | repeated p ≤ c_k → 拒绝→护栏→full-pass；FAIL = 序贯兼容上界<MES（终期，β_r） | 同左 + 清算失败率护栏 | 同左 + MDD/CVaR 护栏 | 同左（无护栏） |
| Failure state | 配对数未达 n_target→INCONCLUSIVE；MATCH_BALANCE_FAILED→该 look 取消；Gate0 未过→locked | 池空占比超限→INCONCLUSIVE | 日历块不足→INCONCLUSIVE | 池 ≥4 事件 < n_Z3→INCONCLUSIVE；Gate3 未解锁→locked（不拖延上游） |
（H-Z1：非推断节点，§7.4 决策函数；不占 α；判词身份 = 项目资源决策。）

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
资格线：带 trade_date 每日历史成分；覆盖 ≥3 年、缺失日率 ≤2%；ID 年度稳定率 ≥95%。评分：覆盖年数 → [8,100] 带内占比 → KPL>DC>THS。第二源原生复现；THS 交叉校验。`vendor_reconstructed_history` / `self_collected`；终审只认后者。

### 2.2 题材宇宙与聚类
合格题材成分 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`（目检+哈希）。聚类：每日 Members_{D−1} 全对 Jaccard；J>0.5 按 (J 降序, ID 对字典序) 依次 clique 校验；canonical_id merge 继承 first_seen 最早（并列 ID 小）、split 由最大 Jaccard 子簇继承；lineage append-only；Episode 锁定点火身份；左截断 120 日；谱系 J>0.7。

### 2.3 快照库、双成员集、时钟 PIT
每日收盘后快照全部源（append-only+时间戳）；点火检测集 Members_{D−1}；基集 Members_{D0−1}；MembershipExpansion 日记；22:00 截止；文本类回测 D+2。

### 2.4 行情、canonical 单位、合格宇宙、市场状态与总回报账本
canonical 单位：price=元/股、volume=股、amount=元、turnover=小数、mcap=元（摄入层一次换算：Tushare vol 手×100、amount 千元×1000；VWAP=amount/volume）。合格宇宙 = 上市 ≥60 日 ∧ 非 ST/停牌/退市整理；封板 close_raw≥up_limit、触板 high_raw≥up_limit（pre-2019 回退 pct_chg≥+9.8%∧close==high）；20 日特征 ≥15 有效日；股性 250 日（60-249 扩展窗）；质量闸门失败 flag 阻断。STATE_D = UP iff HS300≥MA200；年度状态仅生成器资格。科学收益事实源 = 不可变 raw close + PIT 公司行动 total-return ledger（outcome ledger 哈希链）。

### 2.5 本体漂移治理与审计
硬漂移即停（schema 破坏/ID 重置/发布越 22:00）。统计漂移：五指标 EWMA（λ=0.2）+ UP/DOWN 分状态 Phase-I 固定基线（某状态 Stage-B <30 日 → 推迟至影子首 30 个该状态日，标 baseline_deferred）+ 连续两月；正式要求 P(稳定 5 年误 reset)≤10% 联合校准（ARL 派生）；近零分母双阈值。125 日审计：120 日 warm-up + 250 日滚动窗重放 ×200；触发 t-UCB(95%)≤3.0；FalseCapitalDays boot-UCB(95%)≤60；一次挂旗、连续两次暂停；UP/DOWN 分报；误暂停 OC 校准（5 年 ≤10%）。

## 3. 日度零模型（minP；宇宙/家族分离——C3 已闭确认）
MarginalUniverse_D = 当日全部 native 合格题材（(B+1)×C_M 矩阵、p_marg 与 CoordinationState 全体可得）；FWERFamily_D = D−1 判定 DORMANT 的子集（m_b 仅家族内取最小；p_FWER 仅家族定义；Ignition 仅家族内裁决）。分层（板块×市值3×波动3×动量3×股性3；层 ≥8；粗化序动量→波动→股性→市值）；置换（层内 Fisher-Yates；子流 SHA-256(trade_date‖src‖spec‖b)；B=2000 临界带全族升 20000，前 2000 行不可变）；p[b,c] 全行含自身取秩；点火 LU≥2 ∧ p_FWER≤α_day；行业条件三态标签。

## 4. Episode 状态机（公式集）
```
CrowdPctl = rank_pct(Share20 于自身历史)；Share20 = 20 日均(题材成交额占全市场合格股比)
  ≥120 自史 / 60-119 扩展窗 / <60 横截面（三级分层报告）
MaxBoard = 成员最大连续封板天数；BombRate(窗) = 触板未封数/触板数（触板 ≥3 定义）
成员分类（剔最高连板链本股）: ClosedLimit=close≥up_limit；TouchedOnly=high≥up_limit∧close<；
  StrongResidual=未触板∧日收益≥+5%
p_base_marg = 冻结基集成员在当日全市场置换矩阵下封板计数的边际尾概率
  （成员按当日 PIT 特征入当日分层；不可交易不进分子；可交易基集<8 → 不可检验）
DORMANT: 20 日 CoordinationState≥2 天数 ≤1 ∧ CrowdPctl<0.80
IGNITION: 次日起 LU≥2∧p_FWER≤α_day；同簇取 p_marg 小；EpisodeID 锁定；基集 Members_{D0−1}
CONFIRM(D0+4): 新增 ClosedLimit≥1 ∧ Distinct(CL∪SR)≥2 ∧ [扩散 p_base_marg≤0.10+新增封板
  或 晋级 MaxBoard 抬升∧链起点≥D0−1] ∧ BombRate(Age1..4)≤0.5
时间轴: 入场 D0+5、信号 D0+14、执行 D0+15；SignalEnd 成 14/败 4；冷却 20 日；CAR(1..60) 观察
DetectionLag = D0−最近正向激活段起点；成熟度三分类（+10%/+25%、0.7/0.9）；EpisodeType；
E1（全部 Ignition vs 对照, D0+1 起双窗）；E2（landmark D0+4 分类、D0+5 起测）；
E3（口径 1 纯延迟；口径 2 共同终点财富机会成本）
```

## 5. 条件本体零模型（C4 已闭确认）
候选边 candidate_edge(i←j) = 同 donor 层 ∧ **无共同合格题材标签（块起点，[8,100] 带内未排除题材）** ∧ i≠j ∧ 投影可行（预计算，distance>5% 删边）；self-edge 独立例外。donor 层（板块×市值3×股性3×行业×块起点波动3×动量3；层 ≥8；粗化序①动量②波动③股性④市值；全粗化仍<8 → 该层全体 self-edge 计入 unswapped）。三阶段完美指派（①指派空间 min self-edge ②固定 S* min ΣFeatureDistance[五维 donor 层当块标准化、样本 SD、零方差删维√d、等权、缺失退出、int64×10⁶] ③ID 迭代固定）。路径向量 {O/H/L/C/VWAP 相对 PrevClose, Volume/ADVVol, 停牌旗标}，Amount 派生；投影七步序；块 20 日（敏感 10/40、随机起点、circular）；bijection；unswapped ≤20% ∧ 高题材度 ≤1.5×。验证套件 13 指标（KS/相对误差表沿 v12）；GENERATOR_FAIL → live 路线须在 Stage-B 数据上重过全套件，否则年度零模型不可用。α_day：网格 {0.2,0.4,0.6,0.8,1.2}%（K=5）、合成年 ≥400 对半、验证半 simultaneous UCB（1−0.05/(2K)）取最大 α、禁插值、无解上报。双预算：触发 t-UCB≤2（半宽 ≤0.3）；FalseCapitalDays boot-UCB≤40（相对 ≤15%）；资本政策对象 = Policy C 账本；漏斗全表。

## 6. 载体 ZJ 与第二法庭
容量 ADV20@D0≥3.33e8 ∧ 市值 ≥5e9；纯度 D0−1 在籍 ≥20 日；参与 [Π(1+r_i)−Π(1+r_基)]>0 ∧ mean 换手(D0..D0+4)≥1.2×mean(D0−20..D0−1)；护栏 D0+4 非涨停 ∧ 封板 ≤1 ∧ 累涨<40%；可买 GapLimitRatio=(Open_{D0+5}/Close_{D0+4}−1)/UpLimitPct≤0.70；EventAmountShock=mean(Amount,D0..D0+4)/mean(D0−20..D0−1) 前 2、替补至 4、半仓。H-Z3：Top2Mean−RestOfPoolMean（D0+5 VWAP→D0+14 收盘，成本买 12.5bp/卖 17.5bp）；池 ≥4；两向推断；n_Z3 独立。H-Z2b：estimand=Mean(R_e(T)−R_e(A)) 配对差；B_e=AUM/6=3333.33 万（AUM=2e8）；买 D0+5..D0+7；清算 D0+15..D0+20；haircut=max(2%,10%×残余市值/ADV20@D0+20) 上限 20%；失败率护栏 ≤20%。描述性：池平均口径、C0、N（RS20 截止 D0+4）。

## 7. 四级法庭
**7.1**：匹配（分阶段最优①max 匹配②min 距离③ID 固定；4 协变量 @[D0−20,D0−1] pre-assignment 风险集标准化；卡尺 1.0；Jaccard<0.2；重叠 ≤20%；同日无放回跨日复用；unmatched→registry）；SMD 十变量 ≤0.10 一次判定、序贯 look 失败永久取消；fallback tree（卡尺 1.5 一次→MATCH_INFEASIBLE；ZJ 池<30%→Z3 预判 INCONCLUSIVE；频率 ∉[10,150]→停止；SMD 失败→上报）；科学口径（total-return ledger、零删除、退市三级、起始等权买入持有、ITT 主/PP 副、判词全条件复述）。
**7.2**：InstrumentSet（D0 冻结）= 基集∩ADV20≥1e8∩非 ST/停牌∩上市 ≥60 日；I 全部 Ignition D0+1、C 仅 CONFIRM D0+5；订单生命周期（预算接纳日锁定 min(NAV/6,现金)、<半额拒绝；买入截止入场日+2、未成永久现金；卖出滚动无截止；槽位 =6 全占用规则[部分成交占整槽、完全退出释放、EXIT-3C 长仓占槽、被拒/空池不占]；单股 ≤NAV/12 截断余额留现金；同日净额化；买用日初现金；卖出次日可用；现金 0；ID 序优先；无抢占）；判决 = 252×mean(r_C−r_I) 序贯兼容下界>1% + 护栏。
**7.3**：Breadth/ThemeRS20/StockExcess20 公式；EXIT-3C（A>B2>B1>C；D 收盘判定 D+1 VWAP 执行；V-STOP −15%）vs 固定 10 日组合级对比（描述性；块 60）。
**7.4**：一字 = 价格==涨/跌停价；净额化 5% 参与；Decision-to-VWAP slippage；容量 1/3/5%；动态暴露基准（容量等权指数月度再平衡、同成本模型双口径）；判决量 252×mean；两因子归因；H-Z1 决策函数（晋级 = 点估计 ≥3%∧80% 下界>0∧MDD≤5pp；关线 = 点估计<0∨95% 上界<3%；INCONCLUSIVE→唯一自动延长 125 日一次[点估计 ≥2%∧80% 下界>−1%]→终判）。

## 8. 安慰剂
P3（同日风险集；精确匹配 {STATE_D, 涨停数三分位}+连续 4 维 {dormant_high_count_20, CrowdPctl, ln 成员数, 前 20 日收益}；分阶段指派；卡尺 1.0；ITT 主口径）；P4（簇独立循环位移避 Episode 窗∧活跃度匹配）；双层重采样外层 ≥2000、内层 1 轮；通过线 = 四 endpoint 各自外层 95% CI ⊂ [−0.1,+0.1]d ∧ [−3bp,+3bp]；d=Mean/SD(配对差)（原样本 SD；SD<5bp 降绝对）；Gate0-F 锁 Gate1、Gate0-Z 锁 Z3；通过率进 OC。

## 9. 分法庭主推断
**9.1** H-Z2 族/Z3：配对差 + 两向交叉重采样 bootstrap（第一维 = 处理-对照 lineage 二部图连通分量；第二维 = 20 日入场块；空交集重抽 ≤100；任一维簇<10 → INCONCLUSIVE 标记）；P1a/H-Z1/Z6：日历 spread + stationary bootstrap（块 20；Z6 块 60）+NW。**9.2** 正式 p 值 = 移位零假设 bootstrap：p=(1+#{θ̂*_b−θ̂ ≥ θ̂−MES})/(B+1)；自适应 B ≥100/α_i（阶梯 5k→20k→100k）；Clopper-Pearson 上界 ≤ 边界才拒绝；repeated p 由边界引擎产出。**9.3** FAIL 上界 = stagewise-ordering 序贯兼容构造（边界仿真在"未提前 PASS"条件路径上校准）；固定样本上界仅描述性。seed=SHA-256('inference'‖hypothesis‖spec)；40 日块敏感性；状态覆盖 n≥10∧≥15%；频率闸门 [10,150]。

## 10. 序贯法庭与 OC
各节点自身信息比例 {1/3,2/3,1}；终期分量条件（§1.2）；封存-启封；SMD 取消制。边界仿真联合产出（完整图机制 + 生命周期全项）并在混合真假配置族（全 null/全真/各单真/灰区 ×4/Gate2 半真/护栏失败）逐配置验证 P(错误经济 full-pass)≤α_r ∧ P(错误死亡)≤β_r；效应五情景；四时钟；P(3/5/8 年) 三原点。

## 11. Prospective Run-in（两段制）
Stage-E（≥60 日可延长；10 日时间块 ≥6；双层 cluster bootstrap；分指标阈值：变更率 max(0.5pp,25%)、donor 可行率 ≤3pp、匹配覆盖率 ≤5pp、null 触发率按块半宽 ≤0.5×点估计；真实信号量白名单禁入）。Stage-B（累计 ≥250 日 self-collected；live null replay ≥200 条；历史 GENERATOR_FAIL 则须重过 13 项套件；双预算方法与 §5 逐字一致；UP/DOWN 分状态 Phase-I 基线；正式影子自完成+CONFIG 确认起算）。越带 → 预登记重校准 → 全链重跑 → 重签 → 影子重新起算。

## 12. 冻结流程
```
1 快照库启动【无条件立即】→ 2 引擎+合成自检（§15 断言集）→ 3 历史条件零模型 →
4 盲化可行性审计 → 5 盲化 SSD（n_table: α 网格×假设×PASS/FAIL）→ 6 边界仿真（§10）→
7 Run-in E→B → 8 RESOLVED_CONFIG（图+引擎参数+n_table+OC+四时钟+分状态基线）联合哈希 →
9 ★ 签署 → FREEZE → 10 解锁安慰剂与 DEV/OOS-B 探索 → 11 正式影子 → §0 判决
```

## 13. 可复现性环境
SHA-256 / UTF-8 / canonical JSON / PCG64DXSM / little-endian int64 / IEEE-754 float64 / 稳定 mergesort（ID 序）/ 固定归约序 / 溢出断言。联合哈希包 = {SPEC, RESOLVED_CONFIG, 代码 commit, requirements.lock, 镜像摘要, BLAS, schema 版本, regime_id, 生成器验证报告, Phase-I 分状态基线, outcome ledger 根哈希}。

## 14. 冻结参数总表
（v12.1 §14 全表继续有效；v13 增量：§-1 宪法、§1.2 节点状态机与边界引擎口径、§1.4 十项表、§16 验收协议、§17 登记簿。）

## 15. 给验证 Agent 的交代要点
1. 唯一真相源（零回引，缺口即停）；2. 断言集：MarginalUniverse/FWERFamily 分离、候选边题材零重叠、转入 α 仅未来（构造转移序列对照边界引擎手算）、canonical 单位、订单生命周期、p 值移位中心化、n_table 查找、指派反例 S*=2、minP vs 枚举、时间轴、B 臂代数、SD 地板、ledger 不可变、**§16 八哈希表生成器**；3. 全部登记簿入库；4. 闸门 flag 阻断；影子期改规则 = 作废。

## 16. 验收协议（v13 新增，QUALIFIED 的判定程序）

### 16.1 双 Agent 一致性测试（标准一验收）
```
同一份冻结测试数据（合成 + 真实混合，含边界样例）→ Agent A / Agent B 独立实现 →
逐表哈希比较（全部 SHA-256）:
  daily_universe_hash / concept_cluster_hash / signal_hash / episode_hash /
  matching_hash / trade_ledger_hash / court_sample_hash / verdict_hash
不一致 → 定位为 {SPEC 歧义 | 代码错误 | 数值实现差异}；仅第一类要求改 SPEC（→v13.x）
```

### 16.2 统计装置压力测试（标准二验收）
在 §10 预注册真假配置族下验证：P(错误经济 full-pass) ≤ α_r ∧ P(错误科学死亡) ≤ β_r；并逐节点核对判词人群 = 样本 = estimand（§1.4 十项表为对照基准）。

### 16.3 合格判定
16.1 全部哈希一致 ∧ 16.2 全部配置通过 → **SFL SPEC = QUALIFIED / FREEZE APPROVED**。此后新问题按 §-1 准入门槛处理。

## 17. 非阻断登记簿（v13 新增，初始清单）

| 类别 | 条目 |
|---|---|
| KNOWN_LIMITATION | 事件级强 FWER 仅近似（subset-pivotality）；块际残余重叠（40 日夹逼）；本体反事实不可识别；Stage-B 预算条件于单一本体年；日线 VWAP 为无自冲击代理；matched-sample 结论限共同支持域 |
| FUTURE_ENHANCEMENT | L1 分钟数据法庭（POV/双向冲击）；席位重叠度（top_inst）增强过滤；跨 regime 预登记 meta-analysis；本体状态 bootstrap 生成器 |
| ROBUSTNESS_OPTION | studentized bootstrap 替代 percentile；重叠图社区时间聚类；per-protocol 副口径族；块长 {10,40} 敏感性 |

---

## 附录 A：五阻断项 → v13 状态
C1 图形序贯唯一算法 → §1.2 节点状态机 + 边界引擎口径（**本版关闭**）｜C2 双时钟终期 → §1.2 终期分量条件（v12.1 已闭，确认）｜C3 宇宙/家族分离 → §3（v12.1 已闭，确认）｜C4 候选边题材零重叠 → §5（v12.1 已闭，确认）｜C5 正式法庭可执行公式 → §1.4 十项表 + §4/§6/§7/§9 公式集（**本版汇总关闭**）

## 附录 B：留痕
1. 审查宪法（§-1）由外部审查方起草、项目所有者确认、本版冻结——自此审查采用终止规则而非无限深挖模式；
2. 时序说明：五阻断项针对 v12.0 提出；v12.1（依据同轮 20 红线）已实质关闭 C2/C3/C4 与 C5 大部——v13 的净新增 = C1 状态机、C5 十项表、宪法、验收协议、登记簿；
3. 历轮"更优方法"类建议已归档 §17，不再构成阻断；
4. 下一步 = §16 验收（双 Agent 哈希 + 统计压力测试），通过即 QUALIFIED / FREEZE APPROVED，随后进入实现与前瞻数据阶段。

*登记时间：2026-07-16。冻结对象：全文（含 §-1 宪法）。变更 = v13.x = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
