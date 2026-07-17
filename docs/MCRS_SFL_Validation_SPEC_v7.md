# MCRS SFL 验证规格书 v7.0 — CANONICAL（自包含终版候选）

文档状态：`SPEC / PRE-REGISTERED EXPERIMENT / CANONICAL`
版本：`v7.0`（全文自包含，**零继承引用**；全文替代 v1-v6，任何旧版条款未在本文出现即失效。第五轮外部审查 18 条红线全部核实成立、零驳回；设计权选择见附录 B）
起草日期：`2026-07-16`
可编译性标准：两个独立 Agent 依据本文件 MUST 实现出逐日完全相同的信号、配对、交易与判词。

---

## 0. 终局条款与判决语义（运行前 MUST 由用户签署）

> 本实验（SFL v7）是 MCRS 日频研究线的最终实验。
> - **科学死亡线**：影子数据上 H-Z2a 两个 estimand（均值+中位数）**均** Economically FAIL 于 **MES_sci=10bp** → "题材协调相变过滤器家族死亡"；
> - **项目线**：MES_econ=50bp 及以上各法庭经济门槛——"效应存在但低于经济门槛" = 科学成立、项目关闭，两种判词 MUST 分开书写；
> - 第四法庭为**日线无自冲击 VWAP 执行代理法庭**：非 Economically PASS = 关线的强理由（非"任何执行都不可能"的证明）；PASS 的唯一出口 = 晋级 L1（分钟 POV/冲击模型法庭），MUST NOT 表述为"已验证可交易"；
> - 范围声明：第二/四法庭验证的是**成熟题材本体的协调再激活**，不是全体新叙事启动；
> - 序贯法庭 append-only；提前判决仅限 Economically PASS；OOS-A 原封退库；DEV 为 internal pilot，永不并入最终 CI。
> 签署人：________ 日期：________

## 1. 研究对象与假设层级

**研究对象（冻结措辞）**：检测既有供应商题材本体从分散交易状态进入集中涨停协调状态的**相变**（协调相变检测器）。它可能发生在价格启动之前、同时或之后（DetectionLag 诊断，§4.5）。命题：题材事件**可能包含**超出静态行业分类可解释的协调信息（不宣称"真题材必须跨行业"）。

**Gatekeeping 树（冻结）**：
```
Gate0 经验安慰剂（P1-P4）通过
 → Gate1 第一法庭: H-Z2a1(均值, α=0.04) → 未过则 H-Z2a2(中位数, α=0.01)
    [家族死亡 = 两 estimand 均 Econ-FAIL@10bp（影子）]
 → Gate2（H-Z2a 至少 Statistically Positive 后解锁）: H-Z2b / H-Z2c / H-P1a
 → Gate3: H-Z3 / H-Z3b / H-Z4 / H-Z6 / H-P1b
 → Gate4: H-Z1（第四法庭）
下层法庭失败不上溯；跨法庭多重性由层级门控吸收，法庭内 alpha 分配如上。
```

| ID | 假设 | 判决量 | MES |
|---|---|---|---|
| H-Z2a1/a2 | 科学协调效应（均值/成员中位数） | 配对差值 | 10bp/10日（科学线） |
| H-Z2b | 可投资扩散效应 | 容量子集配对差值 | 50bp |
| H-Z2c | 超行业协调（宣称门） | industry_residual_supported 子集 | 50bp（描述性门） |
| H-P1a | 纯确认政策价值（固定篮子） | 组合级 C−I spread | 年化 1% |
| H-P1b | 系统政策价值（动态 ZJ） | 同上 | 年化 1% |
| H-Z3/Z3b/Z4 | ZJ 排序/约束栈/vs RS | 同池对比 | 20bp |
| H-Z6 | EXIT-3C 增值 | vs 固定退出 | 净期望>0 ∧ CVaR 不劣 |
| H-Z1 | 端到端（VWAP 代理口径） | vs 唯一主基准 | 年化净 alpha 3% |
| H-T1/T2/T3, H-Z5, H-Z7, H-V1 | 点火/确认筛选/延迟、相位、新旧分层、供应商诊断 | 诊断报告义务 | — |

