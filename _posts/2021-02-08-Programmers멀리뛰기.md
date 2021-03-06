---
title: "[Programmers]멀리뛰기"
date: 2021-02-08 00:00:28 -0400
draft: false
description: "[Programmers]멀리뛰기"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는
(1칸, 1칸, 1칸, 1칸)
(1칸, 2칸, 1칸)
(1칸, 1칸, 2칸)
(2칸, 1칸, 1칸)
(2칸, 2칸)
의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.

## 제한사항

제한사항

n은 1 이상, 2000 이하인 정수입니다.

## 입출력예

|routes|return|
|---|---|
|[[-20,15], [-14,-5], [-18,-13], [-5,-3]]|2|


|n|result|
|---|---|
|4|5|
|3|3|

<details>
<summary>소스코드</summary>
<div markdown="1">

```java

class Solution {
  public long solution(int n) {
		long arr[] = new long[n];
		
		arr[0]=1;
		if(n>=2) {
			arr[1]=2;
		}
		if(n>=3) {
			for(int i=2;i<n;i++) {
				arr[i]=(arr[i-1]%1234567+arr[i-2]%1234567)%1234567;
			}
		}
		return arr[n-1];
  }
}
```
</div>
</details>

## 풀이과정

1칸 또는 2칸만 뛸수 있으므로 dp[i]=dp[i-1]+dp[i-2] 점화식을 이용해 dp로 구현한다.