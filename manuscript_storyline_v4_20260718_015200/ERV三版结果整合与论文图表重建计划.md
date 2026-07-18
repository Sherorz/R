# ERV 三版结果整合与论文图表重建计划

## 1. 总目标

以 V3 的发育阶段对齐、Tau 和 nonlinear-age residual cis 为统计骨架，保留 V1 的图谱基础和 V2 的候选 ERV 分析价值。全文围绕以下可检验命题组织：

> 不同哺乳动物具有快速更替的 ERV 位点与家族库；较稳定的跨物种信号主要存在于发育时间窗口、family-like cluster 和器官使用规则，而非精确位点或精确 cis 连接。宿主模块趋同只有在正式随机模型通过后才能作为阳性主结论。

所有新结果写入时间戳隔离目录，不覆盖 V1、V2、V3 或 Concept 原文件。

## 2. 强制交付规则

- 每个 panel 必须具有独立 TSV、PNG、PDF 和独立渲染入口。
- 每张整图必须具有独立 PNG 和 PDF。
- 正式结果目录不允许出现 SVG、TIFF、JPEG、EPS。
- PNG 为 600 dpi、sRGB；PDF 使用矢量文字与线条。
- 单 panel 修改只允许重写该 panel、该 panel 的 source data 和对应整图。
- 所有统计比较保留效应量、95% CI、P、FDR、分母和统计单位。
- 不满足分析条件的值使用 NA，不能填 0。
- 所有 `driver` 统一写作 `candidate developmental ERV` 或 `prioritized ERV locus`。

## 3. 家族命名

保留 `family_raw`，新增物种内展示字段 `family_display` 和跨物种比较字段 `family_cluster_display`。

- 原始值精确为 `HERV`：无论物种，显示为 `ERV-T-like`。
- 人类明确的 HERV-X：物种内图可显示 `HERV-X`。
- 非人物种 HERV-X：显示 `ERV-X-like`。
- 跨物种 recurrence、module 和 family-like cluster 图：人类与非人物种都折叠为 `ERV-X-like`。
- 映射必须写入 `family_nomenclature_audit.tsv`，并通过自动测试。

## 4. 冻结的方法

### 4.1 发育轨迹

先在 native age 上拟合 GAM，再 post-hoc 映射至 aligned stage；禁止超出采样支持范围的外推。跨物种主结果使用 aligned coordinate，`dev01` 仅作为敏感性分析。

主阈值 `q=0.25`，敏感性阈值为 `q=0.10` 和 `q=0.50`。分类顺序固定为 multimodal、persistent、early、intermediate、late；主报告连续指标 T50、激活区间、window width、Tau 和 censoring。

### 4.2 Tau

Tau 轴必须注明 `0 = broad, 1 = restricted`。跨物种推断以 family/family-like cluster 为统计单位，使用共同 aligned support 和共同器官集合；不能把同一家族的 locus 当作独立重复。

### 4.3 候选 ERV

候选分数固定为：

`activity_score = max(0, leave-one-out locus-family Spearman) × mean family TPM`

在 species-organ 内排名，top decile 定义为 candidate。cis、Tau、出生位置与 recurrence 不进入分数，只能作为下游验证。

### 4.4 Residual cis

沿用 V3 nonlinear-age residual 框架。pair 结果保存距离、方向、效应量、P、FDR、有效阶段数和模型状态。正式 matched-background 需要在 species-organ 内进行 1:3 不放回匹配，caliper 为 propensity logit 的 0.2 SD，且全部协变量 SMD <0.10。

如 gene expression、GC、gene density 或 mappability 缺失，则 matched OR 只能标记为 exploratory，不能作为正式主图阳性结论。

### 4.5 Module convergence

正式结果需要 degree-preserving/module-size-matched null、10,000 次最终置换、LOSO 与 LOFO。只有 empirical FDR <0.05 且稳定性门槛通过的单元才进入主图阳性结论；否则 Fig.5f 显示阴性正式检验，详细结果降到 FigS14。

## 5. 六张主图

| 图 | Panel | 内容 |
|---|---|---|
| Fig.1 | a-d | 采样矩阵、全局 PCA、家族框架、eligible denominator |
| Fig.2 | a-f | 阶段对齐、native-age GAM、aligned heatmap、archetypes、器官组成、T50/class 稳定性 |
| Fig.3 | a-f | temporal-organ Tau、stagewise organ Tau、成熟效应、recurrence Tau、family-species heatmap、效应量摘要 |
| Fig.4 | a-f | 独立候选分数、top loci、family recurrence、exact-locus reuse、独立 Tau 评估、LOO 稳定性 |
| Fig.5 | a-f | residual pair/locus rate、matched gate、orthology funnel、residualization、module null |
| Fig.6 | a-e | 正确 cladogram、family-like evidence matrix、保守层级、效应量与 CI、生物学模型 |

系统树固定为：`opossum | ((human, macaque), (rabbit, (mouse, rat)))`。

## 6. 附图和附表

附图：FigS1 RNA/QC；FigS2 alignment gate；FigS3 archetypes；FigS4 GAM QC；FigS5 threshold/censoring；FigS6 derivative；FigS7 class stability；FigS8 Tau comparability；FigS9 amplitude-Tau；FigS10 candidate robustness；FigS11 cis matching；FigS12 cell composition；FigS13 nomenclature；FigS14 complete cis/module null。

FigS12 在没有真实 cell-composition 数据时必须以 blocker 文档交付，不能用模拟数据造图。

附表：TableS1–S13，依次覆盖 metadata、alignment、locus annotation、GAM、Tau、candidate、residual cis、orthogroup、module null、主统计、敏感性、panel source index、版本 crosswalk。

## 7. Gate 顺序

1. Gate 0：冻结输入、建立隔离目录、记录 SHA-256。
2. Gate 1：验证 stage source；完成 nomenclature audit。
3. Gate 2：生成规范数据接口和 V1/V2/V3 crosswalk。
4. Gate 3：完成 Tau、candidate、residual cis、recurrence、module null 和敏感性分析；不能完成者进入 blocker ledger。
5. Gate 4：逐 panel 生成 source data、PNG、PDF，再拼版。
6. Gate 5：统计 QA、视觉 QA、命名 QA、格式 QA 和 panel isolation test。
7. Gate 6：生成 RUN_SUMMARY、claims-evidence、panel guide、manifest 和 checksums。

## 8. 停止或降级条件

- 无正式 machine-readable stage correspondence：跨物种时间结论保持 work-in-progress。
- matched-background 缺少计划协变量或 SMD 不达标：不报告正式 OR。
- module null 不通过：module convergence 不作为阳性主结论。
- 无 cell-composition 数据：结论限定为 organ-level，FigS12 阻塞。
- 无可靠 mappability：限制 locus-level 解释，不阻塞 family-level 主线。
- derivative 无 simultaneous CI：FigS6 仅作探索性可视化。
- 任一裸 `HERV` 被当作展示名称：停止绘图，先修复命名映射。
- 单 panel 重绘改变其他 panel：架构验收失败。
- 结果目录出现禁用格式：交付验收失败。

## 9. 后续单 panel 修改入口

假设结果目录为 `$RUN`：

```bash
Rscript "$RUN/code/R/render_v4.R" "$RUN/code" "$RUN" panel Fig2c
Rscript "$RUN/code/R/render_v4.R" "$RUN/code" "$RUN" figure Fig2
```

第一条只更新 Fig2c 的 source data、PNG、PDF；第二条只重新拼装 Fig2 的 PNG、PDF。
