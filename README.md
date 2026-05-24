# AB Test Revenue Analysis

本项目基于用户 Revenue 数据，对 control 与 variant 两组进行 AB Test 分析，
通过统计检验与 Bootstrap 方法评估实验方案是否能够有效提升用户 Revenue。

## 项目背景

在产品实验中，需要验证新方案（variant）是否能够带来更高的用户 Revenue。

本项目从数据清洗、可视化分析、统计检验以及 Bootstrap 重采样等角度，
对实验结果进行完整分析，并评估实验结论的可靠性。

## 项目亮点（Highlights）

- 完整实现 AB Test 分析流程，包括数据清洗、统计检验与 Bootstrap 分析；
- 针对偏态 Revenue 数据，使用 Mann-Whitney U Test 进行非参数检验；
- 使用 Bootstrap 方法构建均值差置信区间，评估实验结果稳定性；
- 基于用户级聚合（User-Level Aggregation）降低重复行为记录带来的偏差。

## 分析内容

### 数据清洗（Data Cleaning）

- 检查实验污染用户（同时出现在多个实验组中的用户）
- 删除异常值用户
- 对用户行为数据进行用户级聚合（User-Level Aggregation）

### Revenue 分析（Revenue Analysis）

- 分析 Revenue 分布特征
- 观察偏态、长尾以及异常值情况
- 对整体用户与付费用户进行对比分析

### Statistical Analysis

由于 Revenue 数据存在明显偏态与大量零值，
因此采用非参数检验方法进行分析。

主要使用：

- Shapiro-Wilk Test
- Mann-Whitney U Test

### Bootstrap Analysis

使用 Bootstrap 重采样方法：

- 构建均值差分布
- 分析实验结果稳定性
- 计算 95% Confidence Interval

## 核心结论（Key Findings）

- Revenue 数据存在明显偏态与长尾特征；
- 数据不满足正态分布假设；
- Mann-Whitney U Test 未发现统计显著差异；
- Bootstrap 置信区间包含 0。

综合分析结果：

当前实验无法证明 variant 组能够显著提升用户 Revenue。

## Tech Stack

- Python
- Pandas / NumPy
- Matplotlib / Seaborn
- SciPy
- Statistical Testing
- Bootstrap Resampling

## Project Structure

```text
AB-Test-Revenue-Analysis/
│
├── AB_Test_Revenue_Analysis.ipynb
├── AB_Test_Results.csv
├── README.md
└── .gitignore
