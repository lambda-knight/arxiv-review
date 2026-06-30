---
title: "表面符号：大規模量子コンピュータへの実践的アプローチ"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

### 第1章: §I-§II: 背景と量子ビットの基礎

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§I-§II: 背景と量子ビットの基礎</h2>
<h3>§I. Background ── なぜ表面符号か</h3>
<ul>
<li>量子コンピュータは<strong>素因数分解</strong>（Shorのアルゴリズム）や<strong>データ検索</strong>（Groverアルゴリズム）で古典コンピュータを超えられる</li>
<li>表面符号の起源：Kitaevの<strong>トーリック符号</strong>（トーラス面上の位相的符号）→ Bravyi, Kitaev, Freedman, Meyerが平面版（surface code）に発展</li>
<li>Preskillらが「単一面でのエラー率最大<strong>3%</strong>」を示す → Raussendorfらが<strong>ブレイド変換</strong>による論理CNOTを発見</li>
</ul>
<p><strong>他の符号との比較（2D最近傍結合での閾値）:</strong></p>
<table>
<thead>
<tr>
<th>符号</th>
<th>閾値</th>
</tr>
</thead>
<tbody>
<tr>
<td>Steane符号</td>
<td>$\approx 2 \times 10^{-5}$</td>
</tr>
<tr>
<td>Bacon-Shor符号</td>
<td>$\approx 2 \times 10^{-5}$</td>
</tr>
<tr>
<td><strong>表面符号</strong></td>
<td><strong>$\approx 0.57\% \sim 1\%$</strong>（<strong>10万倍有利</strong>）</td>
</tr>
</tbody>
</table>
<ul>
<li>価格：物理量子ビット数は多い（最低13個で論理1個、実用には $10^3 \sim 10^4$ 個）</li>
</ul>
<h3>§II. Introduction ── パウリ演算子と量子エラー</h3>
<p>$$
\hat{X} = \begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
\hat{Z} = \begin{pmatrix}1&0\\0&-1\end{pmatrix},\quad
\hat{Y} = \hat{Z}\hat{X} = \begin{pmatrix}0&-1\\1&0\end{pmatrix}
$$</p>
<blockquote>
<p>注意：この論文では $\hat{Y} = \hat{Z}\hat{X}$（$i\sigma_y$ではない。付録Aを参照）</p>
</blockquote>
<p><strong>反可換関係（エラー検出の核心）：</strong></p>
<p>$$\hat{X}\hat{Z} = -\hat{Z}\hat{X}, \quad \hat{X}^2 = \hat{Z}^2 = \hat{I}$$</p>
<p><strong>ユニバーサルゲートセット：</strong> $\{\hat{X}, \hat{Z}, \hat{H}, \hat{S}, \hat{T}, \text{CNOT}\}$</p>
<p>$$\hat{H} = \frac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix},\quad
\hat{S} = \begin{pmatrix}1&0\\0&i\end{pmatrix},\quad
\hat{T} = \begin{pmatrix}1&0\\0&e^{i\pi/4}\end{pmatrix}$$</p>
<p><strong>量子エラーのモデル：</strong>
- ビット反転エラー $\hat{X}$：$|g\rangle \leftrightarrow |e\rangle$
- 位相反転エラー $\hat{Z}$：$\alpha|g\rangle + \beta|e\rangle \to \alpha|g\rangle - \beta|e\rangle$
- $\hat{Y} = \hat{Z}\hat{X}$：両方同時
- エラーは<strong>修正する必要はない</strong>——測定結果を古典的に補正するだけでよい</p>
<hr />

</details>

### 第2章: §III-§IV: 表面符号と静止状態の測定サイクル

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§III-§IV: 表面符号と静止状態の測定サイクル</h2>
<h3>§III. The Surface Code ── 2次元格子の配置</h3>
<blockquote>
<p>📊 Fig. 1 参照（原論文）</p>
</blockquote>
<p><strong>2種類の量子ビット：</strong></p>
<table>
<thead>
<tr>
<th>種別</th>
<th>役割</th>
<th>記号</th>
</tr>
</thead>
<tbody>
<tr>
<td>データ量子ビット（data qubit）</td>
<td>計算情報を保持</td>
<td>白丸</td>
</tr>
<tr>
<td>測定量子ビット（measure qubit）</td>
<td>エラーを検出</td>
<td>黒丸</td>
</tr>
</tbody>
</table>
<ul>
<li><strong>measure-Zキュービット</strong>（緑）：隣接4データキュービットの $\hat{Z}_a\hat{Z}_b\hat{Z}_c\hat{Z}_d$ を測定</li>
<li><strong>measure-Xキュービット</strong>（橙）：隣接4データキュービットの $\hat{X}_a\hat{X}_b\hat{X}_c\hat{X}_d$ を測定</li>
<li>各データ量子ビットは2個のmeasure-Z と2個のmeasure-X に隣接</li>
</ul>
<h3>§IV. Quiescent State ── 静止状態と測定サイクル</h3>
<p><strong>Zスタビライザー測定（measure-Zキュービット）の手順：</strong></p>
<p>$$|g\rangle \xrightarrow{\text{CNOT×4（データ→measure）}} \text{射影測定} \to Z_{abcd} = \pm 1$$</p>
<p><strong>Xスタビライザー測定（measure-Xキュービット）：</strong></p>
<p>$$|g\rangle \xrightarrow{H} \xrightarrow{\text{CNOT×4（measure→データ）}} \xrightarrow{H} \text{射影測定} \to X_{abcd} = \pm 1$$</p>
<p><strong>静止状態（quiescent state）の特徴：</strong>
- 全スタビライザーの測定値 $Z_{abcd} = X_{abcd} = +1$（全プラケット「ゼロ」）
- 測定サイクルを繰り返しても状態は変化しない
- CNOTの順番（ジグザグ順）は<strong>誤り伝播を防ぐ</strong>ために重要</p>
<p><strong>境界条件：</strong></p>
<pre><code>X境界  Z境界
 ───────────
