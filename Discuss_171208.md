# 智慧醫療雲 - 睡眠呼吸中止症的判斷及醫療建議
## Functional Description
1. 透過手機的資訊分析病人是否碰到疑似睡眠障礙問題　<br>
例：從對話紀錄、搜尋紀錄得知病人最近是否碰到疑似症狀。

2. 透過睡眠資訊判斷病人是否有睡眠呼吸中止症 ( Possibility ) <br>
例：從 apnea module 判斷病人整晚睡眠發生幾次CSA, OSA, Hypopenea ，並判斷具有輕度、中度或重度風險。

3. 透過手機的資訊分析病人的生活習慣是否造成 sleep apnea <br>
例：病人是否熬夜，飲食習慣。

4. 透過病歷與生活習慣、手機資訊交叉比對病因 <br>
例：是否飲食造成過重而致sleep apnea, 是否因天氣影響氣管收縮。

5. 透過病因與症狀判斷是否有潛在其他病症
例：有沒有高血壓、心血管疾病風險。

6. 根據結果提供求醫建議 <br>
例：掛號科別、檢查項目。

7. 根據病症、病歷、與生活習慣給予醫生治療建議 <br>
例：是否在睡眠中心詳細監測整晚睡眠訊號、是否指示病人改變生活習慣、開藥建議。

8. 提供語音對話問診建議 <br>
例：透過語音問答了解病人病徵，並給予正確病症相關知識。

9. 針對環境與病人狀況給予生活建議 (警示) <br>
例：飲食熱量提醒、天氣是否太冷需要早歸。

---
## Issue - It's all about Data

### Big Data issues - 4V's

1. **Volume 資料量** <br>
  紀錄病人的各種活動、文字、影像需要非常大量的取樣資料 (sample/reference) 和測試 (test) 資料。

2. **Variety 資料多元性**<br>
  Struct data - 病歷、睡眠測試結果 (From DSP module) 、病人活動資訊 (From mobile) <br>
  Non-structured data - Text. image. voice. metadata

3. **Velocity 資料即時性**<br>
  病人資料進來後，要能即時分析，除了回饋以外，要能自我學習，把不必要的資料清空 (Clean up)，將有用的資訊保存

4. **Veracity 資料正確性**<br>
  必須嚴謹挑選 sample data ，需要判斷資料是否是我們需要的資訊，資料是否有假，資料是否有異常值 [1]

---
## IBM Big Data Analytics in The Cloud -<br> Cloud Customer Architecture for Big Data and Analytics

Cloud Customer Architecture for Big Data and Analytics [2] 是一個由 Cloud Standards Customer Council (CSCC) [3] 提出來的大數據分析的架構。其架構由3個網路組成，包括 Public Network. Provider Cloud 和 Enterprise Network 。 IBM 的，主要 solution 就是使用此架構 [4]。


![](./image/arch1.jpg)

### Public Network

資料會從 User 端的 SaaS Application ，或是從公共資源中，透過 Edge Services ，將資料輸入。在這裡，我們可以理解 SaaS 就是使用者的 App ，而 Edge Services 簡單來說就是一個 protocal/firewall/load balancer ，確定好資料是從 user 端來的，同時也確定好資料要往哪個伺服器運送。

### Provider Cloud

資料進來後，會分成兩種類型處理

#### Streaming Computing

![](./image/stream.jpg)

Stream Computing 可以從各樣的輸入取得/處理大量、高度動態，且有時效性、持續的數據流 (stream)，以我們使用的例子而言，就是病人的呼吸訊號監測、病人平日的活動監測，或是病人的問診系統。

Stream Computing 包含兩個特點
1. **Real-time analytical processing** <br>
以最低延遲對於儲存進來的資料做分析和決策。
2. **Data augmentation** <br>
將資料過慮後放進 Data integration 作更進一步的 background 分析。

Stream Computing 要能隨著使用量或速度的需求增加/減少使用量。

#### Data Integration

<img src="./image/integration.jpg" width="25%" height="25%">

Data Integration 從各種不同的來源複製資訊，並能讓不同的資訊間產生關聯 (correlates information) ，一個完整的 Data integration 必須要能發現數據來源的特徵 (characteristics)，清理、監控、轉換，和運送 data 。其功能應包括

1. **Data stagging** <br>
將 data 轉換成適合的格式交給下游處理
2. **Data quality** <br>
清理和組織 data ，以便消除冗餘 (redundancies) 和不一致性 (inconsistencies) ，讓 data 滿足使用者的需求。
3. **Provisioning** <br>
轉換、管理以及將 data 交給適合的目標， provisioning 可以在不同的 data repositories 移動 data ，從 data source 轉移 data 出來/進入 (to/from) 。
4. **Entity services** <br>
從不同的來源匹配 data ，以便為關鍵實體 (key entities) 提供更完整的視野 (view) 。

#### Data Repositories

<img src="./image/repo.jpg" width="25%" height="25%">

Data Repositories 是 data 主要儲存的儲存庫，可以使用不同的平台，例如： Hadoop, NoSQL 。儲存在儲存庫中的 data 有可能來自遺留的 (legacy) 、新的、串流來源、企業的應用程式、企業的資料、已清理或是從串流分析輸出的資料。

