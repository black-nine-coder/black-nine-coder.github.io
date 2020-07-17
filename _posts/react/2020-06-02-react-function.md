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

## useState
- useState 를 사용 할 때에는 상태의 기본값을 파라미터로 넣어서 호출, 여기서 첫번째 원소는 현재 상태, 두번째 원소는 Setter 함수입니다.

  ```javascript
  const [number, setNumber] = useState(0);
  // number에 0 할당 setter로 setNumber를 사용
  ```

## useRef
- Hook 은 DOM 을 선택 및 컴포넌트 안에서 조회 및 수정(변수를 관리)
```javascript
  const next = useRef(1);
  // 파라미터의 1은 .current 값의 기본값이 됨
```