```
Input:
  1. 胸腹三軸加速器 (XYZ *2)
  2. 血氧濃度

  技師判斷結果
  錄影錄音
  心電圖
  腦電圖
  肌電圖
  呼吸氣流訊號

Output:
  一整晚睡眠的 state list
    Normal, CSA, OSA, Hypopenea
    Time

  病人睡眠時間 (sleep, wake) list
    Time
```
> 技師判斷是一晚發生次數 state ，這個標準 ( event condition, 分級) 會一直更新
> Hypopenea - 淺呼吸，50%
> OSA - 完全阻塞
> CSA - 中樞神經

>睡眠呼吸中止症生率為： 14% 男性成人 5% 女性成人

Reference: P. E. Peppard, T. Young, J. H. Barnet, M. Palta, E. W. Hagen, and K. M. Hla, “Increased prevalence of sleep-disordered breathing in adults,” AmJ Epidemiol., vol. 177, no. 9, pp. 1006–1014, 2013
