---
layout: single

title:  "\[Algorithms\] Union-Find"
excerpt: ""

categories: 
    - Algorithms
tags: [algorithms]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

### Goal

- Disjoint Set과 Union-Find의 개념을 이해할 수 있다
- Union-Find 알고리즘 구현할 수 있다.

### Disjoint Set

서로 **중복되지 않는 부분 집합들**로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조

- 즉, 공통 원소가 없는, 즉 “상호 배타적”인 부분 집합들로 나눠진 원소들에 대한 자료구조
- Disjoint Set = 서로소 집합 자료구조

### Union-Find의 개념

Disjoin Set을 표현할 때 사용하는 알고리즘

- 집합을 구현하는 데는 비트 벡터, 배열, 연결 리스트를 이용할 수 있음
- 중복되지 않는 부분 집합들

### Union-Find의 연산

- **make-set(x) :** 초기화 / x를 유일한 원소로 하는 새로운 집합
- **union(x, y) :** 합하기 / x가 속한 집합과 y가 속한 집합을 합침. 즉, x와 y가 속한 두 집합을 합치는 연산
- **find(x) :** 찾기 / x가 속한 집합의 대표값(루트 노드 값) 반환. 즉, x가 어떤 집합에 속해 있는지 찾는 연산

### Union-Find의 사용 예시

- Kruskal MST 알고리즘에서 새로 추가할 간선의 양끝 정점이 같은 집합에 속해 있는지
(사이클 형성 여부 확인)에 대해 검사하는 경우
- 초기에 {0}, {1}, {2}, …{n}이 각각 n+1개의 집합을 이루고 있다. 여기에 합집합 연산과, 
두 원소가 같은 집합에 포함되어 있는지를 확인하는 연산 (백준 1717)