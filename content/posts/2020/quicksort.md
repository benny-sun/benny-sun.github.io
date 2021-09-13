---
title: "Quicksort"
date: 2020-03-05T23:46:25+08:00
draft: false
---

# Quicksort

> 快速排序，屬於**不穩定排序**。
>
> 運用分而治之思想 (Divide and Conquer) 來優化排序效率。

![sorting-quicksort](https://picbed.stdcdn.com/2021/09/63bdbe25896c2e78e98c77ddf252a364.gif)

#### Divide

在數列中選定任意一元素當作基準點，叫它 `pivot`；將小於 `pivot` 的數字放在左側，大於 `pivot` 的數字放右側，這個行為稱作 **Partition**。

#### Conquer

最後數列被分為大小兩堆，將這兩堆數列重複 **Divide** 操作，達到排序效果。



|  Case   | Time complexity  | Space complexity |
| :-----: | :--------------: | :--------------: |
|  Best   |     O(nlogn)     |       O(1)       |
| Average |     O(nlogn)     |       O(1)       |
|  Worst  | O(n<sup>2</sup>) |       O(1)       |



## 方法一

固定取數列的最後一個數值當作`pivot`(不一定要最後，可任意選)，**由左至右掃描數列**

```php
/**
 * 主程式
 * 定義數列的排序範圍
 */
function main(array $nums) {
    $front = 0;
    $end = count($nums) - 1;
    quickSort($nums, $front, $end);

    return $nums;
}

/**
 * Divide and Conquer
 * 遞迴將數列分為兩堆
 */
function quickSort(array &$nums, int $front, int $end) {
    if ($front < $end) {
        $pivot = partition($nums, $front, $end); // Divide
        quickSort($nums, $front, $pivot - 1); // Conquer
        quickSort($nums, $pivot + 1, $end);
    }
}

/**
 * 將數列分為左右兩堆
 * $i 表示「pivot 左邊數列最後一位」的 index
 * $j 走訪每個元素並跟 pivot 比大小
 * index $i, $j 都由左至右移動
 */
function partition(array &$nums, $front, $end) {
    $i = $front - 1;
    for ($j = $front; $j < $end; $j++) {
        if ($nums[$j] < $nums[$end]) {  // 若當前元素大於pivot
            $i++;                       // 則 index $i 往前走一步
            swap($nums[$i], $nums[$j]); // 並與該元素交換
        }
    }
    $i++;                           
    swap($nums[$i], $nums[$end]); // 把 pivot 移到數列中間(形成左小右大)

    return $i;
}

function swap(&$a, &$b) {
    $tmp = $a;
    $a = $b;
    $b = $tmp;
}
```

## 方法二

修改 `partition()`，選擇數列中間的數當作`pivot`(不一定要中間，可任意選)，**頭尾兩端向數列中間掃描**

```php
/**
 * 兩個 pointer $front, $end 分別從數列頭尾相向出發，並跟 pivot 比較
 * 符合條件時 $front, $end 兩兩交換值
 */
function partition(array &$nums, int $front, int $end)
{
    $pivot = $nums[($front + $end) / 2];
    while ($front < $end) {
        while ($nums[$front] < $pivot) $front++;
        while ($nums[$end] > $pivot) $end--;
        if ($front < $end) swap($nums[$front], $nums[$end]);
    }

    return $end;
}
```