|  X  Z  X  |  ← 上辺: Z境界（Zスタビライザーが境界に来る）
|  Z  X  Z  |
|  X  Z  X  |  ← 下辺: Z境界
 ───────────
↑左辺: X境界   ↑右辺: X境界
</code></pre>
<hr />

</details>

### 第3章: §V-§VI: エラー検出と論理演算子

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§V-§VI: エラー検出と論理演算子</h2>
<h3>§V. Single Qubit Errors ── 1量子ビットエラーの検出</h3>
<p><strong>$\hat{Z}_a$ エラーが起きたとき（位相反転）：</strong></p>
<p>$$\hat{X}_a\hat{X}_b\hat{X}_c\hat{X}_d \cdot \hat{Z}_a|\psi\rangle = -X_{abcd}\cdot\hat{Z}_a|\psi\rangle$$</p>
<p>→ 隣接2個のmeasure-Xキュービットの測定値が <strong>反転</strong>（$+1 \to -1$）</p>
<p><strong>$\hat{X}_a$ エラーが起きたとき（ビット反転）：</strong></p>
<p>$$\hat{Z}_a\hat{Z}_b\hat{Z}_c\hat{Z}_d \cdot \hat{X}_a|\psi\rangle = -Z_{abcd}\cdot\hat{X}_a|\psi\rangle$$</p>
<p>→ 隣接2個のmeasure-Zキュービットの測定値が <strong>反転</strong></p>
<blockquote>
<p>📊 Fig. 2 参照（原論文）</p>
</blockquote>
<p><strong>エラー検出のまとめ：</strong>
- $\hat{Z}$ エラー（位相反転）→ <strong>Xスタビライザーが反応</strong>
- $\hat{X}$ エラー（ビット反転）→ <strong>Zスタビライザーが反応</strong>
- $\hat{Y} = \hat{Z}\hat{X}$ エラー → <strong>両方が反応</strong>
- エラーが小さければ射影によって消去される（確率 $\approx 1-\epsilon^2$）</p>
<h3>§VI. Logical Operators ── 論理演算子</h3>
<blockquote>
<p>📊 Fig. 3 参照（原論文）</p>
</blockquote>
<p><strong>X境界を結ぶ $\hat{X}_L$ チェーン（$d=5$ の例）：</strong></p>
<p>$$\hat{X}_L = \hat{X}_1\hat{X}_2\hat{X}_3\hat{X}_4\hat{X}_5$$</p>
<p>全Zスタビライザーと可換 → 状態を壊さずに論理ビット反転</p>
<p><strong>Z境界を結ぶ $\hat{Z}_L$ チェーン：</strong></p>
<p>$$\hat{Z}_L = \hat{Z}_6\hat{Z}_7\hat{Z}_3\hat{Z}_8\hat{Z}_9$$</p>
<p><strong>反可換性（論理量子ビットの核心）：</strong></p>
<p>$$\hat{X}_L\hat{Z}_L = -\hat{Z}_L\hat{X}_L$$</p>
<p>→ 古典情報のコピーに対応する代わりに、位相空間での情報をエンコード</p>
<p><strong>$\hat{X}_L$ チェーンの変形：</strong></p>
<p>$$\hat{X}'_L = \hat{X}_1\hat{X}_{10}\hat{X}_{11}\hat{X}_{12}\hat{X}_3\hat{X}_4\hat{X}_5 = X_{2,10,11,12} \cdot \hat{X}_L$$</p>
<p>→ スタビライザーで変形しても論理的に同等（測定値の積で違いが吸収される）</p>
<hr />

</details>

