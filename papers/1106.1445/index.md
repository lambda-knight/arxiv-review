---
title: "From Classical to Quantum Shannon Theory — Part II 解説"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

- arXiv: [1106.1445](https://arxiv.org/abs/1106.1445)
- Internet Archive: [paper-explain-1106-1445](https://archive.org/details/paper-explain-1106-1445)

---

## 概要

量子コンピュータ・量子通信の数学的な土台を全4章+付録で完全解説。Mark Wildeの「From Classical to Quantum Shannon Theory」Part IIをベースに、ずんだもん＆四国めたんが量子状態・密度行列・測定・量子チャネルを数式とともに丁寧に説明します。

▼ 章別動画ラインナップ
・量子状態とヒルベルト空間 — 純粋状態・ディラック記法・テンソル積・量子もつれ
・密度行列と混合状態 — 密度演算子の3条件・部分トレース・純粋化定理・ブロッホ球
・量子測定：射影測定とPOVM — フォン・ノイマン測定・POVM・ナイマルクの拡張定理
・量子チャネルとクラウス表現 — CPTP写像・クラウス定理・スタインスプリング拡張・チョイ行列
・Appendix A: 線形代数の基礎 — 内積・スペクトル定理・トレース・テンソル積・シュミット分解

▼ 参考文献
https://arxiv.org/abs/1106.1445  — Mark M. Wilde, "From Classical to Quantum Shannon Theory" (arXiv, 2nd ed.)

#量子コンピュータ #量子情報 #密度行列 #POVM #量子チャネル #量子力学 #論文解説 #ゆっくり解説 #ずんだもん #線形代数 #数式でわかる #テクノロジー #大学院

---

## 章別動画・解説

### 第1章: 量子状態とヒルベルト空間

<video controls width="100%" src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子状態とヒルベルト空間</h2>
<h3>複素ヒルベルト空間</h3>
<p>量子力学の舞台は <strong>複素ヒルベルト空間</strong> $\mathcal{H}$。</p>
<p>$$\mathcal{H} = \mathbb{C}^d, \quad d = 2^n \text{（n量子ビット）}$$</p>
<p><strong>ディラック記法（ブラケット記法）:</strong>
- ケット: $|\psi\rangle \in \mathcal{H}$（列ベクトル）
- ブラ: $\langle\psi| = |\psi\rangle^\dagger$（行ベクトル＝エルミート転置）
- 内積: $\langle\phi|\psi\rangle \in \mathbb{C}$</p>
<h3>純粋状態</h3>
<p>規格化された状態ベクトル $|\psi\rangle$ で表される状態を<strong>純粋状態</strong>という。</p>
<p>$$\langle\psi|\psi\rangle = 1$$</p>
<p><strong>量子ビット（qubit）の例:</strong></p>
<p>$$|\psi\rangle = \alpha|0\rangle + \beta|1\rangle, \quad |\alpha|^2 + |\beta|^2 = 1$$</p>
<ul>
<li>$|0\rangle = \begin{pmatrix}1\\0\end{pmatrix}$, $|1\rangle = \begin{pmatrix}0\\1\end{pmatrix}$（計算基底）</li>
<li>$\alpha, \beta \in \mathbb{C}$: 複素確率振幅</li>
<li>$|\alpha|^2$: 0を測定する確率、$|\beta|^2$: 1を測定する確率</li>
</ul>
<p><strong>ブロッホ球（Bloch sphere）:</strong></p>
<p>$$|\psi\rangle = \cos\frac{\theta}{2}|0\rangle + e^{i\varphi}\sin\frac{\theta}{2}|1\rangle$$</p>
<blockquote>
<p>📊 Fig. 3.1 参照（原論文）: ブロッホ球上の点として純粋な量子ビット状態を表す</p>
</blockquote>
<ul>
<li>$\theta \in [0, \pi]$: 極角（北極 = $|0\rangle$、南極 = $|1\rangle$）</li>
<li>$\varphi \in [0, 2\pi)$: 方位角</li>
</ul>
<h3>複合系とテンソル積</h3>
<p>2つの量子系 A, B の複合系は<strong>テンソル積</strong>空間 $\mathcal{H}_A \otimes \mathcal{H}_B$:</p>
<p>$$|\psi\rangle_{AB} \in \mathcal{H}_A \otimes \mathcal{H}_B, \quad \dim(\mathcal{H}_A \otimes \mathcal{H}_B) = d_A \cdot d_B$$</p>
<p><strong>積状態（product state）:</strong> $|\psi\rangle_{AB} = |\phi\rangle_A \otimes |\chi\rangle_B$</p>
<p><strong>もつれ状態（entangled state）:</strong> 積状態に書けない状態。例としてベル状態:</p>
<p>$$|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$$</p>
<p>$|\Phi^+\rangle$ は $|\phi\rangle_A \otimes |\chi\rangle_B$ の形に書けない。</p>
<hr />

</details>

### 第2章: 密度行列と混合状態

<video controls width="100%" src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>密度行列と混合状態</h2>
<h3>密度演算子の定義</h3>
<p><strong>密度演算子</strong>（密度行列）$\rho$ は量子状態をより一般的に表す道具:</p>
<p>$$\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$$</p>
<ul>
<li>$p_i \geq 0$: 確率（$\sum_i p_i = 1$）</li>
<li>$|\psi_i\rangle$: 純粋状態</li>
</ul>
<p><strong>純粋状態の場合:</strong> $\rho = |\psi\rangle\langle\psi|$（射影演算子）</p>
<h3>密度演算子の3条件</h3>
<p>$\rho$ が物理的な量子状態 ⟺ 以下の3条件:</p>
<p>$$\rho^\dagger = \rho \quad\text{（エルミート性）}$$
$$\rho \geq 0 \quad\text{（半正定値性: すべての固有値} \geq 0\text{）}$$
$$\text{Tr}(\rho) = 1 \quad\text{（トレース規格化）}$$</p>
<h3>純粋状態と混合状態の判別</h3>
<p><strong>純粋度（purity）:</strong>
$$P(\rho) = \text{Tr}(\rho^2), \quad \frac{1}{d} \leq P(\rho) \leq 1$$</p>
<ul>
<li>$P(\rho) = 1$ ⟺ 純粋状態（$\rho = |\psi\rangle\langle\psi|$）</li>
<li>$P(\rho) < 1$ ⟺ 混合状態</li>
</ul>
<p><strong>量子ビットの密度行列（ブロッホ球表示）:</strong></p>
<p>$$\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma}), \quad |\vec{r}| \leq 1$$</p>
<ul>
<li>$\vec{r} = (r_x, r_y, r_z)$: ブロッホベクトル</li>
<li>$\vec{\sigma} = (X, Y, Z)$: パウリ行列</li>
<li>$|\vec{r}| = 1$: 純粋状態、$|\vec{r}| < 1$: 混合状態、$\vec{r} = 0$: 最大混合状態 $I/2$</li>
</ul>
<blockquote>
<p>📊 Fig. 4.2 参照（原論文）: ブロッホ球の内部が混合状態、球面が純粋状態</p>
</blockquote>
<h3>部分トレース（Partial Trace）</h3>
<p>複合系 AB から一方の系 B を「忘れる」操作:</p>
<p>$$\rho_A = \text{Tr}_B(\rho_{AB}) = \sum_j \langle j|_B \rho_{AB} |j\rangle_B$$</p>
<ul>
<li>$\{|j\rangle_B\}$: B の正規直交基底</li>
<li>$\rho_A$: A の<strong>周辺状態（marginal state）</strong></li>
</ul>
<p><strong>もつれ状態に部分トレースを取ると混合状態が生まれる:</strong></p>
<p>$$\rho_{AB} = |\Phi^+\rangle\langle\Phi^+|, \quad \rho_A = \text{Tr}_B(\rho_{AB}) = \frac{I}{2} \quad\text{（最大混合状態）}$$</p>
<h3>純粋化定理（Purification Theorem）</h3>
<p>任意の混合状態 $\rho_A$ に対し、補助系 B を追加すると純粋状態 $|\psi\rangle_{AB}$ が存在する:</p>
<p>$$\rho_A = \text{Tr}_B(|\psi\rangle\langle\psi|_{AB})$$</p>
<p><strong>スペクトル分解を使った構成:</strong> $\rho_A = \sum_i \lambda_i |i\rangle_A\langle i|_A$ から:</p>
<p>$$|\psi\rangle_{AB} = \sum_i \sqrt{\lambda_i} |i\rangle_A |i\rangle_B$$</p>
<p>純粋化はユニーク（補助系 B のユニタリ変換の自由度を除く）。</p>
<hr />

