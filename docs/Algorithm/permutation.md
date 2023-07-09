---
layout: default
title: 순열(permutation)
parent: 알고리즘(Algorithm)
nav_order: 4
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

# 순열(permutation)
>nPr = n!/(n-r)!

## 설명
순열은 주어진 n 개의 배열에서 r개를
<span style="text-decoration:underline">
중복없이 순서에 상관 있게</span> 선택/나열하는 것을 순열이라고 합니다.


## 특징
### 순서 중요
순열은 조합과 다르게 순서가 중요합니다. 순열에서는 순서가 중요하기 때문에 
{1, 2} 와 {2, 1}은 다른 요소지만,
조합에서는 {1, 2}, {2, 1} 은 동일한 요소입니다.

## 예시
3개의 요소(1, 2, 3) 중 2개를 선택한다면 총: 6개  
> 3P2 = 3!/(3-2)! = 3! = 3 * 2 * 1 = 6

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
        <th>1</th>
    </tr>
</table>

4개:
<table>
    <tr>
        <th>2</th>
        <th>3</th>
    </tr>
</table>

5개:
<table>
    <tr>
        <th>3</th>
        <th>1</th>
    </tr>
</table>

6개:
<table>
    <tr>
        <th>3</th>
        <th>2</th>
    </tr>
</table>

## 코드
```java
public class Permutation {
    static int[] a = {1, 2, 3};

    private static void swap(int[] a, int first, int second) {
        int temp = a[first];
        a[first] = a[second];
        a[second] = temp;
    }


    private static void makePermutation(int n, int r, int depth) {

        if(depth == r) {
            for(int i: a) System.out.print(i + " ");
            System.out.println();
            return;
        }

        for(int i = depth; i < n; i++) {
            swap(a, i, depth);
            makePermutation(n, r, depth + 1);
            swap(a, i, depth);
        }
    }

    public static void main(String[] args) {
        makePermutation(3, 3, 0);
    }

}


```