### 第4章: §VII: エラー検出とデコード

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§VII: エラー検出とデコード</h2>
<h3>エラーの種類（§VII）</h3>
<blockquote>
<p>📊 Fig. 4, 5 参照（原論文）</p>
</blockquote>
<p>シミュレーションで考慮するエラー：
1. <strong>データ量子ビットの $\hat{I} \to \hat{X}, \hat{Y}, \hat{Z}$</strong>：各 $p/3$ の確率
2. <strong>初期化エラー</strong>：$|g\rangle$ の代わりに $|e\rangle$ に初期化（確率 $p$）
3. <strong>アダマールエラー</strong>：$\hat{H}$ に加えて $\hat{X}, \hat{Y}, \hat{Z}$（各 $p/3$）
4. <strong>測定エラー</strong>：誤った値を報告（確率 $p$）
5. <strong>CNOTエラー</strong>：15種の2量子ビットエラー（各 $p/15$）</p>
<h3>閾値と論理エラー率のスケーリング</h3>
<p><strong>論理エラー率のスケーリング（$p < p_{\rm th}$ のとき）：</strong></p>
<p>$$P_L \approx 0.03 \left(\frac{p}{p_{\rm th}}\right)^{d_e}, \quad d_e = \left\lceil\frac{d+1}{2}\right\rceil$$</p>
<p>$$p_{\rm th} \approx 0.57\% \quad (\text{この論文の実装では})$$</p>
<table>
<thead>
<tr>
<th>距離 $d$</th>
<th>$d_e$</th>
<th>$p=0.1\%$ での $P_L$</th>
</tr>
</thead>
<tbody>
<tr>
<td>5</td>
<td>3</td>
<td>$\sim 3\times 10^{-5}$</td>
</tr>
<tr>
<td>25</td>
<td>13</td>
<td>$\sim 10^{-28}$</td>
</tr>
<tr>
<td>55</td>
<td>28</td>
<td>$< 10^{-60}$</td>
</tr>
</tbody>
</table>
<h3>最小重みパーフェクトマッチング（Edmondsアルゴリズム）</h3>
<p>$$\text{エラーチェーンを空間-時間の3次元グラフとして表現}$$</p>
<ul>
<li>シンドローム変化点（-1になったプラケット）をノードとする</li>
<li>ノード間を結ぶ最短パスを「最もありそうなエラーチェーン」と推定</li>
<li>計算コスト：$O(n^3)$（$n$ = エラー検出点数）</li>
</ul>
<hr />

</details>

### 第5章: §VIII-§IX: 論理量子ビットの生成とパウリフレーム

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§VIII-§IX: 論理量子ビットの生成とパウリフレーム</h2>
<h3>§VIII. Creating Logical Qubits ── 欠陥（穴）による論理量子ビット</h3>
<blockquote>
<p>📊 Fig. 9, 10, 11 参照（原論文）</p>
</blockquote>
<p><strong>Z-cut欠陥（Z-cut hole）：</strong>
- measure-Zキュービットを1個停止 → X境界の穴が内部に生まれる</p>
<p>$$\hat{X}_L = \hat{X}_1\hat{X}_2\hat{X}_3 \quad (\text{外側X境界から穴のX境界へのチェーン})$$</p>
<p>$$\hat{Z}_L = \hat{Z}_3\hat{Z}_4\hat{Z}_5\hat{Z}_6 \quad (\text{穴を囲むループ})$$</p>
<p>$$\hat{X}_L\hat{Z}_L = -\hat{Z}_L\hat{X}_L \quad (\text{data qubit 3を共有→反可換})$$</p>
<p><strong>X-cut欠陥（X-cut hole）：</strong>
- measure-Xキュービットを停止 → Z境界の穴</p>
<p><strong>2穴で1論理量子ビット（double-cut qubit）：</strong></p>
<p>$$\hat{X}_L = \hat{X}_1\hat{X}_2\hat{X}_3 \quad (\text{2穴をつなぐチェーン})$$
$$\hat{Z}_L = \text{いずれかの穴を囲むループ}$$</p>
<p>距離 $d$：$\hat{X}_L$ チェーンの長さ（穴の間隔）と $\hat{Z}_L$ ループの長さの<strong>小さい方</strong></p>
<h3>§IX. Software-Implemented $\hat{Z}_L$ and $\hat{X}_L$ ── パウリフレーム</h3>
<ul>
<li>表面符号では <strong>$\hat{X}_L, \hat{Z}_L$ を直接実行しない</strong></li>
<li>測定結果のビットをソフトウェア（パウリフレーム）で追跡</li>
<li>例：$Z_{abcd} = -1$ の測定 → フレームに $\hat{X}_L$ を記録 → 後続の測定結果を自動補正</li>
<li>これにより<strong>物理的な操作コストなし</strong>でパウリ補正を実現</li>
</ul>
<hr />

</details>

