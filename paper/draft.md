# 从 Expenditure Horizon 到 Junior SWE 招聘拐点：一个分层、区域化的成本—能力框架

## 摘要

本文建立一个用于分析生成式 AI 与 coding agents 如何影响初级软件工程师（Junior SWE）招聘的概念模型。核心观点是：**AI 能力提升本身并不直接决定 junior headcount；真正决定招聘拐点的是 AI 在特定任务上的风险调整后有效成本何时低于人类劳动成本，以及企业是否将由此产生的生产率红利转化为更高软件产出还是更低劳动投入。**

METR 的 Expenditure Horizon 为这一分析提供了重要原型。该指标比较相同预算投入给 AI agent 与人类后所产生的任务进展，并用两条成本—产出曲线的交点刻画 AI 的经济优势能够延伸到多大的预算尺度。本文认为，该思想可以用于构建软件劳动力市场模型，但 METR 在 NanoGPT 上得到的具体美元数值不能直接解释为等额的软件工程劳动替代。

本文进一步提出 **Senior-Attention Leverage（SAL）**：一个单位 senior supervision time 能够释放多少经过可靠验收的人类等价工程产出。随着 token price 下降，SAL、可靠性、生产环境接入、验证成本与失败风险可能比 inference price 本身更接近决定 junior hiring compression 的关键变量。

---

## 1. 从 benchmark capability 到劳动替代

AI 与软件就业之间至少存在四个不同阶段：

1. **Capability**：agent 能否完成任务；
2. **Economic viability**：风险调整后的 agent 成本是否低于人类成本；
3. **Organizational adoption**：企业能否把 agent 接入真实代码、工具、权限和生产环境；
4. **Hiring response**：企业最终选择扩大软件生产还是减少人力投入。

因此：

\[
\text{benchmark improvement}
\not\Rightarrow
\text{economic substitution}
\not\Rightarrow
\text{employment decline}.
\]

METR Time Horizon 主要约束第一阶段；Expenditure Horizon 开始触及第二阶段；就业预测则必须同时建模第三与第四阶段。

---

## 2. 任务级人类成本与 AI 成本

对于任务 \(T_i\)，定义人类完成一次合格工作的完全成本为：

\[
C_i^H=\lambda_{r,s}w_{r,s}h_i,
\]

其中 \(w_{r,s}\) 为地区 \(r\)、岗位层次 \(s\) 的单位劳动报酬，\(h_i\) 为人类完成任务所需时间，\(\lambda_{r,s}\) 为 fully-loaded employer cost multiplier。

定义 AI 完成该任务的风险调整后期望成本：

\[
C_i^A
=
\frac{c_i^{inf}+c_i^{tool}+c_i^{comp}+w_Sv_i}{p_i}+L_i.
\]

其中：

- \(c_i^{inf}\)：token / inference expenditure；
- \(c_i^{tool}\)：sandbox、API 与工具调用成本；
- \(c_i^{comp}\)：构建、测试、GPU/VM 等外部 compute；
- \(v_i\)：senior 用于 specification、review、debug 和验收的时间；
- \(w_S\)：senior 单位时间成本；
- \(p_i\)：agent trajectory 获得可接受结果的概率；
- \(L_i\)：未被及时发现的 production、安全、合规与事故风险的期望损失。

一个任务进入经济可替代集合的必要条件为：

\[
C_i^A<C_i^H,
\]

并且可靠性必须满足任务特定阈值：

\[
\rho_i\geq\bar\rho_i.
\]

这一区分意味着，“AI 能做”与“AI 值得做”不是同一个问题。

---

## 3. 为什么 METR 的美元值不能直接移植到 SWE 市场

METR 的 NanoGPT Expenditure Horizon 使用高薪 AI researcher 作为 human baseline，同时 agent 需要大量 H100 training experiments。因此至少存在三个方向不同的修正项。

### 3.1 工资修正

如果本地 junior SWE 的 hourly labor cost 明显低于 METR 的 human baseline，则其他条件相同时，人类成本—产出曲线更陡，AI 的 expenditure horizon 会下降。

\[
w_H\downarrow\quad\Rightarrow\quad H_{AI}\downarrow.
\]

因此，高工资市场通常具有更强的 AI substitution incentive。

### 3.2 Compute 修正

NanoGPT optimization 的大量成本来自训练实验；普通 backend / platform engineering 更常见的反馈循环是：

\[
\text{edit}\rightarrow\text{compile}\rightarrow\text{unit test}\rightarrow\text{CI}\rightarrow\text{logs}.
\]

这通常远比几十张 H100 便宜，因此：

