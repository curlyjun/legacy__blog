---
layout: post
title: package.json
category: Nodejs
tags: JavaScript Nodejs
comments: true
---



npm에서 핵심적인 역할을 하는게 package.json 이라고 한다. package.json은 패키지에 관한 정보와 의존중인 버전에 관한 정보를 담고있다. 

```json
{
  "name": "chatterbox-server",
  "version": "1.1.0",
  "description": "Implement a chat server",
  "license": "UNLICENSED",
  "private": true,
  "engines": {
    "node": ">=4.0.0"
  },
  "scripts": {
    "start": "nodemon server/basic-server.js",
    "test": "node __test__/getReview && jest",
    "test:circleci": "node __test__/getReview && jest --json --outputFile=.circleci/results.json"
  },
  "devDependencies": {
    "husky": "^1.3.1",
    "request": "^2.70.0",
    "supertest": "^3.4.2",
    "eslint": "^5.12.0",
    "jest": "^24.1.0"
  },
  "husky": {
    "hooks": {
      "pre-commit": "eslint ./server"
    }
  }
}

```

위는 현재 진행중인 스프린트의 package.json 내용이다. 위에서부터 살펴보면 

**name** 과 **version**은 필수로 입력해야하는 부분이다. 이 둘이 누락되면 패키지를 설치할 수 없다. 

**description**은 설명을 기술하는 부분이다. 패키지를 찾아내고 이해할 때 도움이 될 수 있다. 

**license**부분은 이 패키지를 사용하기 위해 어떻게 권한을 얻는지, 어떤 금기사항이 있는지 명시하는 부분이다. 

**private**는 이 패키지를 공개할 것인지 비공개할지를 정하는 부분이다.

**engines**를 통해 node의 버전을 지정할 수 있다. 사용자가 engin-strict config flag 를 설정하지 않으면 단지 조언용으로만 사용된다고 한다.

**scripts**항목에서의 key는 이벤트고 value는 입력시 실행될 커맨드이다. 예를들어 npm start를 하게되면 nodemon server/basic-server.js를 실행한 것과 동일하다. 중요한 부분이라니 나중에 [자세한 내용(npm-script)](https://docs.npmjs.com/misc/scripts)을 참고해서 봐야겠다.

**dependencies, devDependencies, peerDependencies**    package.json은 현재 의존중인 패키지 버전을 다음과 같은 세 가지 종류로 기록해 준다. **dependencies**는 일반적인 경우 의존하고 있다는 것을 알려주는 곳이고 **devDependencies**는 개발 모드일 때만 의존하고 있다는 것을 알려주는 곳이다. 예를 들어 배포에 필요없는 웹팩, 바벨같은 것들을 넣어두면 된다고한다. 마지막으로 **peerDependencies**는 만든 패키지가 다른 패키지에 직접 require가 되는 것은 아니지만 그 호스트 패키지와 호환성을 가지고 있는 것을 표현할 때(이런 것을 플러그인이라고 한다) 사용된다. (이 부분은 잘 이해가가지 않았다.)

**husky**부분도 정확한 이해는 아니지만 설치한 husky를 사용하는 것 같은데, 커밋하기 전에 eslint 로 검사를 하게 해주는 것 같다. 이부분도 다시 공부를 해서 정리를 해야겠다.



### 참고사이트

[https://programmingsummaries.tistory.com/385](https://programmingsummaries.tistory.com/385)

[https://www.zerocho.com/category/NodeJS/post/5825a3caaff5c70018279975](https://www.zerocho.com/category/NodeJS/post/5825a3caaff5c70018279975)

