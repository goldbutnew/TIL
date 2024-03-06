### 리액트 네이티브란?
1. React의 앱 플랫폼의 기본 기능을 사용하여 Android 및 IOS 애플리케이션을 빌드하기 위한 오픈 소스 프레임워크 
2. 모바일 플랫폼을 대상으로 함
3. 웹 개발자도 JS를 사용하여 네이티브 모양과 느낌을 줄 수 있음
4. React Native를 사용하면 Android와 IOS 모두에서 동시에 쉽게 개발 가능

### 리액트 네이티브의 장점

- 다른 크로스 플랫폼(웹으로 만든 다음 앱에 임베딩 해서 사용)과는 다르게 실제 호스트 플랫폼의 표준 렌더링 API를 사용해서 렌더링
- 리액트 네이티브는 소스 코드로 작성하면 네이티브 요소로 변환해 줌
- 리액트의 state, props 등 사용 가능

### Core Components, Native Components

- Native Component
    - React Native 앱이 다른 앱과 같은 모양, 느낌, 성능을 제공하도록 하는 플랫폼 지원 구성 요소
    - 각자 원하는 바에 맞게 만들 수 있음
- Core Component
    - 리액트에서 기본 제공하는 Native Component
    - 예시      
        | WEB ANALOG | React Native UI Component |
        |--- | --- |
        | non-scrolling `<div>` | `<View>` |
        | `<p>` | `<Text>` |
        | `<img>` | `<Image>` |
        | `<div>` | `<ScrollView>` |
        | `<input type="text">` | `<TextInput>` |

### 리액트 네이티브 개발환경

- Expo: 무료 3rd Party 서비스
    - 장점
        - 배포와 버전 업데이트 등이 쉬움
        - 휴대폰 테스트 가능
        - 간단한 설치 및 환경 설정
    - 단점
        - Expo에서 제공하는 기능만 사용 가능
        - 모듈 만들어 사용 불가
        - native 파일 제어 불가
        - 간단하지만 복잡하고 섬세하게 제어 못 함
- React Native CLI: 리액트 팀에서 만든 React Native만 이용해서 개발하는 것
    - 장점
        - 네이티브 파일 및 모듈 사용 가능
        - 네이티브 소스 코드 작성 가능
    - 단점
        - Expo에 비해서 편의성 부족
        - 사용자가 직접 기본 구성을 해야 해서 시간이 오래 걸림
        - Android Studio와 X code 다 설치해서 빌드/배포 해야 함