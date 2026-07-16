# MCRS SFL 验证规格书 v12.0 — FINAL CANONICAL（经济图与完美运输 Closure）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / FINAL CANONICAL`
版本：`v12.0`（完全自包含单文件、零回引；替代 v1-v11。第十二轮外部审查 18 条红线全部核实成立、零驳回，含运输第一阶段数学错误与经济声明无家族保护两处要害）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文 + RESOLVED_CONFIG + §13 环境产生逐日完全相同输出。`D+k` 均为交易日。

---

## 0. 终局条款、识别边界与生命周期治理

**三层条件识别边界**：最终科学结论限定于——供应商本体稳定期（未触发 regime reset）、风险集匹配共同支持域内、且该测量制度的安慰剂装置已被证明在预登记等效边界（±3bp）内的条件下，给定供应商实际输出的题材本体，协调相变是否携带未来收益信息。本体反事实形成不可识别；漂移可能与强叙事相关（信息性删失限制永久写入判词）；漂移期 Episode 隔离分层。

**科学死亡线（全条件复述）**："在本体稳定期、**安慰剂装置被证明在 ±3bp 等效边界内**、且具有风险集共同支持的点火事件中，题材协调相变未能在点火后 0-4 或 5-14 交易日窗口向题材全体成员产生 ≥10bp 的平均或中心收益扩散"——由四个经济节点（§1）在影子数据上全部 Economically FAIL 触发。

**生命周期双预算（v12 修订）**：正式 regime ≤3；**α 预算 0.03/0.015/0.005；β（误死亡）预算 0.015/0.0075/0.0025**（各 regime 的经济图与 FAIL 判定水平按预算缩放）；第 2 个 INCONCLUSIVE regime 关线；全部 regime 共同披露；meta 须预登记。**时钟与上限（v12 修订）**：ResearchClock（正式影子累计）≤6 年；**WallClock（自快照库启动）≤8 年硬上限**；四时钟（Research/Wall/ActiveShadow/PausedRunIn）全部进 OC 与 RESOLVED_CONFIG。

**判决语义**：四分法判词；四人群分层；DEV/OOS-B = 工程与方向性证据；终审只认 self_collected；H-Z1 = 项目资源指标（§7.4 决策函数 + 唯一自动延长）。
签署人：________ 日期：________

## 1. 经济假设图（正式主图，Bretz 动态更新）

**v12 核心修订：正式图直接检验经济零假设** H_i: θ_i ≤ MES_i（Economically PASS = 图内正式拒绝）。θ>0 的统计阳性降为描述性标签（不占 α、不触发任何 Gate）。

```
节点（MES: 科学 10bp；Z2b 50bp；P1a 年化 1%；Z3 20bp）与初始权重（×α_r）:
  L-mean^econ 0.5 | I-mean^econ 0.3 | L-ctr^econ 0.1 | I-ctr^econ 0.1
初始转移矩阵 g（行 = 被拒节点，列 = 接收节点）:
  L-mean → {Z2b 0.4, P1a 0.4, L-ctr 0.2}
  I-mean → {Z2b 0.4, P1a 0.4, I-ctr 0.2}
  L-ctr  → {Z2b 0.5, P1a 0.5} | I-ctr → {Z2b 0.5, P1a 0.5}
  Z2b → {Z3 1.0} | P1a → {Z3 1.0} | Z3 → ∅
**Bretz 动态更新算法（冻结，拒绝节点 j 后）**:
  α_i ← α_i + α_j·g_ji（∀ 存活节点 i）
  g_ik ← (g_ik + g_ij·g_jk) / (1 − g_ij·g_ji)（∀ 存活 i≠k；分母为 0 时 g_ik←0）
  节点 j 状态 → rejected（权重与出边清除）；重复直至无可拒节点
节点状态机: locked（上游 Gate 未开）/ active / rejected / retired（regime 结束）
检验顺序: 任意（图形程序对顺序不变）；实现冻结为按当前 α_i 降序、并列按节点名字典序
α 回收: 全部经由 g 矩阵传播；无隐式回收
Gate 语义（与图统一）: Gate2 内容 = Z2b/P1a 节点解锁条件 = 任一科学经济节点被拒绝；
  Gate3（Z3 解锁）= Z2b 或 P1a **经济节点被拒绝**（业务解锁与 α 转移同一事件——修复双状态机）
FAIL 侧: 各节点 economic-FAIL = 单侧 1−β_r 上界 < MES（β 按 §0 生命周期预算）
验证义务: OC 在混合真假配置族（全 null / 全真 / 各单真 / θ∈(0,MES) 灰区配置 ×4 /
  Gate2 半真）下逐配置验证 regime 内 P(任一错误经济 PASS) ≤ α_r 与 P(错误死亡) ≤ β_r
```
estimand：Immediate = Close_D0→Close_{D0+4}；Landmark = Close_{D0+4}→Close_{D0+14}（全基集科学 MTM）；Z2b = 容量子集可执行 P&L；P1a = 组合政策 spread（**年化公式 = 252×mean(r_C−r_I)**）；Z3 = Top2Mean−RestOfPoolMean。各正式假设独立 n_target；**终期 = 全部正式假设 n_target 之最大值（受 §0 时限封顶；先到时限者判 INCONCLUSIVE）**——修复 n_Z3 被截断。

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
资格线：带 trade_date 每日历史成分；覆盖 ≥3 年、缺失日率 ≤2%；ID 年度稳定率 ≥95%（谱系调整）。评分依序：覆盖年数 → [8,100] 带内占比 → 偏好序 KPL>DC>THS。第二源原生复现；THS 交叉校验。`vendor_reconstructed_history=true`（工程/方向性）；`self_collected=true`（唯一终审资格）。

