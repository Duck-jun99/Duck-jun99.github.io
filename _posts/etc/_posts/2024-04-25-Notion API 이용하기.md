---
layout: post
title: Notion API 이용하기
image: 
  #path: /assets/img/blog/post/termux1.png
description: >
  
sitemap: false
tags: etc
date: 2024-04-25
comments: true
---

## [Notion] Notion API 이용하기


Now-in-Jun 프로젝트를 진행하며 제 포트폴리오 정보를 가져오기 위해 Notion API를 사용하고자 합니다.

이번 게시물에서는 본인의 개인 노션에 저장되어 있는 포트폴리오 Database에 접근하여 해당 정보를 가져오는 방법을 설명하도록 하겠습니다😀

#### 1. Notion API Integration 생성하기

[Notion API Integration 생성]에 접속해서 Integration을 생성해줍니다.
생성하면 개인 Secret Key가 발급이 됩니다. 해당 키를 안전한 곳에 저장해두길 바랍니다.
<br>

#### 2. 노션과 Integration 연동

<a><img src="/assets/img/blog/post/notion-api-1/notion-api-1.png" alt="notion-api-1"></a>

생성한 Integration을 API를 이용할 노션 페이지와 연동해줍니다. <b>Connect to</b> 검색창에 <b>int</b>만 입력해도 해당 생성한 Integration이 뜹니다. 클릭해서 연동을 해줍시다!

> ⚠️ 만약 본인의 Integration이 검색이 안된다면 Integration을 생성한 워크스페이스와 해당 노션 워크스페이스가 일치하는지 확인해주세요!

<br>

#### 3. Database Query 가져오기 테스트(Postman 이용)
<a><img src="/assets/img/blog/post/notion-api-1/notion-api-2.png" alt="notion-api-2"></a>

예시를 보여드리기 위해, 연동한 제 노션 페이지에 임의의 데이터베이스를 만들었습니다. 이 데이터베이스의 쿼리를 조회해보겠습니다.

데이터베이스의 쿼리를 조회하기 위해서는 해당 데이터베이스의 ID를 알아야 합니다. 위 사진에서 링크를 복사해보면 다음과 같이 나올 것입니다.

> https://www.notion.so/[데이터베이스 ID]?[쏼라쏼라...]

해당 링크에서 [데이터베이스 ID]에 해당하는 부분이 본인 데이터베이스의 ID입니다. 다른 부분은 제외하고 해당 부분만 이용할 것입니다.

저희가 Notion API를 이용해 해당 쿼리를 조회하기 위해서는 다음과 같은 정보가 필요합니다.
- Integration Secret Key (1번 단계에서 생성된 개인 키)
- Notion-Version
- 데이터베이스 ID

자 이제 Postman에 접속하고 해당 URL에 POST를 보내보겠습니다.
해당 URL 주소는 아래와 같습니다. [데이터베이스 ID] 부분에 본인의 데이터베이스 ID를 넣어줍니다.
> https://api.notion.com/v1/databases/[데이터베이스 ID]/query

<a><img src="/assets/img/blog/post/notion-api-1/notion-api-3.png" alt="notion-api-3"></a>

그 다음, Authorization에서 Bearer Token을 선택해주고 오른쪽에 본인의 Integration Secret Key를 입력해줍니다.

<a><img src="/assets/img/blog/post/notion-api-1/notion-api-4.png" alt="notion-api-4"></a>

마지막으로, Headers에 Notion-Version을 추가해줍시다. 이 글을 쓰는 지금, 2022-02-22를 사용하면 됩니다.

<a><img src="/assets/img/blog/post/notion-api-1/notion-api-5.png" alt="notion-api-5"></a>

이제 Send 버튼을 눌러 response가 성공적으로 넘어오는지 확인합시다! 쿼리가 제대로 조회된다면 해당 JSON을 이용해 여러분이 사용할 곳에서 예쁘게 사용해주면 됩니다!
만약 response의 상태 코드가 200이 아니고 오류가 발생한다면, 아래 사이트를 참고해서 확인해봅시다.

[Notion API 상태 코드]

<br>

---

<br>

노션 API를 사용하는 방법은 공식 문서에 매우 자세히 설명되어 있습니다. 아래의 사이트를 확인하면 더욱 쉽게 할 수 있을겁니다~

감사합니다😀

<br>

#### 참고 사이트

[Notion API 공식 문서]

[Notion Postman 참고]

[Notion API Integration 생성]: https://www.notion.so/my-integrations

[Notion API 상태 코드]: https://developers.notion.com/reference/status-codes

[Notion API 공식 문서]: https://developers.notion.com

[Notion Postman 참고]: https://www.postman.com/notionhq/workspace/notion-s-api-workspace/request/15568543-cddcc0aa-d534-4744-b37a-ddf36dee7d8f?tab=overview