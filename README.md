# Codelab Jetpack Compose Basics

This is a codelab project guided by [Android Developer: Jetpack Compose Basics](https://developer.android.com/codelabs/jetpack-compose-basics?hl=zh-tw).

## Note

### Step 2

- Compose minimumSdkVersion is API 21.

### Step 3

- `@Composable` 將函式標註為 Composable Functions。
- Composable Functions 可產生 UI 階層。
- `Text` 是由程式庫提供的可組合函式。
- `setContent` Block 負責定義該 Activity 版面配置。
- `ComposeBasicCodelabTheme` 設定樣式主題
- `@Preview` 建立 Android Studio 中的 UI 預覽。

### Step 4

- `Surface` 可以設定背景顏色。
  - 當顏色設定為 `MaterialTheme.colorScheme.primary` 時，因為 `Surface` 也是 MaterialDesign 的元件，所以會自動為文字選合適的顏色。
- 修飾詞 `modifier`: 指示 UI 元素如何在其上層布局內部安排版面配置、顯示或行為。
  - 可以用數十種修飾詞對齊、製作動畫效果、展示、製作可以點擊或捲動的項目、變形。[Compose 修飾詞清單](https://developer.android.com/jetpack/compose/modifiers-list?hl=zh-tw)

### Step 5

- UI 裡加入越多元件，建立的巢狀結構層級也會越來越多。
- 函式變得太大，就會影響程式的判讀容易程度。
- 建立重複利用小型的元件，避免前面兩個問題。