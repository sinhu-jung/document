## npm i 를 했을 때 오류

npm ERR! Error: EPERM: operation not permitted, rename 이러한 오류가 뜨면서 설치가 제대로 안되는 경우가 있음 따라서 아래에 있는 코드처럼 캐시를 지워줘야함

### 1.clean cache

```
 $ npm cache clean --force
```



### 2.npm cache 파일 삭제

1) 내 PC의  C 드라이브의 사용자의 사용자 아이디 폴더에 들어간다.

![캡처](https://user-images.githubusercontent.com/67888402/135223528-501ff790-79f4-4a46-88bf-a067b3b7e9cb.PNG)

2)  상단에 보기를 눌러 숨긴 항목을 체크한다.

![캡처](https://user-images.githubusercontent.com/67888402/135223806-92d2306c-980f-48e2-9c1b-b23e2a769ecd.PNG)

3) AppData의 Roaming 폴더에 들어간다.

![캡처](https://user-images.githubusercontent.com/67888402/135224035-29c2d6b2-b63b-470d-a679-7fe348ddd631.PNG)

4) npm-cache 폴더를 삭제

### 3.clean cache

```
 $ npm cache clean --force
```