## 2. 数据层

### 2.1 题材数据主源
- 原生全链路原则：主实验在单一供应商原生体系内端到端运行；MUST NOT 跨供应商映射作主真相源；
- 主源选定（普查 `CONCEPT_DATA_CENSUS.md` 后按判据机械触发）：① 带日期历史快照可得性（硬门槛；预判 KPL `kpl_concept_cons` 或 DC `dc_member`，THS `ths_member` in/out 日期缺失不可作历史源）；② 时段覆盖；③ 语义匹配（叙事标注>分类学）。第二源作原生复现；THS 仅交叉校验；
- 三源一致度（谢林收敛度）作事件级诊断。

### 2.2 快照库与双成员集
- 自登记日起每交易日收盘后快照全部可得源成分，append-only + 抓取时间戳；
- **点火检测集** = Members_{D−1}（当日新增成员不得参与当日信号）；**Episode 冻结基集** = Members_{D0−1}（Episode 内一切收益/广度/退潮的主口径）；MembershipExpansion 逐日记录（H-V1 供应商诊断：新增成员 vs 基集成员收益差、动态 vs 冻结成员信号差）。

### 2.3 时钟级 PIT
每字段记录 vendor_publish_time?/first_fetch_time/last_revision_time；**D 日 22:00 前已抓取且未依赖修订**方可用于 D+1；发布时刻不可考的字段（异动/涨停原因文本）回测按 **D+2 可用**；违反 = 装置失败。

### 2.4 题材宇宙治理
- 合格题材：成分数 ∈[8,100]；机械/风格概念排除表（名称模式冻结名单 + 开跑前人类目检）；
- **ConceptCluster**：每日以 Members_{D−1} 计算成分 Jaccard，complete-linkage（簇内任意两概念 >0.5 才归并），仅向前使用；ClusterLineage 表（cluster_id/effective_date/parent/child/merge/split/canonical_id）；Episode 创建即锁定点火时 canonical_id 与基集，至 Episode 结束不变；冷却与 Dormant 历史沿 canonical_id；
- **左截断**：主源历史起始后前 120 交易日"首次出现"标 left_censored，禁入 new_concept；谱系：消失/新现概念成分 Jaccard>0.7 = 同谱系（仅用 ≤D 数据）。

### 2.5 行情与辅助数据
个股日线/复权/涨跌停价（stk_limit 查表禁自算；pre-2019 回退：pct_chg≥+9.8% ∧ close_raw==high_raw）；触板 = high_raw≥up_limit；封板 = close_raw≥up_limit；龙虎榜 top_list/top_inst（诊断用）；两融 margin_detail（诊断用，T+1 滞后建模）；沪深300；全市场 daily。数据质量闸门（单位锚定、完整性、涨停价抽核、覆盖率）失败 → GATE_FAILED.flag，下游全部拒跑。

## 3. 状态变量与日度零模型

### 3.1 三个冻结对象（修复 DORMANT 未定义变量）

```
对每个合格题材 c、交易日 D（成员集按 §2.2）:
[分层] 全市场可交易股按: 交易板块 × 流通市值三分位 × 20日波动三分位
       × 20日动量三分位 × 股性三分位（过去250日涨停次数分位）
       层内不足 8 只时按冻结粗化树逐级合并: ①并动量 ②并波动 ③并股性 ④并市值；板块永不合并
[置换] 保留当日各层真实涨停股数，层内重排涨停标签；identity 排列计为 b=0，
       观测与置换在完全相同流程中计算（对称处理）
(1) T_raw(c,D)  = ( LU_c − μ_perm ) / σ_perm        # 学生化富集统计量
    退化处置: σ_perm < 0.5（计数单位）→ 弃学生化，改用精确置换计数尾概率;
              置换分布全退化 → 该题材当日不可检验（记 degenerate_stratum）
(2) p_FWER(c,D) = (1 + #{ M_b ≥ T_raw_obs }) / (B + 1),  M_b = max_c' T_raw(c',b)
                  # 标准 Westfall-Young maxT，族 = 当日全部处于 DORMANT 的合格题材
(3) CoordinationState(c,D) = −log10( p_emp_unadj(c,D) )   # 未校正经验尾概率，
                  全部合格题材每日计算——专用于 DORMANT 历史，不受当日族结构影响
```
- **证据边界（冻结措辞）**：本装置严格校准**全局零假设下的日度扫描错误**；部分题材真实有效且高度重叠时，事件级强 FWER 依赖额外条件，仅作近似解释——判词禁用"强 FWER 证明"表述；
- **两阶段 Monte Carlo（修复可选停止）**：全部候选先 B1=2000（含 identity）；若 p̂_FWER ∈ [α_day/3, 3α_day]（冻结区间），**无条件**升至 B2=20000 并以合并样本判决；程序级有效性由 §5 路径仿真端到端吸收（仿真运行同一两阶段流程）；seed = hash(trade_date, source_version, spec_version)；
- 5 种子稳定性规则**删除**（被两阶段 B2=20000 取代，留痕附录 B）。

