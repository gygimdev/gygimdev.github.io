---
layout: default
title: 버블정렬(bubble-sort)
parent: 알고리즘(Algorithm)
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

## 특징
### 안정 정렬
동일한 값의 요소들의 순서가 보장된다.  
### 제자리 정렬
추가적인 메모리 공간을 사용하지 않고 주어진 배열 내에서
요소의 위치를 변경하여 정렬하는 알고리즘

## 시간 복잡도
> 버블정렬의 시간복잡도는 O(n^2)

배열의 길이가 n일 때, 아우터 루프 마다 n-i 번의 연산이 일어 나고 이를 풀어서 타나내면
(n-1) + (n-2) + ... + 2 + 1 이런 형식으로 나타낼 수 있습니다.
좀더 쉽게 풀어서 설명한다면(n이 5일 때),

n이 5일 때:  
o o o o x  
o o o x x  
o x x x x

(n-1) + (n-2) + ... 2 + 1 = n(n-1)/2 = (n^2-n)/2  
(5-1) + (5-2) + (5-3) + (5-4) = 5(5-1)/2 = (5^2-5)/2  
임으로 시간복잡도는 O(n^2)가 됩니다.

## 예시
loop1:

<table>
  <tr>
    <th><span style="color:red;">6</span></th>
    <th><span style="color:red;">2</span></th>
    <th>8</th>
    <th>4</th>
    <th>10</th>
  </tr>
</table>

<table>
  <tr>
    <th>2</th>
    <th><span style="color:red;">6</span></th>
    <th><span style="color:red;">8</span></th>
    <th>4</th>
    <th>10</th>
  </tr>
</table>

<table>
  <tr>
    <th>2</th>
    <th>6</th>
    <th><span style="color:red;">8</span></th>
    <th><span style="color:red;">4</span></th>
    <th>10</th>
  </tr>
</table>

<table>
  <tr>
    <th>2</th>
    <th>6</th>
    <th>4</th>
    <th><span style="color:red;">8</span></th>
    <th><span style="color:red;">10</span></th>
  </tr>
</table>

<table>
  <tr>
    <th>2</th>
    <th>6</th>
    <th>4</th>
    <th>8</th>
    <th><span style="color:blue;">10</span></th>
  </tr>
</table>

loop 2:

<table>
  <tr>
    <th><span style="color:red;">2</span></th>
    <th><span style="color:red;">6</span></th>
    <th>4</th>
    <th>8</th>
    <th><span style="color:blue;">10</span></th>
  </tr>
</table>
...

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
