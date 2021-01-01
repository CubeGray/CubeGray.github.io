---
title: "[Programmers]2Xn타일링"
date: 2020-12-31 00:26:28 -0400
draft: false
description: "[Programmers]2Xn타일링"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

문제 설명
가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

타일을 가로로 배치 하는 경우
타일을 세로로 배치 하는 경우
예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

<img src:"https://i.imgur.com/29ANX0f.png">

직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

## 제한사항

가로의 길이 n은 60,000이하의 자연수 입니다.
경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

## 입출력 예

|n|result|
|---|---|
|4|5|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
class Solution {
    public int solution(int n) {
        int[] arr = new int[n];
        
        if(n>=1) arr[0]=1;
        if(n>=2) arr[1]=2;
        if(n>=3){
            for(int i=2;i<n;i++){
                arr[i]=(arr[i-1]%1000000007+arr[i-2]%1000000007)%1000000007;
            }            
        }
        return arr[n-1];
    }
}
```
</div>
</details>

## 풀이과정
1칸일 때는 1가지 방법
2번째 칸일때는 2가지 방법으로 타일을 놓을 수 있다.
3번째 부터는 (n-1)칸 에서 세로타일 1개를 놓는 방법과 (n-2)칸에서 가로타일을 2행으로 놓는 방법밖에 없으므로(세로로 놓아지는 경우는 n-1번째에서 카운트 됨) 피보나치 수열과 같은 점화식을 세울 수 있다.