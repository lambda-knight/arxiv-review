---
title: "量子誤り訂正：入門ガイド"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 量子誤り訂正：入門ガイド

*Joschka Roffe (2019) — arXiv:1907.11157*

- arXiv: [1907.11157](https://arxiv.org/abs/1907.11157)
- Internet Archive: [paper-explain-1907-11157](https://archive.org/details/paper-explain-1907-11157)

---

## 概要

表面符号・CSS符号・ステアン符号・閾値定理まで、量子誤り訂正の入門として最も読まれるレビュー論文（Roffe 2019）を5章にわたって徹底解説します。Googleの量子チップ「ウィロー」や IBMの誤り訂正実験の理論的背景として必須の内容です。

▼ 全5章の構成
・第1章: 量子誤り訂正の必要性とノイズモデル
・第2章: 古典符号から量子符号へ ── 繰り返し符号と安定化符号
・第3章: CSS符号の代数構造 ── ステアン符号
・第4章: 表面符号 ── 最も実用的な量子誤り訂正符号
・第5章: 耐障害性と閾値定理

▼ 論文情報
Joschka Roffe, "Quantum Error Correction: An Introductory Guide"
Contemporary Physics, 60(3), 226-245 (2019)
arXiv: https://arxiv.org/abs/1907.11157

#量子コンピュータ #量子誤り訂正 #表面符号 #ずんだもん #四国めたん #ゆっくり解説 #arxiv #論文解説 #量子情報 #QEC #stabilizer #surfacecode

---

## 章別動画・解説

### 第1章: 量子誤り訂正の背景と量子エラーの性質

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子誤り訂正の背景と量子エラーの性質</h2>
<h3>なぜ量子誤り訂正が必要か</h3>
<ul>
<li>量子コンピュータは光子・トラップイオン・超伝導回路・半導体スピンなど多様な量子ビットで実装が試みられている</li>
<li>すべての実装に共通する問題：<strong>量子ビットを外部ノイズから十分に遮断できない</strong></li>
<li>古典ビットはトランジスタの ON/OFF で実現され、数十億電子の差による高いノイズ耐性を持つが、量子ビットにはそのような余裕がない</li>
<li>現在・将来の量子ビット技術に基づくすべての回路型量子コンピュータには<strong>能動的な誤り訂正</strong>が不可欠</li>
</ul>
<h3>量子ビットとは</h3>
<p>一般的な量子ビット状態：</p>
<p>$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$$</p>
<ul>
<li>$\alpha, \beta$：複素振幅、$|\alpha|^2 + |\beta|^2 = 1$ を満たす</li>
<li>$|\alpha|^2$：$|0\rangle$ を測定する確率、$|\beta|^2$：$|1\rangle$ を測定する確率</li>
<li>量子ビットは <strong>$2^n$ 次元計算空間</strong>を利用できる（古典は $n$ 次元）</li>
</ul>
<p>ブロッホ球表現：</p>
<p>$$|\psi\rangle = \cos\frac{\theta}{2}|0\rangle + e^{i\phi}\sin\frac{\theta}{2}|1\rangle$$</p>
<ul>
<li>$\theta, \phi$ でブロッホ球表面の1点を指定</li>
<li>量子エラー = ブロッホ球上の点が連続的にずれる現象</li>
</ul>
<h3>量子エラーのデジタル化（最重要）</h3>
<p>連続的な量子エラーは、パウリ行列の基底に展開できる：</p>
<p>$$U(\delta\theta, \delta\phi)|\psi\rangle = \alpha_I|\psi\rangle + \alpha_X X|\psi\rangle + \alpha_Z Z|\psi\rangle + \alpha_{XZ} XZ|\psi\rangle$$</p>
<ul>
<li>$X, Y, Z$：パウリ行列（量子ビット操作の基本）</li>
<li>$\alpha_{I,X,Z,XZ}$：展開係数</li>
</ul>
<p><strong>重要な結論</strong>：シンドローム測定（後述）を行うと、この重ね合わせが $\{I, X, Z, XZ\}$ のどれかに収縮する。つまり<strong>有限個のエラーを訂正できれば、任意の連続エラーを訂正できる</strong>。</p>
<p>パウリ行列：</p>
<p>$$X = \begin{pmatrix}0&1\\1&0\end{pmatrix}, \quad Y = \begin{pmatrix}0&-i\\i&0\end{pmatrix}, \quad Z = \begin{pmatrix}1&0\\0&-1\end{pmatrix}$$</p>
<blockquote>
<p>📊 Fig. 1 参照（原論文）— ブロッホ球上の量子状態表現</p>
</blockquote>
<h3>2種類の量子エラー</h3>
<table>
<thead>
<tr>
<th>エラー</th>
<th>演算子</th>
<th>作用</th>
</tr>
</thead>
<tbody>
<tr>
<td>ビット反転（X エラー）</td>
<td>$X$</td>
<td>$X|0\rangle=|1\rangle$, $X|1\rangle=|0\rangle$</td>
</tr>
<tr>
<td>位相反転（Z エラー）</td>
<td>$Z$</td>
<td>$Z|0\rangle=|0\rangle$, $Z|1\rangle=-|1\rangle$</td>
</tr>
<tr>
<td>両方（Y エラー）</td>
<td>$Y = iXZ$</td>
<td>ビット反転＋位相反転</td>
</tr>
</tbody>
</table>
<ul>
<li>X エラー（ビット反転）：古典の誤りに相当</li>
<li>Z エラー（位相反転）：<strong>古典には類似物がない量子固有のエラー</strong></li>
<li>位相反転は共役基底 $\{|+\rangle, |-\rangle\}$ で「ビット反転」として現れる</li>
</ul>
<h3>量子誤り訂正の3つの困難</h3>
<ol>
<li><strong>複製禁止定理</strong>：未知の量子状態をコピーできない → 古典の繰り返し符号と同じ方法は使えない</li>
<li><strong>波動関数の収縮</strong>：量子ビットを直接測定すると情報が失われる → 間接測定（スタビライザー測定）が必要</li>
<li><strong>X/Z 両方のエラー</strong>：古典ではビット反転だけだが、量子では位相反転も扱わなければならない</li>
</ol>
<hr />

</details>

### 第2章: 量子冗長性とスタビライザー測定

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子冗長性とスタビライザー測定</h2>
<h3>2量子ビット符号：コードスペースとエラースペース</h3>
<p>エンコード操作：</p>
<p>$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle \xrightarrow{\text{encoder}} |\psi\rangle_L = \alpha|00\rangle + \beta|11\rangle$$</p>
<ul>
<li>これは<strong>複製ではない</strong>（$\alpha|00\rangle + \beta|11\rangle \neq |\psi\rangle \otimes |\psi\rangle$）</li>
<li>情報を「エンタングルした2量子ビット状態」に分散してエンコード</li>
<li>コードスペース：$\mathcal{C} = \text{span}\{|00\rangle, |11\rangle\} \subset \mathcal{H}_4$</li>
</ul>
<p>X エラーが発生した場合：</p>
<p>$$X_1|\psi\rangle_L = \alpha|10\rangle + \beta|01\rangle \in \mathcal{F}$$</p>
<ul>
<li>$\mathcal{C}$（コードスペース）と $\mathcal{F}$（エラースペース）は直交</li>
<li>直接測定せずに「どちらにいるか」を判定 → スタビライザー測定</li>
</ul>
<p><strong>スタビライザー $Z_1Z_2$ の測定</strong>：</p>
<p>$$Z_1Z_2|\psi\rangle_L = (+1)|\psi\rangle_L \quad \text{（コードスペース：シンドローム 0）}$$
$$Z_1Z_2 \cdot X_1|\psi\rangle_L = (-1) \cdot X_1|\psi\rangle_L \quad \text{（エラースペース：シンドローム 1）}$$</p>
<blockquote>
<p>📊 Fig. 2 参照（原論文）— 2量子ビット符号の回路図（エンコード・エラー・シンドローム抽出）</p>
</blockquote>
<h3>論理エラー率の抑制</h3>
<p>2量子ビット符号での論理エラー率（シンドローム測定後）：</p>
<p>$$p_L = \frac{p_x^2}{(1-p_x)^2 + p_x^2} \approx p_x^2$$</p>
<ul>
<li>物理エラー率 $p_x$ に対して、論理エラー率は $p_x^2$（2次で抑制）</li>
<li>これが<strong>量子誤り訂正が機能する証明</strong></li>
</ul>
<h3>3量子ビット符号：誤り訂正へ</h3>
<p>2量子ビット符号は<strong>検出</strong>はできるが<strong>どちらの量子ビットが壊れたかは分からない</strong>。訂正のために3量子ビット符号を使う。</p>
<p>論理状態：</p>
<p>$$|\psi\rangle_L = \alpha|000\rangle + \beta|111\rangle$$</p>
<p>8次元ヒルベルト空間を4つの2次元部分空間に分割：</p>
<p>$$\mathcal{C} = \text{span}\{|000\rangle, |111\rangle\}, \quad \mathcal{F}_1 = \text{span}\{|100\rangle, |011\rangle\}, \quad \mathcal{F}_2 = \text{span}\{|010\rangle, |101\rangle\}, \quad \mathcal{F}_3 = \text{span}\{|001\rangle, |110\rangle\}$$</p>
<p>2つのスタビライザー $Z_1Z_2$ と $Z_2Z_3$ を測定して2ビットシンドローム $S = s_1s_2$ を得る：</p>
<table>
<thead>
<tr>
<th>エラー</th>
<th>シンドローム $S$</th>
</tr>
</thead>
<tbody>
<tr>
<td>エラーなし</td>
<td>00</td>
</tr>
<tr>
<td>$X_1$</td>
<td>10</td>
</tr>
<tr>
<td>$X_2$</td>
<td>11</td>
</tr>
<tr>
<td>$X_3$</td>
<td>01</td>
</tr>
</tbody>
</table>
<blockquote>
<p>📊 Fig. 3 参照（原論文）— 3量子ビット符号の回路図</p>
</blockquote>
<h3>符号距離</h3>
<p><strong>符号距離の定義</strong>：一つの符号語を別の符号語に変える最小エラーのサイズ</p>
<p>$$d = 2t + 1$$</p>
<ul>
<li>$t$：訂正できるエラー数</li>
<li>3量子ビット符号では $\bar{X} = X_1X_2X_3$（3つのXエラーで論理エラー）→ Xエラーに対して $d=3$</li>
</ul>
<p><strong>重要な問題点</strong>：3量子ビット符号はXエラー（ビット反転）しか訂正できない！</p>
<ul>
<li>論理Z演算子 $\bar{Z} = Z_1$（1つのZエラーで論理エラー）→ Zエラーに対して $d=1$</li>
<li>つまり3量子ビット符号の量子符号距離は $d=1$</li>
</ul>
<hr />

</details>

### 第3章: スタビライザー符号の一般理論とショア符号

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>スタビライザー符号の一般理論とショア符号</h2>
<h3>[[n,k,d]] スタビライザー符号の一般構造</h3>
<blockquote>
<p>📊 Fig. 4 参照（原論文）— [[n,k,d]] 符号の回路構造</p>
</blockquote>
<p>$n$ 個の物理量子ビットで $k$ 個の論理量子ビットを符号距離 $d$ で守る：</p>
<ul>
<li>$k$ データ量子ビット $|\psi\rangle_D$ を $(n-k)$ 冗長量子ビット $|0\rangle_R$ とエンタングル</li>
<li>$m = n-k$ 個のスタビライザー測定 $P_i$ を実行 → $m$ ビットシンドローム</li>
<li>古典符号との区別：量子符号はダブルブラケット $[[n,k,d]]$（古典は $[n,k,d]$）</li>
</ul>
<h3>スタビライザーの代数的性質</h3>
<p>スタビライザー群 $\mathcal{S}$：
- $m$ 個の<strong>互いに可換なパウリ演算子</strong> $P_i$ で生成される群
- 符号空間 $\mathcal{C}$：全 $P_i$ の固有値 $+1$ の共通固有空間
- $n$ 量子ビットのパウリ群 $\mathcal{P}_n = \{I,X,Y,Z\}^{\otimes n}$ から選ぶ</p>
<h3>論理演算子</h3>
<p>$[[n,k,d]]$ 符号の論理 $\bar{X}$ と $\bar{Z}$ 演算子の条件：
- すべてのスタビライザーと<strong>可換</strong>（符号空間を保存）
- 論理 $\bar{X}$ と $\bar{Z}$ は<strong>互いに反可換</strong>（$\bar{X}\bar{Z} = -\bar{Z}\bar{X}$）
- スタビライザーそのものでない（自明でない論理演算）</p>
<p>符号距離 $d$ = 論理演算子の最小重み（非恒等要素の数）</p>
<h3>例：[[4,2,2]] 検出符号</h3>
<blockquote>
<p>📊 Fig. 5 参照（原論文）— [[4,2,2]] 符号の回路図</p>
</blockquote>
<p>4量子ビットで2論理量子ビットを符号距離2で守る<strong>最小の量子検出符号</strong>：</p>
<p>$$\mathcal{S}_{[[4,2,2]]} = \langle XXXX, ZZZZ \rangle$$</p>
<ul>
<li>$XXXX$ と $ZZZZ$：各2演算子が符号を定義</li>
<li>1エラーは検出可能（$d=2$）だが訂正不能</li>
<li>量子ビット数に対して最も効率的な量子符号の一つ</li>
</ul>
<h3>汎用エンコード回路</h3>
<p>一般的なスタビライザー符号のエンコード回路（Section 4.4）：
- データ量子ビットにアダマールゲートを適用して重ね合わせを作る
- CNOTゲートで冗長量子ビットとエンタングルする
- スタビライザー測定のアンシラ量子ビットを用意する</p>
<h3>量子誤り訂正の手順</h3>
<ol>
<li>スタビライザー測定でシンドローム $S$ を取得</li>
<li>訂正操作 $\mathcal{R}$ を選択（ルックアップテーブルまたはデコーダー）</li>
<li>$\mathcal{R} \cdot E|\psi\rangle_L = |\psi\rangle_L$ となれば成功</li>
<li>$\mathcal{R} \cdot E = L$（論理演算子）になると<strong>論理エラー</strong>（失敗）</li>
</ol>
<h3>例：ショア [[9,1,3]] 符号</h3>
<p><strong>符号連接（Code Concatenation）</strong>：小さい符号を入れ子にして大きい符号を作る手法</p>
<p>ビット反転3量子ビット符号 $\mathcal{C}_{3b}$：</p>
<p>$$|0\rangle_{3b} = |000\rangle, \quad |1\rangle_{3b} = |111\rangle, \quad \mathcal{S}_{3b} = \langle Z_1Z_2, Z_2Z_3 \rangle$$</p>
<p>位相反転3量子ビット符号 $\mathcal{C}_{3p}$：</p>
<p>$$|0\rangle_{3p} = |{+}{+}{+}\rangle, \quad |1\rangle_{3p} = |{-}{-}{-}\rangle, \quad \mathcal{S}_{3p} = \langle X_1X_2, X_2X_3 \rangle$$</p>
<p>連接で9量子ビット符号を構成（$|+\rangle_{3b} = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)$）：</p>
<p>$$|0\rangle_9 = |{+}\rangle_{3b}|{+}\rangle_{3b}|{+}\rangle_{3b}, \quad |1\rangle_9 = |{-}\rangle_{3b}|{-}\rangle_{3b}|{-}\rangle_{3b}$$</p>
<p>スタビライザー群（8個）：</p>
<p>$$\mathcal{S}_{[[9,1,3]]} = \langle Z_1Z_2, Z_2Z_3, Z_4Z_5, Z_5Z_6, Z_7Z_8, Z_8Z_9, X_1X_2X_3X_4X_5X_6, X_4X_5X_6X_7X_8X_9 \rangle$$</p>
<ul>
<li>最初の6項：ビット反転符号のスタビライザー</li>
<li>最後の2項：位相反転符号のスタビライザー</li>
<li><strong>縮退符号（degenerate code）</strong>：$Z_1$ と $Z_2$ は同じシンドロームを持つが、どちらの回復操作でも論理エラーを防げる</li>
</ul>
<hr />

</details>

### 第4章: 表面符号──四サイクルから格子へ

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>表面符号──四サイクルから格子へ</h2>
<h3>表面符号の基本構成要素：四サイクル</h3>
<blockquote>
<p>📊 Fig. 7 参照（原論文）— 表面符号の四サイクル（絵表示と回路表示）</p>
</blockquote>
<p><strong>四サイクル</strong>：表面符号の基本構成要素</p>
<ul>
<li>データ量子ビット $D_1, D_2$（円）とアンシラ量子ビット $A_1, A_2$（四角）</li>
<li>赤エッジ：アンシラ制御のCXゲート → $X_{D_1}X_{D_2}$ スタビライザーを測定</li>
<li>青エッジ：アンシラ制御のCZゲート → $Z_{D_1}Z_{D_2}$ スタビライザーを測定</li>
<li>$X_{D_1}X_{D_2}$ と $Z_{D_1}Z_{D_2}$ は<strong>可換</strong>（偶数個の量子ビットで非自明に交わる）</li>
<li>四サイクル単体では $n=2, m=2, k=n-m=0$：<strong>論理量子ビットを符号化しない</strong>（タイル状に並べる前提）</li>
</ul>
<p><strong>表面符号の最大の利点</strong>：<strong>最近接相互作用のみ</strong>を使う → 現行の量子ハードウェアに実装しやすい</p>
<h3>[[5,1,2]] 表面符号</h3>
<p>4つの四サイクルを正方格子状に並べると [[5,1,2]] 表面符号が構成される：</p>
<blockquote>
<p>📊 Fig. 8 参照（原論文）— [[5,1,2]] 表面符号の格子とエラー検出の例</p>
</blockquote>
<p>スタビライザー群：</p>
<p>$$\mathcal{S}_{[[5,1,2]]} = \langle X_{D_1}X_{D_2}X_{D_3},\ Z_{D_1}Z_{D_3}Z_{D_4},\ Z_{D_2}Z_{D_3}Z_{D_5},\ X_{D_3}X_{D_4}X_{D_5} \rangle$$</p>
<ul>
<li>5データ量子ビット、4スタビライザー → $k = 5-4 = 1$ 論理量子ビット</li>
</ul>
<p>エラー検出の例：
- $Z_{D_1}$ エラー → $X_{D_1}X_{D_2}X_{D_3}$ スタビライザーと反可換 → アンシラ $A_1$ が「1」（赤く点灯）
- $X_{D_5}$ エラー → $Z_{D_2}Z_{D_3}Z_{D_5}$ スタビライザーと反可換 → アンシラ $A_3$ が「1」</p>
<h3>[[5,1,2]] 表面符号の論理演算子</h3>
<blockquote>
<p>📊 Fig. 9 参照（原論文）— 表面符号の論理演算子（境界チェーン）</p>
</blockquote>
<p>論理演算子は格子の境界に沿ったパウリ演算子のチェーン：</p>
<p>$$\bar{X} = X_{D_1}X_{D_4}, \quad \bar{Z} = Z_{D_1}Z_{D_2}$$</p>
<ul>
<li>$\bar{X}$ は Z スタビライザーが測定される境界（左辺）に沿う</li>
<li>$\bar{Z}$ は X スタビライザーが測定される境界（上辺）に沿う</li>
<li>$\bar{X}$ と $\bar{Z}$ は<strong>反可換</strong>（1量子ビットで非自明に交わる）</li>
<li>論理演算子の最小重みが 2 → $d=2$（検出符号）</li>
</ul>
<h3>表面符号のスケーリング</h3>
<p>格子サイズを増やすだけで符号距離を上げられる：</p>
<p>$$[[n = \lambda^2 + (\lambda-1)^2,\ k=1,\ d=\lambda]]$$</p>
<p>距離3の例：[[13,1,3]] 表面符号</p>
<blockquote>
<p>📊 Fig. 10 参照（原論文）— 距離3の [[13,1,3]] 表面符号</p>
</blockquote>
<p>$$\bar{X} = X_{D_1}X_{D_6}X_{D_{11}}, \quad \bar{Z} = Z_{D_1}Z_{D_2}Z_{D_3}$$</p>
<table>
<thead>
<tr>
<th>符号距離 $d$</th>
<th>物理量子ビット数 $n$</th>
</tr>
</thead>
<tbody>
<tr>
<td>2</td>
<td>$4+1=5$</td>
</tr>
<tr>
<td>3</td>
<td>$9+4=13$</td>
</tr>
<tr>
<td>5</td>
<td>$25+16=41$</td>
</tr>
<tr>
<td>7</td>
<td>$49+36=85$</td>
</tr>
</tbody>
</table>
<p><strong>[[13,1,3]] は誤りの検出と訂正の両方ができる最小の表面符号</strong></p>
<hr />

</details>

### 第5章: 実装の課題──復号・閾値・フォルトトレラント計算

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>実装の課題──復号・閾値・フォルトトレラント計算</h2>
<h3>効率的な復号アルゴリズム</h3>
<p>$[[n,k,d]]$ 符号のシンドロームは $m = n-k$ ビット → $2^m$ 通りの可能なシンドローム</p>
<p><strong>問題</strong>：ルックアップテーブルはコードが大きくなると指数的に増大
- 距離5表面符号 $[[41,1,5]]$：$2^{40} \approx 10^{12}$ 通り → 実用不可能</p>
<p><strong>解決策</strong>：近似推論アルゴリズムによるリアルタイム復号</p>
<p><strong>表面符号向け：最小重みパーフェクトマッチング（MWPM）デコーダー</strong>
- 正のシンドローム測定（アニオン）の間のエラーチェーンを特定
- すべてのアニオンをペアにして、最短距離でマッチング
- ブロッサムアルゴリズム（多項式時間）で効率的に解ける
- 訂正失敗条件：$\mathcal{R} \cdot E = L$（訂正操作がエラーと組み合わさって論理演算子になる）</p>
<h3>閾値定理</h3>
<p><strong>閾値定理</strong>：物理エラー率 $p$ が閾値 $p_{th}$ を下回れば、符号サイズを増やすことで論理エラー率を指数的に下げられる</p>
<table>
<thead>
<tr>
<th>状況</th>
<th>表面符号の閾値</th>
</tr>
</thead>
<tbody>
<tr>
<td>理想的なアンシラ測定</td>
<td>$\approx 10.9\%$（統計力学的上界）</td>
</tr>
<tr>
<td>MWPM デコーダー</td>
<td>$\approx 10.3\%$</td>
</tr>
<tr>
<td>雑音のあるアンシラ測定</td>
<td>$\approx 1\%$</td>
</tr>
</tbody>
</table>
<ul>
<li>Google Willow・IBM Heron など最先端の量子ビットのエラー率はすでに $\sim 0.1\%$ → 物理エラー率はすでに閾値を下回る</li>
<li>しかし論理エラー率を実用水準に下げるには「論理量子ビット vs 非符号化量子ビット」のブレーク・イーブンポイントを超える大規模スケーリングが必要</li>
</ul>
<h3>フォルトトレラント性（耐障害性）</h3>
<p><strong>問題</strong>：シンドローム測定回路自体にもエラーが入る（2量子ビットゲートや測定操作は主要なエラー源）</p>
<p><strong>フォルトトレラント設計の原則</strong>：サブ距離エラーが回路中で制御不能に増幅されないこと</p>
<p>Shor の耐障害性シンドローム抽出法：
- 各スタビライザーを測定するのに $\lambda$ 個のアンシラ量子ビットを使用（$\lambda$ = スタビライザーの非恒等要素数）
- 測定エラーを区別するために<strong>複数ラウンドのシンドローム測定が必要</strong>
- 雑音のあるアンシラでは閾値が $\approx 10\%$ から $\approx 1\%$ に低下する原因</p>
<h3>符号化された計算（エンコードされた論理ゲート）</h3>
<p>万能量子コンピュータに必要な万能ゲートセット：</p>
<p>$$\langle\mathcal{U}\rangle = \langle X, Z, Y, H, \text{CNOT}, T \rangle, \quad T = \text{diag}(1, e^{i\pi/4})$$</p>
<p><strong>トランスバーサルゲート</strong>：各物理量子ビットに独立に同じゲートを適用する耐障害的な実装法
- 多くの符号でCliffordゲート（$X, Z, H, \text{CNOT}$）をトランスバーサルに実装可能
- しかし<strong>ノーゴー定理</strong>：万能ゲートセット全体をトランスバーサルに実装することは不可能</p>
<p><strong>Tゲートの問題</strong>：TゲートはCliffordゲートでなく、トランスバーサル実装できない</p>
<p><strong>解決策：マジック状態注入（Magic State Injection）</strong></p>
<p>$$|T\rangle = \frac{|0\rangle + e^{i\pi/4}|1\rangle}{\sqrt{2}}$$</p>
<ul>
<li>低品質な $|T\rangle$ 状態を多数用意し、蒸留プロトコルで高品質に精製</li>
<li>推定コスト：万能フォルトトレラント量子コンピュータの<strong>総量子ビットが1桁増加</strong>する可能性</li>
</ul>
<h3>実験的実装の現状と展望</h3>
<p>現在の取り組み（2019年時点、その後急速に進展）：
- Google・IBM Research・TU Delft：超伝導量子ビットで表面符号論理量子ビットの実現を目標
- イオントラップ・量子光学の取り組みも並行</p>
<p>現実的な課題（論文の見積もり）：
- 最初のフォルトトレラント表面符号論理量子ビット：<strong>1,000以上の量子ビットが必要</strong>
- 古典計算機に勝てる実用的タスク：<strong>100万以上の量子ビットが必要</strong>
- 当時（2019年）の最大量子コンピュータは100量子ビット未満</p>
<p><strong>表面符号の欠点と代替案</strong>：
- 符号レート $R = k/n \to 0$（量子ビット数増加に対して論理量子ビット数が増えない）
- Tゲートに資源集約的な手法が必要
- 代替：高次元トポロジカル符号・LDPC符号（非消滅レート、長距離相互作用が必要）</p>
<h3>まとめ</h3>
<p><strong>量子誤り訂正の全体像</strong>：</p>
<table>
<thead>
<tr>
<th>要素</th>
<th>内容</th>
</tr>
</thead>
<tbody>
<tr>
<td>問題</td>
<td>量子デコヒーレンス・ビット反転・位相反転</td>
</tr>
<tr>
<td>解決原理</td>
<td>エンタングルメントによる冗長エンコード＋シンドローム測定</td>
</tr>
<tr>
<td>最有力候補</td>
<td>表面符号（最近接相互作用・高閾値・スケーラブル）</td>
</tr>
<tr>
<td>実装の鍵</td>
<td>MWPM復号・フォルトトレラント回路・マジック状態蒸留</td>
</tr>
<tr>
<td>残された課題</td>
<td>百万量子ビット規模でのスケーリング</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第6章: 付録──記法の手引き（ブラケット・パウリ群・回路・可換性）

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch06.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch06.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>付録──記法の手引き（ブラケット・パウリ群・回路・可換性）</h2>
<h3>付録A：量子状態の記法（Dirac ブラケット）</h3>
<p>一般的な量子ビット状態（式48）：</p>
<p>$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$$</p>
<ul>
<li>$\alpha, \beta$：複素振幅、$|\alpha|^2 + |\beta|^2 = 1$</li>
<li>計算基底：$\{|0\rangle, |1\rangle\}$（ブロッホ球の北極・南極）</li>
<li>$|\phi\rangle$：ケット（ベクトル）、$\langle\phi|$：ブラ（双対ベクトル）</li>
<li>内積 $\langle\phi|\psi\rangle$ → 「ブラケット」が名前の由来</li>
</ul>
<p>多量子ビット表記の規則：量子ビットを左から右へ $1, 2, \ldots, n$ と番号づけ</p>
<p>$$|010\rangle = |0\rangle_1 \otimes |1\rangle_2 \otimes |0\rangle_3$$</p>
<ul>
<li>$\otimes$：テンソル積（複数量子系を合わせた空間を作る）</li>
<li>省略表記 $|010\rangle$ を使うことで複数量子ビット状態を簡潔に表現</li>
</ul>
<h3>付録B：パウリ演算子の記法</h3>
<p>1量子ビットパウリ群 $\mathcal{G}_1$（式49）：</p>
<p>$$\mathcal{G}_1 = \{\pm I, \pm iI, \pm X, \pm iX, \pm Y, \pm iY, \pm Z, \pm iZ\}$$</p>
<ul>
<li>$\pm 1, \pm i$ の係数を含めることで乗算に閉じた群となる
  （例：$XY = iZ$ → $iZ$ も群に含まれる必要がある）</li>
</ul>
<p>4つのパウリ演算子の行列形（式50）：</p>
<p>$$I = \begin{pmatrix}1&0\\0&1\end{pmatrix},\quad X = \begin{pmatrix}0&1\\1&0\end{pmatrix},\quad Y = \begin{pmatrix}0&-i\\i&0\end{pmatrix},\quad Z = \begin{pmatrix}1&0\\0&-1\end{pmatrix}$$</p>
<p>一般パウリ群 $\mathcal{G}$ の例（式51）：</p>
<p>$$I \otimes X \otimes I \otimes Y \in \mathcal{G} \quad \text{（4量子ビットパウリ群の要素）}$$</p>
<p><strong>サポート（support）</strong>：パウリ演算子の恒等でない要素の番号リスト</p>
<p>$$\text{supp}(I \otimes X \otimes I \otimes Y) = X_2 Y_4$$</p>
<ul>
<li>サポートが重なる量子ビットで可換性が決まる（付録D参照）</li>
</ul>
<h3>付録C：量子回路記法</h3>
<p><strong>C.1 1量子ビットゲート</strong>
- 各量子ビットに水平なワイヤーを割り当てる
- ゲートを左から右の順に並べる（時間は左→右）
- 注意：数式は右→左の順（$X_1Z_1|\psi\rangle$ はまず $Z_1$ が作用）</p>
<p><strong>C.2 多量子ビットゲート</strong>
- 複数のワイヤーをまたぐゲートボックスが複数量子ビット演算を示す</p>
<p><strong>C.3 制御ゲート（Controlled gates）</strong>
- 制御量子ビット（●）の値が $|1\rangle$ の時のみターゲットにゲートを作用
- CX（CNOT）：制御付き $X$ ゲート、CZ：制御付き $Z$ ゲート
- 表面符号のシンドローム抽出回路で多用（アンシラが制御、データがターゲット）</p>
<p><strong>C.4 計算基底での測定</strong>
- 全回路で計算基底 $\{|0\rangle, |1\rangle\}$ で測定
- 量子乱数生成（量子コンピュータの Hello World）：
  $$|0\rangle \xrightarrow{H} \frac{|0\rangle + |1\rangle}{\sqrt{2}} \xrightarrow{\text{測定}} \begin{cases}0 & 50\%\\1 & 50\%\end{cases}$$</p>
<h3>付録D：パウリ演算子の可換性</h3>
<p><strong>定義</strong>：$F_i F_j = F_j F_i$ なら可換、$F_i F_j = -F_j F_i$ なら反可換</p>
<p>1量子ビットパウリ演算子の性質（式55）：異なるパウリは<strong>すべて反可換</strong></p>
<p>$$X_1Z_1 = -Z_1X_1,\quad X_1Y_1 = -Y_1X_1,\quad Z_1Y_1 = -Y_1Z_1$$</p>
<p>多量子ビットの例（式56）：$Z_1Z_2$ と $X_1X_2$</p>
<p>$$Z_1Z_2 \cdot X_1X_2 = Z_1X_1 \cdot Z_2X_2 = (-1)X_1Z_1 \cdot (-1)X_2Z_2 = X_1X_2 \cdot Z_1Z_2$$</p>
<p>各量子ビットで反可換（$\times(-1)$）が2回→ $(-1)^2=+1$ → <strong>可換</strong></p>
<p><strong>一般規則</strong>（付録Dの核心）：</p>
<table>
<thead>
<tr>
<th>非自明な交わりの数</th>
<th>可換性</th>
</tr>
</thead>
<tbody>
<tr>
<td>偶数</td>
<td><strong>可換</strong></td>
</tr>
<tr>
<td>奇数</td>
<td><strong>反可換</strong></td>
</tr>
</tbody>
</table>
<ul>
<li><strong>非自明な交わり</strong>：両演算子がサポートを持つ量子ビットで、異なるパウリ（反可換の組み合わせ）を持つ場合</li>
</ul>
<p><strong>例</strong>：$X_1Z_2Z_3Z_5X_7$ と $X_1X_2X_5Z_7$</p>
<table>
<thead>
<tr>
<th>量子ビット</th>
<th>演算子1</th>
<th>演算子2</th>
<th>交わり</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>X</td>
<td>X</td>
<td>自明（可換）</td>
</tr>
<tr>
<td>2</td>
<td>Z</td>
<td>X</td>
<td><strong>非自明</strong></td>
</tr>
<tr>
<td>5</td>
<td>Z</td>
<td>X</td>
<td><strong>非自明</strong></td>
</tr>
<tr>
<td>7</td>
<td>X</td>
<td>Z</td>
<td><strong>非自明</strong></td>
</tr>
</tbody>
</table>
<p>非自明な交わり = 3（奇数）→ <strong>反可換</strong></p>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