### 2.2 题材宇宙与聚类
合格题材成分 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`（目检+哈希）。确定性聚类：每日以 Members_{D−1} 算全对 Jaccard；候选对 J>0.5 按 (J 降序, ID 对字典序) 依次处理（双方未入簇建簇；一方在簇需与全员 J>0.5 并入；异簇合并需全对 >0.5；否则跳过；未入簇单簇）。canonical_id：merge 继承 first_seen 最早（并列 ID 小）；split 由最大 Jaccard 子簇继承；lineage append-only；Episode 锁定点火时身份。左截断 120 日；谱系 J>0.7。

### 2.3 快照库、双成员集、时钟 PIT
每日收盘后快照全部源（append-only+时间戳）；点火检测集 Members_{D−1}；基集 Members_{D0−1}；MembershipExpansion 日记（H-V1）；22:00 抓取截止；文本类回测 D+2。

### 2.4 行情、合格宇宙、市场状态与**总回报账本**（v12 修订）
- 合格宇宙 = 上市 ≥60 日 ∧ 非 ST/停牌/退市整理；封板 close_raw≥up_limit、触板 high_raw≥up_limit（pre-2019 回退）；20 日特征 ≥15 有效日；股性 250 日（60-249 扩展窗）；质量闸门失败 flag 阻断；
- 日度状态：STATE_D = UP iff HS300≥MA200；年度状态仅生成器资格；
- **科学收益事实源（修复前复权可变性）**：保存不可变 raw close + PIT 公司行动记录（分红/送转/换股）；窗口收益 = 仅用窗口内已发生的公司行动计算的 total return；D0+4/D0+14 结果生成后写入**不可修改 outcome ledger**（append-only 哈希链）；禁止依赖任何未来可重算的前复权序列。

### 2.5 本体漂移治理
硬漂移（schema 破坏/ID 重置/发布越 22:00）即停。统计漂移：五指标 EWMA（λ=0.2）+ 固定 Phase-I 基线（Stage-B 形成，正式期不更新）+ 连续两月确认；**正式要求（v12 修订）= P(稳定 regime 5 年内误 reset) ≤10%（五指标联合 OC 校准）**，ARL 仅派生报告；近零分母双阈值（绝对 ≥5/月 ∧ 相对 ≥30%）。审计：每 125 日执行携带 120 日 warm-up 的完整 250 日滚动窗重放 ×200 条；t-UCB 对照预算 ×1.5；一次越界挂旗、连续两次暂停；UP/DOWN 分报；误暂停率 OC 校准（5 年 ≤10%）。触发处置：暂停 → regime+1 → 重 Run-in → 重校准 → §0 治理；漂移期 Episode quarantine。

## 3. 日度零模型（minP）

```
**日度假设家族（v12 冻结，修复 C 未定义）**:
  DailyFamily_D = 以 D−1 信息判定为 DORMANT 的全部 native 合格题材
  （在读取任何 D 日涨停结果之前冻结；LU≥2 不作家族筛选；ConceptCluster 仅点火后去重）
