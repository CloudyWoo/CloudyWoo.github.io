---
layout: single

title:  "[Dart] 매개변수"
excerpt: ""

categories: 
    - Dart
tags: [Dart, parameters, basics]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-27
last_modified_at: 2022-08-27
---

### 선택 매개변수

함수 정의에서 { }로 감싼 매개변수는 선택적으로 사용할 수 있다.
호출할 때 매개변수명을 값 앞에 써주면 된다. 그래서 **이름 있는 매개변수(Named Parametrt)**라고도 부른다.

```dart
// 실습 #1
bool canDrink(int age, bool haveEnoughMoney, {String? name}) {
  // age, haveEnoughMoney는 필수 매개변수
  // name은 선택 매개변수
  if(age < 20){
    return false;
  }
  return true;
}

void main() {
  print(canDrink(21, true, name: "Sungmin Woo"));
}

// 결과: true
```