### 3.2 行业条件口径
- 每个点火事件加算 ThemeShock|Industry（分层加入申万一级行业 × 市值三分位，其余维度按粗化树先行合并；行业内层不足 8 只 → 记 industry_condition_uninformative）；
- **三态标签（禁因果暗示）**：p_cond ≤0.10 → `industry_residual_supported`；>0.10 且检验有效 → `not_supported`；层稀/精度不足 → `uninformative`；
- H-Z2a 主判决用**全部事件**；"超行业协调"宣称需 H-Z2c（supported 子集）在 Gate2 通过。

## 4. Episode 状态机

### 4.1 状态定义
```
DORMANT（协调休眠——只声明涨停协调休眠，不声明价格早期）:
  过去 20 交易日内 CoordinationState ≥ 2 的天数 ≤ 1
  ∧ CrowdPctl(c,D−1) < 0.80
    [CrowdPctl = 题材成交额占全市场份额(20日平滑)在自身≥120日历史中的分位;
     历史<120日 → 该条件不适用并标 crowd_short_history]
IGNITION: DORMANT 成立次日起，LU_real ≥ 2 ∧ p_FWER ≤ α_day（α_day 由 §5 校准冻结）
  同簇同日多概念点火 → 取 T_raw 最高者为获胜概念；EpisodeID=(canonical_id, D0) 即刻锁定
CONFIRMATION（固定 landmark，D0+4 收盘统一裁决）: 见 §4.2
MATURITY/退潮: 确认失败、或 CrowdPctl>0.90、或确认后进入持仓管理; 冷却 20 交易日/canonical_id
```

### 4.2 确认（landmark，全部量在 Age1..4 累计、成员按冻结基集）
```
成员三分类（均剔除最高连板链本股）:
  ClosedLimitMember: 收盘封板 | TouchedOnlyMember: 仅盘中触板 |
  StrongResidualMember: 收盘涨幅 ≥ +5%（未封板）
CONFIRM =
  [ 新增 ClosedLimitMember（相对 D0 当日封板集）≥ 1 ]
∧ [ Distinct(ClosedLimit ∪ StrongResidual) ≥ 2 ]        # 纯 TouchedOnly 不得确认
∧ [ 扩散: Age1..4 内任一日 T_raw ≥ 1 且当日有新增封板成员
    或 晋级: MaxBoard 抬升 ∧ 连板链起点 ≥ D0−1 ]
∧ [ BombRate(Age1..4 合并触板 ≥3 时) ≤ 0.5 ]
确认成立 → 入场 D0+5；失败 → 夭折点火，全量入库（E2 与 Policy I 原料）
```
路径仿真（§5）MUST 输出：假点火数 → 假确认通过率（分扩散/晋级分支）→ 假触发数 → 确认对召回的杀伤。

### 4.3 EpisodeType 分层
new_concept（首现 ≤120 交易日内，剔 left_censored）/ reactivation；分别报告（H-Z7），禁止合并宣称。

### 4.4 检测滞后诊断（DORMANT ≠ 价格早期的诚实标注）
每 Episode 必报：PreIgnitionCAR20、D0 前 20 日最大回撤、D0 前成交额冲击、D0 价格在过去 120 日分位、DetectionLagProxy = D0 − min(首次价格冲击日, 首次成交冲击日)；三态分类 coordination_early / price_advanced_but_coordination_new / fully_mature（仅诊断，不改触发）。

