---
title: "[Programmers]베스트앨범"
date: 2020-12-26 22:26:28 -0400
draft: false
description: "[Programmers]베스트앨범"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제
문제 설명
스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

속한 노래가 많이 재생된 장르를 먼저 수록합니다.
장르 내에서 많이 재생된 노래를 먼저 수록합니다.
장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

## 제한사항
제한사항
genres[i]는 고유번호가 i인 노래의 장르입니다.
plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
장르 종류는 100개 미만입니다.
장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
모든 장르는 재생된 횟수가 다릅니다.

## 입출력 예
|genres|plays|return|
|------|-----|--------|
|[classic, pop, classic, classic, pop]	|[500, 600, 150, 800, 2500]|[4, 1, 3, 0]|

## 소스코드
```java
import java.util.*;

class Solution {
    	public int[] solution(String[] genres, int[] plays) {
		int[] answer;
		ArrayList<Integer> result = new ArrayList<>();
		HashMap<String,Integer> gmap = new HashMap<>(); //장르별 재생횟수 저장
		TreeMap<Integer,String> tmap = new TreeMap<>(Collections.reverseOrder()); //정렬용 -> new map(재생횟수, 장르)

		for(int i=0;i<plays.length;i++){            
			if(gmap.containsKey(genres[i])){
				gmap.put(genres[i],gmap.get(genres[i])+plays[i]);
			}else{
				gmap.put(genres[i],plays[i]);
			}
            
		}

		gmap.forEach((k,v)->tmap.put(v, k));		

		for(String g:tmap.values()) {
			ArrayList<Integer> temp = new ArrayList<>();

			for(int i=0;i<genres.length;i++) {
				if(genres[i].equals(g)) {
					temp.add(i);
				}
			}

		    Collections.sort(temp,new Comparator<Integer>() {
				@Override
				public int compare(Integer o1, Integer o2) {
					if(plays[o1]>plays[o2]) {
						return -1;
					}else if (plays[o1]<plays[o2]) {
						return 1;
					}else {
						return 0;
					}
				}
			});

			result.add(temp.get(0));
			if(temp.size()>1)	result.add(temp.get(1));
		}
            
        answer = new int[result.size()];
		for(int i=0;i<result.size();i++) {
			answer[i] = result.get(i);
		}

		return answer;
	}
}
```

## 풀이과정
