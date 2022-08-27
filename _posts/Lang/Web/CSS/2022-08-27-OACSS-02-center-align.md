---
layout: single
title:  "\\[CSS\\] 너비높이를 알 수 없는 div 가로세로 모두 가운데 정렬"
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
.box {
	background-color: white;
	
	width: 300px;
	**height: 400px;** /* margin 값을 적용하기 위해서 height를 지정해줄 수 밖에 없음 */

	text-align: center; /* text 가운데 정렬*/
	overflow: hidden; /* margin이랑 content랑 겹침 방지 */
	
	**position: absolute;**
	**left: 50%;** /* 기준점(**부모기준**,왼쪽윗끝)으로부터 왼쪽으로 50%만큼 떨어져 있음 */
	**top:50%;** /* 기준점으로부터 위쪽으로 50%만큼 떨어져 있음  */

	**margin-left: -150px;** /* 요소의 기준점도 윗쪽 끝이므로 가운데 정렬이 정확히 안됨 */
	**margin-top: -200px;** /* 따라서 기준점을 속여주기 위해 negative margin 사용이 필요함 */

}
```

```css
.box {
	transform: translate(-50%, -50%); 
	/*
		얘는 **자기자신(너비, 높이)이 기준
		따라서 너비인 300px의 50%인 150px만큼 x축 이동됨.
		높이 또한 지정하진 않았지만 auto의 절반만큼 y축 이동이 진행된다.**
	*/
}
```