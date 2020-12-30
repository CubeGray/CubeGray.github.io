---
title: "[Programmers]방문길이"
date: 2020-12-31 00:26:28 -0400
draft: false
description: "[Programmers]방문길이"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

U: 위쪽으로 한 칸 가기

D: 아래쪽으로 한 칸 가기

R: 오른쪽으로 한 칸 가기

L: 왼쪽으로 한 칸 가기

캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.

<img src="https://res.cloudinary.com/jistring93/image/upload/v1495542181/%EB%B0%A9%EB%AC%B8%EA%B8%B8%EC%9D%B41_qpp9l3.png">

예를 들어, ULURRDLLU로 명령했다면

<img src="https://res.cloudinary.com/jistring93/image/upload/v1495542443/%EB%B0%A9%EB%AC%B8%EA%B8%B8%EC%9D%B42_lezmdo.png">

1번 명령어부터 7번 명령어까지 다음과 같이 움직입니다.

<img src="https://res.cloudinary.com/jistring93/image/upload/v1495542704/%EB%B0%A9%EB%AC%B8%EA%B8%B8%EC%9D%B43_sootjd.png">

8번 명령어부터 9번 명령어까지 다음과 같이 움직입니다.

<img src="https://res.cloudinary.com/jistring93/image/upload/v1495542767/%EB%B0%A9%EB%AC%B8%EA%B8%B8%EC%9D%B44_hlpiej.png">

이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)

단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.

## 제한사항

최고의 집합은 오름차순으로 정렬된 1차원 배열(list, vector) 로 return 해주세요.
만약 최고의 집합이 존재하지 않는 경우에 크기가 1인 1차원 배열(list, vector) 에 -1 을 채워서 return 해주세요.
자연수의 개수 n은 1 이상 10,000 이하의 자연수입니다.
모든 원소들의 합 s는 1 이상, 100,000,000 이하의 자연수입니다.

## 입출력 예

|dirs|answer|
|---|---|
|ULURRDLLU|7|
|LULLLLLLU|7|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
import java.util.*;
class Solution {
  public int solution(String dirs) {
		int answer = 0;
		HashSet <String> set = new HashSet<String>();

		int inx = 5;
		int iny = 5;
		for(int i=0;i<dirs.length();i++) {
            int tx=inx, ty=iny; //출발점
			if(dirs.charAt(i)=='U') {
				if(iny!=10)	iny++;				
			}else if(dirs.charAt(i)=='D') {
				if(iny!=0) iny--;
			}else if(dirs.charAt(i)=='R') {
				if(inx!=10) inx++;
			}else if(dirs.charAt(i)=='L') {
				if(inx!=0) inx--;
			}
            if(!(tx==inx && ty==iny) && !set.contains(tx+" "+ty+" "+inx+" "+iny)&&
						!set.contains(inx+" "+iny+" "+tx+" "+ty)) {
					set.add(tx+" "+ty+" "+inx+" "+iny);
                    System.out.println(tx+" "+ty+" "+inx+" "+iny);
					answer++;
			}
		}
		return answer;
	}
}
```
</div>
</details>

## 풀이과정
아래와 같은 조건을 만족할 때만 HashSet에 출발점(tx,ty)와 도착점(inx,iny)를 집어 넣는다. 이때 answer를 1씩 증가시킨다.
1. 출발점과 도착점이 같지 않을때(!(tx==inx && ty==iny)), 즉 (0,5)에서 L로 이동하여 (0,5)로 이동하는 경우는 set에 추가되지 않음.
2. 출발점, 도착점이 이미 set에 담겨 있을 때 
3. 도착점, 출발점이 이미 set에 담겨 있을 때