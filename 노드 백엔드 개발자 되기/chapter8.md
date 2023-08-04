# 8장 NestJS 시작하기
- Fastify : 익스프레스와 하피(Hapi)에 영감을 받은 웹 프레임워크
- 데코레이터 : A.4.4절 '데코레이터' 참고
- 타입스크립트 문법 : 부록 A

## 왜 NestJS가 필요할까?
익스프레스로 개발도 물론 가능하다. 하지만 익스프레스를 사용하면 어떤 아키텍처를 사용해야할지 모든 사람이 고민해야하는 문제가 있었다. NestJS는 이러한 문제를 해결한 웹 서버 프레임워크다.
NestJS는 서버 개발 시의 아키텍처를 누구든 비슷하게 설계하도록 아키텍처 문제를 해결하는 데 중점을 두고 있다.

## NestJS 소개
1. Node.js에서 실행하는 서버사이드 프레임워크
2. 타입스크립트를 완벽하게 지원
3. 자바스크립트의 최신 스펙을 사용, 바닐라 자바스크립트를 사용한다면 babel 사용이 필수
4. HTTP 요청 부분은 추상화된 코드를 제공해 익스프레스와 패스티파이를 사용할 수 있음.

서버개발에 아키텍처는 쉽게 테스트하고, 쉽게 확장이 가능하고, 각 모듈간의 의존성은 줄이도록 해야 유지보수가 쉽기에 좋은 아키텍처는 필수다.

### NestJS 둘러보기
- 핵심 기능 : 의존성 주입 -> 모듈 간의 결합도를 낮춰서 코드의 재사용을 용이하게 한다. -> 모듈 내에서의 코드의 응집도는 높이고 모듈의 재사용성을 꾀하고 모듈 간에는 결합도를 낮춰서 다양한 아키텍처를 활용할 수 있게 한다.

| NestJS | Spring Boot | 설명 |
| --- | --- | --- |
| 클라이언트 | 클라이언트 | HTTP 요청을 생성하고 서버에 보냅니다. |
| 파이프(Pipes) | - | 요청을 받아 데이터 유효성 검사, 변환, 검증 등의 작업을 수행합니다. |
| 가드(Guards) | 인터셉터(Interceptors) | 요청이 특정 라우트 핸들러에 도달하기 전에 실행되며, 일반적으로 인증이나 권한 확인 등의 작업을 수행합니다. |
| 컨트롤러(Controller) | 컨트롤러(Controller) | 요청을 받아 필요한 처리를 수행하거나, 다른 서비스를 호출하여 처리를 위임합니다. |
| 서비스(Service) | 서비스(Service) | 비즈니스 로직을 수행합니다. 데이터베이스와의 상호작용이 필요한 경우 리포지토리를 호출할 수 있습니다. |
| 리포지토리(Repository) | 리포지토리(Repository) | 데이터베이스와의 상호작용을 담당합니다. 데이터를 생성, 조회, 업데이트, 삭제하는 작업을 수행합니다. |
| 서비스(Service) | 서비스(Service) | 데이터베이스 작업이 완료되면 결과를 컨트롤러에 반환합니다. |
| 컨트롤러(Controller) | 컨트롤러(Controller) | 처리 결과를 HTTP 응답으로 포맷팅하고 클라이언트에 반환합니다. |
| 클라이언트 | 클라이언트 | HTTP 응답을 받아 필요한 후속 처리를 수행합니다. |


## NestJS의 네이밍 규칙
```typescript
<모듈명>.<컴포넌트명>.ts
hello.controller.ts
my-first.controller.ts
```
- 클래스명은 낙타 표기법(Camel Case)로 사용
```
<모듈명><컴포넌트명>
HelloController
```
- 같은 디렉토리에 있는 클래스는 index.ts를 통해서 임포트하는것을 권장
```typescript
// index.ts를 사용하지 않는 경우
import { MyFirstController } from './controllers/my-first.controller'
import { MySecondController } from './controllers/my-second.controller'

// index.ts를 사용하는 경우
import { MyFirstController, MySecondController } './controllers';
```