</details>

### 第3章: 量子測定：射影測定とPOVM

<video controls width="100%" src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子測定：射影測定とPOVM</h2>
<h3>射影測定</h3>
<p><strong>射影測定（Projective Measurement / von Neumann Measurement）:</strong></p>
<p>射影演算子の集合 $\{P_m\}$:
$$P_m P_{m'} = \delta_{mm'} P_m, \quad \sum_m P_m = I, \quad P_m^\dagger = P_m = P_m^2$$</p>
<p>測定結果 $m$ が得られる確率と測定後の状態:</p>
<p>$$p(m) = \text{Tr}(P_m \rho), \quad \rho_m = \frac{P_m \rho P_m}{p(m)}$$</p>
<p><strong>物理量の期待値:</strong></p>
<p>$$\langle M \rangle = \text{Tr}(M\rho), \quad M = \sum_m m P_m \quad\text{（観測量のスペクトル分解）}$$</p>
<blockquote>
<p>📊 Fig. 5.1 参照（原論文）: 射影測定の概念図</p>
</blockquote>
<p><strong>例: 量子ビットの計算基底測定</strong></p>
<p>$$P_0 = |0\rangle\langle 0|, \quad P_1 = |1\rangle\langle 1|$$</p>
<p>$$p(0) = \langle 0|\rho|0\rangle = \rho_{00}, \quad p(1) = \rho_{11}$$</p>
<h3>POVM（正演算子値測度）</h3>
<p>射影測定は「完全な測定」で、測定後に系が射影される。<strong>POVM</strong>（Positive Operator-Valued Measure）は測定結果の確率だけを記述するより一般的な枠組み:</p>
<p>正半定値演算子の集合 $\{E_m\}$:
$$E_m \geq 0, \quad \sum_m E_m = I$$</p>
<p>$$p(m|\rho) = \text{Tr}(E_m \rho)$$</p>
<p><strong>射影測定との違い:</strong>
- 射影測定: $E_m = P_m$（射影演算子）、測定後の状態が定まる
- POVM: $E_m$ は一般の正半定値演算子、測定後状態は指定不要
- POVMは「確率のみ」を計算する — 測定後の状態を問わない場合に使う</p>
<h3>クラウス演算子による測定（一般測定）</h3>
<p>測定後の状態まで記述するには<strong>クラウス演算子</strong>（測定演算子）$\{M_m\}$ を使う:</p>
<p>$$E_m = M_m^\dagger M_m, \quad \sum_m M_m^\dagger M_m = I$$</p>
<p>$$p(m) = \text{Tr}(M_m^\dagger M_m \rho) = \text{Tr}(E_m \rho)$$</p>
<p>$$\rho_m = \frac{M_m \rho M_m^\dagger}{p(m)}$$</p>
<p><strong>射影測定との関係:</strong> $M_m = P_m$（射影演算子）のとき射影測定に一致する。</p>
<h3>ナイマルクの拡張定理（Naimark's Dilation Theorem）</h3>
<p>任意の POVM $\{E_m\}$ on $\mathcal{H}_A$ は、補助系 $\mathcal{H}_B$ を追加した拡大空間上の射影測定として実現できる:</p>
<p>$$p(m) = \text{Tr}_{AB}(P_m \cdot \rho_A \otimes |0\rangle\langle 0|_B)$$</p>
<ul>
<li>物理的に「POVM = 系を拡大してユニタリ変換 + 射影測定」</li>
<li>量子情報処理のあらゆる「一般測定」はユニタリ + 射影測定で実装可能</li>
</ul>
<hr />

