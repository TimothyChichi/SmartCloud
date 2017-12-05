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
  }
```

```
Output:
  Sleep Apnea (normal, mild, moderate, severe)
  Etiology <list> // 病因
  Correlated diseases <list>
  Cure advices <list>
```
