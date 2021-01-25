---
title: "[Programmers]디스크컨트롤러"
date: 2021-01-24 00:00:28 -0400
draft: false
description: "[Programmers]디스크컨트롤러"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어

- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청

와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.

<impg src="https://grepp-programmers.s3.amazonaws.com/files/production/b68eb5cec6/38dc6a53-2d21-4c72-90ac-f059729c51d5.png">

한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.

<img src="https://grepp-programmers.s3.amazonaws.com/files/production/5e677b4646/90b91fde-cac4-42c1-98b8-8f8431c52dcf.png">

- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면

<img src="https://grepp-programmers.s3.amazonaws.com/files/production/9eb7c5a6f1/a6cff04d-86bb-4b5b-98bf-6359158940ac.png">

- A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
- C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
- B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

## 제한사항

jobs의 길이는 1 이상 500 이하입니다.
jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

## 입출력예

|jobs|return|
|----|------|
|[[0, 3], [1, 9], [2, 6]]|9|

문제에 주어진 예와 같습니다.

0ms 시점에 3ms 걸리는 작업 요청이 들어옵니다.
1ms 시점에 9ms 걸리는 작업 요청이 들어옵니다.
2ms 시점에 6ms 걸리는 작업 요청이 들어옵니다.


<details>
<summary>소스코드</summary>
<div markdown="1">

```java

package programmers;

import java.util.Arrays;
import java.util.Comparator;
import java.util.PriorityQueue;

public class Programmers디스크컨트롤러 {

	public static void main(String[] args) {
		
	}

	public static int solution(int[][] jobs) {
		Arrays.sort(jobs,new Comparator<int[]>() {
			@Override
			public int compare(int[] t1, int[] t2) {
				if(t1[0]>t2[0]) return 1;
				else if(t1[0]<t2[0]) return -1;
				else {
					if(t1[1]>t2[1]) return 1;
					else if(t1[1]<t2[1]) return -1;
					else return 0;
				}
			}
		});	//도착한 작업 시작순서로 오름차순 정렬
		PriorityQueue<int[]> queue = new PriorityQueue<>((o1,o2)->o1[1]-o2[1]);
		//작업들의 작업시간을 기준으로 오름차순하기 위한 priority queue

		int endtime = 0;	//진행중인 작업의 종료시간
		int index = 0;	
		int count=0;	//작업완료된 작업의 수
		int answer = 0;	//총 작업들의 작업시간 + 대기시간
		
		while(count < jobs.length) {
			while(index<jobs.length && jobs[index][0]<=endtime) {
				queue.add(jobs[index]);
				index++;
			}
			if(queue.isEmpty()) {
				endtime=jobs[index][0]+jobs[index][1];
				answer+=jobs[index][1];
				count++;
				index++;				
			}else {
				int temp[]=queue.poll();
				answer+=endtime-temp[0]+temp[1];
				endtime+=temp[1];
				count++;
			}
		}

		return answer/jobs.length;
	}
}

```
</div>
</details>

## 풀이과정
우선순위 큐 이용