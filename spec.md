# Functional Description
1. 透過手機的資訊分析病人是否碰到疑似睡眠障礙問題　<br>
例：從對話紀錄、搜尋紀錄得知病人最近是否碰到疑似症狀。
2. 透過睡眠資訊判斷病人是否有睡眠呼吸中止症 ( Possibility ) <br>
例：從 apnea module 判斷病人整晚睡眠發生幾次CSA, OSA, Hypopenea ，並判斷具有輕度、中度或重度風險。
3. 透過手機的資訊分析病人的生活習慣是否造成 sleep apnea <br>
例：病人是否熬夜，飲食習慣。
4. 透過病歷與生活習慣、手機資訊交叉比對病因
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

```
Input:
  struct {                // from DCIC Lab module
    一整晚睡眠的 state <list>
      Normal, CSA, OSA, Hypopenea
      Time
    病人睡眠時間 (sleep, wake) <list> //測試當晚
      Time
  }
  struct {                // from hospital
    Sex
    Age
    Weight
    Medical history <list>
      慢性病：
        過敏、COPD 、糖尿病、高血壓 ... etc.
    藥物過敏
  }
  non_struct {            // from mobile
    voice
    text
    search
    sleep/wake //平日
    activity // 出門、回家
    exercise // 運動習慣
    walk //走幾步路
    eat
		weather

  }
```

功能（要描述）
scenario. functional

```
Output:
  Sleep Apnea (normal, mild, moderate, severe) possibility
  Etiology <list> // 病因
  Correlated diseases <list>
  Cure advices <list>
```
