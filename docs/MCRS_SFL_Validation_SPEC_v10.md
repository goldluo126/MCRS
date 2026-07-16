# MCRS SFL 验证规格书 v10.0 — FINAL CANONICAL（生命周期治理与轨迹运输 Closure）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / FINAL CANONICAL`
版本：`v10.0`（完全自包含单文件，替代 v1-v9.1；本文未出现的旧条款一律失效。第十轮外部审查 20 条红线全部核实成立、零驳回，含设计方自认的 Run-in 信号依赖停止条件错误）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文 + RESOLVED_CONFIG + §13 冻结环境产生逐日完全相同的输出。`D+k` 均为交易日。

---

## 0. 终局条款、识别边界与判决语义

**三层条件识别边界（冻结）**：本实验最终科学结论的完整限定为——**在供应商本体稳定（未触发 measurement-regime reset）的时期内、风险集匹配共同支持域内、且安慰剂装置可执行的条件下**，给定供应商实际输出的题材本体，协调相变是否携带未来收益信息。供应商本体在反事实市场中的形成不可识别；本体漂移可能与强叙事相关（信息性删失），漂移期事件隔离分层报告、不得静默丢弃。

**科学死亡线**：影子数据上四判定（Immediate/Landmark × 均值/中心）全部 Economically FAIL 于 MES_sci=10bp → 死亡命题（完整措辞）："在本体稳定期、风险集共同支持域内的点火事件中，题材协调相变未能在点火后 0-4 或 5-14 交易日窗口向题材全体成员产生 ≥10bp 的平均或中心收益扩散"。

**生命周期治理（v10 新增）**：正式 measurement regime 总数 ≤3；第 2 个 INCONCLUSIVE regime 出现 → 项目管理强制关线；每 regime 判词限定"Regime R 条件下"；全部 regime 结果（含失败与 INCONCLUSIVE）必须共同披露，禁止只展示通过者；跨 regime meta-analysis 须预登记；禁止"SFL 整体已验证"表述。

**判决语义**：false-PASS 按 hypothesis graph local α（§1）；false-death β=0.025；四分法判词；四人群分层报告；DEV/OOS-B = 工程与方向性证据；终审只认 self_collected；H-Z1 = 项目资源指标（决策函数 §7.4）；RESOLVED_CONFIG 必含 §10.4 OC 表（含 **P(3/5/10 年内达成判决)**）。
签署人：________ 日期：________

## 1. 假设层级与机器可读假设图

```
Gate0-F（锁 Gate1）: P3 ∧ P4 四 endpoint 等效性（§8）
Gate0-Z（锁 H-Z3）: B 臂引擎自检
Gate1: L-a1（Landmark 均值）→ 未达 Econ-PASS 解锁 L-a2（中心）
       I-a1（Immediate 均值）→ 同规则解锁 I-a2
Gate2（四判定任一 Stat-Positive 解锁）: H-Z2b / H-P1a
Gate3（H-Z2b 或 H-P1a 任一 Econ-PASS 解锁）: H-Z3
Gate4（同 Gate3 解锁）: H-Z1（项目指标，不占 α）
```

**hypothesis graph（RESOLVED_CONFIG 内以 canonical YAML 冻结；此处为规范定义）**：每个节点显式声明零假设类型与 α；positive-null（H: θ≤0）与 economic-null（H: θ≤MES 用于 PASS；H: θ≥MES 用于 FAIL）分离：

| 节点 | 零假设 | local α | 拒绝后转移 |
|---|---|---|---|
| L_mean_pos | θ_L,mean ≤ 0 | 0.025 | 解锁 L_mean_econ 与 Gate2 |
| L_center_pos | θ_L,ctr ≤ 0 | 0.005（仅当 L_mean_econ 未 PASS） | 同上 |
| I_mean_pos | θ_I,mean ≤ 0 | 0.015 | 同上 |
| I_center_pos | θ_I,ctr ≤ 0 | 0.005（仅当 I_mean_econ 未 PASS） | 同上 |
| \*_econ_PASS | θ ≤ MES_sci | 同节点 α（CI 下界 > MES） | — |
| \*_econ_FAIL | θ ≥ MES_sci | β_death=0.025（上界 < MES） | 四节点全 FAIL → 家族死亡 |
| Z2b / P1a | θ ≤ 0 与 θ ≤ MES | 各 0.025 | 解锁 Gate3/4 |
| Z3 | θ ≤ 0 与 θ ≤ 20bp | 0.05 | — |
| Z1 | （非推断） | — | 决策函数 §7.4 |

