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

React HOOK 위주로 작성 Category를 따로 관리 예정..

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

## useEffect
- 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 실행할 수 있도록 하는 Hook

+ useEffect 실행 
  - 화면이 처음 떴을때 실행.
  - deps에 [] 빈배열을 넣을 떄.
  - life cycle중 componentDidmount처럼 실행
  - 화면이 사라질때 실행(clean up함수).
  - componentWillUnmount처럼 실행
  - deps에 넣은 파라미터값이 업데이트 됬을때 실행.
  - componentDidUpdate처럼 실행.

+ 마운트 시에 하는 작업들은 사항
  - props 로 받은 값을 컴포넌트의 로컬 상태로 설정
  - 외부 API 요청 
  - 라이브러리 사용
  - setInterval 을 통한 반복작업 혹은 setTimeout 을 통한 작업 예약

- useEffect 를 사용 할 때에는 첫번째 파라미터에는 함수, 두번째 파라미터에는 의존값이 들어있는 배열(deps)을 넣는다.

```javascript
    useEffect(() => {
      console.log('컴포넌트 나타남!!');
      return () => {
        console.log('컴포넌트 사라짐!!');
      };
    }, [AAA]);
```

## useMemo