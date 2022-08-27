---
layout: single

title:  "[MongoDB] 도큐먼츠(Documents)"
excerpt: ""

categories: 
    - MongoDB
tags: [nosql, mongodb]

toc: true
author_profile: false
sidebar:
    nav: "docs"

date: 2022-08-20
last_modified_at: 2022-08-20
---

#### 목표
- 컬렉션에 새 도큐먼트 추가
- 컬렉션에서 도큐먼트 삭제
- 기존 도큐먼트 업데이트
- operation 수행할 때 안전성과 속도 필요한 정도 판단

---

#### 도큐먼트 삽입
##### insertMany
##### 삽입 유효성 검사
##### 삽입

---

#### 도큐먼트 삭제
db.movies.find()
db.movies.deleteOne({"_id" : 4})
db.movies.find()

db.movies.find()
db.movies.deleteMany({"year" : 1984})
db.movies.find()

db.mailing.list.deleteMant({"opt-out" : true})

##### drop
db.movies.find()
db.movies.deleteMany({})
db.movies.drop()

---

#### 도큐먼트 업데이트


##### 도큐먼트 replace
```
{
  "_id" : ObjectId("~~~"),
  "name" : "joe",
  "friends" : 32,
  "enemies" : 2
}
```

```
var joe = db.users.findOne({"name" : "joe"});
joe.relationships = {"friends" : joe.friends, "enemies" : joe.enemies};

joe.username = joe.name;
delete joe.friends;
delete joe.enemies;
delete joe.name;
db.users.replaceOne({"name" : "joe"}, joe);
```

```
{
  "_id" : 
}
```

##### update 연산자
- "$set" 제한자(원어는?) 사용하기
- 증가와 감소
- 배열 연산자
- 요소 추가하기
- 배열을 집합으로 사용하기
- 요소 제거하기
- 배열의 위치 기반 변경
- 배열 필터를 이용한 갱신

---
#### upsert, 갱신 입력

---
#### 다중 도큐먼트 업데이트

---
#### 업데이트한 도큐먼트 반환