\[
c^{comp}_{SWE}\ll c^{comp}_{NanoGPT}.
\]

这会让普通 coding agent 的直接计算成本比照搬 METR 曲线更有利。

### 3.3 Production-risk 修正

真实软件工程包含权限、组织知识、灰度、rollback、跨团队协调、合规与事故责任，因此往往有：

\[
v_{production}>v_{benchmark},\qquad
L_{production}>L_{benchmark}.
\]

这又会削弱 benchmark 映射到生产环境后的自动化优势。

因此：

\[
H_{SWE}\neq H_{METR}\times\text{简单比例}.
\]

---

## 4. 监督成本下界与 Senior-Attention Leverage

当 token price 持续下降：

\[
c_i^{inf}\rightarrow0,
\]

AI 的风险调整后成本并不会同步趋近于零：

\[
C_i^A
\rightarrow
\frac{c_i^{tool}+c_i^{comp}+w_Sv_i}{p_i}+L_i.
\]

由此提出一个监督成本下界：**只要任务仍需大量高薪人类 supervision，或失败损失不可忽略，低 token price 本身并不足以触发劳动替代。**

本文定义候选指标：

\[
SAL
=
\frac{\text{accepted human-equivalent engineering output}}
{\text{senior supervision hours}}.
\]

SAL 接近 1 时，AI 更像个人效率工具；SAL 达到数倍时，一个 senior 开始可以监督多个 agent execution streams；如果 SAL 能稳定跨越一个数量级，传统的 `senior + multiple junior implementers` 组织结构可能出现明显压力。

因此，我们提出：

\[
\left|\frac{\partial J^*}{\partial v}\right|
\]

可能比在当前低 token price 区间内的

\[
\left|\frac{\partial J^*}{\partial c_{token}}\right|
\]

更大。该命题需要未来真实工程数据验证。

---

## 5. 一个监督约束下的生产模型

设企业使用 senior labor \(S\)、junior labor \(J\) 与 agent execution \(A\)。可以从如下生产函数开始：

\[
Y=S^\alpha(J+\theta(M)A_{effective})^\beta,
\]

其中 \(M\) 表示模型能力。

Agent execution 受到 senior supervision capacity 限制：

\[
A_{effective}\leq\lambda(M)S.
\]

\(\lambda(M)\) 可解释为与 SAL 密切相关的 supervision leverage。企业选择 \(S,J,A\) 最大化：

\[
\Pi=P_YY-w_SS-w_JJ-c_AA-\mathcal R(A,M).
\]

真正需要推导的理论对象，是是否存在能力阈值 \(M^*\)，使得：

\[
M<M^*:
\quad \frac{\partial J^*}{\partial M}\ge0,
\]

而在某一区间后：

\[
M>M^*:
\quad \frac{\partial J^*}{\partial M}<0.
\]

这才是理论意义上可以称为 Junior Compression Point 的对象，而不是任意一个 benchmark score。

---

## 6. 为什么不存在统一的 Junior SWE 拐点

岗位薪酬与自动化压力之间存在两种方向相反的机制。

第一，工资越高：

\[
w_H\uparrow\Rightarrow C_H\uparrow,
\]

企业采用 AI 的经济诱因越强。

第二，高端工程岗位往往同时具有更高的 architecture、production judgement、domain knowledge、security、cross-team coordination 与 accountability，从而提高：

\[
v_i,\quad L_i,\quad\bar\rho_i.
\]

因此薪资与可替代性不应被假设成单调关系。

本文暂时把市场划分为：

- **T3**：外包、普通 CRUD/web、低复杂度 implementation；
- **T2**：中位数 enterprise / product SWE；
- **T1**：大型银行、交易所、大厂 backend/platform/infra、成熟 fintech；
- **T0**：HFT/quant、frontier AI 与高复杂度基础设施。

预测上，T2/T3 更可能首先在任务层面出现 automation；T1 的近期表现更可能是 graduate intake 缩小、bar 上升和工作内容向 ownership 迁移；T0/T1 虽然工资高，但复杂性与责任约束使完整替代更难。

---

## 7. 招聘流量、自然更替与人才梯队

Junior hiring 可以概念性分解为：

\[
J_{r,s,t}
=
E_{r,s,t}+R_{r,s,t}+P_{r,s,t}+N_{r,s,t}
-D^{AI}_{r,s,t}-D^{Macro}_{r,s,t}.
\]

其中：

