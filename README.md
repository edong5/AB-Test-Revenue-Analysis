```markdown
# AB Test Revenue Analysis

本项目基于用户 Revenue 数据，对 control 与 variant 两组进行 AB Test 分析，
通过统计检验与 Bootstrap 方法评估实验方案是否能够有效提升用户 Revenue。

---

## 导入库（Import Libraries）

使用 Pandas、NumPy 完成数据处理，
使用 Matplotlib、Seaborn 进行可视化分析，
并结合 SciPy 完成统计检验与 Bootstrap 分析。

---

## 数据读取（Data Loading）

读取 AB Test 原始数据，
查看数据规模、字段结构以及基础统计信息。

主要关注：

- 用户数量（USER_ID）
- 实验分组（VARIANT_NAME）
- Revenue 分布情况

---

## 初步数据探索（Exploratory Data Analysis）

对数据进行初步探索，分析：

- 实验组分布是否均衡；
- Revenue 是否存在明显偏态；
- 用户行为是否存在异常情况。

通过 `describe()`、`nunique()` 等方法，
观察数据整体分布特征。

---

## 数据清洗（Data Cleaning）

为保证实验结果可靠性，对数据进行清洗：

### 1. 删除实验污染用户

检查用户是否同时出现在多个实验组中。

由于同一用户只能属于一个实验组，
因此删除实验污染用户，避免干扰实验结果。

### 2. 删除异常值

发现部分用户 Revenue 明显异常，
可能对整体均值产生较强影响。

因此移除极端异常值用户，
降低异常点对实验分析的干扰。

---

## Revenue 分析（Revenue Analysis）

通过箱线图分析 Revenue 分布特征：

- Revenue 存在明显长尾与偏态；
- 大量用户 Revenue 为 0；
- 付费用户与整体用户分布差异明显。

同时发现：

部分用户同时存在 Revenue=0 与 Revenue>0 的行为记录，
说明一个用户可能对应多条行为数据。

因此后续分析需要进行用户级聚合。

---

## 用户级聚合（User-Level Aggregation）

由于实验分析单位应为“用户”，
因此将同一用户的多条行为记录进行聚合。

聚合后：

- 每个用户仅保留一条记录；
- Revenue 按用户维度进行汇总；
- 避免重复统计带来的偏差。

---

## 指标分析（Metrics Analysis）

对 control 与 variant 两组进行核心指标对比：

### 分析指标

- 用户数（User Count）
- 总 Revenue
- 平均 Revenue（Mean）
- 中位数（Median）
- ARPU（Average Revenue Per User）
- 人均订单数

### 分析结果

variant 组部分指标存在波动，
但整体差异并不明显。

同时由于 Revenue 数据偏态严重，
均值容易受到异常值影响，
因此需要进一步进行统计检验。

---

## 统计检验（Statistical Analysis）

### 正态性检验（Shapiro-Wilk Test）

使用 Shapiro-Wilk Test 检验 Revenue 是否服从正态分布。

结果表明：

- p-value 显著小于 0.05；
- Revenue 数据不服从正态分布。

因此不适合直接使用 t-test。

### Mann-Whitney U Test

由于数据非正态且包含大量零值，
因此采用非参数检验 Mann-Whitney U Test。

检验结果显示：

- control 与 variant 组 p-value > 0.05；
- 未发现统计显著差异。

说明当前实验无法证明 variant 能够显著提升 Revenue。

---

## Bootstrap 分析（Bootstrap Analysis）

为进一步验证实验结果稳定性，
使用 Bootstrap 重采样方法构建均值差分布。

### Bootstrap 过程

- 对 control 与 variant 组重复随机抽样；
- 计算均值差分布；
- 构建 95% Confidence Interval。

### 分析结果

Bootstrap 置信区间包含 0，
说明两组均值差可能来源于随机波动。

因此实验结果缺乏稳定的显著提升证据。

---

## 最终结论（Conclusion）

本次 AB Test 分析表明：

- Revenue 数据存在明显偏态与长尾特征；
- 数据包含大量 Revenue 为 0 的用户；
- 实验数据不满足正态分布假设；
- Mann-Whitney U Test 未发现统计显著差异；
- Bootstrap 结果同样未支持 Revenue 提升结论。

综合统计检验与 Bootstrap 分析结果：

当前实验无法证明 variant 组能够显著提升用户 Revenue。
```
