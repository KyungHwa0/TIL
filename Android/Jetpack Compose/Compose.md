# Jetpack Compose 란?
네이티브 Android UI를 빌드하기 위한 최신 도구키트이다.
Jetpack Compose는 더 적은 수의 코드, 강력한 도구, 직관적인 Kotlin API로 Android에서의 UI 개발을 간소화하고 가속화한다.
> 기존의 뷰를 업데이트하는 방식과 달리 Compose를 사용하면 필요한 영역의 뷰를 다시 그려주는 방식으로 작업할 수 있다.

## 구글에서 설명하는 Compose를 이용시 얻을수 있는 장점

### Less Code - 코드 감소
적은 수의 코드로 더 많은 작업을 하고 전체 버그 클래스를 방지할 수 있으므로 코드가 간단하며 유지 관리하기 쉽다.
### Intuitive - 직관적
UI만 설명하면 나머지는 Compose에서 처리한다. 앱 상태가 변경되면 UI가 자동으로 업데이트된다.
### Accelerate Development - 빠른 개발 과정
기존의 모든 코드와 호환되므로 언제 어디서든 원하는 대로 사용할 수 있다. 실시간 미리보기 및 완전한 Android 스튜디오 지원으로 빠르게 반복할 수 있다.
### Powerful - 강력한 성능
Android 플랫폼 API에 직접 액세스하고 MaterialDesign, DarkTheme, 애니메이션 등을 기본적으로 지원하는 멋진 앱을 만들 수 있습니다.

#### MainActivity
```kotlin

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyFirstComposeApplicationTheme {
                // A surface container using the 'background' color from the theme
                Surface(color = MaterialTheme.colors.background) {
                    Greeting("Android")
                }
            }
        }
    }
}

@Composable
fun Greeting(name: String) {
    Text(text = "Hello $name!")
}

@Preview(showBackground = true)
@Composable
fun DefaultPreview() {
    MyFirstComposeApplicationTheme {
        Greeting("Android")
    }
}
```

> Greeting("Android")는 Greeting이라는 Composable 함수를 호출하며, "Android"라는 문자열을 인자로 전달한다. 이 함수의 내부 구현에 따라 화면에 어떤 내용이 표시될지 결정된다.

#### ui/theme/Theme/kt
```kotlin
private val DarkColorPalette = darkColors(
    primary = Purple200,
    primaryVariant = Purple700,
    secondary = Teal200
)

private val LightColorPalette = lightColors(
    primary = Purple500,
    primaryVariant = Purple700,
    secondary = Teal200*

    /* Other default colors to override
    background = Color.White,
    surface = Color.White,
    onPrimary = Color.White,
    onSecondary = Color.Black,
    onBackground = Color.Black,
    onSurface = Color.Black,
    */
)

@Composable
fun MyFirstComposeApplicationTheme(darkTheme: Boolean = isSystemInDarkTheme(), content: @Composable () -> Unit) {
    val colors = if (darkTheme) {
        DarkColorPalette*
    } else {
        LightColorPalette*
    }

    MaterialTheme(
        colors = colors,
        typography = Typography,
        shapes = Shapes,
        content = content
    )
}
```

> Compose는 총 3가지의 구성 요소를 가지는 것으로 추측할 수 있다.
 1. 위젯을 포함하는 Composable 함수
 2. Preview를 하기 위한 Preview Composable 함수
 3. setContent 람다 표현식으로 실제 화면에 노출하는 코드

 * 일반적으로 우리가 아는 Activity의 라이프사이클 콜백 onCreate()에서 setContentView(Int) 함수를 호출하던것이 setContent() 함수로 바뀐것이 가장 큰 특징으로 보여진다.

 ## Composable Function
어노테이션을 이용한 기술이다. 함수위에 @Composable 어노테이션을 붙이게 되면 함수 안 다른 함수를 호출할 수 있게된다.