### 4.5 总滞后分解报告义务
TotalLag = DetectionLag(诊断) + ConfirmationLag(D0→D0+5, E3 计量) + ExecutionLag(决策→VWAP)。

## 5. 年度错误预算：路径级零模型（修复日度⇏年度）

```
预算（冻结）: 全局零假设下 E[假 Episode 数] ≤ 2 / 年（期望口径，非 P(V≥1)）
生成器（冻结）: 在 (板块 × 市值三分位 × 股性三分位) 层内，
  以 20 交易日为块，在可比股票间置换整段 涨停/触板 轨迹
  ——保留个股连板序列、日历市场情绪与题材热度聚集
校准流程: 对 ≥200 条合成年，运行完整装置
  （DORMANT→两阶段 maxT IGNITION→landmark CONFIRMATION→冷却→簇去重）
  反推满足预算的 α_day 并冻结；输出 §4.2 漏斗全表
```
工程初值 α_day=0.8% 仅为占位，正式值以本节校准为准；预算 ≤1 与 ≤5 档进敏感性扫描。

## 6. 载体：大容量题材核心（ZJ）

- 容量（AUM 2 亿推导）：单股 = AUM/12；ADV20 ≥ (AUM/12)/5% = 3.33 亿 ∧ 流通市值 ≥ 50 亿；
- 纯度主资格：D0−1 已在籍 ≥ 20 交易日（非点火后添加）；增强证据（原因文本[D+2 可用性]、跨源一致）仅作排序分层与诊断；
- 参与：基集口径 D0→D0+4 累计超额 > 0 ∧ 换手 ≥ 自身 20 日均值 1.2 倍；
- 护栏：D0+4 收盘非涨停 ∧ Episode 内涨停 ≤1 ∧ Episode 累涨 <40%；可交易（非停牌/ST/退市整理）；
- 可买性（D0+5）：非开盘涨停/停牌 ∧ GapLimitRatio=(Open/PrevClose−1)/当日涨停幅 ≤0.70；顺位替补至第 4；仅 1 只投半仓；0 只持现金记 zj_pool_empty；
- 排序 = EventAmountShock = mean(Amount[D0..D0+4]) / mean(Amount[D0−20..D0−1])，取前 2（Z1/Z2）；
- **common support（冻结）**：H-Z3/Z4 用"完整池 ≥3 且可执行"事件集（池 ≤4 时 B 臂精确枚举全部组合）；H-Z3b 用"完整池 ≥2 ∧ C0 池 ≥2"事件集；各差值只在各自集合内计算；池不足题材属性必报；
- 范围声明：在籍 ≥20 日使新概念首月无合格 ZJ——第二/四法庭为成熟本体再激活法庭。

## 7. 四级法庭

### 7.1 第一法庭（题材层，零 ZJ 条件）

**目标试验九要素**（每实验冻结）：Eligibility/Assignment/Treatment/Control/Time-zero/Follow-up/Outcome/Estimand/Switching。Switching 主口径 = **ITT**（D0 未点火即终身对照）；副口径 per-protocol（对照自身点火日删失）。

**匹配（修复复用冲突）**：k=1、**无放回**、禁止控制复用；候选 = 同日 DORMANT 且未点火的合格题材；协变量冻结于 D0−1（窗口 [D0−20, D0−1]）：成分数、题材收益、成交份额、主板占比；标准化欧氏距离、卡尺 1.0σ；附加约束：T-A 成分 Jaccard <0.2、处理/控制组合个股重叠 ≤20%；匹配失败 → 事件退出 H-Z2（记 unmatched，>30% 警报）；**一次生成、整体判定**：审计协变量（匹配 4 项 + 市值/波动/涨停倾向/题材年龄/换手/标签泛化）任一 |SMD|>0.10 → MATCH_BALANCE_FAILED（禁止迭代删对）。

