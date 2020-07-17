---
title: Javascript
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Javascript
toc: true
toc_sticky: true
toc_label: 목차

article_tag1: Javascript
article_tag2: function 
# article_section: Javascript
# meta_keywords: Rest Spread
last_modified_at: '2020-06-23 09:00:00 +0800'
---

## 브라우저의 동작 방식
1. HTML을 읽기 시작한다.
1. HTML을 파싱한다.
1. DOM 트리를 생성한다.
1. Render 트리(DOM tree + CSS의 CSSOM 트리 결합)가 생성되고
1. Display에 표시한다.

## Hello javascript 
```javascript
console.log('Hello javascript');
```
## Rest 파라미터와 Spread 연산자
- Rest 파라미터 (Rest Parameter)

    - Rest 파라미터는 Spread 연산자(...)를 사용하여 함수의 파라미터를 작성한 형태
    즉, Rest 파라미터를 사용하면 함수의 파라미터로 오는 값들을 "배열"로 전달받을 수 있다.

        ```javascript
        function exam(...args) {
            console.log(Array.isArray(args)); 
            console.log(args); 
        }
        exam(1, 2, 3, 4, 5);
        // true
        // [ 1, 2, 3, 4, 5 ]
        ```
        ※ 단, Rest 파라미터는 항상 마지막 파라미터로 있어야 한다.


- Spread 연산자 (Spread Operator)

    - Spread 연산자는 배열, 문자열 등의 iterable(간단히 배열을 분해라고 생각..)을 분해해서 __개별요소__ 로 만들 수 있습니다.

## 프로토타입 과 클래스
##### javascript는 클래스 개념은 없고, 객체를 cloning 후 새로운 객체를 생성하는 프로토타입 기반의 언어 
- 객체 생성자 함수 아래에 .prototype.[원하는키] = 코드를 입력하여 설정

## 비구조화 할당
- 리액트 상태에서 객체를 수정해야 할 때에는, 새로운 객체를 만들어서 새로운 객체에 변화를 주고, 이를 상태로 사용해주어야 합니다.

  ```javascript
  const [inputs, setInputs] = useState({
      name: '',
      nickname: ''
  });
  .
  .
  .
  setInputs({
    ...inputs,
    [name]: value
  });
  ```