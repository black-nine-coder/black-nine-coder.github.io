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
# article_section: React useState
# meta_keywords: React useState
last_modified_at: '2020-06-02 09:00:00 +0800'
---

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
