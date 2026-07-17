# 科研主线工作流
本工作流目的是想让科研思想从一个模糊概念进化到一份完整的项目文件
这套配置只保留三次交接：Chat 交付 Idea，Work 交付实现任务或研究报告，Codex 交付训练证据。

## 一次性配置

1. 在 ChatGPT 的“科研”项目设置中，用 `Chat项目指令.md` 的全文替换现有项目指令。
2. 从项目来源中删除 `科研工作流SOP_v1.md` 和 `视觉动作研究_思路创新闭环SOP_v1.md`。两者的有效约束已合并进精简指令，继续保留只会重复占用上下文；它们不属于当前有效配置，因此不复制到本目录。
3. 把 `Work主线指令.md` 添加为该项目来源。进入 Work 工作时，明确要求它遵循此文件。
4. 选定基线仓库后，把 `Codex主线AGENTS.md` 复制到仓库根目录并改名为 `AGENTS.md`。若已有 `AGENTS.md`，合并内容，不要覆盖仓库原约定。

## 启动与交接

Chat 首次启动：

> 请遵循项目指令，围绕以下模糊方向开始闭环 Idea：……。当前已有观察/约束：……。先识别最关键的未知与原因假设，不要提前设计代码。

实验后返回 Chat：

> 请基于 `RESEARCH_REPORT_vNNN.md` 修正当前 Idea。先判断哪些证据改变了原因假设，再生成新的 `IDEA_vNNN.md`；闭环未成立则继续讨论。

Work 选择基线并设计落地：

> 请遵循 `Work主线指令.md` 的模式 A，分析 `IDEA_vNNN.md`，核实候选基线并输出下一版 `CODEX_TASK_vNNN.md`。只生成一份任务文件。

Codex 实现和运行：

> 请遵循仓库根目录 `AGENTS.md`，执行 `CODEX_TASK_vNNN.md`。先复现和冒烟测试，再实现、训练与评估；完成后输出版本化 `TRAINING_PACKET_vNNN_r01.md` 及最小必要附件。

Work 分析训练数据包：

> 请遵循 `Work主线指令.md` 的模式 B，分析 `TRAINING_PACKET_vNNN_rRR.md`。若值得继续，输出下一版 `CODEX_TASK_vNNN.md`；否则输出下一版 `RESEARCH_REPORT_vNNN.md` 交回 Chat。只生成一种交付物。

## 文件版本

| 文件 | 产生者 | 规则 |
|---|---|---|
| `IDEA_vNNN.md` | Chat | 三位版本号，递增且不覆盖 |
| `CODEX_TASK_vNNN.md` | Work | 独立递增，精确引用 Idea/数据包 |
| `TRAINING_PACKET_vTTT_rRR.md` | Codex | 任务版本 + 两位运行号 |
| `RESEARCH_REPORT_vNNN.md` | Work | 独立递增，供 Chat 修正思路 |

大文件、权重和完整日志留在训练环境；跨窗口只传当前阶段需要的最新版 Markdown 和少量诊断附件。
