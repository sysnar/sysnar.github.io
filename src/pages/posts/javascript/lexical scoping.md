---
title: Javascript Lexical Scoping
excerpt: >-
  Javascript 동작구조인 Lexical Scope에 대해 기록합니다.
date: "2021-10-07 00:20"
thumb_img_path: images/jsLogo.png
thumb_img_alt: Hikers on the trail
content_img_path: images/jsLogo.png
content_img_alt: Hikers on the trail
seo:
  title: Javascript Gatter와 Setter
  description: >-
    Hiking refers to difficult walking through dense forest, undergrowth, or
    bushes.
  extra:
    - name: "og:type"
      value: article
      keyName: property
    - name: "og:title"
      value: Basic Rules For Walking In The Mountains
      keyName: property
    - name: "og:description"
      value: >-
        Hiking refers to difficult walking through dense forest, undergrowth, or
        bushes.
      keyName: property
    - name: "og:image"
      value: images/jsLogo.png
      keyName: property
      relativeUrl: true
    - name: "twitter:card"
      value: summary_large_image
    - name: "twitter:title"
      value: Basic Rules For Walking In The Mountains
    - name: "twitter:description"
      value: >-
        Hiking refers to difficult walking through dense forest, undergrowth, or
        bushes.
    - name: "twitter:image"
      value: images/jsLogo.png
      relativeUrl: true
template: post
---

# Javascript Lexical Scoping

javascript 에서의 this를 공부하기 전 scope의 개념을 정확하게 설명할 수 있도록 정리하려고 합니다.

1. [실행 컨텍스트 (Execution Context)](https://sysnar.github.io/posts/javascript/scope/)
2. [클로저](https://sysnar.github.io/posts/javascript/closure/)
3. [lexical scoping](https://sysnar.github.io/posts/javascript/lexical%20scoping/)

## Scope란?

javascript를 쓰다보면 `Scope`라는 단어를 참 많이도 접하지만, 정작 한줄로 설명하기는 어려운 것 같습니다.

`Scope`는 한마디로 <mark>변수에 접근할 수 있는 범위</mark>라고 정의할 수 있습니다.

이런 Scope에는 2가지 종류가 있습니다.

1. 전역 스코프(Global Scope)
2. 지역 스코드(Local Scope)

Global Scope는 웹 브라우저의 경우(window, docuement), Node.js의 경우(global) 등의 객체에 선언되어 어느 곳이던지 해당 변수에 접근하여 사용할 수 있다는 뜻이며,  
Local Scope는 특정 범위가 주어지고 그 범위 안에서만 접근할 수 있다는 것을 의미합니다.

이 내용을 이해하기 위한 간단한 예시가 있습니다.

```js {numberLines}
let x = "global";
function ex() {
  x = "change";
}
ex();
alert(x); // 'change'
```

javascript의 특성상 변수의 범위를 호출한 함수의 Local Scope부터 전역 변수들이 있는
Global Scope까지 범위를 점차 넓혀가며 찾기 때문에 함수 ex의 Scope 내에 없는 변수 x를 찾아 값을 변경하게 됩니다.  
만약 함수 ex 내에 변수 x가 존재했다면 지역변수 x에 값을 할당하고 전역변수의 값은 변경되지 않았을 것 입니다.

![Awesome image](../../../images/scopeExample.png)

## Scope Chain

전역변수와 지역변수 같의 관계에서 나오는 개념이다.  
내부 함수에서는 외부에 접근이 가능하지만 외부에서는 접근이 불가능한 특성을 가진다.  
아래의 예시에서 확인이 가능하듯이 내부 함수에서 선언되어 있지 않은 name이라는 변수를 호출할 때  
계속적으로 스코프를 확장해나가며 결과적으로는 전역변수를 호출하는 것을 확인할 수 있다.

```js {numberLines}
var name = "zero";
function outer() {
  console.log("외부", name);
  function inner() {
    var enemy = "nero";
    console.log("내부", name);
  }
  inner();
}
outer();
console.log(enemy); // undefined
```

## Lexical Scoping

```js {numberLines}
var name = "zero";
function log() {
  console.log(name);
}

function wrapper() {
  name = "nero";
  log();
}
wrapper(); // nero
```

```js {numberLines}
var name = "zero";
function log() {
  console.log(name);
}

function wrapper() {
  var name = "nero";
  log();
}
wrapper(); //zero
```

출처 :  
https://www.zerocho.com/category/Javascript/post/5740531574288ebc5f2ba97e  
https://medium.com/@su_bak/javascript-스코프-scope-란-bc761cba1023
