---
layout: single
title:  "\\[CSS\\] 텍스트 요소 가로, 세로 가운데 정렬"
excerpt: ""

categories: 
    - CSS
tag: [web, lang, css, basics]
toc: true
author_profile: false
sidebar:
    nav: "docs"
---

```css
body {
	background-color: #999;
}
.box {
	background-color: white;
	width: 300px;

	/* box 자체의 위치*/ 
	**margin: 50px auto; /* 가로 가운데 정렬 */
	/* margin: 위아래, 양옆(절반씩 양옆에 분배함) */**

	/* box 내 text의 위치 */
	**text-align: center; /* box 내의 모든 inline들이 box 내에서 가로중앙정렬됨 */**
}
```

- 1번 결과
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/578e5b66-7624-4582-a9fd-b7185017b419/margin_0_auto.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/578e5b66-7624-4582-a9fd-b7185017b419/margin_0_auto.png)
    

```html
<div class="box">
	<span>wow!</span>
</div>
```

```css
.box {
	background-color: white;
	width: 300px;
	**height: 200px; /* 높이, 즉 height 값이 설정된다면? */**
	margin: 50px auto;
	text-align: center;
}
span { /* test용 span*/
	background-color: orange;
	display: inline-block;
	/* 배경색이 정상적으로 표현이 되기 위해서는 
		 width, height를 지정할 수 있는 block화가 되어야 
		 테스트가 된다. */
}
/* 
line-height : 줄 간격을 바꿔줄 때 사용하는 속성
	
*/
```

- 2번 결과
    
    ![height 값만 설정해주고, 다른 조치를 하지 않은 상황
    **이 상황을 해결하려면 어떻게 해야할까?**](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1ea9d796-3bd8-4b0d-8ad1-e24eeb525875/span_test1.png)
    
    height 값만 설정해주고, 다른 조치를 하지 않은 상황
    **이 상황을 해결하려면 어떻게 해야할까?**
    

```css
span {
	background-color: orange;
	display: inline-block;
	**height: 200px; 
	/* block 기준에서의 height이므로 text엔 영향이 없다. 
		 그래서 wow!는 계속 상단에 위치한다. 
		 그러면 어떻게 하면 해결할 수 있을까?
		 바로, inline 세계에서의 height property를 적용하면 된다.
		 다음예제와 비교해보자.
	*/**
}
```

- ****height: 200px; 결과
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/81b64e37-edea-4667-83ae-34c567941af0/2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/81b64e37-edea-4667-83ae-34c567941af0/2.png)
    

```css
span {
	background-color: orange;
	display: inline-block;
	**line-height: 200px; 
  /* inline 세계에서의 height이다. 
     한 줄의 높이가 200px이 되었다! 텍스트를 기준으로 윗공간, 아래공간이 
		 늘어나게 된다.** **하지만 이 방법도 완벽하게 중앙에 텍스트가 위치하진 않는다.
		 다양한 폰트의 글자들이 최대한 중앙에 배치될 수 있게 만들어져 있기 때문이다.
		 이건 어떻게 해결할 수 있을까?
	*/**
}
```

- line-height: 200px; 결과
    
    ![한 줄의 높이가 200px이 되었다! 텍스트를 기준으로 
    윗공간, 아래공간이 늘어나게 된다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/651efc2c-738e-497c-874f-42be4953492e/3.png)
    
    한 줄의 높이가 200px이 되었다! 텍스트를 기준으로 
    윗공간, 아래공간이 늘어나게 된다.
    

```css
span {
	background-color: orange;
	display: inline-block;
	line-height: 210px; 
	/* **line-height 값을 더 주어 해결한다.**
		 **하지만 이런 방법도 잘 쓰이지 않는다.** 
     **반응형 웹의 발전으로 화면이 달라져도 레이아웃이 유지되어야 하는데
		 이 방법은 다소 불안정하기 때문이다. 결과부분을 보면서 이해해보자.**
	*/
}
```

- line-height를 더 부여 결과
    
    ![line-height: 210px;](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4cddb21-acf9-40de-97f6-f7fe77088e91/4.png)
    
    line-height: 210px;
    
    ![이 방법의 문제점. 줄의 높이가 전부 200px이라 한 줄 간의 간격이 위와 같이 너무 차이가 나는 
    사태가 발생한다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44516983-f354-4c0b-b5c4-6f752c1c8bb2/5.png)
    
    이 방법의 문제점. 줄의 높이가 전부 200px이라 한 줄 간의 간격이 위와 같이 너무 차이가 나는 
    사태가 발생한다.
    

```css
.box {
	background-color: white;
	width: 300px;
	**~~height: 200px;~~ /* 부모 요소의 height값을 삭제하고*/**         
	margin: 50px auto;
	text-align: center;
	**padding: 3em; /* 그냥 padding값을 부여하는게 좋다! */
	/* padding: 1em 0; 
     1em: .box가 가진 font-size와 비례해서 padding값 부여
		 이후 font-size가 변경이 되어도 이에 비례하여 padding값이 부여되어,
		 세로 중앙 정렬이 유지되고, 궁극적으로 레이아웃이 유지된다.
     또한 text가 추가되어도 가운데 정렬이 깨지지 않고 유지된다!!!
  */**
}
```

