---
layout: default
title: 버즐정렬(bubble-sort)
parent: 알고리즘(Algorithm)
has_children: tru
nav_order: 1
---
{: .no_toc }
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# 버블정렬(Bubble Sort)

> 버블 정렬은 두 숫자씩 비교하면서 정렬을 수행하는 정렬 알고리즘입니다.  
매 반복마다 인접한 두 숫자를 비교하여 순서가 잘못된 경우 위치를 교환합니다.  
아우터 루프(outer loop)가 한 번 실행될 때마다 한 자리수가 결정됩니다.

## 예시
loop1:

| <span style="color:red"> 6 </span> | <span style="color:red"> 2 </span>  | 8 | 4 | 10 |  
|:-----------------------------------|:------------------------------------|:--|:--|:---|

| 2 | <span style="color:red"> 6 </span>  | <span style="color:red"> 8 </span> | 4 | 10 |  
|:--|:------------------------------------|:-----------------------------------|:--|:---|

| 2 | 6 | <span style="color:red"> 8 </span> | <span style="color:red"> 4 </span> | 10 |  
|:--|:--|:-----------------------------------|:-----------------------------------|:---|

| 2 | 6 | 4 | <span style="color:red"> 8 </span> | <span style="color:red"> 10 </span> |  
|:--|:--|:--|:-----------------------------------|:------------------------------------|

| 2 | 6 | 4 | 8  | <span style="color:blue"> 10 </span> |  
|:--|:--|:--|:---|:-------------------------------------|

loop2

| <span style="color:red"> 2 </span> | <span style="color:red"> 6 </span> | 4 | 8  | <span style="color:blue"> 10 </span> |  
|:-----------------------------------|:-----------------------------------|:--|:---|:-------------------------------------|

...

---
table test purpose:

| 2 | 6 | 4 | 8  | 10 |
|:--|:--|:--|:---|:---|
| a | d | d | d  | f  |

---

---

## 코드
```java
public class Test {

    static int[] a = {6, 2, 8, 4, 10};

    public static void main(String[] args) {

        int n = a.length;

        // outer loop
        for(int i = 0; i < n; i++) {

            // inner loop
            for(int j = 0; j < n - 1 - i; j++){
                if (a[j + 1] < a[j]) swap(a, j+1, j);
            }
        }

        for(int i : a) System.out.print(i + " "); // 2 4 6 8 10
    }

    public static void swap(int a[], int first, int second) {
        int temp = a[first];
        a[first] = a[second];
        a[second] = temp;
    }
}

```
