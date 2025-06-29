

Automation workflow dla refinementów 

Mermaid grafy o zrozumienia struktury


Pisanie z czatem jak programowanie funkcyjne ?


## Stronka z tips and tricks
## Argumentowanie czemu jak dev zasługujesz na ten kurs

---

Endpoint -> to postman import ADW


USER STORY -> Specification -> Solution


ADW from design to UI

-----

CursorRules

Chcemy aby każda lekcja zaczynała się małym wprowadzeniem opisując treść tej lekcji i jej istotność.


--- 
Prompts

Both "Task you must focus" and "You must focus on the task" convey a similar message, but they have different structures and slightly different emphasis. Here's a breakdown:

- **"Task you must focus"**: This is a more emphatic or poetic phrasing. It places the "task" in the prominent position at the beginning of the sentence. This construction highlights the _task itself_ as the primary focus. It's less common in everyday speech but can be used for dramatic effect. It sounds somewhat like Yoda from Star Wars.
    
- **"You must focus on the task"**: This is a more standard and direct sentence structure. The emphasis is more balanced between "you" and "the task." It's a clear instruction, directly telling the person what to do.

Take your time on examples do it extremely thoroughly


----
Tworzenie planu na podstawie wcześniej zebranych danych np na podstawie designu niech AI sam to ogarnie, zamiast próbowac pisać to samemu.
Czyli etap eksploracji jest konieczny podobnie jka u deweloperów


Create ExerciseTask feature with propriate structure.

The feature has nested navigator.
All three screens are connected by single navigator-connected screen model - ExerciseScreenModel (sample can be found in feature/ring_connection)

```kotlin
data class State(
    val preMeasurement: Int,
    val postMeasurement: Int,
    val headers: Map<String, String> // headers passed to WebView inc. accessToken from TokensRepository
) {
    
    val url = "${BuildKonfig.API_BASE_URL}/patient/kemtai/exercise"
}
```

The feature is composed of 3 screens:
1. PreExerciseScreen
2. ExerciseScreen 
3. PostExerciseScreen

## PreExerciseScreen
The screen responsible for blood presure measurement displayed in similar manner as educational task.

## ExerciseScreen
The screen with webview

```kotlin
@Composable
    internal fun WebViewSample(token: String) {
        MaterialTheme {
            val webViewState = rememberWebViewState(
                url = "https://e0b3-46-151-18-11.ngrok-free.app",
                additionalHttpHeaders = mapOf(
                    "Authorization" to "Bearer $token",
                    "Content-Type" to "html/text",
                )
            ).apply {
                webSettings.isJavaScriptEnabled = true
                webSettings.androidWebSettings.domStorageEnabled = true
                webSettings.androidWebSettings.mediaPlaybackRequiresUserGesture = false
                webSettings.androidWebSettings.allowFileAccess = true
            }

            val navigator = rememberWebViewNavigator()

            Column(Modifier.fillMaxSize()) {
                // WebView
                WebView(
                    state = webViewState,
                    navigator = navigator,
                    modifier = Modifier.fillMaxSize(),
                )
            }
        }
    }
```

## PostExerciseScreen
The screen responsible for blood presure measurement displayed in similar manner as educational task
Displays

Use TasksRepository to mark task as opened or completed.