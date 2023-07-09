---
layout: default
title: 조합(combination)
parent: 알고리즘(Algorithm)
nav_order: 5
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

# 조합(Combination)

## 설명
조합이란 n 개의 배열에서 r개의 요소 순서에상관없이 선택/나열하는 것을 조합이라고합니다.

## 특징
### 순서가 중요하지 않음
조합은 순열과 다르게 어떤 순서로 요소를 선택했는는 중요하지 않습니다.
순열에서 {1, 2} 와 {2, 1} 은 순서가 다르기 때문에 다른 요소로 구분되지만,
조합에서는 순서가 상관없기 때문에 {1, 2} 와 {2, 1} 은 같은 요소입니다.

## 예시
> nCr = n!/r!(n-r)! = 3C2 = 3!/2!(3-2)! = 3


<table>
    <tr>
        <th>1</th>
        <th>2</th>
        <th>3</th>
    </tr>
</table>

1개:
<table>
    <tr>
        <th>1</th>
        <th>2</th>
    </tr>
</table>

2개:
<table>
    <tr>
        <th>1</th>
        <th>3</th>
    </tr>
</table>

3개:
<table>
    <tr>
        <th>2</th>
        <th>3</th>
    </tr>
</table>



## 코드
```java
import java.util.ArrayList;

public class Combination {

    public static int[] a = {1, 2, 3};
    public static int n = 3;
    public static int r = 2;


    public static void combi(int start, ArrayList<Integer> b) {

        if(b.size() == r) {
            for(int i: b) System.out.print(a[i] + " ");
            System.out.println();
            return;
        }

        for(int i = start + 1; i < n; i++) {
            b.add(i);
            combi(i, b);
            b.remove(b.size() -1);
        }
        return;
    }

    public static void main(String[] args) {
        ArrayList<Integer> b = new ArrayList<>();
        combi(-1, b);
    }
}
```
