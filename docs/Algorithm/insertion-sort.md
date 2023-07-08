---
layout: default
title: 삽입 정렬(insertion-sort)
parent: 알고리즘(Algorithm)
nav_order: 3
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

# 삽입 정렬(Insertion Sort)

> 삽입 정렬은 <span style="text-decoration: underline">
원소 두번째</span> 부터 그 앞의 원소를 비교하여 정렬할 위치를 지정한 후,
나머지 원소들을 뒤로 옮기고 지정한 자리에 원소를 삽입하는 정렬 알고리즘입니다.

## 특징
### 제자리 정렬
삽입 정렬은 정렬을 위해 추가적인 메모리 공간이 필요하지 않습니다.
### 안정 정렬 
삽입 정렬은 동일한 요소들의 상대적인 순서를 보장합니다. 정렬전의 순서와 정렬 후의 순서가 동일합니다.

## 시간 복잡도
> 삽입 정렬의 시간 복잡도는 O(n^2) 입니다.

선택 정렬과 마찬가지로 (n-1) + (n-2) + ... 2 + 1 = n(n-1)/2, n^2 의 시간 복잡도를 가지게 된다.

## 예시
배열:
<table>
  <tr>
    <th>8</th>
    <th>4</th>
    <th>6</th>
    <th>10</th>
    <th>2</th>
  </tr>
</table>

loop 1:

<table>
  <tr>
    <th>8</th>
    <th>4</th>
  </tr>
</table>

<table>
  <tr>
    <th><span style="color:red;">4</span></th>
    <th><span style="color:orange;">8</span></th>
  </tr>
</table>


loop 2:
<table>
  <tr>
    <th>4</th>
    <th>8</th>
    <th>6</th>
  </tr>
</table>

<table>
  <tr>
    <th><span style="color:orange;">4</span></th>
    <th><span style="color:red;">6</span></th>
    <th><span style="color:orange;">8</span></th>
  </tr>
</table>

loop 3:
<table>
  <tr>
    <th>4</th>
    <th>8</th>
    <th>6</th>
    <th>10</th>
  </tr>
</table>
<table>
  <tr>
    <th><span style="color:orange;">4</span></th>
    <th><span style="color:orange;">6</span></th>
    <th><span style="color:orange;">8</span></th>
    <th><span style="color:red;">10</span></th>
  </tr>
</table>

loop4:
<table>
  <tr>
    <th>4</th>
    <th>8</th>
    <th>6</th>
    <th>10</th>
    <th>2</th>
  </tr>
</table>


<table>
  <tr>
    <th><span style="color:red;">2</span></th>
    <th><span style="color:orange;">4</span></th>
    <th><span style="color:orange;">6</span></th>
    <th><span style="color:orange;">8</span></th>
    <th><span style="color:orange;">10</span></th>
  </tr>
</table>


## 코드
```java
public class Test {
    static int[] a  = {8, 4, 6, 10, 2};

    public static void main(String[] args) {
        
        int n = a.length;
        //삽입 정렬
        for(int end = 1; end < n; end++) {
            int idx = end;
            int toInsert = a[idx];

            while(0 < idx  && toInsert < a[idx-1]) {
                a[idx] = a[idx-1];
                idx--;
            }
            a[idx] = toInsert;
        }
        for(int i : a) System.out.print(i + " ");
    }
}

```
