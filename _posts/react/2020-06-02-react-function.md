---
title: React
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- React
toc: true
toc_sticky: true
toc_label: 목차

article_tag1: React
article_tag2: useState 
article_section: React useState
meta_keywords: React useState
last_modified_at: '2020-06-02 09:00:00 +0800'
---

## useState 를 통해 컴포넌트 관리
- useState 를 사용 할 때에는 상태의 기본값을 파라미터로 넣어서 호출, 여기서 첫번째 원소는 현재 상태, 두번째 원소는 Setter 함수입니다.

  ```javascript
  const [number, setNumber] = useState(0);
  ```

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

  이어 다음은 spread 문법 ...