### 第6章: §X-§XII: 初期化・測定と大きな論理量子ビット

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§X-§XII: 初期化・測定と大きな論理量子ビット</h2>
<h3>§X. Logical Qubit Initialization and Measurement</h3>
<p><strong>Easy初期化（欠陥の種類と同じ基底）：</strong></p>
<table>
<thead>
<tr>
<th>量子ビット</th>
<th>Easy初期化</th>
</tr>
</thead>
<tbody>
<tr>
<td>X-cut qubit</td>
<td>$\hat{X}_L$ 固有状態（$|+_L\rangle$ または $|-_L\rangle$）</td>
</tr>
<tr>
<td>Z-cut qubit</td>
<td>$\hat{Z}_L$ 固有状態（$|g_L\rangle$ または $|e_L\rangle$）</td>
</tr>
</tbody>
</table>
<p>→ 穴を作る直前のスタビライザー測定値から初期状態が決まる</p>
<p><strong>Difficult初期化（逆基底）：</strong>
- Xスタビライザーの帯（strip）を停止 → 孤立データ量子ビットを $\hat{Z}$ 測定 → $|g\rangle$ にセット → スタビライザー復元</p>
<h3>§XI. Errors During Stabilizer Measurement</h3>
<ul>
<li>スタビライザー測定の<strong>誤りは時間方向にも伝播</strong>する</li>
<li>時空間3次元（水平方向2D + 時間方向）でエラーチェーンを追跡</li>
<li>測定値の変化を時空間グラフでマッチングして訂正</li>
</ul>
<h3>§XII. Larger Logical Qubits ── 大きな論理量子ビット</h3>
<blockquote>
<p>📊 Fig. 11, 16 参照（原論文）</p>
</blockquote>
<p><strong>穴のサイズと距離 $d$ の関係：</strong></p>
<ul>
<li>最小欠陥（1スタビライザー停止）：$d = 3$（$\hat{X}_L = 3$ 量子ビット、$\hat{Z}_L = 4$ 量子ビット）</li>
<li>5スタビライザー停止：$\hat{Z}_L = 8$ 量子ビット → $d = 8$（穴の間隔を調整）</li>
<li>$d$ を2倍にすると物理量子ビット数は4倍、論理エラー率は指数的に改善</li>
</ul>
<p>$$P_L \sim p^{d_e}, \quad n_{\rm phys} \approx 2d^2 \quad (\text{1論理量子ビットあたり})$$</p>
<hr />

</details>

### 第7章: §XIII-§XIV: 論理量子ビットの移動とブレイド変換

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch07.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch07.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§XIII-§XIV: 論理量子ビットの移動とブレイド変換</h2>
<h3>§XIII. Moving Qubits ── 欠陥の移動</h3>
<blockquote>
<p>📊 Fig. 17, 18 参照（原論文）</p>
</blockquote>
<p><strong>欠陥移動の原理（ハイゼンベルク描像）：</strong>
- 波動関数でなく演算子を変換：$\hat{A} \to \hat{U}^\dagger\hat{A}\hat{U}$
- 欠陥を1セル移動 → $\hat{X}_L$ と $\hat{Z}_L$ を対応して更新</p>
<p><strong>1セル移動の手順：</strong>
1. 隣のスタビライザーを停止（穴を拡張）
2. 孤立データ量子ビットを $\hat{X}$ または $\hat{Z}$ で測定
3. 元のスタビライザーを再起動（穴を縮小）
4. $d$ サイクル待機（時間方向のエラーマッチングのため）</p>
<p><strong>マルチセル移動：</strong> 長い切り込みを1ステップで実行 → 同じ $1 + d$ サイクルで長距離移動可能</p>
<h3>§XIV. The Braiding Transformation ── 論理 CNOT</h3>
<blockquote>
<p>📊 Fig. 19, 20, 21, 22 参照（原論文）</p>
</blockquote>
<p><strong>ブレイドの概念：</strong>
- Qubit 1の片方の穴を、Qubit 2の2つの穴の<strong>間を通るように</strong>周回移動させる
- 経路が閉ループを描く → <strong>論理 CNOT</strong></p>
<p><strong>2量子ビットブレイドの変換（$\hat{X}_{L1}, \hat{Z}_{L1}, \hat{X}_{L2}, \hat{Z}_{L2}$）：</strong></p>
<table>
<thead>
<tr>
<th>演算子</th>
<th>ブレイド後</th>
</tr>
</thead>
<tbody>
<tr>
<td>$\hat{X}_{L1}$</td>
<td>$\hat{X}_{L1}\hat{X}_{L2}$ （制御XがターゲットにXを掛ける）</td>
</tr>
<tr>
<td>$\hat{Z}_{L1}$</td>
<td>$\hat{Z}_{L1}$</td>
</tr>
<tr>
<td>$\hat{X}_{L2}$</td>
<td>$\hat{X}_{L2}$</td>
</tr>
<tr>
<td>$\hat{Z}_{L2}$</td>
<td>$\hat{Z}_{L1}\hat{Z}_{L2}$</td>
</tr>
</tbody>
</table>
<p>→ これが論理 CNOT の変換規則と完全一致（Qubit 1 が制御、Qubit 2 が標的）</p>
<p><strong>CNOTのコスト：</strong> $O(d^2)$ サイクル（ブレイドの周長 × 距離 $d$）</p>
<hr />

</details>

