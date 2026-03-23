# 大连理工大学本科外文翻译

---

**外文题目（中文）：** 多时期双重差分法

**外文题目（英文）：** Difference-in-Differences with Multiple Time Periods

**学　　院：**　（请填写）

**专　　业：**　（请填写）

**学生姓名：**　（请填写）

**学　　号：**　（请填写）

**指导教师：**　（请填写）

**完成日期：**　（请填写）

---

**原文出处：** Callaway, B., & Sant'Anna, P. H. C. (2021). Difference-in-Differences with Multiple Time Periods. *Journal of Econometrics*, 225(2), 200–230.

---

# 多时期双重差分法

**Brantly Callaway** 　佐治亚大学经济学系

**Pedro H. C. Sant'Anna** 　范德堡大学经济学系

（2020年12月1日）

---

## 摘要

在本文中，我们考虑了使用双重差分法（DiD）进行处理效应参数的识别、估计和推断程序，具体涉及以下情形：（i）多个时间段，（ii）处理时间的变异，以及（iii）"平行趋势假设"可能仅在以观测协变量为条件后才成立的情况。我们证明，即使观测特征的差异导致各组之间出现非平行的结果动态变化，在交错DiD设置中仍可识别出一族因果效应参数。我们的识别结果允许使用结果回归、逆概率加权或双重稳健估计量。我们还提出了不同的聚合方案，可用于突出不同维度的处理效应异质性，以及汇总参与处理的总体效果。我们建立了所提估计量的渐近性质，并证明了一种计算便捷的自助法程序的有效性，以进行渐近有效的同时推断（而非逐点推断）。最后，我们通过分析2001至2007年最低工资对青少年就业的影响来说明所提工具的实际相关性。已有开源软件可用于实施所提方法。

**JEL分类号：** C14, C21, C23, J23, J38

**关键词：** 双重差分法，动态处理效应，双重稳健，事件研究，处理时间变异，处理效应异质性，半参数

---

## 1　引言

双重差分法（DiD）已成为评估政策干预因果效应最常用的研究设计之一。在其经典形式中，有两个时期和两个组：在第一个时期没有人接受处理，在第二个时期一些单位接受了处理（处理组），另一些单位没有（对照组）。如果在没有处理的情况下，处理组和对照组的平均结果在时间上会遵循平行路径（即所谓的平行趋势假设），则可以通过比较处理组经历的结果平均变化与对照组经历的结果平均变化，来估计处理子总体的平均处理效应（ATT）。DiD方法的方法论扩展通常关注这种标准的两期两组设置；参见，例如，Heckman et al. (1997, 1998)、Abadie (2005)、Athey and Imbens (2006)、Qin and Zhang (2008)、Bonhomme and Sauder (2011)、de Chaisemartin and D'Haultfœuille (2017)、Botosaru and Gutierrez (2018)、Callaway et al. (2018)以及Sant'Anna and Zhao (2020)。

然而，许多DiD的实证应用偏离了经典DiD设置，拥有两个以上的时期和处理时间的变异。在本文中，我们提供了一个统一框架，用于在多时期、处理时间有变异以及平行趋势假设可能仅在以观测协变量为条件后才成立的DiD设置中估计平均处理效应。我们将注意力集中在交错采纳的DiD上，即一旦单位接受处理，它们在随后的时期中将保持处理状态的设置。

我们提议的核心在于将DiD分析分为三个独立步骤：（i）识别与政策相关的分解因果参数；（ii）将这些参数聚合形成因果效应的汇总度量；以及（iii）对这些不同目标参数的估计和推断。我们的方法允许对可解释的因果参数进行估计和推断，这些参数允许任意的处理效应异质性和动态效应，从而完全避免了将标准双向固定效应（TWFE）回归结果解释为DiD设置中因果效应的问题，正如Borusyak and Jaravel (2017)、de Chaisemartin and D'Haultfœuille (2020)、Goodman-Bacon (2019)、Sun and Abraham (2020)以及Athey and Imbens (2018)所指出的那样。此外，它增加了分析的透明性和客观性（Rubin, 2007, 2008），并允许研究者利用多种估计方法来回答不同的研究问题。

分析的识别步骤为其他步骤提供了蓝图。在本文中，我们特别关注一个分解的因果参数，我们称之为**组—时间平均处理效应**，即组 $g$ 在时间 $t$ 的平均处理效应，其中"组"由单位首次接受处理的时间段定义。在经典的两期两组DiD设置中，这些参数简化为ATT，这通常是该设置中的目标参数。组—时间平均处理效应参数的一个有吸引力的特征是，它们不直接限制关于观测协变量、单位首次接受处理的时期或处理效应随时间演变的异质性。因此，这些易于解释的因果参数可以直接用于了解处理效应异质性，和/或构建许多其他更加聚合的因果参数。我们认为这种一般性和灵活性水平是我们提议的主要优势之一。

我们提供了与处理预期行为和条件平行趋势相关的充分条件，在这些条件下，组—时间平均处理效应可以非参数点识别。我们框架的一个独特特征是它展示了研究者如何灵活地将协变量纳入具有多组和多时期的交错DiD设置中。这在观测特征差异导致不同组之间出现非平行结果动态的应用中尤为重要——在这种情况下，无条件DiD策略通常不适合恢复合理的目标因果参数（Heckman et al., 1997, 1998; Abadie, 2005）。我们提出了三种不同类型的DiD估计量用于交错处理采纳设置：一种基于结果回归（Heckman et al., 1997, 1998），一种基于逆概率加权（Abadie, 2005），一种基于双重稳健方法（Sant'Anna and Zhao, 2020）。我们提供了这些估计量在面板数据和重复截面数据情形下的版本。据我们所知，本文是第一篇展示如何在具有处理时间变异的DiD设置中允许特定协变量趋势的论文。我们的结果还强调，在实践中，研究者可以依赖不同类型的平行趋势假设，并允许某些类型的处理预期行为；我们提出的估计量明确反映了这些假设。

我们的框架认识到，在某些应用中可能存在许多组—时间平均处理效应，研究者可能希望将它们聚合为不同的因果效应汇总度量。这构成了分析的聚合步骤。我们提供了将潜在大量的组—时间平均处理效应聚合为多种直观的汇总参数的方法，并讨论了可用于突出不同来源的处理效应异质性的具体聚合方案。特别是，我们考虑了以下聚合方案：提供与两期两组情形中ATT相似的单一总体处理效应参数，以及突出以下某些维度异质性的部分聚合——（a）平均处理效应如何随处理暴露时长变化（事件研究型估计量）；（b）平均处理效应如何在处理组之间变化；以及（c）累积平均处理效应如何随日历时间演变。我们还提供了关于在分析动态处理效应时是否以"事件时间"平衡样本的成本和收益的正式讨论。总体而言，我们的设置清楚表明，一般来说，"最佳"聚合方案是因应用而异的，因为它取决于人们想要回答的问题类型。

鉴于我们的识别结果是建设性的，我们提出了易于使用的嵌入型（参数）估计量来估计感兴趣的因果参数。虽然结果回归、逆概率加权和双重稳健估计量从识别角度来看是等价的，但它们意味着实践中可以使用不同类型的DiD估计量。在此，我们注意到使用双重稳健估计量可能特别有吸引力，因为它们依赖于比结果回归和逆概率加权程序更弱的建模条件。

为了进行渐近有效的推断，我们证明了使用计算便捷的乘数型自助法程序的合理性。该方法可用于获得组—时间平均处理效应的同时置信带。与常用的逐点置信带不同，我们的同时置信带以固定的概率渐近地覆盖组—时间平均处理效应的**整个路径**，并考虑了不同组—时间平均处理效应估计量之间的依赖性。因此，我们提议的置信带在可视化整体估计不确定性方面比更传统的逐点置信区间更为合适。

我们通过分析最低工资对青少年就业的影响来说明我们提议的实际相关性。在此，我们遵循关于最低工资影响的大量实证研究，利用面板数据和各州处理时间的变异（例如，Card and Krueger, 1994; Neumark and Wascher, 2000, 2008; Dube et al., 2010等）来估计最低工资对就业的影响。有趣的是，在我们的设置中，使用我们的方法得出的结果与TWFE估计量的结果在质量上不同。这表明，至少在某些应用中，使用对处理效应异质性稳健的方法可以导致与更标准的TWFE回归有意义的差异。

**近期相关文献：** 本文与近期关于DiD中异质处理效应和/或具有处理时间变异的事件研究的新兴文献相关；参见，例如，de Chaisemartin and D'Haultfœuille (2020)、Goodman-Bacon (2019)、Imai et al. (2018)、Borusyak and Jaravel (2017)、Athey and Imbens (2018)以及Sun and Abraham (2020)。所有这些论文都提出了关于标准TWFE线性回归规范关联参数解释的一些负面结果；另见Laporte and Windmeijer (2005)、Wooldridge (2005a)、Chernozhukov et al. (2013)以及Gibbons et al. (2018)基于（单向）固定效应估计量的早期相关结果。我们提出的程序完全绕过了这些论文中突出的陷阱，因为我们清楚地将分析的识别、聚合和估计/推断步骤分开。

