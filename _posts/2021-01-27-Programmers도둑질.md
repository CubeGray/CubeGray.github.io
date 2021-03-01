---
title: "[Programmers]도둑질"
date: 2021-01-27 00:00:28 -0400
draft: false
description: "[Programmers]도둑질"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

도둑이 어느 마을을 털 계획을 하고 있습니다. 이 마을의 모든 집들은 아래 그림과 같이 동그랗게 배치되어 있습니다.

<img src="https://grepp-programmers.s3.amazonaws.com/files/ybm/e7dd4f51c3/a228c73d-1cbe-4d59-bb5d-833fd18d3382.png">

각 집들은 서로 인접한 집들과 방범장치가 연결되어 있기 때문에 인접한 두 집을 털면 경보가 울립니다.

각 집에 있는 돈이 담긴 배열 money가 주어질 때, 도둑이 훔칠 수 있는 돈의 최댓값을 return 하도록 solution 함수를 작성하세요.


## 제한사항

이 마을에 있는 집은 3개 이상 1,000,000개 이하입니다.
money 배열의 각 원소는 0 이상 1,000 이하인 정수입니다.


## 입출력예

|money|return|
|---|---|
|[1, 2, 3, 1]|4|



<details>
<summary>소스코드</summary>
<div markdown="1">

```java

class Solution {
public int solution(int[] money) {
		int answer = 0 ;
		int dp[] = new int [money.length];	//1집부터
		int dp2[] = new int [money.length];	//2집부터
		
		dp[0]=money[0];
		dp2[0]=0;
		dp[1]=Math.max(dp[0],money[1]);
		dp2[1]=money[1];
		
		for(int i=2;i<money.length;i++) {
			dp[i]=Math.max(dp[i-1],dp[i-2]+money[i]);
			dp2[i]=Math.max(dp2[i-1],dp2[i-2]+money[i]);
		}
		
		return Math.max(dp[money.length-2], dp2[money.length-1]);
	}
}

```
</div>
</details>

## 풀이과정

보통의 dp문제이지만 처음과 끝집이 붙어있다는 특이점이 있다.
따라서 첫집을 선택했을 경우의 dp배열과 첫집을 선택하지 않고 두번째 집부터 선택하는 경우의 dp배열(dp2)가 필요하다.
두 집을 연달아 선택할 수 없기 때문에, 현재 위치까지의 최대 money(dp[i])는 이전 집까지의 최대 money(dp[i-1])와 전전집까지의 최대money+현재 위치의 집 money(dp[i-2]+money[i])중 큰 값이 된다.
첫번째 집을 선택한 경우(dp)에는 마지막 집은 선택할 수 없으므로 dp[money.length-2]가 도둑이 털수 있는 최대 money를 갖고 있으며,
첫번째 집을 선택하지 않은 경우(dp2)에는 마지막 집을 선택할 수 있으므로 dp2[money.length-1]가 도둑이 털수 있는 최대 money를 갖게 되므로
이 두 값중 큰값이 정답이 된다.