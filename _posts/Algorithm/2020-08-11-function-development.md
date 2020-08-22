---
layout: post
title: "프로그래머스 알고리즘 - 기능개발(파이썬,자바스크립트)"
author: "Oizys18"
categories: Algorithm
comments: true
tags: [Algorithm, Programmers, Javascript, Python, Stack,Queue]
---

* TOC 
{:toc}
* * *
   
## [문제](https://programmers.co.kr/learn/courses/30/lessons/42586)

## 풀이

- Stack/Queue 파트의 문제
- 개발 순서와 개발 속도는 별개
- 개발 속도가 빨라서 앞 순서의 기능개발보다 빨리 완료되어도, 앞의 기능개발이 완료되지 않으면 배포될 수 없다.
- 맨 앞의 개발이 완료되었을 시점에 만약 개발이 완료된 기능이 있다면(단, 앞순서에 완료되지 않은 기능이 있으면 해당 X) 함께 포된다.
- 개발이 완료되어 배포되는 시점마다 배포되는 기능의 갯수를 `Array`형태로 반환한다.
- 순서상 맨 앞의 기능이 배포되는 시점을 한 턴으로 생각했을 때,
  - 매 턴마다 소요되는 시간은 `math.ceil((100 - progresses[0])/speeds[0])`이다.
  - 즉, 매 턴마다 맨 앞의 기능개발이 완료되는 시간은 진행시키고 그 때 다른 프로젝트들의 진행경과를 확인하여 함께 배포되는 기능의 갯수를 `answer`에 추가하면 된다.

## 예시코드

### Javascript

- 예시 1
  - 아래 파이썬 예시2와 동일하다.
  - ~~파이썬 직후 풀었더니 `pop(0)`을 써서 한 번 틀렸다. 꼭 `shift`를 사용하자.~~

```javascript
function solution(progresses, speeds) {
  var answer = [];
  let time = 0;
  let count = 0;
  while (progresses.length) {
    if (progresses[0] + speeds[0] * time >= 100) {
      progresses.shift();
      speeds.shift();
      count += 1;
    } else {
      if (count > 0) {
        answer.push(count);
        count = 0;
      }
      time += 1;
    }
  }
  answer.push(count);
  return answer;
}
```

### Python

#### 예시 1

```python
def solution(progresses, speeds):
    import math
    answer = []
    def pass_day(progresses,speeds):
        completed_count = 0
        remain = 100 - progresses[0]
        passed_day =  math.ceil(remain/speeds[0])
        for idx,progress in enumerate(progresses):
            progresses[idx] += speeds[idx]*passed_day
        idx = 0
        while True:

            if progresses[idx] >= 100:
                completed_count += 1
                idx += 1
                if idx >= len(progresses):
                    break
            else:
                break
        return progresses[completed_count:], speeds[completed_count:],completed_count
    while len(progresses):
        progresses,speeds, cnt = pass_day(progresses,speeds)
        answer.append(cnt)
    return answer
```

#### 예시2

- 다른 사람의 코드에서 `time`을 증가시키며 `while`과 조건문을 통해 해결하는 방법을 보고 풀어봤다.

```python
def solution(progresses, speeds):
    answer = []
    time = 0
    count = 0
    while len(progresses):
        if progresses[0] + speeds[0]*time >= 100:
            progresses.pop(0)
            speeds.pop(0)
            count += 1
        else:
            if count > 0:
                answer.append(count)
                count = 0
            time += 1
    answer.append(count)
    return answer
```
