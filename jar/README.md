# .jar 확장자
JAR(Java Archive)  
여러 개의 자바 클래스 파일과, 클래스들이 이용하는 관련 리소스(텍스트, 그림 등) 및 메타데이터를 하나의 파일로 모아서 자바 플랫폼에 응용 소프트웨어나 라이브러리를 배포하기 위한 소프트웨어 패키지 파일 포맷

ZIP 파일 포맷으로 이루어진 압축 파일. 컴퓨터 사용자들은 JDK에 포함된 `jar` 명령어를 이용하여 JAR 파일을 만들거나 압축을 풀 수 있다.

<br/>

## 압축 해제
```bash
jar -xf 파일이름.jar
```

<br/>

## 실행
```bash
java -jar 파일이름.jar
```