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

### Step 6

- Compose 中的三個基本標準版面配置元素為 Column (垂直排列)、Row (水平排列) 和 Box (堆疊)。
- 可組合函式的使用方式和 Kotlin 其他函式相同。可以藉由新增陳述式影響 UI 的顯示方式。
- 尚未幫可組合項設定大小或設定任何尺寸限制，因此每一列都會盡可能採用最小的空間，預覽也是如此。 
- `@Preview` 註解新增 `widthDp` 參數: 設定預覽寬度。
- 修飾詞也可以超載，例如您可以指定幾種不同的邊框間距建立方式。
- 如果想為元素新增多個修飾詞，只要鏈結即可。
- weight 修飾詞可以用元素填滿可用空間，因此屬於「有彈性」，這樣做會推擠其他沒有權重的元素，這些元素屬於「無彈性」。這也會讓 fillMaxWidth 修飾詞變得沒有必要。
- Compose 可以按照質感設計按鈕規格：Button、ElevatedButton、FilledTonalButton、OutlinedButton 和 TextButton 提供多種 Button。