---
layout: post
title: "tsconfig.json"
author: "Oizys18"
categories: [Web]
comments: true
tags: [React, Javascript, Typescript, TS, Intro, Framework, Frontend]
---
* TOC
{:toc}
* * *

# 02-3 tsconfig.json 살펴보기

- `tsc --help`
- compilerOptions
- include

### module

동작 대상 플랫폼이 Web인지 nodeJS인지를 구분해 맞는 모듈방식으로 컴파일 하려는 목적으로 설정한다. 플랫폼에 따라 다음과 같은 값을 설정할 수 있다. 

- web: amd
- nodeJS: commonjs
- TS 코드가 컴파일되어 만들어진 ES5 JS 코드는 Web과 nodeJS 양쪽에서 모두 동작해야한다.
- 그런데 Web과 nodeJS는 물리적 작동 방식이 다르기 때문에, 모듈로 분할된 JS코드 또한 Web과 nodeJS 양쪽에서 다르게 동작한다.
- JS 모듈은 웹에서는 AMD(asynchronous module definition) 방식으로 동작하고 nodeJS처럼 웹이 아닌 환경에서는 commonJS 방식으로 동작한다.

### moduleResolution

module 키의 값이 commonjs면 nodejs라는 뜻이므로 moduleResolution의 값은 항상 node이다. 

반면 module 값이 amd라면 moduleResolution 값은 classic으로 설정한다. 

### target

트랜스파일할 대상 JS의 버전을 설정한다. 

대부분 es5를 값으로 설정한다. 만약 최신버전의 nodejs라면 es6을 설정할 수 있다. 

### baseUrl과 outDir

트랜스파일된 ES5 JS 파일을 저장하는 디렉터리를 설정한다. 

tsc는 tsconfig.json 파일이 있는 디렉터리에서 실행된다. 

baseUrl은 보통 현재 디렉터리인 `.` 로 설정한다. 

OutDir은 baseDir 설정값을 기준으로 하위 디렉터리의 이름이다. 빌드된 결과가 설정값 디렉터리에 만들어진다. 

### paths

소스 파일의 import문에서 from부분을 해석할 때 찾아야 하는 디렉터리를 설정한다. 

import 문이 찾아야 하는 소스가 외부 패키지이면 node_modules 디렉터리에서 찾아야 하므로 키값에 node_modules/* 도 포함한다.

### esModuleInterop

오픈소스 JS 라이브러리 중에는 web에서 동작한다는 가정으로 만들어진 것이 있는데 이것들은 commonJS방식으로 동작하는 TS 코드에 혼란을 줄 수 있다. 따라서 AMD 방식을 전제로 구현된 라이브러리들이 동작하려면 esModuleInterop 값을 반드시 true로 설정해야한다. 

### sourceMap

값이 true이면 트랜스파일 디렉터리에는 .js말고도 .js.map파일이 만들어진다. 이 소스맵 파일은 변환된 js 코드가 ts 코드의 어디에 해당하는지를 알려준다. 주로 디버깅할 때 사용된다. 

### downlevelIteration

생성기 generator 구분이 정상적으로 동작하려면 해당 키값을 true로 설정해야한다. 

### noImplicitAny

ts 컴파일러는 기본적으로 f(a,b)처럼 매개변수 a,b에 타입을 명시하지 않은 코드일 경우 f(a:any, b:any)처럼 암시적으로 any 타입을 설정한 것으로 간주한다. 이런 형태의  코드는 ts 언어의 장점을 사용하지 않는 것이므로, 코드에 문제가 있음을 알려준다. 하지만 에러메세지가 직관적이지 못해서 혼란을 줄 수 있기 때문에, 해당 키값을 false로 설정하면 타입미지정 시에도 에러메세지를 출력하지 않는다.