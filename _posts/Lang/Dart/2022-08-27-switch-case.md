---
layout: single

title:  "[Dart] switch-case문"
excerpt: ""

categories: 
    - Dart
tags: [Dart, switch-case, basics]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

조건에 맞는 값이 여러 개일 때 유용한 문법이다.
특히 열거(enum) 타입과 함께 사용할 때는 모든 케이스를 검사해야 하는 강제성이 생긴다. 사람의 실수를 방지하는 이런 기능이 있어서 특수한 경우엔 if문보다 유용하다.


enum Status { Uninitialized, Authenticated, Authenticating, Unauthenticated }

void main() {
	var status = Status.Authenticated;
	switch (status) {
		case Status.Authenticated;
			print('인증됨');
			break;
		case Status.Authenticated;
			print('인증 처리 중');
			break;
		case Status.Authenticated;
			print('미인증');
			break;
		case Status.Authenticated;
			print('초기화됨');
			break;
}
