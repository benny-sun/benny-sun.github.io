---
title: "Heapsort"
date: 2020-03-29T23:30:16+08:00
draft: false
---

> 又叫堆積排序，屬於穩定排序。

## Time & Space complexity

|  Case   | Time complexity | Space complexity |
| :-----: | :-------------: | :--------------: |
|  Best   |    O(nlogn)     |       O(1)       |
| Average |    O(nlogn)     |       O(1)       |
|  Worst  |    O(nlogn)     |       O(1)       |

## 實作

```php
/**
 * 主函式
 * 將數列由小到大排序
 */
function heapSort(array $array) {
    buildMaxHeap($array);
	$length = count($array);
    for ($i = $length - 1; $i > 0; $i--) {
        swap($array[0], $array[$i]);
        maxHeapify($array, 0, $i);
    }
    return $array;
}

/**
 * 有 child 的節點進行 heapify
 * (因為堆排不考慮 leaf 節點之間的大小)
 */
function buildMaxHeap(array &$array) {
    $length = count($array);
    for ($i = $length / 2; $i >= 0; $i--) {
        maxHeapify($array, $i, $length);
    }
}

/**
 * 由上而下檢查 subtree，使 subtree 滿足 max heap 規則
 * @param array $array 紀錄 heap
 * @param integer $root 當前 subtree 的根節點 index
 * @param integer $length 要處理的陣列長度，也是判斷child是否超出陣列長度
 */
function maxHeapify(array &$array, int $root, int $length) {
    $left = 2 * $root + 1;
    $right = $left + 1;
    $largest = $root; // 紀錄「根、左、右」，值最大的節點 index

    if ($left < $length && $array[$left] > $array[$root])
        $largest = $left;

    if ($right < $length && $array[$right] > $array[$largest])
        $largest = $right;

    if ($root != $largest) {                    // 若根節點不是三者中最大的
        swap($array[$root], $array[$largest]);  // 就與最大那個節點調換
        maxHeapify($array, $largest, $length);
    }
}

/**
 * 數值交換
 */
function swap(&$a, &$b) {
    $tmp = $a;
    $a = $b;
    $b = $tmp;
}
```

