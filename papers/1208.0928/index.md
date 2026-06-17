---
title: "表面符号 ── 大規模量子コンピュータへの実践的アプローチ"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 表面符号 ── 大規模量子コンピュータへの実践的アプローチ

*Austin G. Fowler, Matteo Mariantoni, John M. Martinis, Andrew N. Cleland (2012)*

- arXiv: [1208.0928](https://arxiv.org/abs/1208.0928)
- Internet Archive: [lk-paper-1208-0928](https://archive.org/details/lk-paper-1208-0928)

---

## 概要

Fowler et al. 2012「Surface codes: Towards practical large-scale quantum computation」（arXiv:1208.0928）の第1章を深く読み解きます。量子ビットが脆い理由から、ショアのアルゴリズムに必要な物理量子ビット約400万個という試算まで、数式と対話で丁寧に解説。

▼ 第1章の内容
・なぜ量子エラー訂正が必要か（デコヒーレンス・ゲートエラー）
・古典エラー訂正が量子に使えない2つの理由（no-cloning定理・測定崩壊）
・X/Z/Yエラーの3種類と位相エラーの難しさ
・符号距離dと物理量子ビット数 n ≈ 2d² の関係
・論理エラー率の指数的スケーリング（d=25 で 10の-15乗）
・ショアのアルゴリズム実行に必要な物理量子ビット約400万個の試算
・1サイクル1マイクロ秒・実行時間数時間の試算
・表面符号の3つの強み：近傍のみ・閾値1%・スケーラブル
・現在の量子コンピュータ（Google Willow 105個）との比較

▼ 原論文（arXiv）
https://arxiv.org/abs/1208.0928 — 表面符号：大規模量子コンピュータへの実践的アプローチ

#量子コンピュータ #量子誤り訂正 #表面符号 #arxiv #論文解説 #ゆっくり解説 #ずんだもん #量子情報 #量子力学 #IBM #Google #フォールトトレラント #量子ビット #機械学習 #テクノロジー

---

## 章別動画・解説

### 第1章: Part 1: 導入と規模推計

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 1: 導入と規模推計</h2>
<h3>なぜ量子エラー訂正が必要か（§I）</h3>
<ul>
<li>物理量子ビットは<strong>デコヒーレンス</strong>（環境との結合で量子状態が崩れる）と<strong>ゲートエラー</strong>の2種類の欠陥を持つ</li>
<li>現実のゲートエラー率：超伝導量子ビットで 0.1〜1%（古典コンピュータの $10^{18}$ 分の1に比べ 16桁悪い）</li>
<li><strong>量子エラーの種類</strong>：ビット反転 $X$、位相反転 $Z$、両方同時の $Y=iXZ$（古典の1種類に対し3種類）</li>
<li>Shor のアルゴリズム（RSA-2048 の素因数分解）：$\approx 10^9$ ゲート操作が必要</li>
<li>エラー率 0.1% で $10^9$ 回操作 → エラー <strong>100 万回</strong>：エラー訂正なしでは実用不可能</li>
</ul>
<h3>古典 vs 量子のエラー訂正</h3>
<table>
<thead>
<tr>
<th></th>
<th>古典</th>
<th>量子</th>
</tr>
</thead>
<tbody>
<tr>
<td>コピー</td>
<td>OK（繰り返し符号）</td>
<td><strong>不可</strong>（no-cloning 定理）</td>
</tr>
<tr>
<td>測定</td>
<td>状態を壊さない</td>
<td><strong>崩れる</strong>（射影測定）</td>
</tr>
<tr>
<td>エラー種別</td>
<td>ビット反転のみ</td>
<td>$X$（反転）＋$Z$（位相）＋$Y$ の 3種</td>
</tr>
<tr>
<td>エラー検出法</td>
<td>直接読み出し</td>
<td>スタビライザー（状態を壊さずシンドロームだけ取得）</td>
</tr>
</tbody>
</table>
<h3>規模の推計（§II）</h3>
<blockquote>
<p>📊 Fig. 1 参照（原論文）</p>
</blockquote>
<p><strong>符号距離 $d$</strong>：表面符号格子の一辺サイズ（同時に訂正できるエラー数 $\lfloor(d-1)/2\rfloor$）</p>
<p>$$n_{\text{phys}} \approx 2d^2 \quad (\text{1論理量子ビットあたり物理量子ビット数})$$</p>
<p>論理エラー率のスケーリング（物理エラー率 $p$ が閾値 $p_{\rm th} \approx 1\%$ 以下のとき）：</p>
<p>$$p_L \approx A \left(\frac{p}{p_{\rm th}}\right)^{\lceil d/2 \rceil}$$</p>
<ul>
<li>$d = 25$ のとき：$p_L \approx 10^{-15}$（$10^9$ ゲート操作に耐えられる）</li>
<li>必要な物理量子ビット：$2d^2 \approx 1{,}250$ 個（1論理量子ビットあたり）</li>
<li>Shor（RSA-2048）：論理量子ビット $\approx 2{,}000$ 個 → 基本部 <strong>250万個</strong></li>
<li>マジック状態蒸留ファクトリー込みの総計：物理量子ビット <strong>≈ 400 万個</strong></li>
</ul>
<p><strong>実行時間の試算：</strong></p>
<ul>
<li>1サイクル（スタビライザー測定一回）$\approx 1 \, \mu\text{s}$（ゲート 100 ns + 読み出し 900 ns）</li>
<li>Shor 必要サイクル数：$\approx 10^9$ → 基本計算 <strong>≈ 1000 秒</strong></li>
<li>マジック状態蒸留込み実効時間：<strong>≈ 数時間〜数日</strong>（閾値・蒸留段数依存）</li>
</ul>
<p><strong>現状（2024）との比較：</strong></p>
<table>
<thead>
<tr>
<th>実装</th>
<th>物理量子ビット数</th>
</tr>
</thead>
<tbody>
<tr>
<td>Google Willow (2024)</td>
<td>105 個</td>
</tr>
<tr>
<td>必要 (Shor RSA-2048)</td>
<td>≈ 400 万個</td>
</tr>
<tr>
<td>スケールアップ倍率</td>
<td><strong>≈ 40,000 倍</strong></td>
</tr>
</tbody>
</table>
<h3>表面符号の 3 つの強み</h3>
<table>
<thead>
<tr>
<th>強み</th>
<th>内容</th>
<th>意義</th>
</tr>
</thead>
<tbody>
<tr>
<td>近傍相互作用のみ</td>
<td>隣接4量子ビット操作で完結</td>
<td>超伝導・中性原子等のプラットフォームで製造しやすい</td>
</tr>
<tr>
<td>高い誤り閾値</td>
<td>$p_{\rm th} \approx 1\%$（他の多くの符号より高い）</td>
<td>現行の物理エラー率（0.1〜0.5%）はすでに閾値以下</td>
</tr>
<tr>
<td>スケーラブル</td>
<td>$d$ を大きくするだけで論理エラーが指数的に改善</td>
<td>設計変更不要で規模拡大可能</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第2章: Part 2: スタビライザーと表面符号

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 2: スタビライザーと表面符号</h2>
<h3>パウリ演算子（§III）</h3>
<p>$$
X = \begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
Z = \begin{pmatrix}1&0\\0&-1\end{pmatrix},\quad
Y = iXZ = \begin{pmatrix}0&-i\\i&0\end{pmatrix}
$$</p>
<ul>
<li>$X$：ビット反転，$Z$：位相反転</li>
<li><strong>反可換</strong>：$XZ = -ZX$（この非可換性がエラー検出の鍵）</li>
<li>パウリ群：$\{I, X, Y, Z\}^{\otimes n}$（$n$ 量子ビット系）</li>
</ul>
<h3>スタビライザーの定義</h3>
<p>量子状態 $|\psi\rangle$ を固有値 $+1$ で安定化する演算子 $S$：</p>
<p>$$S|\psi\rangle = +|\psi\rangle$$</p>
<p>エラー $E$ が起きると（$E$ が $S$ と反可換なら）：</p>
<p>$$S(E|\psi\rangle) = -E(S|\psi\rangle) = -(E|\psi\rangle)$$</p>
<p>固有値が $-1$ に反転 → <strong>エラーを状態を崩さずに検出</strong></p>
<h3>2量子ビットの例（§III）</h3>
<p>$S_1 = ZZ$，$S_2 = XX$ でベル状態 $|\Phi^+\rangle = \frac{|00\rangle+|11\rangle}{\sqrt{2}}$ を安定化</p>
<ul>
<li>$X_1$ エラー → $S_1 = ZZ$ の測定値が $-1$ に → 検出！量子状態は破壊されない</li>
<li>量子情報は $Z_1Z_2$ と $X_1X_2$ の固有空間に「エンコード」されている</li>
</ul>
<h3>表面符号のスタビライザー（§IV）</h3>
<blockquote>
<p>📊 Fig. 2, 3 参照（原論文）</p>
</blockquote>
<p>$d \times d$ 格子上に量子ビットを配置（辺上に1個ずつ）：</p>
<p>$$A_v = \prod_{i \in \partial v} X_i \qquad (\text{頂点プラケット：位相エラー検出})$$</p>
<p>$$B_p = \prod_{i \in \partial p} Z_i \qquad (\text{面プラケット：ビット反転エラー検出})$$</p>
<ul>
<li>$[A_v, B_p] = 0$（常に可換 → 同時測定可能、論理状態を壊さない）</li>
<li>正常状態：全プラケット測定値 $= +1$（シンドロームはすべて 0）</li>
</ul>
<pre><code>● ─X─ ● ─X─ ●
|      |      |
Z  Bp  Z  Bp  Z
|      |      |
● ─X─ ● ─X─ ●
</code></pre>
<hr />

</details>

### 第3章: Part 3: 欠陥と論理量子ビットの初期化・測定

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 3: 欠陥と論理量子ビットの初期化・測定</h2>
<h3>欠陥（Defect）とは（§V）</h3>
<blockquote>
<p>📊 Fig. 4, 5 参照（原論文）</p>
</blockquote>
<p>格子上の一部のプラケット測定をあえて止めると「<strong>欠陥（穴）</strong>」が生まれる：</p>
<ul>
<li><strong>$d$タイプ欠陥</strong>：$B_p$（$Z$プラケット）を止めた穴</li>
<li><strong>$p$タイプ欠陥</strong>：$A_v$（$X$プラケット）を止めた穴</li>
<li>同タイプの欠陥ペアで <strong>論理量子ビット 1個</strong> を定義</li>
</ul>
<p>論理演算子：</p>
<p>$$\bar{X} = \prod_{i \in \text{欠陥間の鎖}} X_i, \qquad \bar{Z} = \prod_{i \in \text{欠陥周囲}} Z_i$$</p>
<h3>論理量子ビットの初期化・測定（§VI）</h3>
<blockquote>
<p>📊 Fig. 6 参照（原論文）</p>
</blockquote>
<table>
<thead>
<tr>
<th>操作</th>
<th>手順</th>
</tr>
</thead>
<tbody>
<tr>
<td>$|\bar{0}\rangle$ 初期化</td>
<td>全データ量子ビットを $|0\rangle$ にセット → スタビライザー測定 $d$ 回</td>
</tr>
<tr>
<td>$|\bar{+}\rangle$ 初期化</td>
<td>全データ量子ビットを $|+\rangle$ にセット → スタビライザー測定 $d$ 回</td>
</tr>
<tr>
<td>$\bar{Z}$ 測定</td>
<td>$d$タイプ欠陥間のデータ量子ビットを $Z$ 測定（情報は消滅）</td>
</tr>
<tr>
<td>$\bar{X}$ 測定</td>
<td>$p$タイプ欠陥を囲む量子ビットを $X$ 測定（情報は消滅）</td>
</tr>
</tbody>
</table>
<ul>
<li>測定ノイズを考慮して <strong>$d$ 回繰り返し測定</strong>して多数決</li>
</ul>
<hr />

</details>

### 第4章: Part 4: 論理量子ビットの移動とブレイド

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 4: 論理量子ビットの移動とブレイド</h2>
<h3>論理量子ビットの移動（§VII）</h3>
<blockquote>
<p>📊 Fig. 7, 8 参照（原論文）</p>
</blockquote>
<p>欠陥を格子上で「滑らせる」ことで論理量子ビットを移動：</p>
<ol>
<li>移動先のプラケット測定を停止（穴を拡張）</li>
<li>元の位置の測定を再開（穴を縮小）</li>
<li>移動中もスタビライザー測定を継続 → <strong>フォールトトレラント</strong></li>
</ol>
<p>移動コスト：距離 $\ell$ の移動に $O(\ell \cdot d)$ サイクル</p>
<h3>ブレイドによる論理 CNOT（§VIII）</h3>
<blockquote>
<p>📊 Fig. 9, 10, 11 参照（原論文）</p>
</blockquote>
<p>制御量子ビット（$d$型欠陥）を標的量子ビット（$p$型欠陥）の<strong>周りを一周</strong>させる：</p>
<p>$$|c\rangle|\psi\rangle \xrightarrow{\text{braid}} |c\rangle\, X^c|\psi\rangle \quad (\text{論理 CNOT})$$</p>
<ul>
<li><strong>位相的操作</strong>：経路の細部が変わっても結果は不変（トポロジカル保護）</li>
<li>局所エラーに対して本質的に頑健</li>
<li>ゲートコスト：$O(d^2)$ サイクル</li>
</ul>
<hr />

</details>

### 第5章: Part 5: HゲートとSゲートとTゲート

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 5: HゲートとSゲートとTゲート</h2>
<h3>Hadamard ゲート（§IX）</h3>
<blockquote>
<p>📊 Fig. 12 参照（原論文）</p>
</blockquote>
<p>$$H = \frac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix}, \quad HXH^\dagger = Z,\quad HZH^\dagger = X$$</p>
<p>表面符号での実現：格子を <strong>90°回転</strong> → $X$プラケットと$Z$プラケットが入れ替わる（物理的には量子ビットの再ラベリング）</p>
<h3>$S$ ゲート（§X）</h3>
<blockquote>
<p>📊 Fig. 13 参照（原論文）</p>
</blockquote>
<p>$$S = \begin{pmatrix}1&0\\0&i\end{pmatrix} = \sqrt{Z}$$</p>
<p>アンシラ量子ビットとの<strong>測定ベース操作</strong>で実現：アンシラ準備 → CNOT → $X$ 測定 → パウリ補正</p>
<h3>$T$ ゲート（§XI）</h3>
<p>$$T = \begin{pmatrix}1&0\\0&e^{i\pi/4}\end{pmatrix} = \sqrt{S}$$</p>
<ul>
<li><strong>スタビライザー形式の外</strong>にあるゲート → 直接フォールトトレラントに実現不可</li>
<li>マジック状態を使った「状態注入（state injection）」で実現：</li>
</ul>
<p>$$|T\rangle = T|+\rangle = \frac{|0\rangle + e^{i\pi/4}|1\rangle}{\sqrt{2}}$$</p>
<p>$|T\rangle$ を消費することで $T$ ゲートを 1 回適用できる</p>
<hr />

</details>

### 第6章: Part 6: マジック状態蒸留と物理実装

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp4"></video>

<audio controls src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Part 6: マジック状態蒸留と物理実装</h2>
<h3>マジック状態蒸留（§XII）</h3>
<blockquote>
<p>📊 Fig. 14, 15 参照（原論文）</p>
</blockquote>
<p>低品質な $|T\rangle$（エラー率 $p_{\rm in}$）を多数消費して高品質な $|T\rangle$ を生成：</p>
<p><strong>15-to-1 蒸留プロトコル：</strong></p>
<p>$$p_{\rm out} \approx 35\, p_{\rm in}^3$$</p>
<ul>
<li>15 個の低品質 $|T\rangle$ を消費して 1 個の高品質 $|T\rangle$ を出力</li>
<li>エラー率が 3 乗で改善（$p_{\rm in} = 10^{-3}$ → $p_{\rm out} \approx 3.5 \times 10^{-8}$）</li>
<li>必要に応じて <strong>多段蒸留</strong>（第1段の出力を第2段の入力に使う）</li>
</ul>
<h3>$\{H, S, T, \text{CNOT}\}$ = ユニバーサルゲートセット</h3>
<table>
<thead>
<tr>
<th>ゲート</th>
<th>表面符号での実装</th>
</tr>
</thead>
<tbody>
<tr>
<td>CNOT</td>
<td>ブレイド変換（§VIII）</td>
</tr>
<tr>
<td>$H$</td>
<td>格子 90° 回転</td>
</tr>
<tr>
<td>$S$</td>
<td>測定ベース操作</td>
</tr>
<tr>
<td>$T$</td>
<td>マジック状態注入</td>
</tr>
</tbody>
</table>
<h3>物理実装（§XIV）</h3>
<blockquote>
<p>📊 Fig. 16, 17 参照（原論文）</p>
</blockquote>
<table>
<thead>
<tr>
<th>プラットフォーム</th>
<th>特徴</th>
<th>課題</th>
</tr>
</thead>
<tbody>
<tr>
<td>超伝導量子ビット</td>
<td>高速（ns ゲート）、2次元格子が作りやすい</td>
<td>デコヒーレンス時間 $\sim 100\,\mu$s</td>
</tr>
<tr>
<td>トラップドイオン</td>
<td>長いコヒーレンス時間、高忠実度</td>
<td>操作速度が遅い（$\mu$s ゲート）、スケールアップ困難</td>
</tr>
<tr>
<td>中性原子</td>
<td>光ピンセットで柔軟な配置</td>
<td>読み出し速度、真空技術が課題</td>
</tr>
<tr>
<td>フォトニクス</td>
<td>室温動作可能</td>
<td>決定論的2量子ビットゲートが困難</td>
</tr>
</tbody>
</table>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
