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

1. Volume 資料量 <br>
紀錄病人的各種活動、文字、影像需要非常大量的取樣資料 (sample/reference) 和測試 (test) 資料。
2. Variety 資料多元性<br>
  Struct data - 病歷、睡眠測試結果 (From DSP module) 、病人活動資訊 (From mobile) <br>
  Non-structured data - Text. image. voice. metadata
3. Velocity 資料即時性<br>
  病人資料進來後，要能即時分析，除了回饋以外，要能自我學習，把不必要的資料清空 (Clean up)，把有用的資訊保存下來
4. Veracity 資料正確性<br>
  必須嚴謹挑選 sample data ，需要判斷資料是否是我們需要的資訊，資料是否有假，資料是否有異常值


---
## Reference
[大數據到底是什麼意思？事實上，它是一種精神！](https://hellolynn.hpd.io/2017/06/09/)