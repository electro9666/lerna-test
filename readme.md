### 참고
### https://fors.tistory.com/640
### https://pks2974.medium.com/mono-repo-%EB%A5%BC-%EC%9C%84%ED%95%9C-lerna-%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-65c22029988
### https://ichi.pro/ko/lernalo-mono-lepoleul-mandeuneun-bangbeob-69092600729633

### lerna 시작
npx lerna init

### 패키지1 생성
npx lerna create test1

### 패키지2 생성
npx lerna create test2

### ignore 로 설정된 package 를 제외한 모든 package 의 npm install 을 실행한다.
lerna bootstrap --hoist

### 모든 package 의 node_modules 를 삭제하고, lerna bootstrap 다시 설치할 수 있다.
lerna clean

### 모든 package 에 설정된 devDependencies 을 root devDependencies 으로 옮긴다.
### 그리고, dependencies 에 package 를 file:packages/package-1 형태로 연결한다.
lerna link convert
<!-- "dependencies": {
 "package-1": "file:packages/package-1",
 "package-2": "file:packages/package-2",
} -->
<!-- 이때 각 package 들의 devDependencies 은 모두 root 으로 이동해버렸기 때문에, package 에서 devDependencies 를 실행하면, 예를 들어 webpack 을 실행하면, 작동하지 않는다.
이경우 root 에서 lerna run --scope package-1 start 로 실행하면 root 에 있는 devDependencies 를 참조할 수 있게 된다. -->

### 여기에서 lerna run 명령어는 package.json 에 있는 script 를 실행시킨다. — scope 으로 package 를 선택할 수 있다.

### 종속성 추가
### 이를 여러 패키지로 제한하려면 --scope옵션을 사용할 수 있습니다 .
lerna add <package/dependecy>
lerna add lodash --scope=test1

### https://github.com/lerna/lerna/tree/main/commands/add
### Install module-1 to module-2 in peerDependencies
### 별로 쓸일 없을듯
lerna add axios --scope=test2 --peer

### 함께 실행
npx lerna run start

### ??