### 第8章: §XV-§XVI: 1量子ビットゲート──HゲートとSL・TL演算子

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch08.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch08.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§XV-§XVI: 1量子ビットゲート──HゲートとSL・TL演算子</h2>
<h3>§XV. The Hadamard Transformation</h3>
<blockquote>
<p>📊 Fig. 26, 27, 28 参照（原論文）</p>
</blockquote>
<p><strong>論理アダマールの実現：</strong>
1. 論理量子ビットを囲む $\hat{X}$ スタビライザーを停止 → 「パッチ」を孤立
2. パッチ内の全データ量子ビットに物理 $\hat{H}$ を適用
3. SWAPでパッチを1セル分ずらす（格子アライメント復元）
4. 穴を再作成して論理量子ビットを復元</p>
<p>変換後：$\hat{X}_L \leftrightarrow \hat{Z}_L$（アダマールの定義通り）</p>
<p>$$\hat{H}\hat{X}\hat{H} = \hat{Z}, \quad \hat{H}\hat{Z}\hat{H} = \hat{X}$$</p>
<h3>§XVI. Single Qubit $\hat{S}_L$ and $\hat{T}_L$ Operators</h3>
<p>$$\hat{S}_L = \begin{pmatrix}1&0\\0&i\end{pmatrix},\quad \hat{T}_L = \begin{pmatrix}1&0\\0&e^{i\pi/4}\end{pmatrix}$$</p>
<p><strong>$\hat{S}_L$ ゲートの実現（測定ベース）：</strong></p>
<blockquote>
<p>📊 Fig. 29 参照（原論文）</p>
</blockquote>
<p>アンシラ $|Y_L\rangle = \frac{|g_L\rangle + i|e_L\rangle}{\sqrt{2}}$ を使って測定ベース操作</p>
<p>$$|Y_L\rangle \otimes |\psi_L\rangle \xrightarrow{\text{CNOT}} \xrightarrow{M_Z} \hat{S}_L|\psi_L\rangle \quad (M_Z = +1\text{ のとき})$$</p>
<p><strong>$\hat{T}_L$ ゲート（マジック状態注入）：</strong></p>
<blockquote>
<p>📊 Fig. 30 参照（原論文）</p>
</blockquote>
<p>アンシラ（マジック状態）$|A_L\rangle = \hat{T}|+_L\rangle = \frac{|g_L\rangle + e^{i\pi/4}|e_L\rangle}{\sqrt{2}}$</p>
<p>$$|A_L\rangle \otimes |\psi_L\rangle \xrightarrow{\text{CNOT}} \xrightarrow{M_Z} \begin{cases} \hat{T}_L|\psi_L\rangle & (M_Z = +1)  \\ \hat{X}_L\hat{T}^\dagger_L|\psi_L\rangle & (M_Z = -1) \end{cases}$$</p>
<p>$M_Z = -1$ のとき：$\hat{S}_L\hat{T}^\dagger_L = \hat{T}_L$ なので $\hat{S}_L$ ゲートで変換して $\hat{T}_L$ を得る</p>
<p><strong>マジック状態蒸留（15-to-1プロトコル）：</strong></p>
<p>低品質な $|A_L\rangle$（エラー率 $p_{\rm in}$）15個 → 高品質な $|A_L\rangle$ 1個：</p>
<p>$$p_{\rm out} \approx 35\, p_{\rm in}^3$$</p>
<p>2段蒸留：$p_{\rm in} = 0.5\% \to p_1 \approx 4\times 10^{-6} \to p_2 \approx 2\times 10^{-15}$（十分）</p>
<hr />

</details>

