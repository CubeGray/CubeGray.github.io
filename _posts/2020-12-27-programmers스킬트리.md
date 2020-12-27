---
title: "[Programmers]스킬트리"
date: 2020-12-27 00:26:28 -0400
draft: false
description: "[Programmers]스킬트리"
categories: [알고리즘]
toc : true
toc_sticky : true
toc_label : 목차
---

## 문제

문제 설명
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

## 제한사항

제한 조건
스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
스킬 순서와 스킬트리는 문자열로 표기합니다.
예를 들어, C → B → D 라면 CBD로 표기합니다
선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
skill_trees는 길이 1 이상 20 이하인 배열입니다.
skill_trees의 원소는 스킬을 나타내는 문자열입니다.
skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

## 입출력 예

|skill|skill_trees|return|
|---|---|---|
|"CBD"|["BACDE", "CBADF", "AECB", "BDA"]|2|

## 소스코드

<details>
<summary>소스코드</summary>
<div markdown="1">

```java
import java.util.*;
class Solution {
public int solution(String skill, String[] skill_trees) {
		int answer = 0;
		HashSet<Character> set = new HashSet<>();

		for(int i=0;i<skill.length();i++) {
			set.add(skill.charAt(i));
		}
		for(int i=0;i<skill_trees.length;i++) { 
			boolean flag=true;
			int index=0;
			for(int j=0;j<skill_trees[i].length();j++) {
				if(set.contains(skill_trees[i].charAt(j))) {
					if(skill_trees[i].charAt(j)==skill.charAt(index)) {
						index++;
						if(index==skill.length()) {
							break;
						}
					}else {
						flag=false;
						break;
					}
				}
			}
			if(flag) {
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
선행스킬(skill)을 HashSet에 넣어놓고 Skill_trees를 돌면서 HashSet안에 포함되지만 선행스킬의 앞부분부터 수행되지 않은 경우 flag를 false로 반환해준다.

주의할 점은 선행스킬이 아예 섞여있지 않은 스킬의 경우 수행가능한 스킬이다. 예를 들어 선행스킬이 'XYZ'이라면 'ABCD'와 같은 스킬은 수행가능하다.

