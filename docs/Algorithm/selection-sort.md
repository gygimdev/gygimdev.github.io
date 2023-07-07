---
layout: default
title: 선택정렬(selection-sort)
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

# 선택정렬(Selection Sort)
> 선택 정렬(Selection Sort)은 배열을 정렬하기 위한 간단한 정렬 알고리즘 중 하나입니다. 
아우터 루프마다 가장 큰 혹은 작은 값을 찾아 배열의 시작으로 이동합니다.


## 특징
### 제자리 정렬
선택 정렬은 <span style="text-decoration: underline">안정적인 정렬 알고리즘이 아니며</span>, 
비교적 단순한 알고리즘입니다. 하지만 배열의 크기가 커지면 성능이 저하되는 단점이 있습니다.
선택 정렬은 정렬 과정에서 이동 연산을 수행하기 때문에 비교적 느리지만,
정렬 중간에도 부분적으로 정렬된 배열을 유지한다는 장점이 있습니다.
또한, 정렬을 수행하는 데에 추가적인 공간을 필요로하지 않는
<span style="text-decoration: underline;">"제자리 정렬(In-place Sorting)" 알고리즘</span>이라는 특징도 가지고 있습니다.

## 시간 복잡도
> 선택 정렬의 시간 복잡도는 O(n^2)입니다.  
 
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
<table>
  <tr>
    <th>10</th>
    <th>8</th>
    <th>2</th>
    <th>4</th>
    <th>6</th>
  </tr>
</table>

loop 1:
<table>
  <tr>
    <th><span style="color:red;">10</span></th>
    <th><span style="color:red;">8</span></th>
    <th>2</th>
    <th>4</th>
    <th>6</th>
    <th>Min = 8</th>
  </tr>
</table>

<table>
  <tr>
    <th>10</th>
    <th><span style="color:red;">8</span></th>
    <th><span style="color:red;">2</span></th>
    <th>4</th>
    <th>6</th>
    <th>Min = 2</th>
  </tr>
</table>

<table>
  <tr>
    <th>10</th>
    <th>8</th>
    <th><span style="color:red;">2</span></th>
    <th><span style="color:red;">4</span></th>
    <th>6</th>
    <th>Min = 2</th>
  </tr>
</table>


<table>
  <tr>
    <th>10</th>
    <th>8</th>
    <th><span style="color:red;">2</span></th>
    <th>4</th>
    <th><span style="color:red;">6</span></th>
    <th>Min = 2</th>
  </tr>
</table>

loop 2:
<table>
  <tr>
    <th><span style="color:blue;">2</span></th>
    <th><span style="color:red;">8</span></th>
    <th><span style="color:red;">10</span></th>
    <th>4</th>
    <th>6</th>
    <th>Min = 8</th>
  </tr>
</table>

<table>
  <tr>
    <th><span style="color:blue;">2</span></th>
    <th><span style="color:red;">8</span></th>
    <th>10</th>
    <th><span style="color:red;">4</span></th>
    <th>6</th>
    <th>Min = 4</th>
  </tr>
</table>
...


## 코드

```java
public class 선택정렬 {

    static int[] a = {10, 8, 2, 4, 6};

    public static void main(String[] args) {
        int n = a.length;

        // outer loop
        for(int i = 0; i < n - 1; i++) {
            int minIndex = i;
            int index = i;
            
            // inner loop
            for(int j = i + 1; j < n; j++) {
                if(a[j] < a[minIndex]) minIndex = j;
            }
            if(minIndex != index) swap(a, index, minIndex);
        }
        for(int i : a) System.out.print(i + " ");
    }

    public static void swap(int[] a, int first, int second) {
        int temp = a[first];
        a[first] = a[second];
        a[second] = temp;
    }
}
```
