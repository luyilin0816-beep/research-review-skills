---
name: research-review-01-keyword-calibration-search
description: Use when a Chinese social science project needs pre-writing literature preparation: calibrate research questions and keywords, search CNKI and Google Scholar, stop for human review, and only after approval ingest approved papers with PDFs into Zotero and a structured Obsidian summary.
---

# 前综述 01：关键词校准、文献检索与入库汇总

## 概述

本 skill 用于中文社科项目的研究前文献准备，顺序固定为：

1. 校准研究问题与关键词
2. 调用 `cnki-*` 与 `gs-*` 检索并初筛
3. 输出候选清单并暂停，等待人工审核
4. 审核通过后，再进入“全文获取 + Zotero 入库 + 分类核验”

候选清单生成后必须停下；未经用户明确确认，不得进入 Zotero。

## 原有不变要求

- 关键词校准优先于数据库抓取
- 检索过程本身就要带初筛意识
- 候选清单后必须停止，等待人工审核
- 未经用户明确确认，不得进入 Zotero、分类或 Obsidian 阶段
- 输出至少覆盖：
  - 检索方案
  - 候选文献清单
  - 审核等待区
  - Zotero 结果
  - Obsidian 汇总表
- Obsidian 阶段输出的是文献汇总表，不是逐篇精读笔记
- 整个流程优先追求“高相关 + 高质量”

## 强制规则

### 1. 编码规则（Windows 优先）

如果在 Windows 环境中运行 shell、Python、JSON 或 CSV：

- 默认按 UTF-8 处理
- 中文标题、作者名、路径输出前，优先确认终端编码不会引发 `gbk codec` 或 `UnicodeEncodeError`
- 如果终端编码不稳定，优先写入 UTF-8 临时文件再读取，不要直接把大量中文打到不稳定终端

### 1.5. CNKI 访问修复规则（按需触发）

如果本轮将进入 `CNKI` 检索、详情页抓取或 PDF 下载，先做一次本地按需修复，再打开新的 CNKI 页面。

优先信号：

- `www.cnki.net` 出现证书错误
- `kns.cnki.net/kns8s/search` 返回 `418`

这些情况通常优先意味着：本地 CNKI 直连配置失效，而不是 skill 或关键词本身有问题。

执行原则：

- 只在本轮需要 CNKI 时触发
- 不要常驻后台轮询
- 修复后必须新开页面复测，不要沿用报错旧页

### 2. 技能调用规则

标准链路中优先复用现有 skill：

- 中文检索：`cnki-search`、`cnki-advanced-search`、`cnki-parse-results`、`cnki-paper-detail`、`cnki-download`
- 英文检索：`gs-search`、`gs-advanced-search`、`gs-cited-by`、`gs-fulltext`
- Zotero 管理：优先 `zotero-mcp`

禁止的默认替代方式：

- 用普通网页搜索代替 `cnki-*` / `gs-*`
- 手工拼接书目信息代替标准检索链
- 先只导入元数据，之后再回头补 PDF

允许 fallback 的条件：

- 对应 skill 或 `zotero-mcp` 明确不可用
- 已明确记录阻塞原因
- 已向用户说明为什么需要 fallback

### 3. Zotero 规则

用户确认保留名单后，Zotero 阶段必须优先使用可用的 Zotero 自动化路径进行：

- 目标 collection 确认
- 条目导入
- PDF 附件写入
- 结果回查

如果主路径不稳定，可改用本地 Connector 或其他等效本地路径，但必须保留结果核验。

### 4. PDF 规则

“成功入库”的定义是：

**条目已进入目标 Zotero collection，且 PDF 已附加到对应条目。**

因此：

- 没有 PDF 不算完成
- 不要先整批入库，再单独回头补全文
- 对保留文献，默认执行“元数据 + PDF”同轮处理

### 4.5. CNKI 下载入库最短路径（执行模板）

凡是执行“CNKI 检索后直接下载 PDF 并入 Zotero”的任务，优先按下面这条最短路径做：

1. 先在结果页筛出 `5-10` 篇高相关候选，再逐篇打开详情页
2. 每篇只在详情页点击一次 `PDF下载`
3. 下载后立刻检查真实下载目录，确认 PDF 已落到本地
4. 同轮完成：
   - 条目元数据整理
   - 本地 PDF 附件写入目标 Zotero collection
