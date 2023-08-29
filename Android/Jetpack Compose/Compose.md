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