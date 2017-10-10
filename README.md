## 서버 환경
1. node.js - v6.11.1
2. express.js - v4.14.1

## 클라이언트 환경
1. vue.js - v2.3.3
2. vue-router - v2.7.0
3. bootstrap - v4.0.0-beta
4. webpack - v2.6.1

## 구동하기
1. npm install
2. npm run build
3. npm run start

## 프로젝트 소개
vue.js와 vuex를 사용했습니다. angular 1.x를 사용한 프로젝트는 [여기](https://github.com/cryingnavi/naver_angular)에서 확인할 수 있습니다.

서버는 node와 express.js로 구현했습니다. express.js는 REST API를 통신을 위한 용도와 webpack 플러그인들을 이용한 라이브 리로드 역할도 수행해 줍니다. 별도의 인증 모듈과 디비는 사용하지 않았습니다. 모든 데이터는 메모리에 올렸으며, 서버를 재시작할 경우 초기화 되도록 되어 있습니다.

## 구현된 REST API
1. 로그인
로그인 버튼을 클릭하여 로그인을 시도하면 서버가 고유한 토큰을 발행하여 쿠키에 저장합니다. 그리고 이후 다른 REST API 는 이 토큰을 포함하여 요청됩니다. 이후 REST API는 해당 토큰을 검증하여 유효성을 판단할 수 있지만 이 부분은 구현되지 않았습니다.
2. 로그아웃
토큰을 만료 시키고 로그아웃 시킵니다.
3. 게시글 목록 불러오기
로그인 유무와 상관없이 게시글 목록을 불러올 수 있습니다.
4. 게시글 상세 보기
로그인 유무와 상관없이 게시글 상세를 불러올 수 있습니다.
5. 게시글 수정하기
로그인한 상태에서 해당 게시글을 작성한 유저라면 게시글을 수정할 수 있습니다. API차원에서 토큰 검증은 수행하지 않습니다.
6. 게시글 삭제하기
로그인한 상태에서 해당 게시글을 작성한 유저라면 게시글을 삭제할 수 있습니다. API차원에서 토큰 검증은 수행하지 않습니다.
7. 게시글 생성하기
로그인한 상태라면 게시글을 생성할 수 있습니다.

## 회원 권한 설명
1. 로그인이 가능한 유저는 super, user1, user2 세개 입니다. 비밀번호는 체크하지 않으며 아무렇게나 치고 넘어갈 수 있습니다.
2. super는 관리자 계정으로 모든 유저의 수정/삭제 권한을 가집니다.
3. user1 또는 user2로 로그인 했을 경우, 자신이 쓴글에 대해서만 수정/삭제 권한을 가집니다.


## 빌드하기
1. npm run build 명령어로 빌드할 수 있다.
2. 빌드를 하면 build/build.js가 구동됩니다.
3. 기존 빌드 된 결과는 삭제 되며 새로 빌드하여 dist 폴더를 생성합니다.
4. dist 폴더에는 index.html과 js 파일이 생성됩니다. static폴더는 이미지등의 정적 리소스가 존재하면 static폴더에 들어가게 됩니다.

## 클라이언트 설명
1. main.js
- src폴더의 main.js가 vue 프로젝트를 생성하고 초기화를 수행하는 메인 자바스크립트 파일입니다.
- 이곳에서 관련 모듈들을 import합니다.
- import App from './App' 구문은 메인 컴포넌트를 임포트하는 구문입니다. 해당 컴포넌트가 최상위이며 페이지 진입시 해당 컴포넌트 하위로 각 컴포넌트가 생성됩니다.
- import store from './store'로 스토어를 임포트합니다.
- Home, List, Detail, Edit, User, Writer 컴포넌트를 임포트합니다. 해당 컴포넌트들은 페이지에 해당합니다.
- 라우터를 생성합니다. 라우터 생성시 beforeEnter는 앵귤러로 만든 프로젝트에서 isLogin옵션과 같은 동작을 하도록 구현되었습니다.
- 마지막으로 vue객체를 생성합니다.

2. App.vue
- 프로젝트의 메인 컴포넌트 입니다.
- 해당 컴포넌트 안에는 router-view가 존재하며 하위 컴포넌트들은 router-view 엘리먼트에 생성됩니다.
- 컴포넌트는 vuex를 통해 데이터를 표현한다. vuex는 리액트에서 사용하는 flux 아키텍쳐의 구현체이다.

3. 각 컴포넌트들
- 각각의 컴포넌트들은 components폴더 하위에 존재한다.

4. 스토어
- 스토어는 store폴더에 존재하며 index.html이 스토어를 생성하는 역할을 수행한다.
- vuex는 플러스 아키텍쳐의 구현체로 flux에서 사용되는 Dispatcher와 action이 존재한다.
- 각 컴포넌트들에서는 dispatch로 서버에 데이터 요청을 트리거링 하고 action이 이를 보조하여 데이터 요청을 중계하고 결과를 store에 저장한다.
- 실제 데이터를 요청하는 부분은 src/api 폴더 안의 PostAPI.js에 존재한다. PostAPI.js는 vue에서 http요청시 사용하는 axios를 사용하여 api를 호출한다.







 