### 第9章: §XVII + 付録A-B: 物理実装とスタビライザー回路の詳細

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch09.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch09.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>§XVII + 付録A-B: 物理実装とスタビライザー回路の詳細</h2>
<h3>§XVII. Physical Implementations</h3>
<blockquote>
<p>📊 Fig. 17（superconducting実装の例）参照（原論文）</p>
</blockquote>
<p><strong>必要条件：</strong>
- 単一量子ビットゲート忠実度 $> 99\%$
- 2量子ビットCNOT忠実度 $> 99\%$
- コヒーレンス時間 $\geq 1\,\mu\text{s}$（ゲート時間 10-100 ns の場合）
- 物理量子ビット数：実用的には $\sim 10^8$ 個以上
- 古典制御のクロック：$\sim 10^6 \sim 10^7\,\text{Hz}$（表面符号サイクルに同期）</p>
<p><strong>超伝導回路が最有力：</strong>
- ゲート時間 10-100 ns（要件を満たす）
- 2D格子の集積化が比較的容易
- 課題：コヒーレンス時間・高速古典回路との統合</p>
<p><strong>サイクル時間の目標：</strong> 200 ns（1サイクル = CNOT 4回 + 測定1回）</p>
<h3>付録A. Notation（記号規約）</h3>
<p>$$|g\rangle = \begin{pmatrix}1\\0\end{pmatrix},\quad |e\rangle = \begin{pmatrix}0\\1\end{pmatrix}$$</p>
<p>$$\hat{X}|g\rangle = |e\rangle,\quad \hat{Z}|g\rangle = +|g\rangle,\quad \hat{Z}|e\rangle = -|e\rangle$$</p>
<p>$$|+\rangle = \frac{|g\rangle + |e\rangle}{\sqrt{2}},\quad |-\rangle = \frac{|g\rangle - |e\rangle}{\sqrt{2}}$$</p>
<p>$$\hat{Y} = \hat{Z}\hat{X} = \begin{pmatrix}0&-1\\1&0\end{pmatrix} \quad (\text{注：}i\sigma_y\text{ではない})$$</p>
<p><strong>可換関係（$i$なしの定義のため通常とずれる）：</strong>
$$[\hat{X},\hat{Y}] = -2\hat{Z},\quad [\hat{Y},\hat{Z}] = -2\hat{X},\quad [\hat{Z},\hat{X}] = +2\hat{Y}$$</p>
<h3>付録B. $\hat{Z}$ and $\hat{X}$ Stabilizer Circuits</h3>
<blockquote>
<p>📊 Fig. 34 参照（原論文）</p>
</blockquote>
<p>2量子ビット簡略版（data qubit a, b + measure-Z + measure-X）：</p>
<p><strong>Zスタビライザー回路（4ステップ）：</strong>
1. measure-Z を $|g\rangle$ に初期化
2. data qubit a → measure-Z の CNOT
3. data qubit b → measure-Z の CNOT
4. measure-Z を射影測定 → $Z_{ab} = \pm 1$</p>
<p>→ データキュービットは $\hat{Z}_a\hat{Z}_b$ の固有状態に射影される</p>
<p><strong>ベル状態一覧（Zスタビライザー測定後の状態）：</strong></p>
<table>
<thead>
<tr>
<th>$Z_{ab}$</th>
<th>$X_{ab}$</th>
<th>状態</th>
</tr>
</thead>
<tbody>
<tr>
<td>$+1$</td>
<td>$+1$</td>
<td>$|\Phi^+\rangle = \frac{|gg\rangle + |ee\rangle}{\sqrt{2}}$</td>
</tr>
<tr>
<td>$+1$</td>
<td>$-1$</td>
<td>$|\Phi^-\rangle = \frac{|gg\rangle - |ee\rangle}{\sqrt{2}}$</td>
</tr>
<tr>
<td>$-1$</td>
<td>$+1$</td>
<td>$|\Psi^+\rangle = \frac{|ge\rangle + |eg\rangle}{\sqrt{2}}$</td>
</tr>
<tr>
<td>$-1$</td>
<td>$-1$</td>
<td>$|\Psi^-\rangle = \frac{|ge\rangle - |eg\rangle}{\sqrt{2}}$</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第10章: 付録C-F: 初期化・測定・大型量子ビット・移動の詳細

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch10.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch10.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>付録C-F: 初期化・測定・大型量子ビット・移動の詳細</h2>
<h3>付録C. X-cut Qubit Initialization in $\hat{Z}_L$ Basis（Difficult初期化）</h3>
<blockquote>
<p>📊 Fig. 14 参照（原論文）</p>
</blockquote>
<ol>
<li>完全安定化アレイからスタート</li>
<li>$\hat{X}$ スタビライザーの帯（strip）を停止：帯の両端が穴の原型になる</li>
<li>帯に隣接する $\hat{Z}$ スタビライザーを4端子→3端子に削減</li>
<li>孤立データ量子ビット（1, 2, 3番）を $\hat{Z}$ 測定して1回記録</li>
<li>$|g\rangle$ にセット → $\hat{Z}_L = \hat{Z}_1\hat{Z}_2\hat{Z}_3 = +1$ の状態確定</li>
<li>内部 $\hat{X}$ スタビライザーと3端子 $\hat{Z}$ を元に戻す</li>
</ol>
<p><strong>なぜ $d$ 回ではなく1回の測定でよいか：</strong>
- 3端子 $\hat{Z}$ 測定と後続の4端子測定の比較で<strong>時間方向の距離</strong>を確保できるため</p>
<h3>付録D. Measuring an X-cut Qubit in $\hat{Z}_L$ Basis（Difficult測定）</h3>
<ol>
<li>$\hat{Z}_L$ チェーンが通る $\hat{X}$ スタビライザーの帯を停止</li>
<li>帯に隣接する $\hat{Z}$ スタビライザーを3端子に削減</li>
<li>孤立データ量子ビットを $\hat{X}$ 測定（各 $X_i = \pm 1$）</li>
<li>$X_L = \prod_i X_i$（論理 $\hat{X}_L$ の測定値）</li>
<li>データキュービットを $|g\rangle$ にリセット → 論理量子ビット消滅</li>
</ol>
<h3>付録E. Making a Larger Qubit（大型欠陥の作り方）</h3>
<blockquote>
<p>📊 Fig. 16 参照（原論文）</p>
</blockquote>
<p>5スタビライザー停止（$\hat{Z}_{s1}\sim\hat{Z}_{s4}$ と $\hat{X}_{s1}$）による大型Z-cut qubit：</p>
<ul>
<li>$\hat{Z}_L = \hat{Z}_1\hat{Z}_2\hat{Z}_3\hat{Z}_4\hat{Z}_5\hat{Z}_6\hat{Z}_7\hat{Z}_8$（8量子ビットのループ）</li>
<li>初期値 $= \prod_{k=1}^{4} Z_{sk}$（停止直前のスタビライザー測定値の積）</li>
<li>4つの内部データ量子ビットは $\hat{X}$ 測定でエラー追跡</li>
</ul>
<h3>付録F. One-Cell Qubit Move（1セル移動の詳細）</h3>
<blockquote>
<p>📊 Fig. 17 参照（原論文）</p>
</blockquote>
<p>Z-cut qubitを1セル移動する操作：</p>
<p>$$\hat{X}_L \to \hat{X}'_L = \hat{X}_L \cdot (\text{隣のXスタビライザーから貰う})$$</p>
<p>$$\hat{Z}_L \to \hat{Z}'_L = \hat{Z}_{sn} \quad (\text{新しい穴を囲む最小ループ})$$</p>
<ul>
<li>移動コスト：$1 + d$ サイクル（1サイクルで穴を移動、$d$ サイクル待機）</li>
<li>孤立データ量子ビットの $\hat{X}$ エラーは測定で消去、$\hat{Z}$ エラーは3端子スタビライザーで追跡</li>
</ul>
<hr />

