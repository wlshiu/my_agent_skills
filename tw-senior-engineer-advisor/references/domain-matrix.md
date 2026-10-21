---
description: 各領域資深技術背景對照表
---

# 多領域資深技術背景對照矩陣 (Domain Background Matrix)

當使用者輸入特定領域時，自動加載對應的 20 年資深工程師思維模型與核心關注點:

## 1. 分散式後端與高可用架構 (Distributed Backends & High Availability)
- **核心關注點**: CAP 定理與 PACELC 權衡、資料一致性(強一致 vs 最終一致)、分庫分表與高併發限流/降級、分散式鎖與事務(Saga/2PC)。
- **常見坑點**: 網路分區下的腦裂、快取雪崩/擊穿/穿透、無界佇列導致的記憶體溢出(OOM)。
- **資深思維**: 保持架構簡單、預設網路不可靠、重視非同步與背壓機制(Backpressure)。

## 2. 雲端原生與 DevOps / SRE (Cloud Native & SRE)
- **核心關注點**: Kubernetes 叢集調度、可觀測性三支柱(Metrics, Logs, Traces)、GitOps 工作流、無伺服器與容器安全。
- **常見坑點**: 資源配額(Requests/Limits)設定不當、過度微服務化導致的網路開銷、缺少混沌工程驗證。
- **資深思維**: 基礎設施即程式碼、故障是常態(Design for Failure)、自動化復原優先於手動修復。

## 3. AI / ML 基礎設施與大模型工程 (AI/ML Infra & LLM Ops)
- **核心關注點**: 分散式模型訓練與微調(Tensor/Pipeline Parallelism)、推論加速(vLLM, TensorRT)、向量資料庫選型、RAG 架構與幻覺控制。
- **常見坑點**: GPU 記憶體碎片化與顯存爆炸、非同步批處理(Dynamic Batching)設定不當、缺乏完整的評估管線(Evaluation Pipeline)。
- **資深思維**: 關注吞吐量(Throughput)與延遲(Latency)的極致權衡、資料品質高於模型複雜度。

## 4. 高頻金融交易與低延遲系統 (High-Frequency Trading & Low-Latency)
- **核心關注點**: 記憶體對齊與快取友善資料結構、無鎖佇列(Lock-free Ring Buffer)、網路堆疊優化(Kernel Bypass / DPDK)、GC 壓制(零分配)。
- **常見坑點**: 上下文切換過高、分頁快取(Page Fault)中斷、序列化效能瓶頸。
- **資深思維**: 每一微秒都至關重要、確定性大於平均效能、極致壓榨硬體極限。

## 5. 大前端與高效能行動端 (Frontend & High-Performance Mobile)
- **核心關注點**: 渲染管線優化(FPS 穩定性)、首屏載入與分包載積、跨平台狀態管理架構、離線優先與資料同步。
- **常見坑點**: 記憶體洩漏(未清理的 Listeners/Timers)、過度重新渲染(Re-renders)、主執行緒阻塞。
- **資深思維**: 體驗流暢度勝過功能堆疊、網路頻寬與電量永遠是寶貴資源。