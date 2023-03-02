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

### Step 7

- 為什麼按鈕狀態的變數不能寫在 Composable function 的 Block 裡?
  - 在 Block 內的資料異動並不會讓 Compose 偵測到 "狀態改變" 。(Compose 並未追蹤這個變數)
  - 每次呼叫這個 Composable function 也會讓 Block 內的變數重設。
  - Compose 應用程式會藉由呼叫可組合函式將資料轉換為 UI。當資料變更時，Compose 會用新的資料重新執行這些函式，建立更新過的 UI，這稱為「重新組成」。Compose 也會注意每個可組合項需要哪些資料，以便它只需要重新組成資料有變的元件，並略過不受影響的元件。
- 使用 State 和 MutableState 來儲存狀態
  - 這兩個都是保留值的介面，只要這個值有變化，就會觸發 UI 更新 (重新組成)。
- `remember`: 記住可變動狀態。
    - 因為不能把 mutableStateOf 指派給 Composable function 裡的變數。(每次呼叫值會被重設)
    - 它可以「保護」項目不受重新組成影響，讓系統不會重設狀態。
    - **請注意，如果您從螢幕其他部分呼叫同一項可組合項，您將會建立不同的 UI 元素，每個元素都有自己的狀態版本。您可以把內部狀態當成類別裡的私人變數。**
    - Composable function 會自動「訂閱」這個狀態。當狀態變更時，可組合項會讀取這些重新組成的欄位，以便顯示更新內容。

### Step. 8

- 如果有狀態會由多個函式讀取或修改，就應該放在共通的祖系裡面，這個過程稱為「狀態提升」。「提昇」的意思就是「抬高」或「提高」。
  - 可以避免重複使用狀態和出現錯誤
  - 可以重複利用可組合項
  - 讓可組合項更容易進行測試
- 如果該狀態不該由 Composable's parent 來控制
  - 不該提升
  - 可靠資料來源 (source of truth) 屬於建立和控管該狀態的項目。
- 屬性使用 `by` 關鍵字，而不是 `=`。這是屬性委派，讓您可以不用每次都輸入 .value。
- 在 Compose 當中是不用隱藏 UI 元素的。只需要不把這些元素加到組成裡就好，然後這些元素就不會加入 Compose 產生的 UI 樹狀結構了。
- 如何向上傳遞事件？答案是**向下傳遞回呼**。回呼是傳遞給其他函式當做引數的函式，在發生事件時，系統就會執行這個函式。
  - 藉由傳遞函式 (而不是狀態) 給 `OnboardingScreen`，這個可組合項更容易重複利用，也能保護狀態不會因為其他可組合項而變動。

### Step.9 

- `LazyColumn`
  - 只會轉譯螢幕上看得到的項目，當轉譯龐大清單的時候能夠提昇效能。
  - `LazyColumn` 和 `LazyRow` 在 Android Views 裡和 `RecyclerView` 相等。
  - `items` block: 在這裡寫入個別項目的轉譯邏輯。
    - 請務必確定已經匯入 androidx.compose.foundation.lazy.items，因為 Android Studio 預設會挑選其他項目函式。
  -  不會像 `RecyclerView` 一樣回收子項。當您捲動的時候，這個項目會產生新的可組合項，而依然可以保持優良的效能，因為比起執行個體化 Android Views 來說，產生可組合項耗用的資源較少。