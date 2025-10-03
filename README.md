# Lights Out 遊戲與線性代數解法研究

## 摘要
Lights Out 是一種經典的電子益智遊戲，其玩法簡單但背後蘊含豐富的數學結構。本文透過線性代數的觀點，將遊戲形式化為在有限域 $\mathbb{F}_2$ 上的線性方程組，並探討兩種主要解法：高斯消去法與 Light Chasing 演算法。接著，我們嚴格證明 3×3 棋盤的係數矩陣可逆，因此任何目標盤面皆有唯一解。最後，介紹反矩陣法，並提出公式 $x = A^{-1}\cdot(\text{target}\oplus\text{current})$，提供快速解答方式。此研究顯示了數學建模如何有效解決看似娛樂性的遊戲問題。

---

## 引言

### 研究動機
解決醉夢閣伺服器內獲取符咒的益智遊戲問題。

### 遊戲背景
Lights Out 由 Tiger Electronics 於 1995 年發行，其基本規則為：棋盤為 $n\times n$ 的方格，每格代表一盞燈，具有「亮」與「暗」兩種狀態。玩家每次按下一個格子，該格及其上下左右的相鄰格燈狀態會翻轉。遊戲目標是在有限步驟內將所有燈熄滅。此遊戲具有交換律與二元狀態的性質，為數學建模提供了良好基礎。

---

## 方法

### 線性代數建模
將盤面狀態展平為向量 $b \in \mathbb{F}_2^{n^2}$，按鍵方案為 $x \in \mathbb{F}_2^{n^2}$。定義影響矩陣 $A \in \mathbb{F}_2^{n^2\times n^2}$，其中 $A_{q,p}=1$ 若按下第 $p$ 個按鈕會翻轉第 $q$ 個燈，否則 $A_{q,p}=0$。則遊戲可表達為
\[
A\,x = b \pmod{2}.
\]
此處 $\mathbb{F}_2=\{0,1\}$，加法為 XOR。

### Light Chasing 演算法
Light Chasing 屬於一種啟發式的消元方法。其策略為逐行處理棋盤，對於頂行亮燈，於次行對應位置按下按鈕，使得頂行燈熄滅。此過程自上而下直到倒數第二行。最後，根據最後一行的燈光模式，決定第一行的按鍵組合，再重複過程，即可將盤面全部熄滅。此方法等效於高斯消去的行運算，但更適合人工操作。

### 3×3 棋盤可解性證明
對於 3×3 棋盤，矩陣 $A$ 為 $9\times9$。文獻指出其在 $\mathbb{F}_2$ 上為滿秩矩陣，且行列式為 1，因此可逆。故對任何 $b$，方程組 $A x = b$ 在 $\mathbb{F}_2$ 上均有唯一解。此性質保證 3×3 的 Lights Out 永遠可解。

### 反矩陣法
若已預先計算 $A^{-1}$，則可快速求解：
\[
x = A^{-1} \cdot ( \text{target} \oplus \text{current} ).
\]
此處 $\oplus$ 為 XOR。此方法計算效率高，適用於程式實作中快速獲取解答。

---

## 結果
1. 成功建立 Lights Out 遊戲的線性代數模型。  
2. 證明 3×3 棋盤的矩陣 $A$ 可逆，因此保證必有解。  
3. 提出反矩陣法，將遊戲求解轉化為簡單矩陣乘法，可於實務中即時應用。  

---

## 討論
Lights Out 遊戲的數學模型展示了娛樂問題與線性代數的密切關聯。高斯消去法與 Light Chasing 演算法雖然皆可解題，但在實務應用上，Light Chasing 更適合人工操作；而反矩陣法則適合電腦實作。未來研究可延伸至更大棋盤（如 5×5），或探討矩陣在其他規則變體下的秩與可解性。

---

## 結論
本文從線性代數觀點剖析 Lights Out 遊戲，展示了建模、演算法設計與可逆性證明。3×3 棋盤的可逆性確保所有盤面均可解，而反矩陣法提供了高效的解題途徑。此研究顯示數學與遊戲設計之間的深刻聯繫。

---

## 參考文獻
- Anderson, M., & Feil, T. (1998). Turning lights out with linear algebra. *Mathematics Magazine, 71*(4), 300–303. https://doi.org/10.2307/2690705
- Eisele, R. (2018). *Solving LightsOut using linear algebra*. Retrieved from https://raw.org/research/solving-lightsout-using-linear-algebra/
- Weisstein, E. W. (n.d.). *Lights out puzzle*. In *MathWorld–A Wolfram Web Resource*. Wolfram Research. Retrieved from https://mathworld.wolfram.com/LightsOutPuzzle.html  
- Wikipedia contributors. (2023, December 29). *Lights Out (game)*. In *Wikipedia*. https://en.wikipedia.org/wiki/Lights_Out_(game)  
- Jaap’s Puzzle Page. (n.d.). *Lights Out*. Retrieved from https://www.jaapsch.net/puzzles/lights.htm  
- DouO. (2007). *LightsOut 解法小探* [Blog post]. Retrieved from https://dourok.info/2012/05/31/lights-out-solution/