这些论文还提出了不受TWFE相关陷阱影响的替代DiD估计量。其中，与我们的提议最接近的可能是de Chaisemartin and D'Haultfœuille (2020)和Sun and Abraham (2020)的方法，尽管有几个主要区别值得强调。

de Chaisemartin and D'Haultfœuille (2020)关注的是恢复一个即时处理效应度量，而我们特别关注处理效应动态。事实上，我们的框架允许以统一的方式形成不同的聚合参数**族**。其次，我们特别关注处理前协变量的作用，而de Chaisemartin and D'Haultfœuille (2020)主要关注无条件DiD设计。另一方面，de Chaisemartin and D'Haultfœuille (2020)中的设置比我们的更一般，因为我们考虑的是交错采纳设计，而他们允许更一般的处理选择。尽管如此，我们注意到，即使将他们的设置特化为交错采纳设计，我们平行趋势假设的无条件版本也比他们的更弱。

Sun and Abraham (2020)提出了一个参数——队列特定平均处理效应——将我们的组—时间平均处理效应从日历时间转换为事件时间。Sun and Abraham (2020)提出了这些参数的基于回归的估计量，在无条件版本的平行趋势假设下、交错处理采纳的特定情况下，其性质与我们的估计量相似。然而，我们的方法在几个方面更为一般。首先，我们允许平行趋势假设在以协变量为条件后成立，而如何将Sun and Abraham (2020)中基于回归的估计量适用于这种情况并不清楚。其次，我们考虑了多种可能的组—时间平均处理效应聚合方式，而Sun and Abraham (2020)特别关注事件研究类型的聚合。第三，我们使用了明确考虑潜在多重检验问题的同时推断程序；Sun and Abraham (2020)关注的是逐点推断。另一方面，我们没有任何关于使用带有处理指标前导和滞后的TWFE规范进行因果推断陷阱的结果；这些是Sun and Abraham (2020)独有的。

我们还注意到，Athey and Imbens (2018)考虑了与我们类似的交错处理采纳设置。然而，Athey and Imbens (2018)的出发点是处理采纳日期完全随机化的假设，这比我们的平行趋势假设更强。我们还注意到，Athey and Imbens (2018)忽略了协变量在DiD分析中的重要作用，也没有像我们那样考虑总结处理效应异质性的聚合方案。另一方面，我们强调他们论文的主要焦点是为具有随机处理日期的交错DiD设置提供基于设计的推断程序。他们基于设计的推断程序是我们基于抽样的推断程序的补充。

**本文的组织结构：** 本文余下部分的组织如下。第2节介绍我们的主要识别结果。我们在第3节讨论不同的聚合方案。感兴趣的处理效应的估计和推断程序在第4节中给出。第5节重新审视最低工资对就业的影响。第6节为结论。证明以及额外的方法论结果在附录中报告。在补充附录中，我们给出了仅有重复截面数据时结果的证明，提供了实证应用的额外细节，并呈现了一个小规模的蒙特卡洛模拟来说明我们所提估计量的有限样本性质。

---

## 2　识别

### 2.1　设置

我们首先介绍本文中使用的记号。我们考虑 $\mathcal{T}$ 个时期的情形，用 $t$ 表示某一特定时期，其中 $t = 1, \ldots, \mathcal{T}$。在经典DiD设置中，$\mathcal{T} = 2$ 且在时期 $t = 1$ 没有人接受处理。令 $D_{i,t}$ 为二元变量，当单位 $i$ 在时期 $t$ 接受处理时等于1，否则等于0。我们对处理过程作如下假设：

**假设1**（处理的不可逆性）。$D_1 = 0$ 几乎处处成立（a.s.）。对于 $t = 2, \ldots, \mathcal{T}$，$D_{t-1} = 1$ 意味着 $D_t = 1$ 几乎处处成立。

假设1声明在时期 $t = 1$ 没有人接受处理，且一旦单位接受处理，该单位将在下一时期保持处理状态。此假设在文献中也被称为交错处理采纳。我们将此假设解释为单位不会"忘记"处理经历。

定义 $G$ 为单位首次接受处理的时间段。在假设1下，对于所有最终参与处理的单位，$G$ 定义了它们所属的"组"。如果一个单位在任何时期都不参与处理，我们任意设定 $G = \infty$。我们定义 $G_g$ 为二元变量，当单位首次在时期 $g$ 接受处理时等于1（即 $G_{i,g} = \mathbf{1}\{G_i = g\}$），并定义 $C$ 为二元变量，当单位在任何时期都不参与处理时等于1（即 $C_i = \mathbf{1}\{G_i = \infty\} = 1 - D_{i,\mathcal{T}}$）。令 $\bar{g} = \max_{i=1,\ldots,n} G_i$ 为数据集中 $G$ 的最大值。接下来，将广义倾向得分定义为 $p_{g,s}(X) = P(G_g = 1 | X, G_g + (1 - D_s)(1 - G_g) = 1)$。注意 $p_{g,s}(X)$ 表示在协变量 $X$ 条件下，给定属于组 $g$ 或在时期 $s$ 未接受处理的情况下，首次在时期 $g$ 接受处理的概率。此后，我们定义 $p_g(X) = p_{g,\mathcal{T}}(X) = P(G_g = 1 | X, G_g + C = 1)$，即给定协变量且属于组 $g$ 或不参与任何时期处理的条件下，在时期 $g$ 首次接受处理的概率。令 $\mathcal{G} = \text{supp}(G) \setminus \{\bar{g}\} \subseteq \{2, 3, \ldots, \mathcal{T}\}$ 表示 $G$ 的支撑去掉 $\bar{g}$。类似地，令 $\mathcal{X} = \text{supp}(X) \subseteq \mathbb{R}^k$ 表示处理前协变量 $X$ 的支撑。

接下来，我们建立潜在结果框架。在此，我们将 Robins (1986, 1987) 的动态潜在结果框架与 Heckman et al. (2016) 讨论的多阶段处理采纳设置相结合；另见 Sianesi (2004)。令 $Y_{i,t}(0)$ 表示单位 $i$ 在时期 $t$ 的未处理潜在结果，即如果该单位在时期 $\mathcal{T}$ 之前一直未接受处理时的结果。对于 $g = 2, \ldots, \mathcal{T}$，令 $Y_{i,t}(g)$ 表示如果单位 $i$ 首次在时期 $g$ 接受处理时在时期 $t$ 将经历的潜在结果。注意，我们的潜在结果记号考虑了潜在的动态处理选择，但也适用于（预先指定的）处理方案 (Murphy et al., 2001; Murphy, 2003)。每个单位 $i$ 的观测结果与潜在结果之间的关系为

$$Y_{i,t} = Y_{i,t}(0) + \sum_{g=2}^{\mathcal{T}} (Y_{i,t}(g) - Y_{i,t}(0)) \cdot G_{i,g} \tag{2.1}$$

换言之，我们对每个单位只观察到一条潜在结果路径。对于在任何时期都未参与处理的单位，所有时期的观测结果都是未处理潜在结果。对于参与处理的单位，观测结果是对应于该单位采纳处理的特定时期的单位特定潜在结果。

我们还施加以下随机抽样假设。

**假设2**（随机抽样）。$\{Y_{i,1}, Y_{i,2}, \ldots, Y_{i,\mathcal{T}}, X_i, D_{i,1}, D_{i,2}, \ldots, D_{i,\mathcal{T}}\}_{i=1}^n$ 是独立同分布（i.i.d.）的。

假设2意味着我们有面板数据；我们的结果基本上可以立即扩展到重复截面数据的情况，这一情形在附录B中展开。这里我们注意到，假设2允许我们将所有潜在结果视为随机的。此外，它不对潜在结果与处理分配之间的关系施加限制，也不限制观测随机变量的时间序列相关性。另一方面，假设2要求每个单位 $i$ 是从一个大的目标总体中随机抽取的。关于另一种基于设计的推断方法，见 Athey and Imbens (2018)。

此后，为使记号更简洁，我们将在记号中省略单位下标 $i$。

### 2.2 组—时间平均处理效应参数

鉴于同一单位在同一时间不能观察到不同的潜在结果，研究者通常关注识别和估计某些平均因果效应。例如，在经典的两期DiD设置中，最常用的处理效应参数是处理组的平均处理效应，表示为

$$ATT = \mathbb{E}[Y_2(2) - Y_2(0) | G_2 = 1]$$

在本文中，我们考虑 $ATT$ 的一种自然推广，使其适用于多处理组和多时期的设置。更准确地说，我们使用特定组 $g$ 在特定时期 $t$ 的成员的平均处理效应，表示为

$$ATT(g,t) = \mathbb{E}[Y_t(g) - Y_t(0) | G_g = 1]$$

作为我们框架的主要构建模块。我们称此因果参数为**组—时间平均处理效应**。

