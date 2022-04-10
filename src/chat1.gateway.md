### Namespace 구분 없는 단순 실시간 통신 구현

Only `chat.gateway.ts` file

```JSX
import { Logger } from '@nestjs/common';
import { OnGatewayConnection, OnGatewayDisconnect, OnGatewayInit, SubscribeMessage, WebSocketGateway, WebSocketServer, WsResponse } from '@nestjs/websockets';
import { Server, Socket } from 'socket.io';

@WebSocketGateway(3001, { path: '/websockets', serveClient: true, cors: true, namespace: '/' })
// 서버를 실행하면 3001번 포트와 기본 네임스페이스로 웹 소켓 서버가 실행된다.

export class AppGateway implements OnGatewayInit, OnGatewayConnection, OnGatewayDisconnect {
  // OnGatewayConnection: 클라이언트가 서버에 연결될 때 가동된다.

  @WebSocketServer() wss: Server;
  private logger: Logger = new Logger('AppGateway'); // 작동하는지 로깅 추가

  // 서버 시작할 때마다 동작
  // server 변수로 서버 내의 클라이언트들에게 이벤트를 발생시킬 수 있다.
  afterInit(server: Server) {
    this.logger.log('Initialized!!');
  }

  handleConnection(client: Socket, ...args: any[]) {
    this.logger.log(`Client connected: ${client.id}`);
  }

  handleDisconnect(client: Socket) {
    this.logger.log(`Client disconnected: ${client.id}`);
  }

  @SubscribeMessage('msgToServer')
  handleMessage(client: Socket, text: string): void {
    this.wss.emit('msgToClient', text);
  }

  // @SubscribeMessage('msgToServer')
  // handleMessage(client: Socket, text: string): WsResponse<string> {
  //   return { event: 'msgToClient', data: text };
  // }
  // 이 상태로는 현재 메시지 송신자만 메시지를 확인할 수 있다.
/*
  리턴 타입을 지정해주지 않은 아래 코드와 동일하다.
  handleMessage(client: Socket, text: string): void {
    client.emit('msgToClient', text);
  }
*/
}
```