Data repositories 包含以下幾個類型：

1. **Catalog** <br>
來自 discovery 和 IT 資料組織的結果建立一個目錄，來提供一個反應信息 (information) 的視角 (view) 。Big data 的引入使得資料庫對於儲存資料的內容、分類、所有權、信息的相關性需求增加，從這個目錄，使用者可以控制資料的使用。

2. **Data virtualization** <br>
允許應用程式可以快速的 (Agile) 檢索和操作資料，而不需要關於資料的技術細節、落地、探索和歸檔：允許使用各種工具來儲存、探索和擴充大型的資料集合。因為大規模和非結構性 (non-structured) 的資料引入，意味著"在資料輸入前就設計資料庫"的這個方法已經不再可行。資料可以用於存檔，可以藉由分散在各個儲存空間的副本，來獲得更高的可靠性和恢復能力。

3. **Deep analytics and modeling**<br>
應用統計模型可以從非結構化和半結構化 (semi-structured) 的大型資料集合中獲得信息。深度分析從　PB(petabytes) 和 EB(Exabytes) 中取得精確的結過。 未來在即時的或接近即時性的 (near real-time) 的反應需求會越來越普遍。

4. **Interactive analysis and reporting**<br>
針對自助資料訪問可視化，用應用程式操作 API 訪問資料庫。

5. **Data warehousing**<br>
歷史資料、摘要資料或是其他來源的資料儲存的地方，通常會放主題導向的、非揮發性的時序資料 (time-series data) ，這些資料可以用於企業決策。通常工作量是密集的，會訪問數百萬條來方便掃描、合併和聚合，吞吐量 (throughput) 和反應時間通常是最優先考量。

####  Analytics Discovery & Exploration

<img src="./image/discovery.jpg" width="25%" height="25%">

1. **Self-service** <br>
用戶能夠自己註冊，訪問來自分析系統的輸出，能自己定義分析處理。

2. **Visualization** <br>
用戶可以自行建立儀表板來探索資料庫，可以操作觀察數據。

3. **Data preparation** <br>
使用戶能將資料從原始型式轉換成更容易分析的格式。

4. **Sandbox** <br>
把資料複製到一個私有區域來進行沙盒實驗。

#### Deployed Analytics

<img src="./image/deployed.jpg" width="25%" height="25%">

Deployed Analytics 是一個 anylistcs applications 的集合，其用來
* 基於分析的決策管理，使組織能夠制定經過分析的自動化決策。
* 預測分析服務，從現有的資訊和資料來識別模型 (patterns) ，預測未來趨勢。
* 分析並向管理者報告和操作資料庫。
* 內容分析服務，讓使用者觀察並理解結構化和非結構化的資料。公司內大部分的訊息被作為非結構化資料來維護，例如文件、資料庫中的本文片斷、 Wikis 等內容。
* 計劃和預報 (forecasting) 未來的場景。


### Enterprise Network

Enterprise network 包含了 enterprise applications ，以及 enterprise data <br>
<img src="./image/enterprise.jpg" width="25%" height="25%">

#### Enterprise Data

Enterprise Data 承載著應用程式裡面的關鍵資料，包含

1. **Reference data**
提供有效值或查找資料（例如：zip code）。

2. **Maser data**
儲存關鍵實體的屬性 (attributes) ，例如：帳戶資料。

3. **Transactional data**

4. **Application data**

5. **Log data**

6. **Enterprise content data**

7. **Historical data**


### Overview
![](./image/overview.jpg)

---
## Azure solution for Big Data Analytics

![](./image/azure1.png)

![](./image/azure2.png)

Azure 也有對於 Big data analytics 的 solution [5],[6]，與 CSCC 提出架構有部份相同，例如資料進來後也分成　straming comuting 和 data integration，但剩下的部份，在 Azure 中是較沒有架構，不過看起來所有的 components 都可以在 Azure marketplace 找到，也就是說,只要有 CSCC 的架構， Azure 也能兜出一樣的 Big data anylitics cloud 。

另外，目前 CSCC 提出的 Cloud Customer Architecture for Big Data and Analytics 目前是 V2.0 ，如果你上他們的網站的話，就會看到在 12/19 他們即將發佈 V3.0 的架構。

---
## Reference

[1] [大數據到底是什麼意思？事實上，它是一種精神！](https://hellolynn.hpd.io/2017/06/09/)

[2] [Cloud Customer Architecture for Big Data and Analytics V2.0](http://www.cloud-council.org/deliverables/CSCC-Cloud-Customer-Architecture-for-Big-Data-and-Analytics.pdf)

[3] [Cloud Standards Customer Council](http://www.cloud-council.org/)

[4] [How IBM leads in building big data analytics solutions in the cloud](https://www.ibm.com/developerworks/cloud/library/cl-ibm-leads-building-big-data-analytics-solutions-cloud-trs/index.html#N10315)

[5] [Understanding Microsoft big data solutions](https://msdn.microsoft.com/zh-tw/library/dn749804.aspx)

[6] [巨量資料架構樣式](https://docs.microsoft.com/zh-tw/azure/architecture/guide/architecture-styles/big-data)
