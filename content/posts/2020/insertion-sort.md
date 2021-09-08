---
title: "Insertion Sort"
date: 2020-03-04T22:59:24+08:00
draft: true
---

# Insertion Sort

> 又叫插入排序，屬於**穩定排序**。
>
> 就好像玩撲克牌整理牌組，將未排序的牌堆插入已排序的牌堆那樣，如果在大部分的元素已有序，使用此排序法效率較好。

![sorting-insertion-sort](https://picbed.stdcdn.com/2021/09/3ca2435acd8cbc3a61e253e3d6a20ac1.gif)

|  Case   | Time complexity  | Space complexity |
| :-----: | :--------------: | :--------------: |
|  Best   |       O(n)       |       O(1)       |
| Average | O(n<sup>2</sup>) |       O(1)       |
|  Worst  | O(n<sup>2</sup>) |       O(1)       |



```php
function insertionSort(array $nums) {
    $len = count($nums);
    for ($i = 1; $i < $len; $i++) {
        $temp = $nums[$i];
        for ($j = $i; $j > 0 && $nums[$j - 1] > $temp; $j--) {
            $nums[$j] = $nums[$j - 1];
        }
        $nums[$j] = $temp;
    }
    return $nums;
}
```