注意 $ATT(g,t)$ 不对跨组或跨时间的处理效应异质性施加任何限制。因此，关注 $ATT(g,t)$ 族使我们能够以统一的方式分析平均处理效应如何在不同维度上变化。例如，通过固定组 $g$ 并变化时间 $t$，可以了解该特定组的平均处理效应如何随时间演变。通过对不同组执行此操作，我们可以更好地理解处理效应动态如何在组间变化。此外，如第3节所讨论的，可以在 $ATT(g,t)$ 的基础上构建更多聚合的因果参数，这些参数旨在回答具体问题，如：（a）到时期 $\mathcal{T}$ 为止，所有参与处理的组的平均处理效应是什么？（b）平均处理效应在组间是否存在异质性？（c）平均处理效应如何随处理暴露时长变化？（d）累积平均处理效应如何随日历时间演变？我们认为这种首先关注 $ATT(g,t)$ 族的一般性和灵活性水平是我们框架的主要优势之一。

### 2.3 识别假设

为了识别 $ATT(g,t)$ 及其泛函，我们施加以下假设。

**假设3**（有限的处理预期）。存在已知的 $\delta \geq 0$ 使得

$$\mathbb{E}[Y_t(g) | X, G_g = 1] = \mathbb{E}[Y_t(0) | X, G_g = 1] \quad \text{a.s.}$$

对所有 $g \in \mathcal{G}$，$t \in \{1, \ldots, \mathcal{T}\}$ 使得 $t < g - \delta$ 成立。

假设3限制了所有"最终受处理"组对处理的预期。当 $\delta = 0$ 时，它施加了"无预期"假设，参见，例如，Abbring and van den Berg (2003) 和 Sianesi (2004)。当处理路径不是先验已知的和/或单位不是"选择"处理状态的人时，这很可能是合适的。然而，假设3也允许预期行为，只要我们对预期范围 $\delta$ 有良好的理解。例如，如果单位提前一期预期处理，则假设3在 $\delta = 1$ 时成立；参见，例如，Laporte and Windmeijer (2005) 和 Malani and Reif (2015) 关于考虑潜在预期行为重要性的讨论。注意，在假设3下，对所有 $t < g - \delta$ 的处理前时期，$ATT(g,t) = 0$。

接下来，我们考虑两种对未处理潜在结果演变施加限制的替代假设。

**假设4**（基于"从未处理"组的条件平行趋势）。令 $\delta$ 如假设3中所定义。对每个 $g \in \mathcal{G}$ 和 $t \in \{2, \ldots, \mathcal{T}\}$ 使得 $t \geq g - \delta$，

$$\mathbb{E}[Y_t(0) - Y_{t-1}(0) | X, G_g = 1] = \mathbb{E}[Y_t(0) - Y_{t-1}(0) | X, C = 1] \quad \text{a.s.}$$

**假设5**（基于"尚未处理"组的条件平行趋势）。令 $\delta$ 如假设3中所定义。对每个 $g \in \mathcal{G}$ 和每个 $(s,t) \in \{2, \ldots, \mathcal{T}\} \times \{2, \ldots, \mathcal{T}\}$ 使得 $t \geq g - \delta$ 且 $t + \delta \leq s < \bar{g}$，

$$\mathbb{E}[Y_t(0) - Y_{t-1}(0) | X, G_g = 1] = \mathbb{E}[Y_t(0) - Y_{t-1}(0) | X, D_s = 0, G_g = 0] \quad \text{a.s.}$$

假设4和假设5是两种不同的条件平行趋势假设，它们将两期平行趋势假设推广到多时期和多处理组的情形；参见，例如，Heckman et al. (1997, 1998)、Abadie (2005) 和 Sant'Anna and Zhao (2020)。两个假设都在以协变量 $X$ 为条件后成立。这在经济学的许多应用中可能很重要，特别是在结果随时间存在特定协变量趋势且协变量分布在组间不同的情况下。例如，Heckman et al. (1997) 在评估职业培训项目的背景下论证了条件平行趋势假设。在评估职业培训项目时，年龄、就业历史和受教育年限等观测协变量的分布在参与培训的个体和不参与的个体之间通常差异很大。当劳动力市场结果的路径（在不参与职业培训的情况下）取决于这些协变量时，条件平行趋势比无条件平行趋势假设更为合理。事实上，在使用无条件DiD方法评估政策干预的因果效应时，忽略特定协变量趋势的存在可能导致重大偏差。

假设4和假设5的区别在于在给定应用中愿意使用的对照组。更具体地说，假设4声明，在以协变量为条件的情况下，首次在时期 $g$ 接受处理的组与"从未处理"组在没有处理的情况下，平均结果会遵循平行路径。假设5将条件平行趋势施加在组 $g$ 与在时期 $t + \delta$ 之前"尚未接受处理"的组之间。重要的是，这两个假设都允许特定协变量趋势，且不限制处理时间与潜在结果 $Y_t(g)$ 之间的关系。因此，它们比Athey and Imbens (2018)作出的随机化假设更弱。我们还注意到，假设4和假设5的无条件版本比de Chaisemartin and D'Haultfœuille (2020)和Sun and Abraham (2020)施加的平行趋势假设更弱，因为它们对处理前时期 $Y_t(0)$ 的演变施加了更少的限制；参见，例如，Marcus and Sant'Anna (2020)的比较。

在我们看来，当存在大量从未参与处理的单位群体，且同时这些单位与"最终受处理"的单位足够相似时，从业者可能偏好假设4而非假设5。当"从未处理"的单位群体不可用或"太小"时，研究者可能偏好假设5，因为它允许使用更多组作为有效对照单位，这可能导致更具信息量的推断程序。然而，必须强调，偏好假设5而非假设4也涉及潜在的缺点。例如，在没有处理预期（$\delta = 0$）的情况下，假设4不限制各组处理前趋势的观测，而假设5限制了；参见，例如，Marcus and Sant'Anna (2020)。不限制处理前趋势在"早期"的经济环境可能不同于"后期"的应用中特别有意义。在这些情况下，不同组的结果可能在"早期"以非平行方式演变，也许因为各组受到了不同的冲击，而趋势在"后期"变得平行。我们建议在决定哪个条件平行趋势假设更适合给定应用时考虑这些权衡。

我们施加的最后一个识别假设是重叠条件。

**假设6**（重叠）。对每个 $t \in \{2, \ldots, \mathcal{T}\}$, $g \in \mathcal{G}$, 存在某个 $\varepsilon > 0$ 使得 $P(G_g = 1) > \varepsilon$ 且 $p_{g,t}(X) < 1 - \varepsilon$ 几乎处处成立。

假设6将Heckman et al. (1997, 1998)、Abadie (2005)和Sant'Anna and Zhao (2020)中的重叠假设扩展到多组和多时期的设置。它声明总体中有正比例的人群在时期 $g$ 开始处理，且对所有 $g$ 和 $t$，广义倾向得分一致地远离1。假设6排除了"不规则识别"，参见，例如，Khan and Tamer (2010)。

**注1。** 注意假设3和假设4（假设5）是内在相关的。例如，当施加"无预期"条件（使得 $\delta = 0$）时，假设4将仅对处理后时期 $t \geq g$ 施加条件平行趋势。如果允许预期行为（使得 $\delta > 0$），假设4将对某些处理前时期也施加条件平行趋势。事实上，平行趋势假设随着 $\delta$ 增大而变强。据我们所知，这些假设之间强度的权衡此前未被注意到。

**注2。** 在某些应用中，从业者可能不愿意使用"从未处理"的单位作为对照组的一部分，因为它们与其他"最终受处理"的单位表现非常不同。在这些情况下，从业者可以将所有"从未处理"的单位从分析中删除，然后使用假设5。

### 2.4 组—时间平均处理效应的非参数识别

在本节中，我们证明组—时间平均处理效应族在上述假设下可以非参数点识别。此外，我们证明可以使用结果回归（OR）、逆概率加权（IPW）或双重稳健（DR）估计量来恢复 $ATT(g,t)$。此外，我们还强调了假设3以及假设4和假设5在形成这些不同估计量时所扮演的角色。

在形式化所有结果之前，我们需要引入一些额外记号。令 $m_{g,t,\delta}^{nev}(X) = \mathbb{E}[Y_t - Y_{g-\delta-1} | X, C = 1]$ 和 $m_{g,t,\delta}^{ny}(X) = \mathbb{E}[Y_t - Y_{g-\delta-1} | X, D_{t+\delta} = 0, G_g = 0]$。这些是从未处理组和在时期 $t + \delta$ 之前"尚未处理"组的总体结果回归。

基于"从未处理"的对照组，IPW估计量定义为

$$ATT_{ipw}^{nev}(g,t;\delta) = \mathbb{E}\left[\left(\frac{G_g}{\mathbb{E}[G_g]} - \frac{\frac{p_g(X) \cdot C}{1 - p_g(X)}}{\mathbb{E}\left[\frac{p_g(X) \cdot C}{1 - p_g(X)}\right]}\right)(Y_t - Y_{g-\delta-1})\right] \tag{2.2}$$

OR估计量定义为

$$ATT_{or}^{nev}(g,t;\delta) = \mathbb{E}\left[\frac{G_g}{\mathbb{E}[G_g]}\left((Y_t - Y_{g-\delta-1}) - m_{g,t,\delta}^{nev}(X)\right)\right] \tag{2.3}$$

