# Chapter 05. 플로터 입문하기

## 플로터 소개
- 구글이 개발한 크로스플랫폼 프레임워크
- 임베더,엔진,프레임워크 3단계로 프레임워크가 구성.
- Enbedder : 플랫폼의 통신과 디바이스를 제어하는 계층.
- Engine  : C,C++로 만들어져 있는 Flutter 코어 API 계층.
- Framerowk : 개발자가 구현하는 기능들을 모아놓은 계층.

<img src="https://velog.velcdn.com/images/error/post/9e1f990d-33d9-4287-93b6-1aebd321f1cf/image.png" width="600px" height="400px" title="px(픽셀) 크기 설정" alt=""></img><br/>

## Hello Flutter 앱 만들기
### 안드로이드 스튜디오 기준
- dart 플러그인 설치.
- Flutter 플러그인 및 sdk 설치.
- 환경변수 설정.
- 프로젝트 생성 화면에서 new flutter project 선택.
- sdk 폴더 위치 설정.
- 프로젝트 정보 입력.

### VS 코드 기준
- dart 플러그인 설치.
- Flutter 플러그인 및 sdk 설치.
- 환경변수 설정.
- 프로젝트 생성 화면에서 Flutter:New Project 선택.
- Application 선택.
- 프로젝트를 저장할 폴더 선택 및 이름 설정.

### Hello World 출력
- 프로젝트를 생성하면 프로젝트 폴더/lib/main.dart 파일 생성.
- MaterialApp 위젯: 디자인 기반의 위젯 사용.
- Scaffold 위젯 : 화면 전체의 UI 담당 위젯.
- Text 위젯 : 텍스트 담당 위젯
- 플로터에서는 마지막 매개변수 끝에 ,를 붙임
```dart
void main() {
 runApp(
  const MaterialApp(
    home: Scaffold(
      body: Text(
        "hello world!",
        ),
    ),
  ),
 );
}
```
