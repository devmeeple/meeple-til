# npm과 yarn으로 패키지 관리하기
## npm 소개
자바스크립트용 패키지 매니저
- Java / Maven, 
- Python / Pypl

패키지 매니저 : 프로젝트에 필요한 의존성 패키지를 관리하는 프로그램

## 패키지와 모듈
- 패키지 : package.json으로 정의한 코드 뭉치
- 모듈 : [node_modules] 디렉토리 아래에 있는 파일 또는 디렉토리를 의미한다. `require()` 함수로 읽을 수 있다.
- [node_modules]에는 `npm install` 명령으로 설치한 패지키들이 저장된다. 따라서 모든 패키지는 모듈이다.
- npm 굉장히 많은 I/O를 수행한다. 이것은 `requrie()` 함수가 무거워지는 원인을 제공한다. 이 문제를 해결하기 위해 `yarn`이 등장했다.

## 패키지 설치
```
npm install [<@scope>]<name>@<tag/version/version range>
npm i
npm add
```
세가지 명령어 모두 사용가능하다.
### [<@scope>]
패키지 스코프, 일종의 네임스페스 이다. 스코프를 사용해서 패키지명이 같더라도 안전하게 사용할 수 있게 되었다.
- @cat 스코프 밑에 test와 @rabbit 스코프 밑에 test는 패키지명은 같지만 스코프가 다르다. 따라서 @cat/test, @rabbit/test로 각각 사용할 수 있어 충돌이 발생하지 않는다.

### 개발환경
```
npm install jest -D
```
개발환경에서만 사용하는 패키지는 -D 옵션으로 설치한다.

## 패키지 업데이트
```
npm update [-g] [패키지명1, 패키지명2...패키지명N]
npm up
npm upgrade
```
-g 옵션은 install과 마찬가지로 node가 설치되어 있는 디렉토리의 의존성 패키지를 업데이트 할 때 사용

## 설치한 패키지 확인하기
```
npm ls [@스코프/] 패키지명
npm list
npm la
npm ll
```

### 패키지 삭제하기
```
npm uninstall [@스코프/] 패키지명[@버전] [-S|--save|-D|--save-dev|-O|--save-optional]
npm remove
npm rm
npm r
npm un
npm unlink
```

## 스크립트 기능과 NPX
### NPX로 코드 포매팅 명령어 prettier 실행하기
NPX는 Node Package eXecute의 약자다. Node 패키지 실행자 라고도 한다. Node.js 패키지는 대부분 프로젝트에 임포트해서 사용하지만 개발할 때는 실행, 관리, 테스트 등에 명령형 패키지를 다수 사용한다. 대표적으로 prettier, eslint, jest와 같은 포매팅, 문법검사, 단위테스트 도구들이다.
- prettier : 같은 포매팅을 사용해야 가독성이 높아진다. 파일 저장 시 혹은 저장소에 커밋이나 푸쉬하기 전에 자동으로 적용되도록 하면 유용하다.

## 패키지 잠금
패키지 매니저를 제대로 알지 못하면 이따금 터지는 문제에 고생을 하게 된다.

5버전 이상의 npm은 패키지를 처음 설치 혹은 업데이트하는 시점과 똑같은 버전을 설치하도록 `package-lock.json`에 패키지의 의존성 트리 정보를 저장해두고 설치 시 `package.json`이 아닌 `package-lock.json`을 확인하고 설치한다. 이를 패키지 잠금이라고 한다.

- 개발시에는 꼭 필요한 패키지가 아니라면 설치하지 않는것이 좋다. 
- 너무 많은 의존성을 가진 패키지는 꼭 필요하지 않다면 사용하지 않는 것이 좋다.
- 패키지 의존성을 최소화하는것도 Node.js 개발에서는 중요하다.
- npm instlal은 `package.json` 정보를 참고하여 의존성 패키지를 설치한다. 
- npm ci 명령어 사용시 `package.json` / `package-lock.json` 버전이 일치하는지 확인한다. 맞지 않으면 에러를 발생시킨다. 또한 의존성 패키지 모듈이 저장되어 있는 `node_modules` 디렉토리를 삭제 후 모든 의존성 패키지를 다시 설치한다.
- npm ci 명령은 개발에서 사용한 패키지 그대로 테스트 서버나, 프로덕션 환경에 사용할 때 적합하다.

## yarn
npm은 용량문제, 패키지 내려받기 속도 문제, 보안 문제를 갖고 있다. yarn은 2016년에 페이스북에서 만든 패키지 관리 프로그램이다. yarn을 사용하면 매우 깔끔하게 패키지를 관리 할 수 있다. 다만 yarn에서 지원하지 않는 기능을 사용하는 패키지도 있으므로 이 부분을 잘 확인해야 한다.
- yarn2는 PnP 전략을 사용해 `[node_modules]` 디렉터리를 사용하지 않고 의존성 패키지를 관리한다.