DR估计量定义为

$$ATT_{dr}^{nev}(g,t;\delta) = \mathbb{E}\left[\left(\frac{G_g}{\mathbb{E}[G_g]} - \frac{\frac{p_g(X) \cdot C}{1 - p_g(X)}}{\mathbb{E}\left[\frac{p_g(X) \cdot C}{1 - p_g(X)}\right]}\right)(Y_t - Y_{g-\delta-1} - m_{g,t,\delta}^{nev}(X))\right] \tag{2.4}$$

类似地，基于"尚未处理"的对照组，可以定义IPW、OR和DR估计量（等式2.5-2.7）。

**定理1。** 令假设1、2、3和6成立。

（i）如果假设4成立，则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$，$t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$，

$$ATT(g,t) = ATT_{ipw}^{nev}(g,t;\delta) = ATT_{or}^{nev}(g,t;\delta) = ATT_{dr}^{nev}(g,t;\delta)$$

（ii）如果假设5成立，则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$，$t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $g - \delta \leq t < \bar{g} - \delta$，

$$ATT(g,t) = ATT_{ipw}^{ny}(g,t;\delta) = ATT_{or}^{ny}(g,t;\delta) = ATT_{dr}^{ny}(g,t;\delta)$$

定理1是本文的第一个主要结果。它提供了强大的识别结果，将基于Heckman et al. (1997, 1998)的结果回归方法、Abadie (2005)的IPW方法和Sant'Anna and Zhao (2020)的DR方法的DiD识别结果扩展到多期、多组设置。换言之，定理1表明，从识别的角度来看，可以通过利用数据生成过程的不同部分来恢复 $ATT(g,t)$：OR方法仅依赖于对照组结果变化的条件期望建模，IPW方法依赖于对属于组 $g$ 的条件概率建模，而DR方法同时利用OR和IPW两个组成部分。

为了将Heckman et al. (1997, 1998)、Abadie (2005)和Sant'Anna and Zhao (2020)的结果扩展到多组、多期框架，我们必须解决两个不同的挑战：一个与适当的参考时间段有关，一个与适当的对照组有关。定理1突出了这两个挑战的解决方案如何直接与有限预期和条件平行趋势假设相关。更具体地说，定理1表明我们可以在假设3以及假设4或假设5下使用时期 $t = g - \delta - 1$ 作为适当的参考时间段。这是组 $g$ 中单位未处理潜在结果被观察到的最近时期。有趣的是，允许的处理预期越多（即 $\delta$ 越高），需要回溯的时间就越远。定理1还表明对照组的选择直接与条件平行趋势假设相关：在假设4下，可以使用"从未处理"的单位作为所有"最终受处理"单位的固定对照组；而在假设5下，可以使用在时期 $t + \delta$ 之前"尚未处理"的单位作为首次在时期 $g$ 接受处理的组的有效对照组。在后一种情况下，定理1还强调，当所有单位最终都接受处理（$\bar{g} < \infty$）时，只能识别最后一个处理组"有效"开始处理之前时期的 $ATT(g,t)$，即 $t < \bar{g} - \delta$。

最后，我们注意到当处理前协变量在识别中不起作用时（即假设3、4和5无条件地在 $X$ 上成立），(2.2)-(2.4)退化为

$$ATT_{unc}^{nev}(g,t;\delta) = E[Y_t - Y_{g-\delta-1} | G_g = 1] - E[Y_t - Y_{g-\delta-1} | C = 1] \tag{2.8}$$

且(2.5)-(2.7)退化为

$$ATT_{unc}^{ny}(g,t;\delta) = E[Y_t - Y_{g-\delta-1} | G_g = 1] - E[Y_t - Y_{g-\delta-1} | D_{t+\delta} = 0] \tag{2.9}$$

这些 $ATT(g,t)$ 的表达式清楚地类似于经典两期两组情形中的 $ATT$ 表达式。与那种情况一样，组 $g$ 中单位参与处理的平均效应通过以下方式来识别：取该组实际经历的结果路径（即从他们受处理影响之前的最近时期到当前时期的结果变化），并用对照组经历的结果路径进行调整。在平行趋势假设下，后者是组 $g$ 中单位如果未参与处理将会经历的结果路径。

**注3。** 从(2.8)可以看出，当假设3和假设4无条件成立且没有预期时，$ATT(g,t)$ 参数可以通过以下方式获得：首先将数据子集限制为仅包含在时间 $t$ 和 $g - 1$，来自 $G_g = 1$ 或 $C = 1$ 的单位的观测，然后，仅使用此子集的观测，运行（总体）线性回归

$$Y = \alpha_1^{g,t} + \alpha_2^{g,t} \cdot G_g + \alpha_3^{g,t} \cdot \mathbf{1}\{T = t\} + \beta_{g,t} \cdot (G_g \times \mathbf{1}\{T = t\}) + \epsilon_{g,t} \tag{2.10}$$

容易验证 $\beta_{g,t} = ATT(g,t)$。注意需要考虑数据的不同分区来刻画不同的 $ATT(g,t)$ 作为回归参数。或者，也可以使用Sun and Abraham (2020)提出的交互双向固定效应回归。

**注4。** 当有协变量可用时，使用与注3中相同数据子集的总体线性回归

$$Y = \tilde{\alpha}_1^{g,t} + \tilde{\alpha}_2^{g,t} \cdot G_g + \tilde{\alpha}_3^{g,t} \cdot \mathbf{1}\{T = t\} + \tilde{\beta}_{g,t} \cdot (G_g \times \mathbf{1}\{T = t\}) + \tilde{\gamma} \cdot X + \tilde{\epsilon}_{g,t}$$

的系数 $\tilde{\beta}_{g,t}$ 一般不等于 $ATT(g,t)$，除非愿意假设（i）处理效应关于 $X$ 同质，即 $\mathbb{E}[Y_t(g) - Y_t(0) | G_g = 1, X] = \mathbb{E}[Y_t(g) - Y_t(0) | G_g = 1]$ a.s.，以及（ii）排除特定协变量趋势。

**注5。** 虽然定理1中基于IPW、OR和DR的估计量从识别角度来看是相同的，但在估计和推断 $ATT(g,t)$ 时并非如此。如第4节所讨论的，基于DR估计量(2.4)和(2.7)的DiD估计量通常在模型误设方面比IPW和OR估计量享有额外的稳健性。

**注6。** 定理1表明我们只能对 $\mathcal{G}_\delta \subseteq \mathcal{G}$ 中的组识别 $ATT(g,t)$，这可能涉及由于预期效应而删除某些"早期处理"组。当 $\delta = 0$，即没有预期时，$\mathcal{G}_\delta = \mathcal{G}$。定理1还表明我们只能识别到 $t = \mathcal{T} - \delta$ 为止的 $ATT(g,t)$，因为可能存在处理预期行为。然而，在已知某些单位永远不参与处理（包括时期 $\mathcal{T}$ 之后的时期）的应用中，只要满足适当的平行趋势假设，我们可以使用这些单位作为所有时期 $t = \mathcal{T} - \delta + 1, \ldots, \mathcal{T}$ 的有效对照组，从而识别到 $t = \mathcal{T}$ 的 $ATT(g,t)$。

**注7。** 从定理1中可以清楚地看出，处理前协变量在我们的分析中扮演着重要角色。重要的是，假设4和假设5表明研究者应纳入可能与处理后时期 $Y(0)$ 结果演变相关的处理前协变量。我们明确排除纳入处理后协变量，因为它们可能受到处理的影响；参见，例如，Wooldridge (2005b)在不可混淆设置下的相关讨论。

---

## 3　汇总组—时间平均处理效应

上一节表明，通过限制处理预期行为和施加条件平行趋势假设，我们可以识别 $ATT(g,t)$。在许多应用中，$ATT(g,t)$ 可以是最终的因果参数。它们可以用来突出不同组 $g$、不同时间点 $t$ 以及不同处理暴露时长 $e = t - g$ 的处理效应异质性。然而，在其他情况下，研究者可能希望将这些不同的 $ATT(g,t)$ 组合形成更加聚合的因果参数。例如，如果组和时期的数量相对较多，解释许多组—时间平均处理效应可能具有挑战性。

在许多实证应用中，从业者使用以下标准的双向固定效应（TWFE）规范来估计处理效应：

**静态TWFE规范：**

$$Y_{i,t} = \alpha_t + \alpha_g + \beta D_{i,t} + \epsilon_{i,t} \tag{3.2}$$

**动态TWFE规范：**

$$Y_{i,t} = \alpha_t + \alpha_g + \sum_{e=-K}^{-2} \delta_e^{antic} \cdot D_{i,t}^e + \sum_{e=0}^{L} \beta_e \cdot D_{i,t}^e + v_{i,t} \tag{3.3}$$

