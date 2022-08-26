---
layout: single

title:  "MongoDB Datatypes"
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
- 셸을 명령행 도구의 일부로 사용하는 방법
- 커스터마이징 방법
- 고급 기능 사용

#### 다른 장비나 포트에 mongod에 연결할 때
로컬 mongod 인스턴스에 연결했지만 사용자 시스템에서 연결할 수 있는 어떤 몽고DB 인스턴스든 셸을 연결할 수 있음
다른 장비나 포트에 mongod에 연결하려면 셸을 시작할 때 **호스트명, 포트, DB**를 명시해야 함
``` shell
$ mongo <호스트명>:<포트>/<DB명>

$ mongo some-host:30000/myDB
MongoDB shell version: 4.2.0
connecting to: some-host:30000/myDB
>
```

#### 셸 활용 팁
mongo는 기본적으로 JS 셸이므로 
- 온라인 자바스크립트 문서 참조
- help로 내장 도움말 조회
  ``` shell
  > help
      db.help()             help on db methods / DB 수준의 도움말
      db.mycoll.help()      help on collection methods / 컬렉션 수준의 도움말
      sh.help()             sharding helpers
      ...

      show dbs              show database names
      show collections      show collections in current database
      show users            show users in current database
      ...
  ```

  ``` shell
  > db.movies.updateOne
  function (filter, update, options) {
      var opts = Object.extend({}, options || {});

      // 갱신문의 첫 번째 키가 $를 포함하는지 확인
      var keys = Object.keys(update);
      if (keys.length == 0){
          throw new Error("the update operation document must contain at
          least one atomic operator");
      }
      ...
  }
  ```
  
#### 셸에서 스크립트 실행
JS 파일을 셸로 전달하여 사용 가능
``` shell
$ mongo script.js script2.js script3.js
MongoDB shell version: 4.2.1
connectiong to: mongodb://127.0.0.1:27017
MongoDB server version: 4.2.1
loading file: script1.js
I am script1.js
loading file: script2.js
I am script2.js
loading file: script3.js
I am script3.js
...
```


``` js
// defineConnectTo.js

// DB에 연결하고 db 설정
var connectTo = function(port, dbname){
  if(!port){
    por = 27017;
  }

  if(!dbname){
    dbname = "test";
  }

  db = connect("localhost:"+port+"/"+dbname);
  return db;
}
```

``` shell
> typeof connectTo
undefined
> load('defineConnectTo.js')
> typeof connectTo
function

```

#### mongorc.js 만들기
``` js
// .mongorc.js

var compliment = ["attractive", "intelligent", "like Batman"];
var index = Math.floor(MAth.random()*3)

print("Hello, you're looking particularly" + compliment[index] + "today!");
```

``` 
$ mongo
MongoDB shell version 4.2.1
connecting to: Test
Hello, you're looking particulary like Batman today!
>
```

#### 프롬프트 커스터마이징

#### 복잡한 변수 수정하기

#### 불편한 컬렉션명

