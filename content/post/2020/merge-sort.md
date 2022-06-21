---
title: "Merge Sort"
date: 2020-03-29T17:33:15+08:00
draft: false
tags: ["algorithm"]
---

> 合併排序，屬於穩定排序。
> 
> 把數列從中間拆分成兩段，直到不能再分，將拆分的元素兩兩比對後再合併起來，達到排序效果。

![sorting-merge-sort](https://picbed.stdcdn.com/2021/09/b64ab5ccf26c4a2373be9013496cc8d8f0599985b402f7de0c2b0e0c109b368c.gif)

## Time & Space complexity

|  Case   | Time complexity | Space complexity |
| :-----: | :-------------: | :--------------: |
|  Best   |    O(nlogn)     |       O(1)       |
| Average |    O(nlogn)     |       O(1)       |
|  Worst  |    O(nlogn)     |       O(1)       |

## 實作
```php
/**
 * 主程式
 * 定義數列要排序的開頭及結尾
 */
function mergeSort(array $nums)
{
    $front = 0;
    $end = count($nums) - 1;
    MSort($nums, $front, $end);
    return $nums;
}

/**
 * 遞迴將數列兩半拆分
 */
function MSort(array &$nums, $front, $end)
{
    if ($front < $end) {
        $mid = intval(($front + $end) / 2);
        MSort($nums, $front, $mid); // 拆分左半邊的數列
        MSort($nums, $mid + 1, $end); // 拆分右半邊的數列
        merge($nums, $front, $mid, $end);
    }
}

/**
 * 將左右兩邊的數列比大小後再合併
 */
function merge(array &$nums, $front, $mid, $end)
{
    $len = ($end - $front) / 2 + 1;
    $leftNums = array_slice($nums, $front, $len);
    $rightNums = array_slice($nums, $mid + 1, $len);

    $left[] = PHP_INT_MAX;
    $right[] = PHP_INT_MAX;
    $idxLeft = 0;
    $idxRight = 0;

    for ($i = $front; $i <= $end; $i++) {
        if ($leftNums[$idxLeft] < $rightNums[$idxRight]) {
            $nums[$i] = $leftNums[$idxLeft];
            $idxLeft++;
        } else {
            $nums[$i] = $rightNums[$idxRight];
            $idxRight++;
        }
    }
}
```

## Reference

- [示意圖](https://www.796t.com/article.php?id=90205)