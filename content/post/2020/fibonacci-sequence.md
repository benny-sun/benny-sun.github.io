---
title: "Fibonacci Sequence"
date: 2020-03-06T22:25:05+08:00
draft: false
---



> 費波那契數列、斐氏數列、黃金分割數列。
>



> 又稱費波那契數列、斐氏數列、黃金分割數列。
>
> 又從 `0` 和 `1` 開始，之後的每個數字都是前兩個數字相加的結果
>
> 例如：`0, 1, 1, 2, 3, 5, 8, 13, 21...`

$$
F_n = F_{n-1} + F_{n-2} \quad (n \geq 2)
$$

![Fibonacci-Spiral](https://picbed.stdcdn.com/2021/09/4aa9589fd482949c70b09135229d67113af40f766e1b3f7cb5535b956bb116e1.png)

## 求第 n 項費波那契數

### 遞迴 (Recursion)

```php
function fib($n) {
    if ($n <= 1) return $n;
    
    return fib($n - 1) + fib($n - 2);
}
```

| Time complexity  | Space complexity |
| :--------------: | :--------------: |
| O(n<sup>2</sup>) |       O(n)       |

###  迭代 (Iteration)

```php
function fib($n) {
    if ($n == 0) return 0;
    $p1 = 0;
    $p2 = 1;
    for ($i = 2; $i <= $n; $i++) {
        $tmp = $p1 + $p2;
        $p1 = $p2;
        $p2 = $tmp;
    }
    
    return $p2;
}
```

| Time complexity | Space complexity |
| :-------------: | :--------------: |
|      O(n)       |       O(1)       |

### 動態規劃 (Dynamic programming)

```php
function fib($n) {
    $result = [];
    $result[0] = 0;
    $result[1] = 1;
    for ($i = 2; $i <= $n; $i++) {
        $result[$i] = $result[$i - 1] + $result[$i - 2];
    }
    
    return $result[$n];
}
```

| Time complexity | Space complexity |
| :-------------: | :--------------: |
|      O(n)       |       O(n)       |

### 黃金比例公式

$$
\varphi = \frac{1+\sqrt5}{2} \approx 1.618...
$$

$$
F_n = \frac{\varphi^n}{\sqrt5} - \frac{(1-\varphi)^2}{\sqrt5}
$$



```php
function fib($n) {
    $phi = (1 + sqrt(5)) / 2;
    
    return pow($phi, $n) / sqrt(5) - pow(1 - $phi, $n) / sqrt(5);
}
```

| Time complexity | Space complexity |
| :-------------: | :--------------: |
|      O(1)       |       O(1)       |



## Reference

- [費波那契數 wikipedia](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0)
- [黃金分割率 wikipedia](https://zh.wikipedia.org/wiki/%E9%BB%84%E9%87%91%E5%88%86%E5%89%B2%E7%8E%87)
- [Mathematics in R Markdown](https://rpruim.github.io/s341/S19/from-class/MathinRmd.html)
