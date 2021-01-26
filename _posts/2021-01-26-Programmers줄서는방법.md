---
title: "[Programmers]줄서는방법"
date: 2021-01-26 00:00:28 -0400
draft: false
description: "[Programmers]줄서는방법"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

n명의 사람이 일렬로 줄을 서고 있습니다. n명의 사람들에게는 각각 1번부터 n번까지 번호가 매겨져 있습니다. n명이 사람을 줄을 서는 방법은 여러가지 방법이 있습니다. 예를 들어서 3명의 사람이 있다면 다음과 같이 6개의 방법이 있습니다.

[1, 2, 3]
[1, 3, 2]
[2, 1, 3]
[2, 3, 1]
[3, 1, 2]
[3, 2, 1]
사람의 수 n과, 자연수 k가 주어질 때, 사람을 나열 하는 방법을 사전 순으로 나열 했을 때, k번째 방법을 return하는 solution 함수를 완성해주세요.

제한사항
n은 20이하의 자연수 입니다.
k는 n! 이하의 자연수 입니다.


## 입출력예

|n|k|result|
|---|---|---|
|3|5|[3,1,2]|



<details>
<summary>소스코드</summary>
<div markdown="1">

```java

import java.util.ArrayList;

public class Solution {
	public int[] solution(int n, long k) {
            long fact[] = new long[n];
			int ans[] = new int[n];
			ArrayList<Long> list = new ArrayList<Long>();
			int index=0;

			fact[0]=1;
			list.add((long)1);
			
			for(int i=1;i<n;i++) {
				fact[i]=fact[i-1]*(i+1);
				list.add((long)(i+1));
			}
			
			for(int i=n-2;i>=0;i--) {
				if(k!=0) {
					if(k%fact[i]!=0) {
						ans[index]=list.get((int)(k/fact[i])).intValue();
						list.remove((int)(k/fact[i]));
						k%=fact[i];
					}else {
						ans[index]=list.get((int)(k/fact[i])-1).intValue();
						list.remove((int)(k/fact[i])-1);
						k%=fact[i];
					}
					index++;
				}else {			
					break;
				}
			}
			
			int index2 = list.size()-1;
			while(index2>=0) {
				ans[index]=list.get(index2).intValue();
				index++;
				index2--;
			}
			return ans;
	}
}

```
</div>
</details>

## 풀이과정