n_target 分假设（§10）；**H-Z3 拥有独立 n_Z3**：正式终期"池 ≥3 有效事件数" < n_Z3 → H-Z3 判 INCONCLUSIVE。

## 2. 数据层

### 2.1 主源评分卡与 PIT 资格
资格线：带 trade_date 每日历史成分；连续覆盖 ≥3 年、缺失日率 ≤2%；ID 年度稳定率 ≥95%（谱系调整）。评分依序：覆盖年数 → [8,100] 带内题材占比 → 偏好序 KPL>DC>THS。第二源原生复现；THS 交叉校验。标签：`vendor_reconstructed_history=true`（工程/方向性）；`self_collected=true`（唯一终审资格）。

### 2.2 题材宇宙治理
- 合格题材：成分 ∈[8,100]；排除正则（冻结）：`融资融券|转融|标的|沪股通|深股通|MSCI|富时|标普|中证|上证|深证|创业板综|科创50|北证50|次新|破净|预增|预亏|摘帽|ST|\*ST|昨日涨停|昨日连板|昨日触板|高送转|低价股|微盘|回购|增持|减持|股权转让|壳资源|基金重仓|社保重仓|QFII|举牌`（开跑前目检+哈希）；
- 确定性聚类（每日，Members_{D−1}）：候选对 J>0.5 按 (J 降序, ID 对字典序) 依次处理，clique 全员校验（同 v9.1 §2.2 算法逐字）；canonical_id：merge 继承 first_seen 最早（并列 ID 小）、split 由最大 Jaccard 子簇继承；lineage append-only；左截断 120 日；谱系 J>0.7。

### 2.3 快照库、双成员集、时钟 PIT
每日收盘后快照全部源（append-only+抓取时间戳）；点火检测集 Members_{D−1}；基集 Members_{D0−1}；MembershipExpansion 日记（H-V1）；D 22:00 抓取截止；文本类回测 D+2 可用。

### 2.4 行情、合格宇宙与市场状态
- 合格宇宙 = 上市 ≥60 交易日 ∧ 非 ST ∧ 非停牌 ∧ 非退市整理；封板 close_raw≥up_limit、触板 high_raw≥up_limit（pre-2019 回退）；20 日特征 ≥15 有效日；股性 250 日（60-249 扩展窗）；质量闸门失败 flag 阻断；
- **日度市场状态（全文唯一定义，v10 封口）**：`STATE_D = UP if HS300 收盘_D ≥ MA200(HS300)_D else DOWN`。用于：事件状态标记、状态覆盖计数、P3 匹配、OC 分层。**年度状态**（仅生成器年资格）：HS300 年收益 ≥0 为 UP 年。

### 2.5 本体漂移治理 v2（错误率化）
- **硬漂移（即停）**：schema 破坏性变更 / ID 体系重置 / 数据发布时间越过 D 22:00 决策截止；
- **统计漂移**：监控{题材总数、平均成员数、日变更率、ID 生灭率、改名率}，基线 = 滚动 6 个月中位数；触发 = EWMA（λ=0.2）越过冻结控制限**且连续两个月**；控制限由 OC 仿真校准至稳定期平均误报间隔 ARL ≥24 个月；近零分母指标用绝对+相对双阈值（如 ID 生灭率：绝对 ≥5 个/月 ∧ 相对 ≥30%）；
- 触发处置：暂停正式影子 → `measurement_regime_id` 递增 → 重新 Run-in → 重校准 → 按 §0 生命周期治理决定继续/关线；漂移期内 Episode 隔离分层（quarantine），报告但不入正式判决；
- **每 125 交易日盲化 null 审计（算法冻结）**：在已收集成员快照上跑 live null replay 200 条合成路径 → 年化（×250/125）→ t-UCB 对照校准预算 ×1.5 容差（双预算齐查）→ 一次越界挂旗、连续两次暂停法庭；审计边界的重复观察误报率由 OC 校准（目标：稳定期 5 年内误暂停概率 ≤10%）。

## 3. 日度零模型（minP）

