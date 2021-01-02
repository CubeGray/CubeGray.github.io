---
title: "[Programmers]섬연결하기"
date: 2021-01-02 00:00:28 -0400
draft: false
description: "[Programmers]섬연결하기"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

## 제한사항

|n|costs|return|
|---|---|---|
|4|[[0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8]]|4|

## 입출력 예

|n|result|
|---|---|
|10|4|
|5|3|

costs를 그림으로 표현하면 다음과 같으며, 이때 초록색 경로로 연결하는 것이 가장 적은 비용으로 모두를 통행할 수 있도록 만드는 방법입니다.
<img src="https://grepp-programmers.s3.amazonaws.com/files/production/13e2952057/f2746a8c-527c-4451-9a73-42129911fe17.png">

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
import java.util.*;
import java.lang.*;
class Solution {
  public int solution(int n, int[][] costs) {
		int answer = 0;
		int[] parent = new int[n];
		
		for(int i=0;i<parent.length;i++) {
			parent[i]=i;
		}
    
		Arrays.sort(costs, new Comparator<int[]>() {
			public int compare(int[] arr1, int[] arr2) {
				if(arr1[2]<arr2[2]) {
					return -1;
				}else if(arr1[2]==arr2[2]) {
					return 0;
				}else {
					return 1;
				}
			}
		});
		
		for(int i=0;i<costs.length;i++) {
			 int first = findroot(parent,costs[i][0]);
	         int second = findroot(parent,costs[i][1]);
	         
			if(first!=second) {
				parent[first]=second;
				answer+=costs[i][2];
            }
		}
		return answer;
	}
	public int findroot(int[]parent,int k) {
		if(parent[k]==k) {
			return k;
		}else{
			return parent[k]=findroot(parent,parent[k]);
		}
	}
}
```
</div>
</details>

## 풀이과정
costs배열을 costs[k][2](다리 건설비용)를 기준으로 오름차순 정렬한다.
기존에는 check함수를 다리길이 N만큼 만들어서 연결이 된 섬인지 여부만 따졌지만, 이렇게 될 경우 1,2,3끼리 연결 4,5끼리 연결되는 경우 check는 모두 true가 되지만 모든 섬이 연결되지 않게 된다.

따라서 섬끼리 cycle을 이루지 않는 전제하에 섬들을 연결시켜줘야한다. cycle을 이루게 될 경우 쓸데 없는 비용이 낭비된다.

섬을 연결하기 전에 각 섬의 root부모를 찾는다. 만약 root가 같다면 cycle을 이루지 않도록 하기위해 연결시키지 않는다. 
root가 다를 경우에만 연결시켜주고 두 섬의 root가 갖도록 해준다.