其中 $\alpha_t$ 是时间固定效应，$\alpha_g$ 是组固定效应，$\epsilon_{i,t}$ 和 $v_{i,t}$ 是误差项，$D_{i,t}^e = \mathbf{1}\{t - G_i = e\}$ 是单位 $i$ 在时间 $t$ 距离初始处理 $e$ 个时期的指示函数，$K$ 和 $L$ 是正常数。静态TWFE规范中的参数 $\beta$ 在应用中通常被解释为跨组和跨时期参与处理的总体效应。在动态TWFE规范中，从业者通常关注 $\beta_e$（$e \geq 0$），这些参数通常被解释为衡量处理后 $e$ 期处理效应的度量。

然而，最近的文献提出了关于将 $\beta$ 和 $\beta_e$ 解释为因果参数的若干担忧。正如Goodman-Bacon (2019)所讨论的，与 $\beta$ 相关的"负权重问题"在处理效应随时间演变时出现。因此，人们可能会想这类问题在考虑更一般的动态规范如(3.3)时是否仍然存在。Sun and Abraham (2020)表明情况确实如此，因为与(3.3)关联的 $\beta_e$ 不能恢复易于解释的因果参数，且通常仍然存在负权重问题。

本节中的结果可以在完全相同的设置中使用，以识别单一可解释的平均处理效应参数，从而提供一种规避更常见方法问题的途径。

### 3.1 聚合方案

我们考虑以下几种聚合方案：

**事件研究聚合。** 一种特别有用的聚合方式是将 $ATT(g,t)$ 变换为事件时间。令 $e = t - g$ 表示处理暴露时长。事件研究类型的聚合参数定义为

$$\theta_{es}(e) = \sum_{g \in \mathcal{G}} \mathbf{1}\{g + e \leq \mathcal{T}\} \cdot P(G = g | G + e \leq \mathcal{T}) \cdot ATT(g, g + e)$$

这给出了暴露于处理 $e$ 个时期的平均效应，在各组之间加权。

**组特定效应聚合。** 该方案对每个组 $g$ 取其所有处理后 $ATT(g,t)$ 的加权平均：

$$\theta_{sel}(\tilde{g}) = \frac{1}{\mathcal{T} - \tilde{g}} \sum_{t=\tilde{g}}^{\mathcal{T}} ATT(\tilde{g}, t)$$

**日历时间效应聚合。** 该方案对每个日历时间 $t$ 取当时所有处理组的 $ATT(g,t)$ 的加权平均：

$$\theta_c(\tilde{t}) = \sum_{g \in \mathcal{G}} \mathbf{1}\{g \leq \tilde{t}\} \cdot P(G = g | G \leq \tilde{t}) \cdot ATT(g, \tilde{t})$$

### 3.2 聚合为总体处理效应参数

最后，我们考虑将组—时间平均处理效应聚合为参与处理的总体效应。一个非常简单的想法是将所有已识别的组—时间平均处理效应平均在一起；即考虑参数

$$\theta_{WO} = \frac{1}{\kappa} \sum_{g \in \mathcal{G}} \sum_{t=2}^{\mathcal{T}} \mathbf{1}\{t \geq g\} \cdot ATT(g,t) \cdot P(G = g | G \leq \mathcal{T}) \tag{3.10}$$

类推，也可以通过对所有事件时间的 $\theta_{es}(e)$ 取平均或对所有时期的 $\theta_c(t)$ 取平均来定义总体处理效应参数，即

$$\theta_{es}^O = \frac{1}{\mathcal{T} - 1} \sum_{e=0}^{\mathcal{T}-2} \theta_{es}(e), \quad \theta_c^O = \frac{1}{\mathcal{T} - 1} \sum_{t=2}^{\mathcal{T}} \theta_c(t) \tag{3.12}$$

我们注意到，本节中讨论的所有聚合参数一般不相等，除非在 $ATT(g,t)$ 对所有组和所有时期相同的特殊情况下。在那种情况下，所有聚合参数，包括TWFE回归的 $\beta$，都相等。

---

## 4　估计与推断

到目前为止，我们关注的是分析的识别和聚合阶段。在本节中，我们展示如何在这些结果的基础上为组—时间平均处理效应及其在第3节中描述的汇总度量形成估计量和进行推断。鉴于 $ATT(g,t)$ 是我们分析的主要构建模块，我们从它们开始。

首先，重要的是注意到我们在定理1中的识别结果是建设性的，它们建议了一种简单直观的两步估计策略来估计 $ATT(g,t)$。在第一步中，对每个组 $g$ 和时期 $t$ 估计干扰函数——如果依赖假设4，则估计 $p_g(x)$ 和/或 $m_{g,t,\delta}^{nev}(X)$；如果依赖假设5，则估计 $p_{g,t+\delta}(x)$ 和/或 $m_{g,t,\delta}^{ny}(X)$。在第二步中，将这些估计的干扰函数的拟合值代入所考虑的 $ATT(g,t)$ 估计量的样本类比中，得到组—时间平均处理效应的估计值。