- .box의 height 삭제, padding 추가 결과
    
    ![text 위아래에 padding이 잡혀있기 때문에
    text가 중간에 위치하게 된다. 직접 지정하지 않았기 때문에 수치적으로 정확한 위치를 알긴 어렵다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a71b1e10-797d-45a7-904d-381b05b2f255/6.png)
    
    text 위아래에 padding이 잡혀있기 때문에
    text가 중간에 위치하게 된다. 직접 지정하지 않았기 때문에 수치적으로 정확한 위치를 알긴 어렵다.
    
    ![em을 사용하면 좋은 점
    이후 font-size가 변경이 되어도 이에 비례하여 
    padding값이 부여되어, 세로 중앙 정렬이 유지되고, 
    궁극적으로 레이아웃이 유지된다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d3a4526-5fe4-4450-ac2a-07c80f379760/7.png)
    
    em을 사용하면 좋은 점
    이후 font-size가 변경이 되어도 이에 비례하여 
    padding값이 부여되어, 세로 중앙 정렬이 유지되고, 
    궁극적으로 레이아웃이 유지된다.
    
    ![두줄이 되어도 세로 중앙 정렬이 유지된다.
    여기서 line-height를 적용하여 두줄 간의 간격을
    조정할 수도 있을 것이다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5bd13b25-3085-4995-8cb1-fe7c561cd6a2/8.png)
    
    두줄이 되어도 세로 중앙 정렬이 유지된다.
    여기서 line-height를 적용하여 두줄 간의 간격을
    조정할 수도 있을 것이다.
    

## line-height에 대해 알아보자!

- half-leading
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4366581-89a9-4ed3-aa5c-b2f2ecddd2b6/leading_area.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4366581-89a9-4ed3-aa5c-b2f2ecddd2b6/leading_area.png)
    

leading 공간을 반으로 분할해 half leading 공간을 위아래에 배치한다.

<aside>
💡 Q. leading 공간은 왜 만들어진 것일까?
A. inline 요소가 여러줄이 되었을 때, 줄과 줄 사이에 존재하여 text를 읽기 편하게 해준다.
    줄 간격, 행간을 의미하는 요소이다.

</aside>

- 그래서 16px이 어디 길이라고?
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46a8aea0-803f-4742-bdf8-3f39256f8230/16px.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46a8aea0-803f-4742-bdf8-3f39256f8230/16px.png)
    

font-size를 기본적으로 바꾸지 않았다면 16px이 부여된다. 

- 라인하르트가 아니고 line-height!
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e306036-bd79-4d08-94c0-a4ef3d3bafa0/line-height.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e306036-bd79-4d08-94c0-a4ef3d3bafa0/line-height.png)
    

<aside>
💡 line-height라는 값은 font-size랑 leading 영역을 포함한 값이다. 
font에 따라 line-height 값이 달라질 수 있으므로 
text 크기에 비례하는 `em`으로 line-height 값을 부여하는 것이 이상적이다.

</aside>

<aside>
💡 Q. 만약 line-height에 큰 값이 적용되었다면?(font-size는 기본값) ex. 500px
A. 500px - 16px = 484px 총 line-height 부여 px
    484 / 2 = 242px 만큼의 half-leading 공간이 위아래에 배치된다.

</aside>

### 실습! image를 가운데 정렬해보자

**image도 inline 요소**이기 때문에 위의 방법을 응용하여 가운데 정렬시킬 수 있다!

```html
<div class="box">
	<img src="images/icon.png">
</div>
```

```css
.box {
	background-color: white;
	width: 300px;
	height: 300px;
	margin: 50px auto;
	**text-align: center; /* 이미지가 가로 중앙정렬된다! */

	/* box의 가운데에 img를 정렬하려면 어떻게 해야될까?!!! */**
	**line-height: 300px;** 
	**/* line-height를 height와 똑같은 값을 준다.
     하지만 inline 관점에서 보았을 때, 이미지는 baseline을 기준으로 배치되기 때문에  
		 완전히 중앙에 오지는 못한다.**		 
		
		 **이를 어떻게 해결할까?**
		 text와 image와의 관계는 baseline을 기준으로 되어있다.
		 **vertical-align: middle;로 해결한다!
		 image는 line-height기준에서 세로 가운데 정렬이 되고, 
     text는 image에 상대적으로 중간에 위치할 수 있다.

		 image나 다른 inline-block element들은
		 text를 가운데 정렬시키는 이 inline 방법을 이용하여
     중앙정렬시킬 수 있다.**
	*/

}

```

- [이미지 중앙정렬] 결과
    
    ![image가 baseline기준으로 배치되어 
    완전히 중앙에 오진 못했다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5276fda3-6a22-422d-8874-61eb00506bac/이미지_중앙정렬.png)
    
    image가 baseline기준으로 배치되어 
    완전히 중앙에 오진 못했다.
    
    ![image와 text는 baseline을 기준으로 
    배치되는 관계이다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/743346ee-9797-4db2-a5b6-6e2ab658ee5c/이미지와_텍스트는_베이스라인_관계.png)
    
    image와 text는 baseline을 기준으로 
    배치되는 관계이다.
    
    ![vertical-align 속성으로 image를 
    중앙정렬시켰다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/edcd507d-95aa-4ad3-add3-d595e8e7df09/vertical-align.png)
    
    vertical-align 속성으로 image를 
    중앙정렬시켰다.
    

[CSS 텍스트 요소 가로, 세로 가운데 정렬 | OACSS 가운데 정렬 특집 | 빔캠프](https://www.youtube.com/watch?v=PEYt17TlTQk&t=456s)