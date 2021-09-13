---
title: "Bubble Sort"
date: 2020-03-04T22:25:23+08:00
draft: false
---

> 又叫氣泡排序、泡沫排序，屬於**穩定排序**。
>
> 由左到右遍歷，當前元素與下一個元素比較，符合條件則兩兩將交換，依次推向數列的右端，就好像冒泡泡一樣，將排序結果一個一個浮上來。

![Sorting_bubblesort_anim](https://picbed.stdcdn.com/2021/09/0e20e19c7c415faa733ec4a1f942b36b.gif)

## Time & Space complexity

|  Case   | Time complexity  | Space complexity |
| :-----: | :--------------: | :--------------: |
|  Best   |       O(n)       |       O(1)       |
| Average | O(n<sup>2</sup>) |       O(1)       |
|  Worst  | O(n<sup>2</sup>) |       O(1)       |

## 實作
### 普通版

```php
function bubbleSort(array $nums) {
    $len = count($nums);
    for ($i = 0; $i < $len; $i++) {
        for ($j = 0; $j < $len - $i - 1; $j++) {
            if ($nums[$j] < $nums[$j + 1]) swap($nums[$j], $nums[$j + 1]);
        }
    }
    return $nums;
}

function swap(&$a, &$b) {
    $tmp = $a;
    $a = $b;
    $b = $tmp;
}
```



### 優化版

用一個變數去紀錄數列的狀態，如果內層迴圈迭代完，數字都沒有交換，表示數列已經是有序的，就中止迴圈:

```php
function bubbleSort(array $nums) {
    $len = count($nums);
    for ($i = 0; $i < $len; $i++) {
        $isSorted = true;
        for ($j = 0; $j < $len - $i - 1; $j++) {
            if ($nums[$j] < $nums[$j + 1]) {
                swap($nums[$j], $nums[$j + 1]);
                $isSorted = false;
            }
        }
        if ($isSorted) break;
    }
    return $nums;
}

function swap(&$a, &$b) {
    $tmp = $a;
    $a = $b;
    $b = $tmp;
}
```