**Estimand 与组合定义**：
- H-Z2a1：基集可交易成员**等权**组合 10 日收益的配对差值（均值 estimand，α=0.04）；
- H-Z2a2：基集成员 10 日收益**中位数**的配对差值（广度 estimand，α=0.01，层级回退）；
- H-Z2b：固定容量子集（ADV20≥1 亿 ∧ D0+5 非开盘涨停；非 ZJ 条件）等权，配对差值；
- 入场统一 D0+5（对照用伪时钟继承 (D0, D0+5)），持有 10 日（主）/20 日（副），CAR(1..60) 必报；
- 判决表：a(任一 estimand)-PASS ∧ b-PASS → 晋级；a-PASS ∧ b-FAIL → 科学成立、不可承载，项目关线；a-FAIL ∧ b-PASS → "全题材扩散假设失败、可投资子集成立"——**必须**加验 Effect_investable−Effect_noninvestable 与匹配题材容量成员对照后才可定性，禁写"容量股只是独立因子"；双 FAIL@MES_sci → 家族死亡。

**分解诊断**：E1（点火 vs 休眠未点火，D0+1 起）；E2（landmark：D0+4 分类，两组统一 D0+5 起测）；E3（延迟成本双口径：R(D0+1→D0+5) 与共同终点差）。

### 7.2 政策比较（第一法庭附属，Gate2/Gate3）

```
H-P1a 纯确认价值: 资产集 = D0 冻结的可投资题材篮子（容量子集），I 与 C 买同一篮子
  Policy I: D0+1 买（含日后夭折者）| Policy C: 确认后 D0+5 买 | 夭折持现金
H-P1b 系统政策价值: C 于 D0+4 重建 ZJ（信息更新+载体重选的综合价值），与 H-P1a 分开报告
资金规则: 非预留主口径；并发 ≤6 事件；优先级 = 先到先得 → 同日按 D0 点火 p_FWER 升序
  → 同分按题材 ID 字典序；无抢占；拒绝事件记 rejected_by_capacity 不补入；空池即时释放名额
判决（H-P1a 主）: CI_lower[年化Return(C) − 年化Return(I)] > 1%（组合级 spread 直接估计）
  护栏（点估计、非推断）: MDD_C − MDD_I ≤ 2pp ∧ CVaR_C 不劣 | 诊断: 暴露调整 spread、
  DiD (C−M_C)−(I−M_I)（M-I/M-C = 匹配题材伪 D0+1 / 伪 D0+5 同规则）
```

### 7.3 第二法庭：T_ZJ / B（同池随机，小池精确枚举）/ C0（仅容量池 + 同排序）/ N（同池 RS20 前 2）/ 影子 L（不交易：机会收益、保守确定性可执行收益[一字/开盘涨停/GapLimit>0.70 不成交]、板型概率表仅描述、龙头 vs ZJ 的 CAR 相位错位 = H-Z5）。

### 7.4 第三法庭：EXIT-3C（Leg A：Age≤10 内基集广度 <0.30 全退；B1：CrowdPctl>0.90 减半一次；B2：广度 ≤峰值−0.20 ∧ 题材 RS20<0 余仓退；C：60 日兜底；优先级 A>B2>B1>C）vs 主退出固定 10 日；V-STOP 变体（个股相对题材 20 日超额 <−15%）。

### 7.5 第四法庭：日线无自冲击 VWAP 执行代理法庭
- 执行：D+1 全日 VWAP、买卖双向参与率 ≤5%、未成交持现金不追单、跌停/停牌顺延诚实建模；滑点命名 = Decision-to-VWAP slippage（禁称 IS 分解）；容量情景 1/3/5% 三档；
- **唯一主经济基准（冻结）**：全 A 容量可交易（ADV20≥1 亿、非 ST/停牌）等权组合、**月度再平衡**、与策略同一成本模型、毛/净双口径（日再平衡等权因高换手不可交易性废除）；沪深300/现金/规模匹配组合辅助；A_sys（匹配题材 + 伪时钟 + 完整管道）仅归因；
- 判决语义见 §0（非 PASS = 强关线理由；PASS = 晋级 L1）。

## 8. 安慰剂与自检

