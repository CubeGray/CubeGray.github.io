---
title: "[Programmers]소수찾기"
date: 2021-01-02 00:00:28 -0400
draft: false
description: "[Programmers]소수찾기(에라토스테네스의 체)"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.
(1은 소수가 아닙니다.)

## 제한사항

n은 2이상 1000000이하의 자연수입니다.

## 입출력 예

|n|result|
|---|---|
|10|4|
|5|3|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        boolean[] arr = new boolean[n+1];
        arr[1]=true;
        
        for(int i=2;i<=Math.sqrt(n)+1;i++){
            int k=2;
            if(!arr[i]){
                while(i*k<=n){
                    arr[i*k]=true;
                    k++;
                }
            }
        }
        for(int i=1;i<=n;i++){
            if(!arr[i]) answer++;
        }
        return answer;
    }
}
```
</div>
</details>

## 풀이과정
n이하의 소수의 갯수를 찾는 과정에서 각 숫자 k마다 소수인지 아닌지 찾으려면 k의 소수여부를 구하는 과정에서 O(N^1/2)의 시간 복잡도가 들고 이를 n번 반복해야하므로 O(N*N^1/2)) 의 시간복잡도가 된다.
하지만 에라토스테네스의 체는 2부터 배수들을 지워나가는 방식이기 때문에 숫자마다 일일이 약수가 있는지 검사할 필요가 전혀 없고, 이미 지워진 숫자는 바로 건너뛰면 되니 실행시간이 매우 짧다.