5. 写入完成后立即回查：
   - 条目是否在目标 collection 中
   - 该条目是否已有 PDF 附件
6. 再继续下一篇，不要把“下载”和“入库”拆成两批做

高效分工建议：

- `cnki-*`：检索、详情页定位、PDF 下载
- 本地 Zotero 写入路径：同轮写入“条目 + 本地 PDF 附件”
- `zotero-mcp`：确认目标 collection、回查条目与附件结果

目标闭环：

`结果页筛选 -> 详情页下载 -> 本地确认 -> 同轮入库 -> 立即回查`

默认避免的低效路径：

- 在结果页或错误页直接裸开下载链接
- 重复点击同一篇 `PDF下载`
- 检查错误下载目录
- 浏览器已经成功下载到本地后，再让脚本重复联网下载同一文件
- 把只有 metadata 没有 PDF 的条目当成完成

### 5. 效率规则

- 先批量，后逐篇
- 用户确认前不做全文下载和 Zotero 入库
- 用户确认后按保留名单一轮完成全文与入库
- 先去重，再导入 Zotero

## 执行流程

### Step 1：读取输入并重述

先提取并重述：

- 研究主题
- 研究对象
- 研究问题
- 学科语境
- 方法取向

如信息不足，最多补问 1-2 个关键问题；若仍可执行，则带着明确假设进入下一步。

### Step 2：关键词校准

至少区分：

- 核心词
- 同义词 / 替代表达
- 更学术化表达
- 邻近概念
- 易误检词

### Step 3：设计检索方案

输出：

- CNKI 主检索式
- Scholar 主检索式
- 纳入标准
- 排除标准
- 优先级标准

### Step 4：标准检索

显式调用：

- `cnki-*`
- `gs-*`

执行原则：

- 若本轮会进入 `CNKI`，先按需修复，再打开新的 CNKI 页面
- 先广后窄，但不要无上限扩张
- 结果页先批量判断，再对高优先级候选抓详情
- 需要 DOI、全文入口、被引信息时，只对 shortlist 抓取

### Step 4.5：滚雪球式检索

当首轮检索已经找到 1-3 篇明显高质量且高度相关的核心文献时，默认补做一轮滚雪球式检索。

目标：

- 扩展经典文献与关键理论链条
- 找到关键词未直接命中的高相关文献
- 识别共引文献

默认规则：

- 只围绕 1-3 篇核心文献做 1-2 轮，不无限扩张
- 英文侧优先用 `gs-cited-by` 做前向引文检索
- 同时结合后向引文检索
- 新命中文献仍需按相关性、质量、去重和排序规则重新判断

候选清单中应标明：

- `keyword`
- `snowball-forward`
- `snowball-backward`

### Step 5：候选清单与人工审核

输出候选文献清单并停止。

标准提示语：

`候选文献清单已生成。请先人工审核，并标记保留 / 删除 / 待核查。未获明确确认前，我不会进入 Zotero。`

### Step 6：确认后的“全文 + 入库”一体化处理

用户确认后，逐篇完成：

1. 确认目标 collection
2. 获取该篇 PDF
3. 导入条目并附加 PDF
4. 核验该条目确实位于目标 collection，且有 PDF

任一保留文献若缺 PDF，则该篇状态记为 `blocked`，并记录原因。

### Step 7：Zotero 分类与标签

默认保持轻量分类，不要过度细分。

最低限度：

- 一个项目主 collection
- 少量必要标签，例如：
  - 主题标签
  - `zh` / `en`
  - `A` / `B`
  - `theory` / `empirical` / `review`

### Step 8：Obsidian 汇总

Zotero 阶段结束后，再生成 Obsidian 用的结构化汇总表。

默认执行方式：

- 在目标 vault 中新建笔记
- 将结构化汇总表写入该笔记
- 对话框中只汇报笔记标题、路径、写入结果和 blocked 项

## 阻塞处理

以下情况必须显式报告：

- 编码错误
- Scholar CAPTCHA
- CNKI 验证或登录失效
- CNKI 证书错误
- CNKI 检索页 `418`
- Zotero 传输异常
- 条目导入成功但没有 PDF
- 条目类型明显不规范

标准处理原则：

- 先报告阻塞
- 再尝试同链路内修复
- 仍不行时才 fallback
