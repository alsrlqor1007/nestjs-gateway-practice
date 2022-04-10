# NestJS 서버로 실시간 대화 기능 개발하기

[NestJS Gateway](https://docs.nestjs.com/websockets/gateways#server) 공식문서
[Socket.io](https://socket.io/docs/v4/) 공식문서
with Brian Johnson's youtube channel [click here](https://www.youtube.com/channel/UCf96AoxAYrgATXOJJi_xmyg)
<br></br>
<strong>

1. Namespace 구분 없는 단순 실시간 통신 구현
2. 2개의 Namespace(chat, alert)가 존재하는 실시간 대화 구현
3. 3개의 Chat Room이 존재하는 실시간 대화 구현

</strong>

<br></br>
NestJS의 Gateway 생성 명령어 `chat 디렉토리`와 `chat.gateway.ts 생성`

```bash
$ nest g gateway chat chat
```
