---
layout: single

title:  "\\[Dart\\] 생성자"
excerpt: ""

categories: 
    - Dart
tags: [Dart, generator, basics]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

클래스에는 생성자가 따른다. 

생성자는 이름처럼 **클래스가 인스턴스화 될 때**, 즉 **객체가 생성될 때 호출**된다.

### 생성자 종류

1. 기본 생성자(Default constructor)
2. 이름 있는 생성자(Named constructor)
3. 초기화 리스트(Initializer list)
4. 리다이렉팅 생성자(Redirecting constructor)
5. 상수 생성자(Constant constructor)
6. 팩토리 생성자(Factory constructor)

### 1. 기본 생성자

클래스를 구현할 때 생성자를 선언하지 않으면(=생략하면) **기본 생성자가 자동 제공**된다.

기본 생성자는 1)클래스명과 동일하면서 2)인자가 없다.

또한 기본 생성자는 **부모 클래스의 인수가 없는 생성자(=기본 생성자)를 호출**한다.(이 문장 이해 안감)

```dart
// 기본 생성자의 형태
class 클래스명 {
	클래스명() {
	}
}

// 예시
class Person {
	Person() {
	}
}
```

부모 클래스느 자식 클래스에게 멤버를 물려주는(=상속하는) 관계이다.

### 2. 이름 있는 생성자

말 그대로 생성자에 이름을 부여한 형태.

**한 클래스 내에 1)많은 생성자를 생성하거나 2)생성자를 명확히 하기 위해 사용**된다.

```dart
// 이름 있는 생성자의 형태
class 클래스명 {
	클래스명.생성자명() {}
}

// 예시
class Person {
	Person.init() {}
}
```

**사용 방법**: 객체 생성 시 이름 있는 생성자로 생성

```dart
// Person.init()이라는 생성자를 선언하였고
// init 객체가 Person.init() 생성자를 통해 생성됨

class Person {
	Person() {
		print("This is Person Constructor!");	
}

Person.init() {
	print("This is Person.init Constructor!");
}

class Student extends Person {
	Student() {
		print("This is Student Constructor");
	}
}

main() {
	var person = Person();
	var init = Person.init();
}
```

(참고) 

이름 없는 생성자는 단 하나만 가질 수 있다.

또한 이름 있는 생성자를 선언하면 기본 생성자는 생략할 수 없다.

![캡처.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8f95460b-6406-47a0-a831-488f989ee744/캡처.png)

![2.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff7c59ac-e174-4b24-839e-042ba67887b3/2.png)