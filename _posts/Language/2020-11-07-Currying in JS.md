---
layout: post
title: "[번역]Currying in Javascript 자바스크립트 커링"
author: "Oizys18"
categories: [Language]
comments: true
tags: [Javascript,Language,Currying]
---
* TOC
{:toc}
* * *
- JS 공부중 도움이 되는 글을 번역한 게시글입니다. 
Author: [Rémi](https://www.codementor.io/@michelre)

Original Post: [Currying in JS](https://www.codementor.io/@michelre/currying-in-javascript-g6212s8qv)

![20201107_1](../assets/../../assets/images/2020-11-07_1.png)


커링은 모든 함수형 프로그래밍 언어의 중심에 있는 중요한 개념이다. 커링이 무엇이고 왜 사용해야하는지 살펴보자. 

## 커링이란?

커링은 N개의 항수(인자)를 갖는 함수 하나를 1개의 항수(인자)를 갖는 N개의 함수로 만들 수 있는 수단입니다. 요컨대, 커링을 사용하면 함수 하나를 호출할 때 한번에 모든 인자를 정확히 지정하지 않아도 됩니다. 간단한 예제를 보겠습니다. 아래와 같은 방식이 익숙할 것입니다. 

```
const add = (a, b) => a + badd(1, 2) //should return 3
```

커리를 적용하면, 대신 이런 방식을 사용할 수 있습니다. 

```
const add = a => b => a + badd(1)(2) //should return 3
```

`add`함수가 작성된 방식을 눈여겨 보십시오. 위 함수는 첫번째 인자 `a` 를 받아서 두번째 인자 `b` 를 받는 또 다른 함수를 반환하는 함수입니다. 모든 인자가 제공되었을 때, 연산이 작동합니다. 이 예시에서는, `add(1)` 를 호출하면 하나의 함수를 반환합니다.

Javascript는 함수가 일급시민(first-class citizen)이기 때문에 커링을 사용할 수 있습니다. 즉, 함수는 다른 값들과 유사합니다. JS의 함수는 변수에 할당되거나, 다른 함수에 인자로 제공되거나 혹은 함수에서 반환될 수도 있습니다.  

## **커링의 중요성**

커링을 사용하면 함수를 부분적으로 수정할 수 있으며 이를 이용해 재사용 가능한 함수를 만들 수 있습니다.  **다른 예시를 살펴보겠습니다. 다음과 같은 collection을 가정해봅시다.** 

```jsx
const movies = [
  {
    "id": 1,
    "name": "Matrix"
  },
  {
    "id": 2,
    "name": "Star Wars"
  },
  {
    "id": 3,
    "name": "The wolf of Wall Street"
  }
]

```

이 collection에서 `id` 들을 추출하고 싶다고 가정합시다. 그냥 간단하게 `map` 함수로 collection 전체를 순회할 수 있습니다.  

```jsx
movies.map((movie) => movie.id) //should return [ 1, 2, 3 ]
```

좋습니다. 시리즈라는 두번째 collection이 있다고 가정합시다. 

```jsx
const series = [
  {
    "id": 4,
    "name": "South Park"
  },
  {
    "id": 5,
    "name": "The Simpsons"
  },
  {
    "id": 6,
    "name": "The Big Bang Theory"
  }
]

```

방금 전과 동일하게 `id` 들을 추출하고 싶다면:

```jsx
series.map((serie) => serie.id) //should return [ 4, 5, 6 ]
```

`map` 의 콜백들은 완전히 동일합니다. 하지만 우린 서로 다른 두 개의 collection에 각각 실행했습니다. 이런 경우에서 커링을 활용할 수 있습니다. 객체에서 속성을 추출하는 `get` 이라는 함수 호출을 작성해 봅시다.  

```jsx
const get = property => object => object[property];
```

또 이 함수에서 `get` 함수의 부분적인 수정본인  `getId` 라는 또 다른 함수를 작성할 수 있습니다. 

```jsx
const getId = get('id');
```

이 단계에서 `getId` 는 아직 함수입니다. 따봉! `map` 호출 내부에서 사용할 수 있어서 유용합니다.

```jsx
movies.map(getId); //should return [ 1, 2, 3 ]
series.map(getId); //should return [ 4, 5, 6 ]
```

훌륭하지 않습니까..? 하지만 한 단계 더 나아갈 수 있습니다. 이제 이 객체들 중에서 이름을 추출하고 싶다고 가정합시다. 어떻게하면 될까요? 그냥 `get` 함수를 수정한 `getName` 함수를 작성하면 됩니다.

```jsx
const getName = get('name');
```

그러면 collection에서 이름을 추출할 때 사용할 수 있습니다. 

```jsx
movies.map(getName); //should return [ 'Matrix', 'Star Wars', 'The wolf of Wall Street' ]
```

## **결론**

커링은 함수형 프로그래밍의 중요한 부분입니다. 이 글에서 작성된 것처럼 따라해보시길 권장합니다. [Ramda](http://ramdajs.com/)나 [Lodash/fp](https://github.com/lodash/lodash/wiki/FP-Guide) 같은 함수형 라이브러리를 사용한다면, 대부분의 함수는 default로 커링이 적용되어 있습니다. 따봉! 

ES6와 람다 함수를 이용하면 N개의 인자를 가진 함수를 1개의 인자를 가진 N개의 함수로 분해하는 것이 어려운 일이 아니라는 것을 잊지마세요! 커링 덕분에 재사용 불가능한 코드를 작성할 이유가 없습니다!