分层（板块×市值3×波动3×动量3×股性3；层 ≥8；粗化序动量→波动→股性→市值；板块不并）；置换（保留当日各层真实涨停数、层内 Fisher-Yates；子流 = SHA256(trade_date‖source_ver‖spec_ver‖b)；B=2000，临界带 [α/3,3α] 全族追加至 20000，前 2000 行不可变）；统计对象（(B+1)×C 矩阵、p[b,c] 全行含自身取秩、p_marg=p[0,c]、m_b=min_c、p_FWER=(1+#{m_b≤p[0,c]})/(B_random+1)）；CoordinationState=−log10 p_marg；点火 = LU≥2 ∧ p_FWER≤α_day；证据边界措辞（全局零假设日度扫描；强 FWER 仅近似）；行业条件三态标签（supported/not_supported/uninformative, p 0.10 线）——全部与 v9.1 §3 逐字一致并入本文。

## 4. Episode 状态机与分解诊断（E 系列全文展开）

### 4.1 状态与时间轴
DORMANT（20 日 CoordState≥2 ≤1 天 ∧ Crowd 三级 fallback<0.80）；IGNITION（次日起，LU≥2∧p_FWER≤α_day；同簇取 p_marg 小；EpisodeID 锁定；基集 Members_{D0−1}）；CONFIRMATION（landmark D0+4：p_base_marg[身份冻结/状态动态/当日分层/当日矩阵/可交易基集<8 不可检验]；新增 ClosedLimit≥1 ∧ Distinct(CL∪SR)≥2 ∧ [扩散 p_base_marg≤0.10+新增封板 或 晋级 MaxBoard 抬升∧链起点≥D0−1] ∧ BombRate≤0.5；剔最高连板链本股）；时间轴（入场 D0+5=持有日 1；信号 D0+14；执行 D0+15；SignalEnd 成 14/败 4；冷却 20 日自次日）；DetectionLag（最近正向激活段起点；负向另记）；成熟度三分类；EpisodeType（new_concept/reactivation）。

### 4.2 E 系列分解诊断（v10 全文展开，修复隐性引用）
```
E1（点火信息）: 全部 Ignition（含夭折）vs 其匹配对照（伪时钟），
  入场 D0+1 收盘（科学 close-to-close 口径），持有至 D0+4 与 D0+14 双窗；
  estimand = 题材级起始等权买入持有组合收益的配对差均值
E2（确认筛选价值, landmark）: D0+4 收盘将全部 Ignition 分类 confirmed/failed；
  两组统一自 D0+5 起测 Close_{D0+4}→Close_{D0+9}/Close_{D0+14}（5/10 日）；
  组间差 = 确认状态的条件预测力（描述性，附 post-ignition selection 警告）
E3（延迟成本, 双口径）: 同一批 confirmed Episode：
  口径 1 = Close_{D0}→Close_{D0+4}（等待确认期间放弃的收益）
  口径 2 = [Close_{D0}→Close_{D0+14}] − [Close_{D0+4}→Close_{D0+14}]（共同终点差）
三者均为诊断报告义务，无通过线；全部使用科学 MTM 规则（§7.1）
```

## 5. 条件本体零模型（轨迹运输 closure）

**零假设**：条件于已观察供应商成员路径，价格协调轨迹与题材身份无特异对齐。

```
路径向量（v10 补全，内部一致性硬约束）:
  { Open/PrevClose, High/PrevClose, Low/PrevClose, Close/PrevClose, VWAP/PrevClose,
    Volume/ADVVol_pre, Amount/ADVAmt_pre, 停牌旗标 }
  重建约束: Low ≤ min(Open,Close,VWAP) ∧ High ≥ max(Open,Close,VWAP)
           ∧ Amount = Volume × VWAP（容差 1e-6）∧ 价格截断于 recipient 板块涨跌停界
           （截断即重判涨停/触板状态；违反一致性的 donor 块 → 该块不可用）
运输算法（v10 修复非 bijection）: 带 self-edge 的最小费用完美指派
  节点 = 层内全部股票；边 = 合格 donor 关系（同层 ∧ 无共同合格题材标签）+ self-edge
  成本 = 量化整数: 合格边 cost = round((1 − ThemeDistance) × 10^6)，
    ThemeDistance = 1 − Jaccard(块起点合格题材标签集_i, 标签集_j)
    self-edge cost = 10^9（目标①最小化 self-edge 数②最大化题材距离的整数实现）
  求解 = 确定性 Jonker-Volgenant（扫描序 = recipient ID 字典序；成本并列由
    (recipient_ID, donor_ID) 字典序打破——整数成本下可证明唯一）
  self-edge 中选者 = unswapped（该股原路径归自己，不可再作他人 donor——保证完美置换）
  unswapped 闸门: 总体 ≤20% ∧ 题材度前 20% 股票 ≤ 总体 1.5×
    （label-degree/涨停倾向/市值条件 unswapped 率必报）
验证套件（v10 增尾部依赖）: 既有八指标（日涨停数 KS≤0.05、连板 P50/90/99 ≤10%、ADV ≤10%、
  行业相关 F/N≤0.05、总成交额 KS≤0.05 与自相关 ≤0.10、份额 KS≤0.05、Crowd KS≤0.05）
  + 尾部五指标: 行业内同日涨停数分布 KS≤0.10；行业共同触板数分布 KS≤0.10；
    行业涨停集中度（HHI）相对误差 ≤15%；行业收益上尾相关（>95 分位共现率）相对误差 ≤15%；
    行业成交冲击日共放大率相对误差 ≤15%
  牛熊年分别达标；任一失败 → GENERATOR_FAIL → 历史校准禁用、仅 live null replay
四阶段分离与状态资格线、simultaneous UCB（v10 修正: Bonferroni 1−0.05/(2K)，K 网格 × 双预算）、
  校准半职责 = 产出候选网格与 nuisance 估计；验证半 = 同时上界选最大 α；
  双预算（触发数 t-UCB 半宽 ≤0.3；FalseCapitalDays bootstrap 上界相对半宽 ≤15%）、
  FalseCapitalDays 定义 —— 沿 v9.1 §5 并按上式修正
```

## 6. 载体 ZJ 与第二法庭

容量（ADV20@D0≥3.33 亿∧市值 ≥50 亿）、纯度（D0−1 在籍 ≥20 日）、参与、护栏、GapLimitRatio≤0.70、EventAmountShock 前 2（替补至 4、半仓、空池记录）、B = D0+5 可买池等权均值（解析）、C0/N 定义、common support（H-Z3 限池 ≥3；H-Z3b 双池 ≥2）、范围声明——沿 v9.1 §6 逐字。**v10 增补**：H-Z3 独立 n_Z3（由其边界世界产出）；终期有效事件 < n_Z3 → INCONCLUSIVE。

## 7. 四级法庭

### 7.1 第一法庭
- 匹配：目标字典序（①max 匹配数 ②min 总距离 ③ID 序）；**数值编码（v10 封口）**：距离 ×10⁶ 取整 int64、dummy/不可行边惩罚 10⁹、确定性 JV 实现、扫描序 ID 字典序；协变量（成分数/前 20 日收益/成交份额/主板占比 @[D0−20,D0−1]）按 pre-assignment 风险集标准化（样本 SD、不 winsorize、零方差剔除后 √d 重归一）；卡尺总距离 ≤1.0；Jaccard<0.2；个股重叠 ≤20%；同日无放回跨日可复用；unmatched → out-of-support registry；
- **SMD 审计变量（v10 全列）**：匹配 4 项 + 流通市值、20 日波动、涨停倾向（股性）、题材年龄、20 日换手、标签泛化度（成员平均题材标签数）——共 10 项全部 |SMD|≤0.10，一次生成整体判定；序贯节点失败该次永久跳过；
- **盲化可行性 fallback tree（v10 全文展开）**：
```
unmatched > 30% → 卡尺 1.0→1.5（一次，留痕）→ 仍超 → MATCH_INFEASIBLE 上报
ZJ 池≥3 占比 < 30% → H-Z3 预判 INCONCLUSIVE（禁调阈值）
年均 Episode ∉ [10,150] → 上报停止（设计层问题，禁自行调 α）
SMD 整体失败 → MATCH_BALANCE_FAILED 上报（禁迭代删对）
以上为全部合法 fallback；逾越 = 版本升级
```
- 科学口径：前复权 close-to-close；起始等权买入持有；中心 = 定义 A（题材内中位→配对差→均值）；**退市三级层级（v10 修正乐观偏差）**：①窗口内有实际清算/换股价用实际值 ②否则最后成交价延续 ③事后结算价仅作稳健性回填不改主日志；stale 占比、退市贡献、剔除敏感性必报；成员零删除；双窗（Immediate/Landmark）；
- **H-Z2b（v10 改现金流 P&L）**：事件预算 B_e = 名义 1 单位；D0+5 起按 VWAP+5% 参与逐日买入（截止 D0+7 未成部分永久现金）；D0+15 起逐日卖出（顺延滚动）；R_e = (终现金 + 终持仓按 D0+15 收盘估值 − B_e)/B_e；含买 12.5bp/卖 17.5bp；命名"容量子集可执行筛选效应"。

### 7.2 政策比较（InstrumentSet 与归属封口）
```
InstrumentSet（I 与 C 完全相同的候选身份，D0 冻结）:
  EpisodeBaseSet ∩ ADV20@D0 ≥1亿 ∩ 非ST/非停牌@D0 ∩ 上市≥60日；事件内等权
Policy I: 买全部 Ignition，D0+1→D0+10 信号→D0+11 执行
Policy C: 仅买 CONFIRM=true，D0+5→D0+14→D0+15；夭折全程现金
共享持仓: 先到事件持有；后到事件该股份额永久留现金（先到退出后不补入）；
  退出信号归属 = 持有事件；单股 ≤CurrentNAV/12
账本: OrderBudget=min(CurrentNAV/6, 可用现金)、<半额拒绝、禁融资、同日净额化、
  买入用日初现金、卖出所得次日可用、现金收益 0、优先级 = 题材 ID 序、无抢占
判决: CI_lower[年化R(C)−R(I)] > 1%（stationary bootstrap 块 20）+ 回撤/CVaR 护栏 + 双口径
```

### 7.3 第三法庭（变量全文展开）
```
Breadth(c,D) = |{基集可交易成员: close_qfq > MA20(close_qfq)}| / |基集可交易成员|
ThemeRS20(c,D) = 基集起始等权组合 20 日收益 − HS300 同期收益
StockExcess20(i,D) = 个股 20 日前复权收益 − 基集起始等权 20 日收益
EXIT-3C: Leg A（入场后 ≤10 日 Breadth<0.30 全退）；B1（CrowdPctl>0.90 减半一次）；
  B2（Breadth ≤ 入场日起峰值−0.20 ∧ ThemeRS20<0 余退）；C（入场日起第 60 日兜底）；
  优先级 A>B2>B1>C；D 收盘判定 D+1 VWAP 执行（5% 参与顺延）；V-STOP（StockExcess20<−15%）
vs 固定 10 日主退出：同一入场流完整组合对比（描述性）；推断块长 60
```

### 7.4 第四法庭（决策函数冻结）
成交/基准/判决量沿 v9.1 §7.4（一字 = 价格==涨/跌停价；净额化 5% 参与；动态暴露基准；252×mean 日差；两因子归因附加）。**H-Z1 项目决策函数（v10 冻结）**：
```
晋级 L1: 点估计 ≥3% ∧ 80% CI 下界 >0 ∧ (MDD_策略 − MDD_基准) ≤ 5pp
关线:   点估计 <0 ∨ 95% CI 上界 <3%
其余:   INCONCLUSIVE → 默认关线（用户书面否决可改为延长观察，属项目治理非科学判决）
```

## 8. 安慰剂

- **P3（v10 修复未来筛选）**：伪处理日从**同日风险集**（DORMANT 未点火合格题材）抽取，匹配 DORMANT 历史、日度市场状态（§2.4）、Crowd 分位、题材规模、前 20 日收益、当日全市场涨停数三分位；**不得以"其后是否点火"筛选**；伪日后发生真实 Ignition → 于点火日删失（不足最短窗 5 日则记 contaminated 并剔除、比例必报）；
- P4：簇独立循环位移避开全部 Episode 窗口 ∧ 伪窗口全市场涨停数分位差 ≤1 三分位；
- 双层重采样（外层 500 簇×块 bootstrap、内层 1 轮伪化）；
- **通过线（d 公式冻结）**：d = Mean(配对差)/SD(配对差)（四 endpoint 各用自身配对差 SD）；四 endpoint 各自外层 95% CI ⊂ [−0.1,+0.1]d ∧ [−10bp,+10bp]，全部通过才开 Gate1；Gate0 通过率进 OC。

## 9. 分法庭主推断
沿 v9.1 §9（H-Z2 两向 bootstrap lineage×20 日块 B=5000；H-P1a/H-Z1 stationary 块 20；H-Z6 块 60；H-Z3 lineage 聚类；块际重叠已知局限 40 日夹逼；状态覆盖 n≥10∧≥15%；频率闸门 [10,150]）。

## 10. 序贯法庭与 OC（生命周期机制全纳入）

- 双时钟（事件钟 = 配对数；日历钟 = 全部非重叠 20 日块）；分 estimand 边界世界（均值/中心/可投资/组合，各产 n_target 与边界；**新增 n_Z3 世界**）；终期 = Gate1/2 主假设 n_target 最大；未达自身 n_target 判 INCONCLUSIVE；提前判仅 Gate1/2 Econ-PASS；封存-启封；SMD 跳过；
- **OC 仿真必含（v10 扩容）**：Gate0 通过率与阻断、SMD 跳过、封存启封、月度 drift gate（含误报）、125 日 null 审计（含误暂停）、run-in 重执行、α 重配置、regime 重启与生命周期上限、状态覆盖等待、效应五情景；
- **OC 表（RESOLVED_CONFIG 必含）**：{Null, MES, 2×MES, Sparse, State-dep} × {P(PASS), P(FAIL), P(INCONCLUSIVE), 决策时间 P50/P90, **P(3 年内判决), P(5 年内), P(10 年内)**, 分状态覆盖时长}。

## 11. Prospective Run-in v3（信号无关化）

### 11.1 终止条件（纯 nuisance 精度制，v10 修复头号错误）
```
全部满足方可结束（无任何真实信号数量条件）:
  self-collected ≥ 60 交易日
  live null replay 合成年 ≥ 200 条且 E[null confirmed triggers] 的 t-UCB 半宽 ≤ 0.3
  成员日变更率估计的 95% CI 半宽 ≤ 自身点估计的 25%
  donor 可行率与匹配覆盖率的 95% CI 半宽 ≤ 10pp（在 live null 世界中评估）
真实 Ignition/Confirmed 数量 MUST NOT 作为停止条件（信号依赖起跑线禁令）；
run-in 期真实事件仅做盲化结构统计（数量、匹配可行性——不看收益方向），
  且 run-in 期事件不进入正式 CI 的规则保持——其存在不影响 run-in 时长
市场状态覆盖 = 报告项（非停止条件）
```

### 11.2 Live Null Replay 与全链重配置
沿 v9.1 §11.2/§11.3 逐字（固定 live 成员快照、条件零模型重放、禁用观测触发数；α 变更 → 全链重跑 → 重签署 → 影子重新起算）。

## 12. 冻结流程

```
1. 快照普查+快照库启动【无条件立即】
2. 全引擎+合成自检（新增: 完美指派 bijection 断言[每条路径恰用一次]、OHLCV 一致性断言、
   P3 无未来筛选断言、run-in 停止条件无信号量断言、E1/E2/E3 公式断言）
3. 历史条件零模型（状态资格线满足时）→ provisional α/config
4. 盲化设计可行性审计（§7.1 fallback tree）→ 5. 盲化 SSD（分 estimand n_target 含 n_Z3）
6. 分 estimand 边界世界 + OC（§10 全机制）
7. Prospective Run-in（§11）→ 确认或重校准
8. RESOLVED_CONFIG（含 hypothesis graph YAML、OC 表、ExpectedYears）联合哈希 → 9. ★ 签署 → FREEZE
10. freeze 后解锁经验安慰剂与 DEV/OOS-B 探索读数 → 11. 正式影子 → §0 判决
```

## 13. 可复现性环境（冻结）
SHA-256 / UTF-8 / canonical JSON / PCG64DXSM / little-endian int64 / IEEE-754 float64 / 稳定 mergesort（并列 ID 序）/ 固定并行归约序；联合哈希包 = {SPEC 全文, RESOLVED_CONFIG.yaml（含 hypothesis graph）, 代码 commit, requirements.lock, 容器镜像摘要, BLAS 版本, 数据 schema 版本, measurement_regime_id, 生成器验证报告}。

## 14. 冻结参数总表（增量与修订索引）

| 域 | 值 |
|---|---|
| Run-in | 纯精度终止（§11.1 四条件）；真实信号量禁作停止条件 |
| 运输 | 最小费用完美指派（self-edge 10⁹、距离 ×10⁶ int64、JV 确定性、ID 序）；ThemeDistance=1−Jaccard(合格标签) |
| 路径向量 | 七元组 O/H/L/C/VWAP/Vol/Amt 无量纲 + 一致性硬约束 |
| 验证 | 8 既有 + 5 尾部指标（§5 容差表）；GENERATOR_FAIL → 仅 live null |
| 生命周期 | regime ≤3；第 2 个 INCONCLUSIVE 关线；共同披露；meta 须预登记 |
| 漂移 | 硬漂移即停；统计漂移 EWMA λ=0.2 + 连续两月 + ARL≥24 月；基线滚动 6 月；双阈值 |
| 审计 | 125 日 ×200 条 ×2 年化 t-UCB；容差 ×1.5；连续两次暂停；OC 校准误暂停 ≤10%/5 年 |
| UCB | Bonferroni 1−0.05/(2K)（网格×双预算） |
| Gate0 | d=Mean/SD(配对差)；四 endpoint 各自 |
| P3 | 风险集困难负对照（六维匹配、无未来筛选、点火删失） |
| H-Z2b | 事件预算现金流 P&L（买至 D0+7、终值 D0+15 收盘） |
| 政策 | InstrumentSet §7.2；共享持仓先到先得不补入；单股 ≤NAV/12 |
| H-Z3 | 独立 n_Z3；不足判 INCONCLUSIVE |
| H-Z1 | 决策函数 §7.4（晋级/关线/默认关线） |
| 退市 | 三级层级；stale 与贡献必报 |
| SMD | 十变量清单 §7.1 |
| 状态 | 日度 = HS300 vs MA200；年度仅生成器资格 |
| OC | 全生命周期机制 + P(3/5/10 年判决) |

## 15. 给验证 Agent 的交代要点
1. 唯一真相源 = 本文件；歧义即停；
2. 强制单测（新增）：完美指派输出为置换的断言（∑donor 使用次数 == 每条恰 1）、OHLCV 重建一致性断言、P3 抽样无未来字段访问断言、run-in 停止函数输入白名单断言（不含任何真实信号计数）、hypothesis graph 与判词一致性断言、H-Z1 决策函数三分支断言；
3. 全部登记簿（四人群/out-of-support/漏斗/unswapped 条件表/regime 日志/quarantine 分层/contaminated 伪事件）入库；
4. 闸门 flag 阻断；影子期改规则 = 作废。

---

## 附录 A：第十轮审查二十红线 → v10 落点
1 Run-in 信号无关化 → §11.1｜2 完美指派运输 → §5｜3 OHLCV 补全 → §5｜4 尾部依赖验证 → §5｜5+18 生命周期治理 → §0｜6 信息性删失+隔离分层 → §0/§2.5｜7 漂移错误率化 → §2.5｜8 审计算法 → §2.5｜9 六处展开（E 系列 §4.2、fallback §7.1、EXIT-3C 变量 §7.3、InstrumentSet §7.2、SMD 清单 §7.1、市场状态 §2.4）｜10 日度状态定义+run-in 状态降报告项 → §2.4/§11.1｜11 P3 困难负对照 → §8｜12 d 公式 → §8｜13 2K 修正 → §5｜14 H-Z2b 现金流 P&L → §7.1｜15 InstrumentSet/归属 → §7.2｜16 n_Z3 → §1/§6｜17 H-Z1 决策函数 → §7.4｜19 OC 扩容+P(判决) → §10｜20 匹配数值编码 → §7.1｜21 退市三级 → §7.1｜22 hypothesis graph → §1/§13

## 附录 B：留痕
1. **自认错误一处**：Run-in 以真实 Ignition/Confirmed 数为停止条件（信号依赖起跑线 + 条件截断）——v9.1 引入、本版废除；
2. HK→最小费用完美指派：接受求解成本上升，换取 bijection 的数学成立；
3. 行业同日共振与题材对齐的张力：完全保留前者且完全破坏后者在题材 ⊂ 行业时不可两全——以尾部验证套件为裁判（不达标即禁用历史校准），属"验证而非假设"的处置；
4. Regime 生命周期上限（≤3、第 2 个 INCONCLUSIVE 关线）：接受"可能过早关线"的代价，换取消除无限重试；
5. Run-in 60 日/200 条/精度带数值为冻结初值，最终由盲化精度仿真确认（§12 步骤 4-6 内，非事后调整）。

*登记时间：2026-07-16。冻结对象：全文。变更 = v10.x = 新试验。签署对象 = §12 步骤 8 联合哈希包。*
