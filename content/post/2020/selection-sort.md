---
title: "Selection Sort"
date: 2020-03-04T23:10:55+08:00
draft: false
---

> 選擇排序，屬於**不穩定排序**。
>
> 由左到右遍歷整個數列，找到最大(或小)元素，與當前的元素交換。



![sorting-selectoin-sort](https://picbed.stdcdn.com/2021/09/0a6d643aeee78b785b8c7b60b8bc9b51.gif)

## Time & Space complexity

|  Case   | Time complexity  | Space complexity |
| :-----: | :--------------: | :--------------: |
|  Best   | O(n<sup>2</sup>) |       O(1)       |
| Average | O(n<sup>2</sup>) |       O(1)       |
|  Worst  | O(n<sup>2</sup>) |       O(1)       |



---

## 實作

```php
function selectionSort(array $nums) {
    $len = count($nums);
    for ($i = 0; $i < $len; $i++) {
        $max = $i;
        for ($j = $i + 1; $j < $len; $j++) { // 找出最大值的 index
            if ($nums[$j] > $nums[$max]) $max = $j;
        }
        if ($nums[$max] > $nums[$i])		// 最大值如果大於當前的元素
            swap($nums[$max], $nums[$i]);	// 就兩兩交換
    }
    return $nums;
}

function swap(&$a, &$b) {
    $tmp = $a;
    $a = $b;
    $b = $tmp;
}
```

---

## 補充說明

關於**不穩定排序**，如果數列中出現元素的數值相同的情況，經過排序後，這些同元素的**相對位置**可能會與排序前不同。

例如：數列  `3,2,3,1`，由小到大排序結果為 `1, 2, 3, 3`

這個結果看起來是沒錯的，但如果排序要求更嚴格的話，就不適合使用此排序法

為什麼呢？

以上述例子，將重複元素 `3` 作記號，排序前是這樣

`3', 2, 3, 1`

由小到大排序完畢後，期望得到的結果是這樣

 `1, 2, 3', 3`

但使用選擇排序的話，實際結果卻是

 `1, 2, 3, 3'`

`3'` 和 `3` 的相對位置在排序後改變了，因此稱作不穩定排序。