**Freeze 前（合成自检，禁触真实收益）**：注入信号检出/无效信号拒出、未来字段哨兵、置换均匀性、maxT 小样本 vs 暴力枚举逐位对照、landmark 断言、盲化脚本输出白名单审计、匹配一次性生成断言。
**Freeze 后（经验安慰剂）**：P1 池内排序置换（T−B 零分布，小池枚举）；P2 匹配对内触发置换（**诊断身份**，非正式 p 值——观察性匹配无可交换性）；P3 伪点火日从"DORMANT 且其后未点火"日抽取；P4 每 canonical 簇独立循环位移且避开全部 Episode 窗口。

## 9. 统计推断（唯一主 CI 方法）

```
主 CI: 两向 cluster bootstrap —— canonical lineage × 非重叠 10 交易日入场块
       （匹配对为最小抽样单元；无放回匹配下无复用冲突）
副 1:  stationary bootstrap（期望块长 20，日历时间序列）
副 2:  Newey-West（lag = max(2×持有期, 自动带宽)）
四分法判词: Statistically Positive（CI_l>0）/ Economically PASS（CI_l>MES）/
            Economically FAIL（CI_u<MES）/ INCONCLUSIVE
状态覆盖: 每市场状态（HS300 vs MA200）独立簇 n≥10 ∧ 占比 ≥15%（同时满足）
触发频率闸门: DEV 年均 Episode ∉ [10,150] → 停止上报
```

## 10. 序贯影子法庭

- **Append-only 铁律**：Episode、配对、簇身份、交易一经形成永不重定义；新数据只追加；
- **分析时钟 = 已锁定配对数 / n_target**（构造性单调）；中期分析于 1/3、2/3 配对数处 + 终期；
- **边界仿真生成器（冻结）**：从盲化 pilot 的配对残差按 (簇 × 10 日时间块) 重采样；处理侧注入常数 MES 位移；保留异方差、缺失、空池与匹配失败结构；每条路径运行与正式分析完全相同的固定代码；在 θ∈{0, MES, 2×MES} 三情景校准 Type I / power / 期望样本量后冻结数值边界；
- 提前判决仅限 Economically PASS；提前"FAIL"仅 non-binding futility；正式 FAIL 只在终期；
- 影子最低门槛：n_target（盲化 SSD 产出）∧ ≥250 交易日 ∧ 状态覆盖达标。

## 11. 冻结流程（顺序即依赖，禁止调换）

```
1. 快照普查 → 主源机械选定 → 快照库启动（时钟 PIT 字段齐备）
2. 全引擎实现 + 合成数据工程自检（§8 前半）
3. 路径级零模型校准 α_day（§5）→ Episode 生成规则冻结
4. 冻结前盲化样本量估计: 盲化脚本访问 DEV（internal pilot），仅输出白名单
   （pooled 方差/ICC/事件频率/n_target），代码审计断言无方向泄漏
   → DEV 永久身份 = internal pilot，不得并入 OOS-B/影子的最终 CI
5. 序贯边界仿真校准（§10）→ 全部边界冻结
6. ★ FREEZE TAG（sfl-v7-freeze）
7. 经验安慰剂 P1-P4 → DEV 探索性读数 → OOS-B 一次
8. 影子运行（append-only 序贯法庭）→ 按 §0 判决
```

## 12. 冻结参数总表（canonical，全量）