- \(E\)：业务扩张需求；
- \(R\)：退休、离职与晋升带来的 replacement demand；
- \(P\)：为培养未来 senior 而产生的 pipeline demand；
- \(N\)：AI、cloud、security 等新技术创造的新需求；
- \(D^{AI}\)：AI productivity displacement；
- \(D^{Macro}\)：宏观经济与财务压力。

这目前只是 accounting framework，而不是完整 structural equation。

一个重要预测是：AI 对招聘的影响可能首先通过**不 backfill** 而不是 layoffs 出现。因此最早需要追踪的变量应包括：

- new-grad openings；
- 0–2 YOE hiring share；
- junior/senior hiring ratio；
- backfill rate。

大型长期机构还具有 graduate pipeline 的期权价值。若：

\[
H_{t+1}=(1-\delta)H_t+\phi J_t,
\]

那么今天少招 junior 会降低未来内部 experienced-engineer stock。因此大型银行、交易所、政府和长期经营的大型科技公司可能保持一个 graduate hiring floor，即使 junior 的即时 implementation value 已受到 AI 侵蚀。

---

## 8. 区域差异与模型接入

定义地区 \(r\) 在时间 \(t\) 的有效可用模型能力：

\[
M_{r,t}
=
\max(A^{closed}_{r,t}M_t^{closed},M_{r,t}^{open/local}).
\]

其中 \(A^{closed}_{r,t}\) 吸收 closed-frontier model 的 API access、enterprise integration、监管和合规可用性。

对于每个真实任务 \(T_i\)，存在能力阈值 \(\theta_i\)。只有：

\[
M_{r,t}\ge\theta_i
\]

后，该任务才进入潜在自动化集合。

因此地区差异可能呈现明显的 threshold / phase-transition 特征：某地区即使 frontier access 受限，只要 open/local models 跨过大量真实 SWE task 的能力门槛，就可能出现快速追平，而不是永久维持固定年份的落后。

---

## 9. 软件需求弹性

生产率提升不等于就业下降。若 AI 让单位软件成本下降后，企业产生了更多软件需求，那么：

\[
\text{labor per project}\downarrow
\]

可以与：

\[
\text{number of projects}\uparrow
\]

同时发生。

因此最终 SWE employment 取决于软件产出需求弹性 \(\eta\)。若 \(\eta>1\)，生产率提升可能被需求扩张吸收；若 \(\eta<1\)，则更容易表现为 headcount compression。

宏观经济、收入增长、利润目标与资本开支因此不是 AI 模型之外的噪声，而是决定生产率冲击如何传导到就业的关键参数。

---

## 10. 可证伪预测

本文提出以下待检验命题：

1. 当 inference 已成为总风险调整成本的小部分后，token 再下降一个数量级的就业影响，应小于 supervision time 显著下降所造成的影响。
2. 能显著降低 senior review/debug time 的 agent 改进，比单纯 benchmark score 上升更容易改变 junior labor demand。
3. AI 相关劳动力调整应首先体现在 entry-level openings、backfill rate 与 junior/senior hiring ratio，而非大规模 junior layoffs。
4. 长期经营、内部晋升价值高的组织，在控制任务自动化程度后，应保留更高 graduate intake。
5. frontier access 较弱地区可能先出现滞后，随后在 local/open models 跨过任务门槛后快速 catch up。
6. 标准化、易验证的 implementation tasks 应比 production ownership、security、architecture 和跨团队协调更早受到压缩。
7. 第一阶段组织结构更可能是 `senior + agents + fewer juniors`；若未来 supervision requirement 大幅下降，implementation-heavy mid/senior 也可能在第二阶段受到替代。

---

## 结论

METR Expenditure Horizon 最重要的启示不是某个模型“值多少钱”，而是一种分析范式：

\[
\boxed{
\text{比较一美元 AI 资本与一美元人类劳动分别能产生多少可靠经济产出}
}.
\]

Junior SWE 的危险拐点因此不能定义为某个 benchmark score，而应定义为：**AI 风险调整后的有效工程成本在足够大的任务份额上低于 junior fully-loaded labor cost，同时 AI displacement 与宏观收缩超过业务扩张、replacement、pipeline 与新技术需求。**

在当前 token 已经明显便宜的环境下，最值得持续测量的候选变量不是单纯的 \$/MTok，而是：

\[
\boxed{
SAL
=
\frac{\text{可靠、经过验收的人类等价 agent 工程产出}}
{\text{senior supervision time}}
}.
\]

当 SAL 仍接近 1 时，AI 更像工程师工具；当它稳定达到数倍时，junior team structure 开始重构；当它跨越一个数量级且 production reliability 同时足够高时，传统 junior SWE career ladder 才真正进入结构性危险区间。