分层: 板块×市值3×波动3×动量3×股性3；层 ≥8；粗化序 动量→波动→股性→市值；板块不并
置换: 保留当日各层真实涨停数、层内 Fisher-Yates；子流 = SHA-256(trade_date‖src‖spec‖b)；
  b 间允许重复；B=2000，临界带 [α/3,3α] 全族追加至 20000（前 2000 行不可变）
(B+1)×C 矩阵（C = |DailyFamily_D|；S[b,c]=LU_{c,b}）:
  p[b,c] = #{b': S[b',c] ≥ S[b,c]}/(B+1)；p_marg = p[0,c]；m_b = min_c p[b,c]（b=1..B）
  p_FWER = (1+#{m_b ≤ p[0,c]})/(B_random+1)；CoordinationState = −log10 p_marg（全部合格题材）
点火: LU_real≥2 ∧ p_FWER≤α_day；证据边界: 全局零假设日度扫描校准，事件级强 FWER 仅近似
行业条件口径与三态标签沿 §3 惯例（p_cond 0.10 线；层<8 uninformative）
```

## 4. Episode 状态机与 E 系列

DORMANT（20 日 CoordinationState≥2 天数 ≤1 ∧ Crowd 三级 fallback<0.80[≥120 自史/60-119 扩展/\<60 横截面，分层报告]）；IGNITION（次日起，同簇同日取 p_marg 小，EpisodeID 锁定，基集 Members_{D0−1}）；CONFIRMATION（landmark D0+4：p_base_marg[基集成员按当日 PIT 特征入当日分层、复用当日矩阵；可交易基集<8 不可检验]；新增 ClosedLimit≥1 ∧ Distinct(CL∪SR)≥2 ∧ [扩散 p_base_marg≤0.10+新增封板 或 晋级 MaxBoard 抬升∧链起点≥D0−1] ∧ BombRate≤0.5；剔最高连板链本股）；时间轴（入场 D0+5=持有日 1、信号 D0+14、执行 D0+15；SignalEnd 成 14/败 4；冷却 20 日自次日；CAR(1..60) 观察窗）；DetectionLag（最近正向激活段起点；负向另记；成熟度三分类 +10%/+25%、0.7/0.9）；EpisodeType（new_concept/reactivation）。
E1（全部 Ignition vs 匹配对照，D0+1 起双窗）；E2（landmark D0+4 分类、统一 D0+5 起测 5/10 日，描述性+选择警告）；E3（口径 1 纯延迟 Close_D0→D0+4；口径 2 = 共同终点财富机会成本 r₁(1+r₂)）——均为诊断，科学 MTM 口径。

## 5. 条件本体零模型（完美运输 v4）

**零假设**：条件于已观察供应商成员路径，价格协调轨迹与题材身份无特异对齐。

```
路径向量: 运输 {O/H/L/C/VWAP 相对 PrevClose, Volume/ADVVol_pre, 停牌旗标}；Amount=Volume×VWAP 派生
**边可行性预计算（v12 修订，先于指派）**:
  对候选边 (i←j) 完整模拟 20 日重建+七步投影（①重建 ②截 O/C ③H/L 修正后截界
  ④VWAP 投影 [L,H] ⑤Amount 重算 ⑥重判涨停/触板/一字 ⑦projection_distance）；
  distance>5% → 边从图中删除（指派前）；递归依赖 → 每块起点重建可行边图
**三阶段完美指派（v12 修复阶段 1 数学错误）**:
  空间 = 完美指派（每 recipient 恰一 donor、每 donor 恰用一次；self-edge 始终可行）
  阶段 1: 在完美指派空间内 min Σ 1{donor(i)=i}（self 边成本 1、其余 0 的指派问题求解）
  阶段 2: 约束 self-edge 数 = 阶段 1 最优值 S*，min Σ FeatureDistance（int64 ×10⁶）
  阶段 3: 在最优解集内按 recipient ID 升序迭代固定可行且保持最优的最小 ID donor → 唯一解
  【禁止】先在非 self 图上求最大匹配再补 self-edge（反例: A→B 合格、B→A 不合格时
   该法给出 S*=1 而真实 S*=2）
**FeatureDistance（v12 全冻结）**: 五维 {ln 流通市值, 20 日波动, 20 日动量, 股性, ln ADV 成交额}
  标准化总体 = 该 donor 层当块起点全部股票；尺度 = 样本 SD；特征 = 块起点合成 PIT 值；
  零方差删维后 √d_valid 重归一；等权；任一特征缺失 → 该股该块退出 donor 资格
donor 层 = 板块×市值3×股性3×申万一级行业×块起点波动3×动量3；层 ≥8；粗化序①动量②波动
  ③股性④市值（行业/板块不并）；块 20 日（敏感 10/40、随机起点、circular）
self-edge 中选者 = unswapped（原路径归自己，不再作他人 donor）；闸门: 总体 ≤20% ∧
  题材度前 20% ≤ 总体 1.5×（条件表必报）
验证套件（13 指标，生成器验证年）: 日涨停数 KS≤0.05；连板 P50/90/99 ≤10%；ADV 中位/P90 ≤10%；
  行业相关 F/N≤0.05；市场日总成交额 KS≤0.05、自相关 ≤0.10；题材份额 KS≤0.05；Crowd KS≤0.05；
  行业同日涨停 KS≤0.10；共同触板 KS≤0.10；行业涨停 HHI ≤15%；上尾共现 ≤15%；冲击共放大 ≤15%；
  牛熊分别达标；失败 → GENERATOR_FAIL → 仅 live null replay
四阶段分离（开发/验证年各含 ≥1 UP ∧ ≥1 DOWN 年；否则禁历史校准）；α 选择 = 验证半
  simultaneous UCB（Bonferroni 1−0.05/(2K)）取满足双预算的最大 α；禁插值
**双预算（两处统一，修复 §5/§11 冲突）**: UCB(E[假确认触发/年]) ≤2 —— **t 上界**（半宽 ≤0.3）；
  UCB(E[FalseCapitalDays/年]) ≤40 —— **bootstrap 分位上界**（相对半宽 ≤15%）
  FalseCapitalDays = Σ MV(假仓)/(NAV/6)；漏斗全表输出
```

## 6. 载体 ZJ 与第二法庭

容量（ADV20@D0≥3.33 亿 ∧ 市值 ≥50 亿）；纯度（D0−1 在籍 ≥20 日）；参与（基集口径超额>0 ∧ 换手 ≥1.2×）；护栏（D0+4 非涨停 ∧ Episode 涨停 ≤1 ∧ 累涨<40%）；可买（D0+5 非开盘涨停/停牌 ∧ GapLimitRatio≤0.70）；排序 EventAmountShock 前 2（替补至 4、半仓、空池记录）。
**H-Z3**：Top2Mean−RestOfPoolMean（D0+5 VWAP→D0+14 收盘；池 ≥4）；MES 20bp；**主推断 = lineage × 20 日入场块两向 bootstrap（v12 修订，补日历相关维）**；n_Z3 独立且进入 §1 终期最大值；池平均政策口径、C0（容量池同排序）、N（池内 RS20 前 2）为描述性；common support 冻结；范围声明：第二/四法庭为成熟本体再激活法庭。

## 7. 四级法庭

### 7.1 第一法庭
- 匹配：分阶段最优（①max 匹配数 ②min 总距离 ③ID 迭代固定唯一化——**指派空间直接求解，无大数技巧**）；协变量（成分数/前 20 日题材收益/成交份额/主板占比 @[D0−20,D0−1]）按 pre-assignment 风险集标准化（样本 SD、不 winsorize、零方差删维 √d 重归一）；距离 int64×10⁶（溢出断言）；卡尺 ≤1.0；Jaccard<0.2；个股重叠 ≤20%；同日无放回、跨日可复用；unmatched → out-of-support registry（属性对比必报）；SMD 十变量（匹配 4 + 市值/波动/股性/题材年龄/换手/标签泛化）≤0.10 一次生成整体判定；序贯节点失败永久跳过；
- fallback tree（全部合法修复）：unmatched>30% → 卡尺 1.5（一次）→ 仍超 MATCH_INFEASIBLE；ZJ 池达标<30% → H-Z3 预判 INCONCLUSIVE；频率 ∉[10,150] → 停止上报；SMD 失败 → 上报；逾越 = 升版本；
- 科学口径：**total-return ledger（§2.4）**；成员零删除（停牌延价；退市三级：实际清算价>延最后价>结算价仅稳健性回填）；题材组合起始等权买入持有；均值 = 组合收益配对差均值；中心 = 成员中位数→配对差→均值；双窗；ITT 主/per-protocol 副；判词 = matched-sample + 共同支持域 + 本体稳定期 + 安慰剂等效条件（全条件复述）；
- **H-Z2b**：B_e=AUM/6=3333.33 万（AUM 2 亿冻结）、事件内等权；D0+5 起买入 min(剩余, 5%×日成交额)、D0+7 截止；D0+15 起卖出、**清算期限 D0+20；残余 haircut = max(2%, 10% × 剩余市值/ADV20)、上限 20%（v12 修订：与流动性挂钩）**；到期残余记 capacity_liquidation_failure + 10%/20% 压力情景并报；R_e=(终现金+终持仓值−B_e)/B_e；含买 12.5bp/卖 17.5bp。

### 7.2 政策比较
InstrumentSet（I/C 同一候选身份，D0 冻结）= 基集 ∩ ADV20@D0≥1 亿 ∩ 非 ST/停牌@D0 ∩ 上市 ≥60 日；事件内等权。Policy I：买全部 Ignition，D0+1→D0+10 信号→D0+11 执行；Policy C：仅 CONFIRM=true，D0+5→D0+14→D0+15，夭折持现金。账本：**max_active_episode_slots = 6（v12 冻结）；部分成交占整槽；持仓（含卖出顺延尾与 EXIT-3C 长仓）完全退出才释放槽；被拒事件不占槽**；OrderBudget=min(CurrentNAV/6, 可用现金)、<半额拒绝、禁融资、Gross≤NAV、单股 ≤NAV/12、同日净额化、买用日初现金、卖出所得次日可用、现金收益 0、同股先到先得不补入、优先级 = 题材 ID 序、无抢占。判决（H-P1a）：**252×mean(r_C−r_I) 的 CI 下界 > 1%**（stationary bootstrap 块 20）+ MDD 差 ≤2pp ∧ CVaR 不劣 + 资本/投入双口径。描述性：H-P1b、M-I/M-C、DiD。

### 7.3 第三法庭
Breadth = 基集可交易成员 close>MA20 占比；ThemeRS20 = 基集等权 20 日 −HS300；StockExcess20 = 个股 −基集等权。EXIT-3C（A：≤10 日 Breadth<0.30 全退 > B2：Breadth≤峰值−0.20∧RS20<0 > B1：Crowd>0.90 减半 > C：60 日兜底；D 收盘判定 D+1 VWAP 执行；V-STOP −15%）vs 固定 10 日，同一入场流完整组合对比（描述性；推断块 60）。

### 7.4 第四法庭
成交（一字 = 价格==涨/跌停价；净额化 5% 参与；Decision-to-VWAP slippage；容量 1/3/5%）；对照 = 动态暴露基准（Exposure 日初 × 容量等权指数月度再平衡 + 现金 0）；判决量 = 252×mean(日 spread)；判词 = "超过动态投入比例匹配的容量指数"；两因子归因附加。H-Z1 决策函数：晋级 = 点估计 ≥3% ∧ 80% 下界>0 ∧ MDD 差 ≤5pp；关线 = 点估计<0 ∨ 95% 上界<3%；INCONCLUSIVE → 唯一自动延长（点估计 ≥2% ∧ 80% 下界>−1% → 125 日一次）→ 终判；无人工否决。

## 8. 安慰剂

- **P3（算法全冻结）**：伪处理日从同日风险集抽取；**精确匹配 {STATE_D, 当日全市场涨停数三分位}** + **连续距离 {dormant_high_count_20（过去 20 日 CoordinationState≥2 天数）, CrowdPctl, ln(成员数), 前 20 日题材收益}**（当日风险集标准化、分阶段指派、卡尺 1.0、同日无放回）；**主口径 ITT**（伪日后真点火不删失）；per-protocol 副口径；
- P4：簇独立循环位移避开全部 Episode 窗 ∧ 涨停数分位差 ≤1 三分位；
- 双层重采样（外层 500 簇×块、内层 1 轮伪化）；
- **通过线（v12 收紧）**：四 endpoint 各自外层 95% CI ⊂ [−0.1,+0.1]d ∧ **[−3bp,+3bp]**（等效边界 ≪ MES_sci=10bp——修复"管道偏差可解释全部科学目标"）；d=Mean/SD(配对差)（原样本固定 SD；SD<5bp → 该 endpoint 仅用绝对等效）；全过才开 Gate1；Gate0 通过率进 OC。

## 9. 分法庭主推断

H-Z2 族与 **H-Z3**：matched-sample / 事件配对差 + lineage × 20 日入场块两向交叉重采样 bootstrap（外层抽 m 簇 + k 块有放回、保留交集配对含重复计数、空交集重抽 ≤100 次、B=5000、percentile CI、任一维簇 <10 → INCONCLUSIVE 标记）。H-P1a/H-Z1/H-Z6：日历 spread + stationary bootstrap（块 20；H-Z6 块 60）+ NW 稳健（带宽 max(2h, Andrews)）。seed = SHA-256('inference'‖hypothesis_id‖spec_version)；40 日块敏感性；状态覆盖 n≥10 ∧ ≥15%；频率闸门 [10,150]/年。

## 10. 序贯法庭与 OC

双时钟（事件钟 = 配对数；日历钟 = 全部非重叠 20 日块）；分 estimand 边界世界（均值/中心[对称位移 Median=10bp]/可投资/组合/Z3 排序）各产 n_target 与边界；**终期 = 全部正式假设 n_target 最大值（§0 时限封顶）**；提前判仅 Gate1/2 经济节点；封存-启封；SMD 跳过。**OC 必含（v12 扩容）**：混合真假配置族（含 θ∈(0,MES) 灰区 ×4）验证 α_r 与 β_r；Bretz 全更新路径逐一模拟；Gate0 阻断；drift 联合误 reset（5 年 ≤10%）；审计误暂停；run-in 重执行；regime 重启与双预算；状态覆盖等待；**四时钟分布（Research/Wall/ActiveShadow/PausedRunIn）**；P(3/5/10 年判决)；效应五情景。

## 11. Prospective Run-in（两段制）

```
Stage-E（≥60 交易日，工程迁移）: 校验发布时间、schema、成员日变更率、donor 可行率、
  匹配覆盖率、日度/60 日窗 null trigger rate
  **精度方法（v12 修订，废除行级 Wilson）**: (日期 20 日块 × canonical lineage) 双层
  cluster bootstrap 构造 95% CI；停止条件 = 各量 CI 半宽 ≤ max(0.5pp, 0.25×点估计)
  真实信号数量 MUST NOT 进入停止条件（输入白名单断言）
Stage-B（累计 ≥250 交易日 self-collected）: 真实 250 日本体路径上 live null replay ≥200 条 →
  确认双预算（**触发数 t-UCB；资本日 bootstrap 分位 UCB——与 §5 逐字一致**）→
  形成 drift Phase-I 固定基线 → 正式影子自 Stage-B 完成 + RESOLVED_CONFIG 确认起算
  诚实限制: 重放消除 Monte Carlo 误差、非本体抽样误差；预算条件于该本体年；年度审计续核
偏差处置: 越带 → 预登记重校准 → 全链重跑 → 重签 → 影子重新起算
```

## 12. 冻结流程

```
1. 快照普查+快照库启动【无条件立即】
2. 引擎+合成自检（新增: 阶段 1 指派空间断言[构造 A→B 合格 B→A 不合格反例，
   S* 必须=2]、边可行性预计算先于指派断言、经济图更新算法断言[构造三节点拒绝序列
   对照手算]、总回报账本不可变断言、槽位占用断言、P3 混合距离断言）
3. 历史条件零模型（状态资格线）→ provisional α/config
4. 盲化可行性审计（fallback tree）→ 5. 盲化 SSD（全部 n_target）
6. 分 estimand 边界世界 + OC（§10 全项）
7. Run-in Stage-E → Stage-B → 确认或重校准
8. RESOLVED_CONFIG（经济图 YAML 含动态更新算法、OC 表、四时钟、Phase-I 基线）联合哈希
9. ★ 签署 → FREEZE → 10. 解锁经验安慰剂与 DEV/OOS-B 探索
11. 正式影子（self_collected、append-only、双时钟、封存-启封、drift、250 日窗审计）→ §0 判决
```

## 13. 可复现性环境
SHA-256 / UTF-8 / canonical JSON / PCG64DXSM / little-endian int64 / IEEE-754 float64 / 稳定 mergesort（并列 ID 序）/ 固定归约序 / int64 溢出断言。联合哈希包 = {SPEC, RESOLVED_CONFIG（含经济图与更新算法）, 代码 commit, requirements.lock, 镜像摘要, BLAS, schema 版本, regime_id, 生成器验证报告, Phase-I 基线, outcome ledger 根哈希}。

## 14. 冻结参数总表（v12 增量索引）

| 域 | 值 |
|---|---|
| 经济图 | 正式主图检验 θ≤MES；Bretz 动态更新公式 §1；统计阳性降描述性；Gate 与转移同一状态机 |
| 生命周期 | α 0.03/0.015/0.005；**β 0.015/0.0075/0.0025**；regime ≤3；Research ≤6 年；**Wall ≤8 年（自快照库启动）** |
| 运输 | 阶段 1 于完美指派空间 min self-edge；边可行性预计算先于指派；FeatureDistance 五维全冻结 |
| 家族 | DailyFamily = D−1 判定 DORMANT 的全部 native 合格题材 |
| Gate0 | 绝对等效 ±3bp；d 0.1；SD<5bp 降绝对 |
| Run-in | Stage-E 双层 cluster bootstrap 精度；Stage-B 双预算方法与 §5 逐字一致 |
| H-Z3 | 两向推断；n_Z3 入终期最大值 |
| H-Z2b | haircut=max(2%,10%×剩余/ADV20) 上限 20%；capacity_liquidation_failure |
| 政策 | 槽位 =6 全占用规则；H-P1a=252×mean(r_C−r_I) |
| 事实源 | raw close + PIT 公司行动 total-return ledger；outcome ledger 哈希链 |
| P3 | 精确匹配 2 类别 + 连续 4 维（dormant_high_count_20 等）冻结 |
| 漂移 | 正式要求 P(5 年误 reset)≤10% 联合校准；ARL 降派生 |
| 其余 | §2-§11 正文即冻结值 |

## 15. 给验证 Agent 的交代要点
1. 唯一真相源（零回引，缺口即停）；2. §12 步骤 2 全部断言 + minP vs 暴力枚举、时间轴、B 臂代数、货币参与率、Gate0 SD 地板；3. 全部登记簿入库；4. 闸门 flag 阻断；影子期改规则 = 作废。

---

## 附录 A：第十二轮审查十八红线 → v12 落点
1 经济图为主图 → §1｜2 Bretz 动态更新 → §1｜3 生命周期 β → §0｜4 阶段 1 指派空间求解 → §5｜5 边可行性预计算 → §5｜6 FeatureDistance 冻结 → §5｜7 Stage-E 双层 bootstrap → §11｜8 双预算方法统一 → §5/§11｜9 Gate0 ±3bp → §8｜10 DailyFamily → §3｜11 Gate-图状态机统一 → §1｜12 H-Z3 两向 → §6/§9｜13 终期 = 全假设最大 → §1/§10｜14 haircut 流动性挂钩 → §7.1｜15 槽位规则 → §7.2｜16 P1a 公式 + total-return ledger → §7.2/§2.4｜17 P3 距离冻结 → §8｜18 漂移正式要求/四时钟/死亡判词全条件/OC 扩容 → §2.5/§0/§10

## 附录 B：留痕
1. **自认错误一处**：运输阶段 1 用"非 self 最大匹配"推导最小 self-edge 数——两股票反例证明该推导不成立（最大匹配与完美指派是不同优化问题）；本版在指派空间内直接求解；
2. Gate0 等效边界从 ±10bp 收至 ±3bp：功效代价真实存在（安慰剂更难通过），但 10bp 边界会让管道偏差与科学目标同量级——保护 10bp 命题必须用 ≪10bp 的偏差预算；
3. 经济图为主图后，"Statistically Positive"仍作为描述性标签保留（有诊断价值），但不再承载任何 Gate 或 α；
4. 墙上时间 8 年上限：与 Research 6 年上限并行——三次 regime 的最坏情形约 9 年被硬截断，"永不开庭的协议"风险以硬时限对冲。

*登记时间：2026-07-16。冻结对象：全文。变更 = v12.x = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
