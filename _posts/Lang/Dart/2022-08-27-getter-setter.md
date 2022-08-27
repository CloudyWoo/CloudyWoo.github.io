---
layout: single

title:  "\[Dart\] Getter & Setter"
excerpt: ""

categories: 
    - Dart
tags: [Dart, getter-setter, basics]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

### Getter

- 게터와 세터는 클래스 생성 시 데이터를 보호하기 위해 사용된다.
- 한 오브젝트의 내부속성을 외부에서 알지 못하게 하고, 접근이 불가능하게 하여 객체지향의 목적인 `정보은닉` 과 `객체의 무결성 보장`을 위함 + validation을 하기 위해서

```dart
// UserManager가 user 프로퍼티를 다른 곳에 read-only로 제공하고 싶을 때 getter 구현
// 다른 파일에서는 user 프로퍼티를 읽을 권한만 가지게 된다.
class User {
	String id;
	String nickname;

	User({this.id, this.nickname});
}

class UserManager {
	User _user;
	User get user => _user; // getter 구현
}

// getter 사용
void main() {
	var manager = User.UserManager();
	print(manager.user);

	// 아래는 모두 컴파일 에러가 발생한다.
	print(manager._user);
	manager._user = User(id: "", nickname: "");
	manager.user = User(id: "", nickname: "");
}
```

### Setter

user가 set될 때마다 다른 작업을 해주고 싶을 때 Setter를 구현해준다.

```dart
// user를 set 해줄 때마다 id가 출력되게 된다.
class UserManager {
	User _user;
	
	User get user => _user;

	set User(User user) {
		_user = user;
		print(user.id);
  }
}

void main() {
	var manager = UserManager();
	manager.user = User(id: "1", nickname: "");

	// 아래는 모두 컴파일 에러가 발생한다.
	print(manager._user);
	manager._user = User(id: "", nickname: "");
}
```

[[Dart] 다트의 Getter와 Setter](https://eunjin3786.tistory.com/273)