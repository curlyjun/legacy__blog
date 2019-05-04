---
layout: post
title: NextJS에서 페이지간 Query로 데이터 전송하기
category: JavaScript
tags: NextJS
comments: true
---

# NextJS에서 페이지간 Query로 데이터 전송하기

> 이번에 맡게된 프로젝트에서 NextJS를 사용했고, 사용하면서 페이지간 데이터를 전송할 일이 생겼습니다. 이 때 쿼리를 이용해 데이터를 전송한 방법에 대해 알려드리도록 하겠습니다.

## NextJS

![](/assets/images/post_img/nextJS.jpg)

시작하기에 앞서 [NextJS](https://nextjs.org/)에 대해 간략히 소개하자면 NextJS는 리액트 위에서 동작하는 프레임워크예요. NextJS가 해주는 일은  React의 서버 사이드 렌더링을 쉽게 할 수 있도록 도와주고 코드 스플리팅도 알아서 해줍니다. 이 뿐만 아니라 다양한 장점들이 존재합니다. React에서 서버 사이드 렌더링을 하려면 복잡해지는 부분들이 있어요. 상태 관리를 해주는 Redux같은 것들과 함께 하려면 더욱 더 복잡해지는 부분들이 있습니다. 이러한 복잡한 부분들을 nextjs를 사용해 쉽게 할 수 있게 해줍니다.



## 페이지간 데이터 전송은 왜..?

![](/assets/images/post_img/passingdata.jpg)

프로젝트를 진행하다보니 페이지 이동을 하면서 이전 페이지에 존재하던 데이터를 이동한 페이지에서도 사용하게 되는 경우가 있었습니다. 중복된 데이터를 서버에 요청을 보내 받아오는 거죠. 이러한 부분들을 개선하고자 쿼리에 이동할 페이지에 필요한 모든 정보를 담아보는 시도를 해보았어요. 



## Query에 데이터 담기

query에 데이터를 담을 때 필요한 작업이 있어요. 바로 **string**으로 형변환을 해줘야 하죠. 저는 전달하고 싶은 데이터가 Object형태였고 이를 <u>JSON.stringify()</u>라는 자바스크립트 내장 함수를 사용해서 변환을 해주었습니다. 왜냐하면 query는 URL에 포함되는 것이고 URL에는 string형태의 데이터만 들어갈 수 있기 때문이에요. string형태로 데이터를 바꾸어준 뒤 쿼리에 담아 보내니 원하던대로 데이터 전송을 할 수 있었습니다. 하지만 URL의 길이가 어마어마해져버리는 문제가 생겼죠.

![](/assets/images/post_img/longurl.png)

### clean url

[clean url](https://en.wikipedia.org/wiki/Clean_URL)이라고 들어보셨나요? 사용자 친화적이고 검색엔진 친화적인 URL을 말합니다. query로 데이터를 전송하게 되면 위처럼 더럽고 긴 url(Uncleaned URL)이 보여지게 되죠. 하지만 걱정마세요! NextJS에서는 이러한 URL을 아주 깔끔하게 바꿔주는 특수한 기능이 있거든요. 어떻게 가능한지 알아보도록 하겠습니다.



## NextJS에서의 Routing

NextJS에서는 크게 두가지 방법으로 페이지 라우팅이 가능합니다.

1. Link라는 컴포넌트를 통한 Client Side Route
2. URL입력, a tag이용 등을 통한 Server Side Route

두 번째는 익숙한 방법일 거라고 생각합니다. NextJS를 사용하지 않아도 접할 수 있는 것들이기 때문이죠. 하지만 Link라는 것은 NextJS에서 제공해주는 컴포넌트입니다. Link 컴포넌트를 사용하면 앞서 말씀드린 원래 URL과 다른 URL을 브라우저 URL 바에 Making해주는  Route Masking이라는 기능을 사용할 수 있습니다.

Link에는 여러가지 props들이 존재합니다. 이 글에서는 필요한 두 가지만 소개해드도록 하겠습니다.

- href : 실제 URL 주소
- as : masking되어 브라우저의 URL 바에 보여질 주소

```javascript
import Link from 'next/link';

//..생략
<Link
	as={`/admin/q/${quetions._id}` }
	href={{
	  pathname: '/admin/question/answer'  
	  query: { qeustion: JSON.stringify(question) }
	}}
>
  <a>{question.title}</a>
</Link>
//..생략
```

위의 코드와 같이 as를 통해서 라우트 마스킹을 해주면 되는 것 입니다. 이러한 작업을 완료하고 나면 이제 `as`에 작성한 endpoint가 브라우저의 url바에 나타나게 됩니다. 

![](/assets/images/post_img/shorturl.png)


이로써 `clean url`을 Link 컴포넌트 as라는 props를 통해 만들 수 있었습니다. 이제 한 가지만 더 완료해주면 끝이 납니다.

## Custom Server Api
NextJS는 라우팅을 프로젝트 내의 `pages` 폴더를 찾고 그 안에서 렌더할 페이지를 찾습니다. 예를 들어서 `http://localhost:3000/about`이라는 요청이 들어오면 pages폴더에서 `about.js`라는 파일을 찾게 됩니다. 하지만 저희는 실제 url과 다른 url을 브라우저에 띄워주었습니다. 이렇게 라우트 마스킹을 해준다면 서버에서도 그 부분에 대해서 원하는 페이지로 넘어갈 수 있도록 커스터마이징을 해줘야 돼요. 
```javascript
rouger.get('/admin/q/:id', checkAmin, function(req, res) {
  const queryParams = { id: req.params.id };
  nextApp.render(req, res, '/admin/question/answer', queryParams);
});
```
위처럼 pages폴더 내에 존재하는 파일의 경로를 렌더하게 해줘야 합니다. 이로써 필요한 모든 작업을 마칠 수 있었어요. 

## 마치며
저는 아직 개발을 배우는 단계이고 NextJS 또한 처음 써보는 사람이기에 이 방법이 틀린 방법일 수도 있음을 말씀드리고 싶습니다. NextJS의 Route Masking이라는 기능이 있었기에 query로 데이터를 모두 넘기려는 시도를 해본 것이구요. 페이지 간에 데이터를 전송할 방법에 대해 많은 고민을 해보고 성공한 방법을 공유하고자 글을 남깁니다. 감사합니다. 🙇‍