</details>

### 第11章: 付録G-J: ブレイドと論理アダマール変換の詳細

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch11.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch11.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>付録G-J: ブレイドと論理アダマール変換の詳細</h2>
<h3>付録G. Multi-Cell Moves（マルチセル移動）</h3>
<blockquote>
<p>📊 Fig. 18 参照（原論文）</p>
</blockquote>
<ul>
<li>長い切り込みを<strong>1ステップ</strong>で作成 → 穴を一気に長距離移動</li>
<li>所要時間：$1 + d$ サイクル（単セル移動と同じ！）</li>
<li>移動中に $\hat{X}$ スタビライザーが「橋」をわたって更新される</li>
</ul>
<p>バイプロダクト演算子の符号追跡：</p>
<p>$$\hat{X}'_L = \prod_i X_{si} \cdot \hat{X}_L \quad (\text{橋わたりで生じる符号})$$</p>
<h3>付録H. Single Qubit Braid Transformation（1量子ビットブレイドの詳細）</h3>
<blockquote>
<p>📊 Fig. 19, 20 参照（原論文）</p>
</blockquote>
<p><strong>第1移動（8セル）後の演算子変換：</strong>
$$\hat{X}_L \to \hat{X}^e_L = \hat{X}_{\rm loop}\cdot\hat{X}_L, \quad \hat{Z}_L \to \hat{Z}^e_L = \hat{Z}_{sn}\cdot\hat{Z}_L$$</p>
<p><strong>第2移動（4セル、ループを閉じる）後：</strong>
$$\hat{X}''_L = X_{\rm loop}\cdot\hat{X}_L \quad (X_{\rm loop} = \text{囲まれたスタビライザー測定値の積})$$
$$\hat{Z}''_L = \hat{Z}_L \quad (\text{ループが元に戻る})$$</p>
<p>→ $\hat{X}_L$ は符号だけ変わって実質同じ、$\hat{Z}_L$ は不変</p>
<h3>付録I. Two-Qubit Braid Transformation（2量子ビットブレイドの詳細）</h3>
<blockquote>
<p>📊 Fig. 21, 22, 23 参照（原論文）</p>
</blockquote>
<p><strong>内部にQubit 2の穴を含むブレイドの変換規則：</strong></p>
<table>
<thead>
<tr>
<th>初期演算子</th>
<th>ブレイド後</th>
</tr>
</thead>
<tbody>
<tr>
<td>$\hat{X}_{L1}$</td>
<td>$\hat{X}_{L1}\hat{X}_{L2}$</td>
</tr>
<tr>
<td>$\hat{Z}_{L1}$</td>
<td>$\hat{Z}_{L1}$</td>
</tr>
<tr>
<td>$\hat{X}_{L2}$</td>
<td>$\hat{X}_{L2}$</td>
</tr>
<tr>
<td>$\hat{Z}_{L2}$</td>
<td>$\hat{Z}_{L1}\hat{Z}_{L2}$</td>
</tr>
</tbody>
</table>
<p>→ CNOT変換（Qubit 1 = 制御、Qubit 2 = 標的）と一致する証明</p>
<h3>付録J. Logical Hadamard Process（論理アダマール変換の詳細）</h3>
<blockquote>
<p>📊 Fig. 26, 27, 28 参照（原論文）</p>
</blockquote>
<p>$d=7$ のZ-cut qubitに対するHadamardの手順（各ステップの測定回数を明記）：</p>
<ol>
<li><strong>第1サイクル</strong>：論理量子ビット周囲の $\hat{X}$ スタビライザーを停止、リングを形成。3端子 $\hat{Z}$ 測定を3回実施（$d=7$ 専用）</li>
<li><strong>第2サイクル</strong>：リングをモートに拡大（外側の $\hat{X}$, $\hat{Z}$ も停止）、孤立データ量子ビットを測定</li>
<li><strong>物理Hadamard</strong>：パッチ内全データ量子ビットに $\hat{H}$ を適用</li>
<li><strong>SWAP操作</strong>：パッチを1セル分ずらして格子位置を合わせる</li>
<li><strong>穴の再作成</strong>：新しい位置に Z-cut 穴を2個作成</li>
<li><strong>帰還移動</strong>：穴を元の位置に移動（距離保護のため2ステップに分割）</li>
</ol>
<hr />