</details>

### 第4章: 量子チャネルとクラウス表現

<video controls width="100%" src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子チャネルとクラウス表現</h2>
<h3>量子チャネルの定義</h3>
<p><strong>量子チャネル（quantum channel）</strong> は入力系 A から出力系 B への量子状態の写像:</p>
<p>$$\mathcal{N}: \mathcal{L}(\mathcal{H}_A) \rightarrow \mathcal{L}(\mathcal{H}_B)$$</p>
<p>（$\mathcal{L}(\mathcal{H})$ = $\mathcal{H}$ 上の線形演算子の空間）</p>
<p>物理的なチャネルであるための条件:
1. <strong>線形性</strong>: $\mathcal{N}(\lambda\rho_1 + \mu\rho_2) = \lambda\mathcal{N}(\rho_1) + \mu\mathcal{N}(\rho_2)$
2. <strong>完全正値性（CP）</strong>: 任意の補助系 R に対し $(\mathcal{I}_R \otimes \mathcal{N})$ が正値性を保つ
3. <strong>トレース保存性（TP）</strong>: $\text{Tr}(\mathcal{N}(\rho)) = \text{Tr}(\rho) = 1$</p>
<p>CP + TP = <strong>CPTP 写像</strong> = 量子チャネル</p>
<h3>クラウス表現定理</h3>
<p><strong>定理（Kraus, 1983）:</strong> $\mathcal{N}$ が CPTP ⟺ クラウス演算子 $\{A_k\}$ が存在して:</p>
<p>$$\mathcal{N}(\rho) = \sum_k A_k \rho A_k^\dagger$$</p>
<p>$$\sum_k A_k^\dagger A_k = I \quad\text{（TP条件）}$$</p>
<ul>
<li>クラウス演算子 $A_k: \mathcal{H}_A \rightarrow \mathcal{H}_B$（$d_A \times d_B$ 行列）</li>
<li>クラウス表現は一意ではない（ユニタリ変換の自由度がある）</li>
</ul>
<blockquote>
<p>📊 Fig. 5.2 参照（原論文）: クラウス演算子による量子チャネルの図解</p>
</blockquote>
<p><strong>代表的なチャネルのクラウス表現:</strong></p>
<p><strong>ビット反転チャネル（bit-flip channel）:</strong>
$$\mathcal{N}(\rho) = (1-p)\rho + p X\rho X, \quad A_0 = \sqrt{1-p}\,I,\; A_1 = \sqrt{p}\,X$$</p>
<p><strong>脱分極チャネル（depolarizing channel）:</strong>
$$\mathcal{N}(\rho) = (1-p)\rho + \frac{p}{3}(X\rho X + Y\rho Y + Z\rho Z)$$</p>
<p><strong>振幅減衰チャネル（amplitude damping）:</strong>
$$A_0 = \begin{pmatrix}1&0\\0&\sqrt{1-\gamma}\end{pmatrix},\; A_1 = \begin{pmatrix}0&\sqrt{\gamma}\\0&0\end{pmatrix}$$</p>
<h3>スタインスプリング拡張定理</h3>
<p><strong>定理（Stinespring Dilation）:</strong> 任意の CPTP 写像 $\mathcal{N}$ は環境系 E を追加した等長写像（ユニタリ $U_{AE}$）で表現できる:</p>
<p>$$\mathcal{N}(\rho_A) = \text{Tr}_E\left(U_{AE}(\rho_A \otimes |0\rangle\langle 0|_E)U_{AE}^\dagger\right)$$</p>
<ul>
<li>「ノイズ = 環境とのもつれ」という直感的解釈</li>
<li>クラウス表現のユニタリ的な起源を明示する</li>
</ul>
<h3>チョイ-ヤミョウコフスキー同型</h3>
<p><strong>Choi-Jamiołkowski 同型:</strong> チャネル $\mathcal{N}$ ↔ 密度行列（チョイ行列）$\rho^{\mathcal{N}}$</p>
<p>$$\rho^{\mathcal{N}} = (\mathcal{I}_R \otimes \mathcal{N})(|\Phi^+\rangle\langle\Phi^+|_{RA}), \quad |\Phi^+\rangle = \frac{1}{\sqrt{d}}\sum_i|ii\rangle_{RA}$$</p>
<ul>
<li>$\mathcal{N}$ が CPTP ⟺ $\rho^{\mathcal{N}} \geq 0$（半正定値）かつ $\text{Tr}_B(\rho^{\mathcal{N}}) = I_R/d$</li>
<li>チャネルの性質をすべて行列の性質として解析できる</li>
</ul>
<hr />