一个自然的问题是在实践中应该使用哪种方法：结果回归、逆概率加权还是双重稳健方法。虽然这三种不同的方法从识别角度来看是等价的，但从估计/推断角度来看并非如此。OR方法要求研究者正确建模对照组的结果变化，以估计组—时间平均处理效应。IPW方法避免了显式建模对照组的结果变化，因此不依赖于直接与目标参数相关的假设性模型限制。然而，IPW方法要求正确建模单位 $i$ 属于组 $g$（给定其协变量 $X$ 且属于组 $g$ 或适当对照组）的条件概率。DR方法结合了OR和IPW两种方法，因为它依赖于同时建模结果变化和倾向得分。然而，它只要求正确指定对照组的结果变化模型或倾向得分模型中的任一（但不一定两个都正确）(Sant'Anna and Zhao, 2020)。因此，与OR和IPW方法相比，DR方法在模型误设方面享有额外的稳健性。此外，DR方法可能允许使用更广泛的估计方法，如涉及惩罚和某些类型模型选择的方法(Belloni et al., 2017)。

鉴于DR方法的这些有吸引力的稳健性特征，在本节中我们考虑DR形式的估计量；关于如何使用OR和IPW方法的讨论是类似的，因此省略。我们还关注干扰函数的参数估计量。

更具体地说，令

$$\widehat{ATT}_{dr}^{nev}(g,t;\delta) = \mathbb{E}_n\left[(\hat{w}_g^{treat} - \hat{w}_g^{comp,nev})(Y_t - Y_{g-\delta-1} - \hat{m}_{g,t,\delta}^{nev}(X; \hat{\beta}_{g,t,\delta}^{nev}))\right] \tag{4.1}$$

$$\widehat{ATT}_{dr}^{ny}(g,t;\delta) = \mathbb{E}_n\left[(\hat{w}_g^{treat} - \hat{w}_g^{comp,ny})(Y_t - Y_{g-\delta-1} - \hat{m}_{g,t,\delta}^{ny}(X; \hat{\beta}_{g,t,\delta}^{ny}))\right] \tag{4.2}$$

其中 $\hat{w}_g^{treat}$、$\hat{w}_g^{comp,nev}$ 和 $\hat{w}_g^{comp,ny}$ 是权重的样本类比，而 $\hat{p}_g(\cdot; \hat{\pi}_g)$、$\hat{m}_{g,t,\delta}^{nev}(\cdot; \hat{\beta}_{g,t,\delta}^{nev})$ 是干扰函数的参数估计量。

### 4.1 组—时间平均处理效应的渐近理论

我们对干扰函数的参数模型和估计量施加以下标准假设。

**假设7。** （i）$g(x;\gamma)$ 是 $g(x)$ 的参数模型，其中 $\gamma \in \Theta \subset \mathbb{R}^k$，$\Theta$ 紧致；（ii）$g(X;\gamma)$ 对每个 $\gamma \in \Theta$ 几乎处处连续；（iii）存在唯一的伪真参数 $\gamma^* \in int(\Theta)$；（iv）$g(X;\gamma)$ 在 $\gamma^*$ 的邻域中几乎处处二阶连续可微。此外，$\sqrt{n}(\hat{\gamma} - \gamma^*)$ 容许渐近线性表示。

**假设8。** 对每个 $g \in \mathcal{G}$ 和 $t = \{2, \ldots, \mathcal{T} - \delta\}$，一些弱可积性条件成立。此外，DR估计量的双重稳健性质要求

$$\exists \pi_g^* \in \Theta_{ps}: P(p_g(X; \pi_g^*) = p_g(X)) = 1 \quad \text{或} \quad \exists \beta_{g,t,\delta}^{*,nev} \in \Theta_{reg}: P(m_{g,t,\delta}^{nev}(X; \beta_{g,t,\delta}^{*,nev}) = m_{g,t,\delta}^{nev}(X)) = 1 \tag{4.5}$$

(4.5)表明，广义倾向得分的参数模型被正确指定，或者对照组的结果回归模型被正确指定。

**定理2。** 在假设1-4, 6-8下，对每个 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$，$t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$，如果(4.5)成立，

$$\sqrt{n}(\widehat{ATT}_{dr}^{nev}(g,t;\delta) - ATT(g,t)) = \frac{1}{\sqrt{n}} \sum_{i=1}^n \psi_{g,t,\delta}^{dr,nev}(W_i; \kappa_{g,t}^{*,nev}) + o_p(1)$$

此外，当 $n \to \infty$，

$$\sqrt{n}(\widehat{ATT}_{t \geq (g-\delta)}^{dr,nev} - ATT_{t \geq (g-\delta)}) \xrightarrow{d} N(0, \Sigma)$$

其中 $\Sigma = \mathbb{E}[\Psi_{t \geq (g-\delta)}^{dr,nev}(W) \Psi_{t \geq (g-\delta)}^{dr,nev}(W)']$。

定理2提供了估计组—时间平均处理效应向量 $ATT_{t \geq (g-\delta)}$ 的影响函数及其极限分布。重要的是，定理2强调了 $\widehat{ATT}_{dr}^{nev}(g,t;\delta)$ 的DR性质：只要倾向得分工作模型或结果回归工作模型被正确指定，它就能恢复 $ATT(g,t)$。

为了进行推断，我们提出使用简单的乘数自助法程序。令 $\{V_i\}_{i=1}^n$ 为一组独立同分布的随机变量，均值为零、方差为1且有有限三阶矩，独立于原始样本。一个流行的例子是Mammen (1993)建议的独立同分布Bernoulli变量。定义自助法抽取为

$$\widehat{ATT}_{t \geq (g-\delta)}^{*,dr,nev} = \widehat{ATT}_{t \geq (g-\delta)}^{dr,nev} + \mathbb{E}_n[V \cdot \hat{\Psi}_{t \geq (g-\delta)}^{dr,nev}(W)] \tag{4.6}$$

**定理3。** 在定理2的假设下，

$$\sqrt{n}(\widehat{ATT}_{t \geq (g-\delta)}^{*,dr,nev} - \widehat{ATT}_{t \geq (g-\delta)}^{dr,nev}) \xrightarrow{*d} N(0, \Sigma)$$

其中 $\Sigma$ 如定理2所述，$\xrightarrow{*d}$ 表示自助法律的弱收敛。此外，对任何连续泛函 $\Gamma(\cdot)$，

$$\Gamma(\sqrt{n}(\widehat{ATT}_{t \geq (g-\delta)}^{*,dr,nev} - \widehat{ATT}_{t \geq (g-\delta)}^{dr,nev})) \xrightarrow{*d} \Gamma(N(0, \Sigma))$$

**算法1**（$ATT(g,t)$ 的同时置信带）。

1）抽取一组 $\{V_i\}_{i=1}^n$ 的实现。

2）按(4.6)计算 $\widehat{ATT}_{t \geq (g-\delta)}^{*,dr,nev}$，记其 $(g,t)$ 元素为 $\widehat{ATT}^*(g,t)$，并形成其极限分布的自助法抽取 $\hat{R}^*(g,t) = \sqrt{n}(\widehat{ATT}^*(g,t) - \widehat{ATT}(g,t))$。

3）重复步骤1-2共 $B$ 次。

4）计算 $\Sigma^{1/2}$ 主对角线的自助法估计量，如归一化的自助法四分位间距 $\hat{\Sigma}^{1/2}(g,t) = (q_{0.75}(g,t) - q_{0.25}(g,t)) / (z_{0.75} - z_{0.25})$。

5）对每次自助法抽取，计算 $t$ 统计量 $\hat{R}^*(g,t) / \hat{\Sigma}^{1/2}(g,t)$，并取所有 $(g,t)$ 上的最大绝对值。取 $B$ 次最大值的 $(1-\alpha)$ 分位数 $\hat{c}_{1-\alpha}$。

6）$ATT(g,t)$ 的同时 $(1-\alpha)$ 置信带为 $\hat{C}(g,t) = [\widehat{ATT}(g,t) \pm \hat{c}_{1-\alpha} \cdot \hat{\Sigma}^{1/2}(g,t) / \sqrt{n}]$。

**推论1。** 在定理2的假设下，对任何 $0 < \alpha < 1$，当 $n \to \infty$，

$$P(ATT(g,t) \in \hat{C}(g,t), \forall t \in \{2, \ldots, \mathcal{T}\}, g \in \mathcal{G}_\delta: t \geq g - \delta) \to 1 - \alpha$$

**注10。** 我们的自助法程序可以直接修改以考虑聚类。只需在聚类级别而非个体级别抽取与乘以 $V$，参见Wooldridge (2003)。

**注11。** 在算法1中我们需要 $\Sigma$ 主对角线的估计量。然而，如果取 $\hat{\Sigma}(g,t) = 1$ 对所有 $(g,t)$，推论1的结果继续成立。但由此得到的"等宽"同时置信带可能长度更大。

**注12。** 上述结果关注的是对（有效）处理后时期 $t \geq g - \delta$ 中 $ATT(g,t)$ 的推断。虽然假设3中的有限预期条件意味着对所有 $t < g - \delta$，$ATT(g,t) = 0$，但通常的做法是也估计这些处理前参数，并用它们来评估潜在识别假设的可信度。注意我们的DiD估计量(2.2)-(2.7)可以通过对所有 $t < g - \delta$ 用"短差分"$(Y_t - Y_{t-1})$替换"长差分"$(Y_t - Y_{g-\delta-1})$来轻松调整以包含这些。

### 4.2 汇总参数的渐近理论

为简便起见，假设假设3在 $\delta = 0$ 时成立。在本节中，我们讨论如何估计第3节中讨论的因果效应汇总度量并进行推断。更简洁地说，我们考虑如(3.1)中定义的 $\theta$ 形式的参数，它涵盖了第3节讨论的所有聚合参数。

一种自然的估计 $\theta$ 的方式是使用嵌入型估计量

$$\hat{\theta} = \sum_{g \in \mathcal{G}} \sum_{t=2}^{\mathcal{T}} \hat{w}(g,t) \widehat{ATT}_{dr}^{nev}(g,t; 0)$$

其中 $\hat{w}(g,t)$ 是 $w(g,t)$ 的估计量。令

$$l_w(W_i) = \sum_{g \in \mathcal{G}} \sum_{t=2}^{\mathcal{T}} \left(w(g,t) \cdot \psi_{g,t,0}^{dr,nev}(W_i; \kappa_{g,t}^{*,nev}) + \xi_{g,t}^w(W_i) \cdot ATT(g,t)\right)$$

**推论2。** 在定理2的假设下，

$$\sqrt{n}(\hat{\theta} - \theta) = \frac{1}{\sqrt{n}} \sum_{i=1}^n l_w(W_i) + o_p(1) \xrightarrow{d} N(0, \mathbb{E}[l_w(W)^2])$$

推论2意味着可以基于 $\mathbb{E}[l_w(W)^2]$ 的一致估计量或使用类似算法1的自助法程序来构造汇总处理效应参数的标准误和置信区间。

---

## 5　最低工资政策对青少年就业的影响

在本节中，我们说明了所提方法的实证相关性。为此，我们将方法应用于研究最低工资对青少年就业的影响。本节的主要目标是比较使用TWFE规范（这在应用中最常见）的结果与使用我们所提方法的结果。我们认为这种比较很重要，以便了解近期工作中讨论的TWFE的理论局限性是否会转化为应用中有意义的差异。此外，人们可能预期理解最低工资变化对就业的影响对TWFE来说是一个具有挑战性的案例，因为最低工资的影响可能是动态的(Meer and West, 2016)，且最低工资变化的时间在各州之间有差异。与TWFE不同，我们在本文中提出的方法对这些挑战是稳健的。

迄今为止，试图理解最低工资对就业影响的最常见方法是利用各州最低工资增加时间的变异。我们的识别策略遵循这一方法。特别是，我们考虑2001年至2007年联邦最低工资固定在每小时5.15美元的时期。我们关注在此期间初始时最低工资等于联邦最低工资的各州的县级青少年就业。这些州中有些在此期间提高了其最低工资——它们成为处理组。特别是，我们按州首次提高最低工资的时期来定义组。其他州没有提高最低工资——它们是未处理组。这一设置使我们拥有比地方案例研究方法更多的数据。另一方面，与拥有更多时期的研究相比，它也提供了更清晰的识别（州级最低工资政策变化）。

### 5.1 结果

以下我们使用不同的识别策略讨论不同的结果集。特别是，我们考虑平行趋势假设无条件成立的情况，以及仅在控制观测特征 $X$ 后成立的情况。在正文中，我们考虑从未处理的县作为对照组且不允许任何预期效应（即 $\delta = 0$）的情况。

第一组结果来自使用无条件平行趋势假设来估计提高最低工资对青少年就业的影响。

表1中的（a）面板报告了无条件平行趋势情况下的结果。TWFE估计量为 $-0.037$（标准误0.006）。然而，使用我们的方法，简单加权平均产生了更大的负效应 $-0.052$（标准误0.006）。看组特定效应，2004年组（$g = 2004$）的效应最大为 $-0.091$（标准误0.019），2006年组为 $-0.047$（标准误0.008），2007年组为 $-0.028$（标准误0.007），总体组特定效应为 $-0.039$（标准误0.007）。事件研究结果表明效应随暴露时间增加而增大：$e = 0$ 时为 $-0.027$（标准误0.006），$e = 1$ 时为 $-0.071$（标准误0.009），$e = 2$ 时为 $-0.125$（标准误0.021），$e = 3$ 时为 $-0.136$（标准误0.023），总体事件研究效应为 $-0.090$。

在展示条件平行趋势的结果之前，我们注意到我们的双重稳健估计程序在计算上要求不高。本节中我们对组—时间平均处理效应的估计（跨所有组和时期，包括1000次迭代的乘数自助法）在配备2.80 GHz Intel i5处理器和8GB RAM的笔记本电脑上运行仅需3.0秒，且未使用任何并行处理。

作为比较，我们首先估计了在包含单位固定效应和区域-年份固定效应模型中处理后虚拟变量的系数。这与Dube et al. (2010)发现能消除最低工资与就业之间相关性的模型类型非常相似。与Dube et al. (2010)一样，使用此规范，我们发现估计系数较小且与0无统计显著差异。然而，必须记住我们在本文中提出的方法不同于双向固定效应回归。特别是，我们明确识别了不同组和不同时间的组—时间平均处理效应，允许任意的处理效应异质性，只要满足条件平行趋势假设。因此，我们的因果参数有清晰的解释。

然而，有两个警告值得注意。首先，图1(a)中处理前时期的伪组—时间平均处理效应估计中有些与零显著不同，这为反对平行趋势假设提供了一些暗示性证据。其次，各州最低工资增幅本身存在一些异质性，这可能使结果的解释复杂化。综合来看，这些表明我们的结果应谨慎解释。话虽如此，我们认为这个应用的关键要点是，在一个经济学中的突出应用中（该应用具有许多非常常见的特征：处理效应异质性、动态效应和交错处理采纳），在（隐含地）保持主要识别假设不变的情况下，估计方法的选择可能导致质量上不同的结论。

---

## 6　结论

本文考虑了在超过两个时期且单位可在不同时间点接受处理的情况下的双重差分方法——这是经济学实证工作中经常遇到的设置。在此设置中，我们提出了组—时间平均处理效应 $ATT(g,t)$，即在时期 $g$ 首次受处理的组在时期 $t$ 的平均处理效应。与更常见的在双向固定效应回归中包含处理后虚拟变量的方法不同，$ATT(g,t)$ 对应于一个定义明确的处理效应参数。我们还表明，一旦对不同的 $g$ 和 $t$ 值获得了 $ATT(g,t)$，它们可以被聚合为其他参数，以更简洁地总结关于某一特定维度（如处理暴露时长）的异质性，或者聚合为单一的总体处理效应参数。此外，我们的方法适用于以下情况：（i）平行趋势假设仅在以协变量为条件后成立；（ii）使用不同的对照组，如从未处理组或尚未处理组；以及（iii）当单位可以预期参与处理并可能在处理实施前调整其行为。我们将这种灵活性视为我们所提方法论的重要组成部分。

我们还提供了导致结果回归、逆概率加权和双重稳健估计量的非参数识别结果。鉴于我们的非参数识别结果是建设性的，我们提出使用其样本类比来估计 $ATT(g,t)$。我们建立了所提估计量的一致性和渐近正态性，并证明了一个强大但易于实施的乘数自助法程序的有效性，用以构造 $ATT(g,t)$ 的同时置信带。我们方法的计算成本通常较低，用于实施我们方法的代码可在R语言的 **did** 包中获得。

最后，我们将方法应用于研究最低工资增加对青少年就业的影响。我们发现了一些证据表明提高最低工资导致了青少年就业的减少。更有趣的是，在某些情况下，我们发现使用我们方法得出的结果与更常见的双向固定效应方法之间存在显著差异。这些差异表明，使用对处理效应异质性和动态稳健的方法应该受到应用研究者的高度重视。

---

## 附录A：主要结果的证明

我们在本附录中提供结果的证明。在进行之前，我们首先陈述并证明几个辅助引理来帮助证明我们的主要定理。

令 $ATT_X(g,t) = \mathbb{E}[Y_t(g) - Y_t(0) | X, G_g = 1]$。

**引理A.1。** 令假设1、2、3、4和6成立。则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$, $t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$，

$$ATT_X(g,t) = \mathbb{E}[Y_t - Y_{g-\delta-1} | X, G_g = 1] - \mathbb{E}[Y_t - Y_{g-\delta-1} | X, C = 1] \quad \text{a.s.}$$

**引理A.1的证明：** 取所有等式几乎处处（a.s.）成立。有

$$ATT_X(g,t) = \mathbb{E}[Y_t(g) - Y_{g-\delta-1}(0) | X, G_g = 1] - \mathbb{E}[Y_t(0) - Y_{g-\delta-1}(0) | X, G_g = 1]$$

其中第一个等式来自加减 $\mathbb{E}[Y_{g-\delta-1}(0) | X, G_g = 1]$，后续步骤通过简单代数、假设4，以及(2.1)和假设3得到。□

**引理A.2。** 令假设1、2、3、5和6成立。则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$, $t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $g - \delta \leq t < \bar{g}$，

$$ATT_X(g,t) = \mathbb{E}[Y_t - Y_{g-\delta-1} | X, G_g = 1] - \mathbb{E}[Y_t - Y_{g-\delta-1} | X, D_{t+\delta} = 0, G_g = 0] \quad \text{a.s.}$$

引理A.2的证明与引理A.1类似，利用假设5（取 $s = t + \delta$）替代假设4。□

**定理1的证明：**

**第一部分：当假设4被使用时的识别。** 根据引理A.1的结果，

$$ATT(g,t) = \mathbb{E}[ATT_X(g,t) | G_g = 1] = \mathbb{E}[Y_t - Y_{g-\delta-1} | G_g = 1] - \mathbb{E}[\mathbb{E}[Y_t - Y_{g-\delta-1} | X, C = 1] | G_g = 1]$$

因此 $ATT(g,t) = ATT_{or}^{nev}(g,t;\delta)$。

对于IPW等式，通过利用 $p_g(X) = \mathbb{E}[G_g|X] / \mathbb{E}[G_g + C|X]$ 和 $1 - p_g(X) = \mathbb{E}[C|X] / \mathbb{E}[G_g + C|X]$，以及迭代期望定律，可以建立 $ATT(g,t) = ATT_{ipw}^{nev}(g,t;\delta)$。

DR等式的证明结合了IPW和OR的结果。□

**定理2的证明：** 由定理1可知所有组 $g$ 和时期 $t$（使得 $g \in \mathcal{G}_\delta$, $t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$）的 $ATT(g,t)$ 被点识别。对每个 $(g,t)$ 对，渐近线性表示由相关引理得到。联合极限分布由Lindeberg-Lévy中心极限定理得出。□

**定理3的证明：** 由条件乘数中心极限定理（van der Vaart and Wellner, 1996, 引理2.9.5），当 $n \to \infty$，

$$\frac{1}{\sqrt{n}} \sum_{i=1}^n V_i \cdot \Psi_{t \geq (g-\delta)}^{dr,nev}(W_i) \xrightarrow{*d} N(0, \Sigma)$$

证明的其余部分通过建立

$$\frac{1}{\sqrt{n}} \sum_{i=1}^n V_i \cdot [\hat{\psi}_{g,t,\delta}^{dr,nev}(W_i; \hat{\kappa}_{g,t}^{nev}) - \psi_{g,t,\delta}^{dr,nev}(W_i; \kappa_{g,t}^{*,nev})] = o_p^*(1)$$

来完成，这通过均值定理、大数强定律以及假设7和假设8得到。□

---

## 附录B：重复截面的额外结果

在本节中，我们将识别结果扩展到有重复截面数据而非面板数据的情况。这里假设对合并样本中的每个单位，观察到 $(Y, G_2, \ldots, G_\mathcal{T}, C, T, X)$，其中 $T \in \{1, \ldots, \mathcal{T}\}$ 表示该单位被观察到的时期。

**假设B.1。** 假设每个时期都有随机样本可用。该假设排除了跨时间的构成变化。

在此设置下，定义OR、IPW和DR估计量分别推广了Heckman et al. (1997)、Abadie (2005)和Sant'Anna and Zhao (2020)的两组两期DiD设置中的估计量到具有多期和多组的交错DiD设置。

**定理B.1。** 令假设1、3、6和B.1成立。

（i）如果主文中的假设4成立，则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$, $t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$，

$$ATT(g,t) = ATT_{ipw,rc}^{nev}(g,t;\delta) = ATT_{or,rc}^{nev}(g,t;\delta) = ATT_{dr,rc}^{nev}(g,t;\delta)$$

（ii）如果主文中的假设5成立，则对所有 $g$ 和 $t$ 使得 $g \in \mathcal{G}_\delta$, $t \in \{2, \ldots, \mathcal{T} - \delta\}$ 且 $t \geq g - \delta$，

$$ATT(g,t) = ATT_{ipw,rc}^{ny}(g,t;\delta) = ATT_{or,rc}^{ny}(g,t;\delta) = ATT_{dr,rc}^{ny}(g,t;\delta)$$

定理B.1的识别结果表明了一种简单的两步估计程序，用于使用重复截面数据估计 $ATT(g,t)$，这与第4节中讨论的面板数据情形类似。此类两步估计量的渐近性质可由类似的论证得出。同样地，我们可以聚合这些估计量以提供因果效应的汇总度量，如第3节中讨论的那样。

---

## 参考文献

Abadie, A. (2005), "Semiparametric difference-in-difference estimators," *Review of Economic Studies*, 72, 1–19.

Abadie, A., Athey, S., Imbens, G., and Wooldridge, J. (2017), "When should you adjust standard errors for clustering?," *Working Paper*.

Abbring, J. H., and van den Berg, G. J. (2003), "The nonparametric identification of treatment effects in duration models," *Econometrica*, 71(5), 1491–1517.

Athey, S., and Imbens, G. W. (2006), "Identification and inference in nonlinear difference in differences models," *Econometrica*, 74(2), 431–497.

Athey, S., and Imbens, G. W. (2018), "Design-based analysis in difference-in-differences settings with staggered adoption," *Working Paper*.

Bailey, M. J., and Goodman-Bacon, A. (2015), "The war on poverty's experiment in public medicine: Community health centers and the mortality of older Americans," *American Economic Review*, 105(3), 1067–1104.

Belloni, A., Chernozhukov, V., Fernández-Val, I., and Hansen, C. (2017), "Program evaluation and causal inference with high-dimensional data," *Econometrica*, 85(1), 233–298.

Bertrand, M., Duflo, E., and Mullainathan, S. (2004), "How much should we trust differences-in-differences estimates?," *The Quarterly Journal of Economics*, 119(1), 249–275.

Bonhomme, S., and Sauder, U. (2011), "Recovering distributions in difference-in-differences models: A comparison of selective and comprehensive schooling," *Review of Economics and Statistics*, 93(May), 479–494.

Borusyak, K., and Jaravel, X. (2017), "Revisiting event study designs," *Working Paper*.

Botosaru, I., and Gutierrez, F. H. (2018), "Difference-in-differences when the treatment status is observed in only one period," *Journal of Applied Econometrics*, 33(1), 73–90.

Busso, M., Dinardo, J., and McCrary, J. (2014), "New evidence on the finite sample properties of propensity score reweighting and matching estimators," *The Review of Economics and Statistics*, 96(5), 885–895.

Callaway, B., Li, T., and Oka, T. (2018), "Quantile treatment effects in difference in differences models under dependence restrictions and with only two time periods," *Journal of Econometrics*, 206(2), 395–413.

Card, D., and Krueger, A. B. (1994), "Minimum wages and employment: A case study of the fast-food industry in New Jersey and Pennsylvania," *American Economic Review*, 84(4), 772–793.

Chernozhukov, V., Fernández-Val, I., Hahn, J., and Newey, W. (2013), "Average and quantile effects in nonseparable panel models," *Econometrica*, 81(2), 535–580.

Crump, R. K., Hotz, V. J., Imbens, G. W., and Mitnik, O. A. (2009), "Dealing with limited overlap in estimation of average treatment effects," *Biometrika*, 96(1), 187–199.

de Chaisemartin, C., and D'Haultfœuille, X. (2017), "Fuzzy differences-in-differences," *The Review of Economic Studies*, 85, 999–1028.

de Chaisemartin, C., and D'Haultfœuille, X. (2020), "Two-way fixed effects estimators with heterogeneous treatment effects," *American Economic Review*, 110(9), 2964–2996.

Dube, A., Lester, T. W., and Reich, M. (2010), "Minimum wage effects across state borders," *Review of Economics and Statistics*, 92(4), 945–964.

Goodman-Bacon, A. (2019), "Difference-in-differences with variation in treatment timing," *Working Paper*.

Graham, B., Pinto, C., and Egel, D. (2012), "Inverse probability tilting for moment condition models with missing data," *The Review of Economic Studies*, 79(3), 1053–1079.

Heckman, J. J., Humphries, J. E., and Veramendi, G. (2016), "Dynamic treatment effects," *Journal of Econometrics*, 191(2), 276–292.

Heckman, J. J., Ichimura, H., Smith, J., and Todd, P. (1998), "Characterizing selection bias using experimental data," *Econometrica*, 66(5), 1017–1098.

Heckman, J. J., Ichimura, H., and Todd, P. (1997), "Matching as an econometric evaluation estimator: Evidence from evaluating a job training programme," *The Review of Economic Studies*, 64(4), 605–654.

Imai, K., Kim, I. S., and Wang, E. (2018), "Matching methods for causal inference with time-series cross-section data," *Working Paper*.

Khan, S., and Tamer, E. (2010), "Irregular identification, support conditions, and inverse weight estimation," *Econometrica*, 78(6), 2021–2042.

Laporte, A., and Windmeijer, F. (2005), "Estimation of panel data models with binary indicators when treatment effects are not constant over time," *Economics Letters*, 88(3), 389–396.

Malani, A., and Reif, J. (2015), "Interpreting pre-trends as anticipation: Impact on estimated treatment effects from tort reform," *Journal of Public Economics*, 124, 1–17.

Mammen, E. (1993), "Bootstrap and wild bootstrap for high dimensional linear models," *The Annals of Statistics*, 21(1), 255–285.

Marcus, M., and Sant'Anna, P. H. C. (2020), "The role of parallel trends in event study settings: An application to environmental economics," *Journal of the Association of Environmental and Resource Economists*, Forthcoming.

Meer, J., and West, J. (2016), "Effects of the minimum wage on employment dynamics," *Journal of Human Resources*, 51(2), 500–522.

Montiel Olea, J. L., and Plagborg-Møller, M. (2018), "Simultaneous confidence bands: Theory, implementation, and an application to SVARs," *Journal of Applied Econometrics*, pp. 1–64.

Murphy, S. A. (2003), "Optimal dynamic treatment regimes," *Journal of the Royal Statistical Society Series B*, 65(2), 331–366.

Murphy, S. A., et al. (2001), "Marginal mean models for dynamic regimes," *Journal of the American Statistical Association*, 96(456), 1410–1423.

Neumark, D., and Wascher, W. (2000), "Minimum wages and employment: A case study of the fast-food industry in New Jersey and Pennsylvania: Comment," *American Economic Review*, 90(5), 1362–1396.

Neumark, D., and Wascher, W. L. (2008), *Minimum Wages*, Cambridge, MA: The MIT Press.

Newey, W. K., and McFadden, D. (1994), "Large sample estimation and hypothesis testing," in *Handbook of Econometrics*, Vol. 4, chapter 36, pp. 2111–2245.

Qin, J., and Zhang, B. (2008), "Empirical-likelihood-based difference-in-differences estimators," *Journal of the Royal Statistical Society. Series B*, 75(8), 329–349.

Robins, J. M. (1986), "A new approach to causal inference in mortality studies with a sustained exposure period – Application to control of the healthy worker survivor effect," *Mathematical Modelling*, 7, 1393–1512.

Robins, J. M. (1987), "Addendum to 'A new approach to causal inference in mortality studies with a sustained exposure period'," *Computers & Mathematics with Applications*, 14(9-12), 923–945.

Rubin, D. B. (2007), "The design versus the analysis of observational studies for causal effects: Parallels with the design of randomized trials," *Statistics in Medicine*, 26(1), 20–36.

Rubin, D. B. (2008), "For objective causal inference, design trumps analysis," *Annals of Applied Statistics*, 2(3), 808–840.

Sant'Anna, P. H., and Zhao, J. (2020), "Doubly robust difference-in-differences estimators," *Journal of Econometrics*, 219(1), 101–122.

Sianesi, B. (2004), "An evaluation of the Swedish system of active labor market programs in the 1990s," *The Review of Economics and Statistics*, 86(1), 133–155.

Sun, L., and Abraham, S. (2020), "Estimating dynamic treatment effects in event studies with heterogeneous treatment effects," *Working Paper*.

van der Vaart, A. W. (1998), *Asymptotic Statistics*, Cambridge: Cambridge University Press.

van der Vaart, A. W., and Wellner, J. A. (1996), *Weak Convergence and Empirical Processes*, New York: Springer.

Wooldridge, J. M. (2003), "Cluster-sample methods in applied econometrics," *American Economic Review P&P*, 93(2), 133–138.

Wooldridge, J. M. (2005a), "Fixed-effects and related estimators for correlated random-coefficient and treatment-effect panel data models," *Review of Economics and Statistics*, 87(2), 385–390.

Wooldridge, J. M. (2005b), "Violating ignorability of treatment by controlling for too many factors," *Econometric Theory*, 21(5), 1026–1028.

Wooldridge, J. M. (2007), "Inverse probability weighted estimation for general missing data problems," *Journal of Econometrics*, 141(2), 1281–1301.

Yang, S., and Ding, P. (2018), "Asymptotic inference of causal effects with observational studies trimmed by the estimated propensity scores," *Biometrika*, 105(2), 487–493.
