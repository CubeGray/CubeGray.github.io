---
title: "[Programmers]네트워크(BFS)"
date: 2020-12-27 00:26:28 -0400
draft: false
description: "[Programmers]네트워크(BFS)"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제
문제 설명
네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.


## 제한사항
제한사항
컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
computer[i][i]는 항상 1입니다.

## 입출력 예
|n|computers|return|
|3|[[1, 1, 0], [1, 1, 0], [0, 0, 1]]|2|
|3|[[1, 1, 0], [1, 1, 1], [0, 1, 1]|1|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
import java.util.*;

class Solution {
public int solution(int n, int[][] computers) {
		int answer = 0;
		boolean check[] = new boolean[n];
		
		for(int i=0;i<computers.length;i++) {
			if(!check[i]) {
                answer++;
				dfs(i,computers,check);
			}
		}
		return answer;
	}
	
	public void dfs(int k, int[][]computers, boolean check[]) {
		check[k] = true;
		for(int i=0;i<computers.length;i++) {
			if(check[i]==false && computers[k][i]==1) {
				dfs(i,computers,check);
			}
		}
	}
}
```
</div>
</details>

## 풀이과정

BFS를 이용하여 인접한 노드들부터 방문하여 재귀함수를 통해 네트워크로 연결된 노드들을 확인한다.
A와 B가 연결되어 있다면 B와 연결된 노드들을 확인하고 재귀함수를 통해 연결된 노드들과 또 연결된 노드들을 확인하며 네트워크를 이루는 노드들을 확인할 수 있다.
네트워크에 연결되지 않을 시에만 anser+=1을 통해 네트워크의 갯수를 파악할 수 있다.

효율성을 위해 dfs메소드를 구현하면서 i의 범위를 k또는 k+1부터로 지정했지만 오답이 나왔다.
확인 결과 대각선을 기준으로 대칭이 아닌 테스트 케이스가 있다고 한다. 

