---
title: "[SWEA]1208 Flatten"
date: 2021-02-26 00:00:28 -0400
draft: false
description: "[백준]17478 1208 Flatten"
categories: [SWEA]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

한 쪽 벽면에 다음과 같이 노란색 상자들이 쌓여 있다.

높은 곳의 상자를 낮은 곳에 옮기는 방식으로 최고점과 최저점의 간격을 줄이는 작업을 평탄화라고 한다.

평탄화를 모두 수행하고 나면, 가장 높은 곳과 가장 낮은 곳의 차이가 최대 1 이내가 된다.

평탄화 작업을 위해서 상자를 옮기는 작업 횟수에 제한이 걸려있을 때, 제한된 횟수만큼 옮기는 작업을 한 후 최고점과 최저점의 차이를 반환하는 프로그램을 작성하시오.
 
## 제약사항


가로 길이는 항상 100으로 주어진다.

모든 위치에서 상자의 높이는 1이상 100이하로 주어진다.

덤프 횟수는 1이상 1000이하로 주어진다.

주어진 덤프 횟수 이내에 평탄화가 완료되면 더 이상 덤프를 수행할 수 없으므로 그 때의 최고점과 최저점의 높이 차를 반환한다 (주어진 data에 따라 0 또는 1이 된다).


## 입력

총 10개의 테스트 케이스가 주어지며, 각 테스트 케이스의 첫 번째 줄에는 덤프 횟수가 주어진다. 그리고 다음 줄에 각 상자의 높이값이 주어진다.


## 출력

#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 최고점과 최저점의 높이 차를 출력한다.



<details>
<summary>소스코드</summary>
<div markdown="1">

```java

import java.util.Scanner;
import java.io.FileInputStream;
import java.util.Arrays;


class Solution
{
	public static void main(String args[]) throws Exception
	{
		Scanner sc = new Scanner(System.in);
		
		for(int test_case = 1; test_case <= 10; test_case++)
		{
			int dump = sc.nextInt();
			int arr[] = new int[100];
			int answer =0;
			
			for(int i=0;i<100;i++){
				arr[i]= sc.nextInt();				
			}
			
			Arrays.sort(arr);

			int maxidx=0, minidx=0;
			
			while(dump>0) {
				maxidx=99;
				minidx=0;
				
				for(int i=0;i<98;i++) {
					if(arr[i]<arr[i+1]) {
						minidx = i;
						break;
					}
				}
				for(int i=99;i>1;i--) {
					if(arr[i]>arr[i-1]) {
						maxidx = i;
						break;
					}
				}
				if(arr[maxidx]-arr[minidx]<=1) {
					break;
				}else {
					arr[maxidx]--;
					arr[minidx]++;
				}
				dump--;
			}
			answer = arr[arr.length-1]-arr[0];
			System.out.println("#"+test_case+" "+answer);
		}
	}
}


```
</div>
</details>

## 풀이과정