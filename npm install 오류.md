## npm i 를 했을 때 오류
npm ERR! Error: EPERM: operation not permitted, rename 이러한 오류가 뜨면서 설치가 제대로 안되는 경우가 있음 따라서 아래에 있는 코드처럼 캐시를 지워줘야함

### 1.clean cache with
```bash
 $ npm cache clean --force
```
### 2.install the latest version of npm globally as admin: 
```bash
 $ npm install -g npm@latest --force
```
### 3.clean cache with
```bash
 $ npm cache clean --force
```