</details>

### 第5章: Appendix A: 線形代数の基礎

<video controls width="100%" src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1106-1445/paper_1106.1445_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Appendix A: 線形代数の基礎</h2>
<h3>ヒルベルト空間と内積</h3>
<p>$d$ 次元複素ヒルベルト空間 $\mathbb{C}^d$ の内積:</p>
<p>$$\langle\phi|\psi\rangle = \sum_{i=1}^d \phi_i^* \psi_i$$</p>
<ul>
<li>共役双線形性: $\langle\phi|\psi\rangle = \overline{\langle\psi|\psi\rangle}$</li>
<li>ノルム: $\||\psi\rangle\| = \sqrt{\langle\psi|\psi\rangle} \geq 0$</li>
</ul>
<h3>演算子とスペクトル定理</h3>
<p><strong>エルミート演算子（自己随伴）:</strong> $A^\dagger = A$</p>
<ul>
<li>固有値はすべて実数</li>
<li>異なる固有値に対応する固有ベクトルは直交する</li>
</ul>
<p><strong>スペクトル定理:</strong> 任意のエルミート演算子 $A$ は:</p>
<p>$$A = \sum_i \lambda_i |i\rangle\langle i|, \quad A|i\rangle = \lambda_i|i\rangle, \quad \{|i\rangle\}\text{: 正規直交固有基底}$$</p>
<p><strong>正規直交基底:</strong> $\langle i|j\rangle = \delta_{ij}$, $\sum_i |i\rangle\langle i| = I$（完全性関係）</p>
<h3>トレースと行列関数</h3>
<p>$$\text{Tr}(A) = \sum_i \langle i|A|i\rangle = \sum_i A_{ii} \quad\text{（基底に依らない）}$$</p>
<p><strong>性質:</strong>
- $\text{Tr}(AB) = \text{Tr}(BA)$（巡回性）
- $\text{Tr}(A \otimes B) = \text{Tr}(A)\text{Tr}(B)$</p>
<p><strong>行列関数（スペクトル定理による）:</strong></p>
<p>$$f(A) = \sum_i f(\lambda_i)|i\rangle\langle i|, \quad A = \sum_i \lambda_i|i\rangle\langle i|$$</p>
<p>例: $e^A = \sum_i e^{\lambda_i}|i\rangle\langle i|$, $\ln\rho = \sum_i \ln\lambda_i|i\rangle\langle i|$</p>
<h3>テンソル積の計算規則</h3>
<p>$$|a\rangle_A \otimes |b\rangle_B = |ab\rangle_{AB}$$</p>
<p>$$A \otimes B: (A\otimes B)(|a\rangle\otimes|b\rangle) = (A|a\rangle)\otimes(B|b\rangle)$$</p>
<p>$(A \otimes B)(C \otimes D) = (AC) \otimes (BD)$</p>
<p>$(A \otimes B)^\dagger = A^\dagger \otimes B^\dagger$</p>
<h3>シュミット分解（Schmidt Decomposition）</h3>
<p>任意の純粋双部系状態 $|\psi\rangle_{AB}$ は:</p>
<p>$$|\psi\rangle_{AB} = \sum_{i=1}^{r} \sqrt{\lambda_i} |i\rangle_A|i'\rangle_B$$</p>
<ul>
<li>$r$: シュミット数（Schmidt rank）</li>
<li>$\{|i\rangle_A\}$, $\{|i'\rangle_B\}$: それぞれの局所正規直交基底</li>
<li>$\lambda_i > 0$, $\sum_i \lambda_i = 1$</li>
<li>$r = 1$: 積状態、$r > 1$: もつれ状態</li>
</ul>
<p><strong>量子もつれの検出:</strong> シュミット数 $r > 1$ ⟺ もつれ状態</p>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
