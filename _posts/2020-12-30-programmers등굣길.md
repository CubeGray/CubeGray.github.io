---
title: "[Programmers]등굣길"
date: 2020-12-30 00:26:28 -0400
draft: false
description: "[Programmers]등굣길"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

문제 설명
계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.
가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.

격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다. 오른쪽과 아래쪽으로만 움직여 집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

## 제한사항
제한사항

격자의 크기 m, n은 1 이상 100 이하인 자연수입니다.
m과 n이 모두 1인 경우는 입력으로 주어지지 않습니다.
물에 잠긴 지역은 0개 이상 10개 이하입니다.
집과 학교가 물에 잠긴 경우는 입력으로 주어지지 않습니다.

## 입출력 예

|m|n|puddles|return|
|---|---|---|---|
|4|3|[[2, 2]]|4|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
class Solution {
   public int solution(int m, int n, int[][] puddles) {
		int answer = 0;
		int[][] arr = new int[m+1][n+1];
		for(int i=0;i<puddles.length;i++) {
			arr[puddles[i][0]][puddles[i][1]]=-1;
		}
		for(int i=1;i<=m;i++) {
			for(int j=1;j<=n;j++) {
				if(i==1&&j==1) arr[i][j]=1;
				else {
					if(arr[i][j]!=-1) {
						arr[i][j]=(arr[i-1][j]%1000000007+arr[i][j-1]%1000000007)%1000000007;
					}else {
						arr[i][j]=0;
					}
				}
			}
		}

		answer = arr[m][n];
		return answer;
	}
}
```
</div>
</details>

## 풀이과정
일반적인 dp문제이지만 웅덩이가 있을 경우를 따져서 웅덩이 위치의 배열에만 0을 할당해주고 나머지 경우는 계속 dp의 점화식대로 채워가면 된다.