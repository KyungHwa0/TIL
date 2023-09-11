# Jetpack Media3
Jetpack Media3는 Android 앱이 풍부한 오디오 및 시각적 경험을 표시할 수 있게 해주는 미디어 라이브러리의 새로운 홈이다. Media3은 조각화로 인한 복잡성을 추상화하기 위해 장치 기능을 기반으로 한 강력한 사용자 정의, 안정성 및 최적화 기능을 갖춘 간단한 아키텍처를 제공한다.

## Playback Components
Media3은 재생 사용 사례를 위한 몇 가지 주요 구성 요소를 제공한다. 이전 Android 미디어 라이브러리를 사용해 본 적이 있다면 이러한 구성 요소를 구성하는 클래스가 익숙하게 다가 올 것이다.
* 미디어 앱의 구성요소
<img width="1192" alt="overview" src="https://github.com/KyungHwa0/TIL/assets/124041716/d5c5c201-82b8-47e5-808c-f9bc4f60e23a">

> 중요: Media3를 이전 미디어 API와 구별하는 주요 특징 중 하나는 더 이상 구성 요소 간에 커넥터가 필요하지 않다는 것이다. 새 클래스는 UI와 마찬가지로 인터페이스를 MediaSession구현하는 모든 클래스를 사용한다. **ExoPlayer** 및 **MediaController** 둘 다 해당 인터페이스를 구현하는 클래스이다. 이를 통해 구성 요소 간의 상호 작용이 훨씬 간단해진다.

### 미디어 플레이어
미디어 플레이어는 미디어 파일을 재생할 수 있는 앱의 구성 요소

| Class | 설명 | 구현노트                       |
| ----- | ---- | ---------------------------- |
| Player | Player재생, 일시 중지, 검색 기능과 같은 미디어 플레이어의 기존 고급 기능을 정의하는 인터페이스. | Media3에서 인터페이스는 및 등을 Player포함한 여러 구성 요소에서 구현되거나 사용되는 공통 API **MediaSessionMediaController** |
| ExoPlayer | **ExoPlayerPlayerMedia3** 인터페이스 의 기본 구현이다.|  |

### MediaSession
미디어 세션은 미디어 플레이어와 상호 작용하는 보편적인 방법을 제공한다. 이를 통해 앱은 외부 소스에 미디어 재생을 광고하고 외부 소스로부터 재생 제어 요청을 수신할 수 있다.
| Class | 설명 | 구현노트                       |
| ----- | ---- | ---------------------------- |
| MediaSession | 미디어 세션을 사용하면 앱이 오디오 또는 비디오 플레이어와 상호 작용할 수 있다. 미디어 재생을 외부에 알리고 외부 소스로부터 재생 명령을 받는다. | Media3에서는 명령을 실행하고 현재 상태를 얻으려면 a가 MediaSession필요하다.|
| MediaSessionService	 | MediaSessionService백그라운드 재생을 용이하게 하기 위해 앱의 기본 서비스와는 별도의 서비스에 미디어 세션과 관련 플레이어를 보유 한다.|  |
| MediaController | 클래스 MediaController는 일반적으로 앱 외부(예: 다른 앱이나 시스템 자체)에서 명령을 보내는 데 사용된다. Player명령은 연결된 의 기본으로 전송된다. | MediaController 클래스는 Player 인터페이스를 구현하지만 메서드를 호출하면 명령이 연결된 MediaSession으로 전송된다. Google Assistant와 같은 클라이언트 앱은 MediaController를 사용하여 연결된 세션에서 재생을 제어할 수 있다. |
| MediaLibraryService	 | MediaLibraryService는 클라이언트 앱에 콘텐츠 라이브러리를 제공할 수 있도록 추가 API를 포함한다는 점을 제외하면 MediaSessionService와 유사하다.|  |
| MediaBrowser	 | 	MediaBrowser 클래스를 사용하면 사용자는 미디어 앱의 콘텐츠 라이브러리를 탐색하고 재생할 항목을 선택할 수 있다.|  |

## Editing components
Media3에는 다음을 포함한 미디어 편집 사용 사례를 위한 Transformer API가 포함되어 있다.
* 필터 및 효과 추가와 같은 오디오 및 비디오 처리
* HDR 비디오 및 슬로우 모션 비디오와 같은 특수 형식 처리
* 여러 입력 파일을 결합하는 등의 구성
* 최종 출력을 파일로 내보내기

> [참고자료 : Android Developers >
Develop > Guides > Jetpack Media3](https://developer.android.com/guide/topics/media/media3)