| 域 | 参数 → 值 |
|---|---|
| 宇宙 | 成分 [8,100]；排除表冻结+目检；Jaccard>0.5 complete-linkage；左截断 120 日；谱系 0.7 |
| 分层 | 板块×市值3×波动3×动量3×股性3；层最小 8；粗化序：动量→波动→股性→市值 |
| 零模型 | B1=2000 / 临界带 [α/3,3α] 无条件升 B2=20000；identity=b0；σ_min=0.5；seed=hash(date,src,ver) |
| 预算 | E[假 Episode]≤2/年；路径生成器 = 层内 20 日块轨迹置换；≥200 合成年 |
| 状态机 | DORMANT：20 日内 CoordState≥2 天数 ≤1 ∧ Crowd<0.80；点火 LU≥2 ∧ p_FWER≤α_day；确认 landmark D0+4（§4.2 组合条件）；入场 D0+5；冷却 20 日 |
| ZJ | ADV20≥3.33 亿 ∧ 市值 ≥50 亿；在籍 ≥20 日；参与超额>0 ∧ 换手 1.2×；护栏（非涨停/涨停 ≤1/累涨<40%）；GapLimit≤0.70；EventAmountShock 前 2、替补至 4、单标的半仓；H-Z3 限池 ≥3 |
| 匹配 | k=1 无放回禁复用；4 协变量@[D0−20,D0−1]；卡尺 1.0σ；Jaccard<0.2；个股重叠 ≤20%；SMD≤0.10 整体判定 |
| 政策 | 非预留；并发 6；优先级 = 先到→D0 p 值→ID；H-P1a 固定篮子 / H-P1b 动态 |
| 执行 | D+1 全日 VWAP；双向参与 ≤5%；成本买 12.5bp/卖 17.5bp（印花税 PIT）；主基准 = 容量等权月度再平衡（同成本模型双口径） |
| 退出 | 主固定 10 日（副 20 日）；EXIT-3C（10/50%/60）第三法庭；V-STOP −15% |
| 推断 | 主 CI = lineage × 10 日入场块两向 bootstrap；副 = stationary(20)/NW；MES：10bp 科学/50bp 一庭经济/20bp 二庭/1% 政策/3% 四庭；alpha：0.04+0.01 层级 |
| 序贯 | 时钟 = 配对数/n_target；中期 1/3、2/3；提前判仅 PASS；生成器 §10 冻结 |
| 覆盖 | 每状态 n≥10 ∧ ≥15%；频率闸门 [10,150]/年 |

## 13. 给验证 Agent 的交代要点

1. 本文件为唯一真相源——发现任何歧义即停止上报，禁止参考旧版本"补全"；
2. 强制单测：maxT vs 暴力枚举、CoordinationState 与 p_FWER 分离断言（DORMANT 不得触及族校正值）、landmark 断言、路径生成器保留连板序列断言、无放回匹配断言、append-only 断言（重跑历史日不得改变既有配对/Episode）、盲化白名单审计；
3. 夭折点火/空池/unmatched/拒绝事件全量入库；
4. 一切闸门失败写 flag 阻断下游；影子期间改规则 = 作废。

---

## 附录 A：第五轮审查十八红线 → v7 落点
1 自包含 → 全文｜2 三状态变量 → §3.1｜3 弱 FWER 措辞 → §3.1｜4 对称置换/σ_min/粗化树 → §3.1｜5 路径级年度校准 → §5｜6 固定两阶段 MC → §3.1｜7 删 5 种子 → 附录 B｜8 行业三态标签+主口径冻结 → §3.2/§1｜9 协调休眠+DetectionLag → §4.1/4.4｜10 确认漏斗校准+成员分类 → §4.2/§5｜11 双 MES → §0/§1｜12 均值+中位数双 estimand → §7.1｜13 H-P1a/b 拆分 → §7.2｜14 优先级/H-P1 闭合 → §7.2｜15 无放回匹配 → §7.1｜16 主 CI 唯一化+10 日块 → §9｜17 append-only+配对数时钟 → §10｜18 生成器冻结/法庭改名/月度基准/顺序依赖 → §10/§7.5/§11

## 附录 B：设计权选择留痕
1. 预算指标取 E[V]≤2/年（期望口径直观可仿真；P(V≥1) 口径作敏感性）；
2. 无放回匹配：接受 unmatched 率上升的功效代价，换推断装置闭合（复用加权估计器的 CI 覆盖验证成本更高）；
3. 删除 5 种子规则：两阶段 B2=20000 使临界带 MC 噪声降至可忽略，该规则冗余且自身改变错误率而未被校准；
4. alpha 分配 0.04/0.01（均值优先、广度回退）：均值是更强的机制主张，广度防稀疏传播误杀；
5. H-Z2a 主口径 = 全部事件（行业宣称走 H-Z2c 门）：条件口径层稀导致的功效损失不应由家族死亡判决承担。

*登记时间：2026-07-16。冻结对象：全文。变更 = v7.x = 新试验。§0 未签署、§5/§11 顺序未完成前不得 freeze。*