</details>

### 第12章: 付録K-M: 短い量子ビット・蒸留回路・規模推計

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch12.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch12.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>付録K-M: 短い量子ビット・蒸留回路・規模推計</h2>
<h3>付録K. Short Qubits（短い量子ビット）</h3>
<blockquote>
<p>📊 Fig. 31 参照（原論文）</p>
</blockquote>
<p>マジック状態 $|A_L\rangle$ の「状態注入」に使う特別な形状の論理量子ビット：</p>
<ul>
<li>短い量子ビット（short qubit）：細長い形状（$d_x \times d_z$ で $d_x \ll d_z$）</li>
<li>小さな物理エラー率での初期注入に特化</li>
<li>注入後すぐに蒸留回路へ渡す</li>
<li>注入エラー率の目安：$p_I \approx 0.5\%$（物理エラー率 $p = 0.1\%$ の場合）</li>
</ul>
<h3>付録L. $\hat{S}_L$ and $\hat{T}_L$ Distillation Sub-circuits</h3>
<blockquote>
<p>📊 Fig. 32, 33, 35 参照（原論文）</p>
</blockquote>
<p><strong>$\hat{S}_L$ 蒸留サブ回路：</strong></p>
<p>$$M'_Z = +1: \quad |\psi'\rangle = \hat{S}|\psi\rangle$$
$$M'_Z = -1: \quad |\psi'\rangle = \hat{X}\hat{Z}\hat{S}|\psi\rangle \xrightarrow{\hat{X}\hat{Z}\text{補正}} \hat{S}|\psi\rangle$$</p>
<p><strong>$\hat{T}^\dagger_L$ 蒸留サブ回路（Table VIIを参照）：</strong></p>
<p>入力状態が $\hat{Z}, \hat{X}, \hat{Y}$ エラーを含む場合の測定結果と補正操作：</p>
<p>$$p_{\rm out} = 35 p_{\rm in}^3 \quad (\text{15-to-1蒸留の精度スケーリング})$$</p>
<p><strong>多段蒸留の数値例（$p_{\rm in} = 0.5\%$）：</strong>
$$p_1 = 35 \times (0.005)^3 \approx 4.4 \times 10^{-6}$$
$$p_2 = 35 \times (4.4 \times 10^{-6})^3 \approx 3 \times 10^{-15}$$</p>
<h3>付録M. Estimating the Time and Size of a Factoring Circuit</h3>
<blockquote>
<p>📊 Table I, Table VII 参照（原論文）</p>
</blockquote>
<p><strong>Shor のアルゴリズム（$N = 2000$ ビット）の資源推計：</strong></p>
<p>$$\text{冪乗剰余回路：} \quad 40N^3 \text{ 逐次 Toffoli ゲート}$$</p>
<p>各 Toffoli ゲート = 7個の $\hat{T}_L$ ゲート（3並列 + 1 + 3並列）</p>
<p>$$\text{総 }T_L\text{ ゲート数} = 7 \times 40N^3 = 280N^3 \approx 2.2 \times 10^{12}$$</p>
<p><strong>実行時間：</strong> 各 $\hat{T}_L$ を $t_M = 100\,\text{ns}$ で実行</p>
<p>$$t_{\rm total} = 120N^3 \times t_M = 120 \times (2000)^3 \times 100\,\text{ns} \approx 26.7\,\text{hours}$$</p>
<p><strong>蒸留回路の規模（2段蒸留）：</strong></p>
<table>
<thead>
<tr>
<th>段</th>
<th>入力状態数</th>
<th>出力エラー率</th>
<th>必要論理量子ビット</th>
</tr>
</thead>
<tbody>
<tr>
<td>第1段</td>
<td>15</td>
<td>$\approx 4\times 10^{-6}$</td>
<td>16</td>
</tr>
<tr>
<td>第2段</td>
<td>15</td>
<td>$\approx 3\times 10^{-15}$</td>
<td>16</td>
</tr>
</tbody>
</table>
<p>必要物理量子ビット総数（$d = 25$, $p = 10^{-3}$）：</p>
<p>$$n_{\rm total} \approx 10^8 \quad (\text{著者の推計；蒸留ファクトリー込み})$$</p>
<hr />

</details>