```kotlin

@Composable
fun Greeting(names: List<String>) {
    for (name in names) {
        Text("Hello $name")
    }
}
```
내부에는 Text라는 함수가 존재하는데, 이를 통해 UI계층 별 요구하는 컴포넌트를 생성해준다. 기본적으로 보이는 text 파라미터는 내부 속성에서 받는 일부 중 하나이다.

위 코드를 실행시키면 Hello로 시작하는 TextView가 화면에 그려진다.

* TextView 만들기

```kotlin
setContent {
  BasicsCodelabTheme {
    // A surface container using the 'background' color from the theme
    Surface(color = MaterialTheme.colors.background) {
      Greeting("Android")
    }
  }
}
```

## @Preview
어노테이션을 이용하여 IDE에서 Preview를하기 위한 용도이다. 아래 코드와 같이 @Preview 어노테이션을 추가하면 다음 결과를 볼 수 있다.

```kotlin
@Preview("Greeting Preview")
@Composable
fun GreetingPreview() {
    BasicsCodelabTheme {
        Surface(color = MaterialTheme.colors.background) {
            Greeting("Android")
        }
    }
}
```

##  setContent / Theme / Surface
1. setContent : Composable 함수를 사용하여 앱의 UI 내용을 설정하는데 사용된다. Android의 전통적인 setContentView() 메서드와 유사한 개념이지만, Jetpack Compose에서는 Composable 함수와 함께 사용된다.

2. XXXTheme : Theme정보를 의미한다. 해당 프로젝트에서는 Theme.kt에 여러 테마에 필요한 정보를 정리하고, 앱의 UI 요소에 적용되는 스타일과 색상을 정의한다.

3. Surface : UI 구성 요소를 포함하는 컨테이너 역할을 한다. 예를들어 Material Design에서는 요소가 어떤 "높이"에 있는지를 나타내기 위해 서피스를 사용한다. Surface는 그림자, 모서리 반올림, 배경색 등을 포함하여 이러한 "높이" 또는 Z축을 시각화한다.

## Declarative UI — 선언형 UI
1. 상태 기반: 선언적 UI는 주어진 상태를 기반으로 UI를 렌더링한다. 상태가 변경되면, UI도 자동으로 업데이트된다. 따라서 개발자는 UI를 어떻게 변경해야 하는지를 상세하게 지정하는 대신, 원하는 최종 상태만 선언하면 된다.

2. 직관적: 선언적 코드는 읽기 쉽고 이해하기 쉽다. UI의 현재 상태와 모습을 직접적으로 나타내기 때문에 코드와 UI 사이의 관계가 직관적이다.

3. 유지보수 용이: UI의 변경이나 확장이 필요할 때, 선언적 접근법은 수정이나 추가가 간편하다.

4. 재사용성: UI 컴포넌트를 재사용하기 쉽게 만들 수 있어서, 다양한 UI 구성 요소를 쉽게 조합할 수 있다.

5. 반응형: 선언적 UI는 자동으로 상태의 변화에 반응하여 UI를 업데이트한다.
> UI의 **"무엇"** 을 명시하며, **"어떻게"** 그려야 하는지에 대한 복잡한 로직을 프레임워크나 라이브러리에 위임한다.

## 레이아웃을 활용한 Compose function의 다중 호출
지금까지는 하나의 컴포넌트만을 갖고 사용했지만, 여러개의 컴포넌트를 넣는것도 가능하다.
```kotlin

@Composable
fun MyScreenContent() {
    Column {
        Greeting("Android")
        Divider(color = Color.Black)
        Greeting("there")
    }
}
```
Column과 위에서부터 사용하던 Greeting 함수를 사용하고, 라인을 그어주기 위한 Divider 를 추가한 결과물은 다음과 같다.

![0_qBQkLkMUBcUUWmVk](https://github.com/KyungHwa0/TIL/assets/124041716/0113973f-6af5-4c7e-a7ec-8a394d2da2bb)

* Column : 항목을 순서대로 배치하기 위해 사용한다.
* Divider : 선 긋기 가능한 Compose 함수이다.
