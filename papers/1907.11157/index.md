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

### 第1章: 量子誤り訂正の必要性とノイズモデル

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子誤り訂正の必要性とノイズモデル</h2>
<h3>なぜ量子誤り訂正が必要か</h3>
<ul>
<li>量子ビット（qubit）は環境との相互作用で<strong>デコヒーレンス</strong>が起きる</li>
<li>古典ビットのノイズ：0→1 または 1→0（ビット反転）</li>
<li>量子ビットのノイズ：3種類のエラーが存在</li>
</ul>
<h3>3種類の量子エラー</h3>
<table>
<thead>
<tr>
<th>エラー</th>
<th>演算子</th>
<th>効果</th>
</tr>
</thead>
<tbody>
<tr>
<td>ビット反転（Bit Flip）</td>
<td>$X = \begin{pmatrix}0&1\\1&0\end{pmatrix}$</td>
<td>$\|0\rangle \leftrightarrow \|1\rangle$</td>
</tr>
<tr>
<td>位相反転（Phase Flip）</td>
<td>$Z = \begin{pmatrix}1&0\\0&-1\end{pmatrix}$</td>
<td>$\|+\rangle \leftrightarrow \|-\rangle$</td>
</tr>
<tr>
<td>両方（Y エラー）</td>
<td>$Y = iXZ$</td>
<td>ビット＋位相反転</td>
</tr>
</tbody>
</table>
<h3>量子チャネルモデル</h3>
<p><strong>脱分極チャネル（Depolarizing Channel）:</strong></p>
<p>$$\mathcal{E}(\rho) = (1-p)\rho + \frac{p}{3}(X\rho X + Y\rho Y + Z\rho Z)$$</p>
<ul>
<li>$\rho$: 量子状態の密度行列</li>
<li>$p$: エラー率（各軸方向に確率 $p/3$）</li>
<li>$p \to 0$ で恒等写像（ノイズなし）</li>
</ul>
<h3>複製禁止定理と量子誤り訂正</h3>
<ul>
<li><strong>複製禁止定理</strong>：未知の量子状態をコピーできない</li>
<li>では情報をどう守るか？→ <strong>冗長性をエンタングルメントで実現</strong></li>
<li>1量子ビットの情報を複数量子ビットに「分散」してエンコード</li>
</ul>
<h3>シンドローム測定の原理</h3>
<ul>
<li>符号空間外へのエラーを「間接測定」で検出</li>
<li>論理量子ビット自体は測定しない → 情報を壊さない</li>
<li>測定結果（シンドローム）からエラー位置を推定 → 訂正</li>
</ul>
<blockquote>
<p>📊 Fig. 1 参照（原論文）— ノイズチャネルと誤り訂正の流れ</p>
</blockquote>
<hr />

</details>

### 第2章: 古典符号から量子符号へ ── 繰り返し符号と安定化符号

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>古典符号から量子符号へ ── 繰り返し符号と安定化符号</h2>
<h3>古典繰り返し符号</h3>
<ul>
<li>$0 \to 000$、$1 \to 111$ とエンコード</li>
<li>多数決で訂正：$011 \to 1$（2個以上のビットが正しい）</li>
<li>符号距離 $d=3$：1エラーを訂正可能</li>
</ul>
<h3>量子ビット反転繰り返し符号</h3>
<p>$$|0\rangle_L = |000\rangle, \quad |1\rangle_L = |111\rangle$$</p>
<p>$$|\psi\rangle_L = \alpha|000\rangle + \beta|111\rangle$$</p>
<ul>
<li>$\alpha, \beta$: 論理量子ビットの振幅（複製禁止定理に違反しない）</li>
<li>Xエラーが1個起きても多数決で回復可能</li>
</ul>
<h3>安定化符号（Stabilizer Code）</h3>
<p><strong>安定化演算子：</strong></p>
<p>$$S_1 = Z \otimes Z \otimes I, \quad S_2 = I \otimes Z \otimes Z$$</p>
<p>$$S_1 |\psi\rangle_L = +|\psi\rangle_L, \quad S_2 |\psi\rangle_L = +|\psi\rangle_L$$</p>
<ul>
<li>符号空間: $S_1$ と $S_2$ の固有値 $+1$ の共通固有空間</li>
<li>$X_1$ エラー（1番目の qubit にX）が起きると $S_1 \to -1$、$S_2 \to +1$</li>
<li>$X_2$ エラーなら $S_1 \to -1$、$S_2 \to -1$</li>
<li>シンドローム $(s_1, s_2)$ でエラー位置を特定</li>
</ul>
<h3>安定化群の代数構造</h3>
<ul>
<li>安定化演算子は互いに<strong>可換</strong>（同時固有状態が存在）</li>
<li>$n$ qubit の Pauli 群 $\mathcal{P}_n$：$\{I, X, Y, Z\}^{\otimes n}$ に位相を加えた群</li>
<li>安定化符号 $[[n, k, d]]$: $n$ 物理 qubit で $k$ 論理 qubit を符号距離 $d$ で守る</li>
</ul>
<blockquote>
<p>📊 Fig. 2 参照（原論文）— 繰り返し符号のシンドローム測定回路</p>
</blockquote>
<hr />

</details>

### 第3章: CSS符号の代数構造 ── ステアン符号

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>CSS符号の代数構造 ── ステアン符号</h2>
<h3>CSS符号の構成</h3>
<p><strong>CSS符号（Calderbank-Shor-Steane Code）の定義：</strong></p>
<p>古典線形符号 $C_1 = [n, k_1, d_1]$ と $C_2 = [n, k_2, d_2]$ で $C_2^\perp \subseteq C_1$ を満たすとき：</p>
<p>$$|c + C_2^\perp\rangle = \frac{1}{\sqrt{|C_2^\perp|}} \sum_{v \in C_2^\perp} |c + v\rangle, \quad c \in C_1$$</p>
<ul>
<li>Xスタビライザー: $C_2^\perp$ のパリティ検査行列 $H_2$ から生成</li>
<li>Zスタビライザー: $C_1^\perp$ のパリティ検査行列 $H_1^T$ から生成</li>
<li>パラメータ: $[[n, k_1 + k_2 - n, \min(d_1, d_2)]]$</li>
</ul>
<h3>ステアン符号 [7,1,3]</h3>
<p><strong>7量子ビット完全符号。[7,4,3] ハミング符号から構成：</strong></p>
<p>$$H = \begin{pmatrix}
0&0&0&1&1&1&1\\
0&1&1&0&0&1&1\\
1&0&1&0&1&0&1
\end{pmatrix}$$</p>
<ul>
<li>6個の安定化演算子（Xタイプ3個 + Zタイプ3個）</li>
<li>論理X演算子: $\bar{X} = X^{\otimes 7}$（全ビットにX）</li>
<li>論理Z演算子: $\bar{Z} = Z^{\otimes 7}$（全ビットにZ）</li>
<li>符号距離3 → 1エラーを訂正可能</li>
</ul>
<h3>論理演算子とトランスバーサルゲート</h3>
<p>$$\bar{X} = X_1 X_2 X_3 X_4 X_5 X_6 X_7, \quad \bar{Z} = Z_1 Z_2 Z_3 Z_4 Z_5 Z_6 Z_7$$</p>
<ul>
<li><strong>トランスバーサル演算</strong>: 各物理 qubit に独立に同じゲートを適用</li>
<li>ステアン符号では H, CNOT, S ゲートがトランスバーサル → フォルトトレラント</li>
</ul>
<blockquote>
<p>📊 Fig. 3 参照（原論文）— CSS符号の構成とステアン符号の安定化演算子</p>
</blockquote>
<hr />

</details>

### 第4章: 表面符号 ── 最も実用的な量子誤り訂正符号

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>表面符号 ── 最も実用的な量子誤り訂正符号</h2>
<h3>表面符号の格子構造</h3>
<ul>
<li>$d \times d$ の格子（開境界）上に量子ビットを配置</li>
<li>量子ビットは<strong>辺</strong>に置く → $2d(d-1) + (d-1)^2 + d^2 - 1$ ... 簡単に言えば $\sim d^2$ 個</li>
<li>パラメータ: $[[d^2 + (d-1)^2, 1, d]]$ ≈ $[[2d^2-2d+1, 1, d]]$</li>
</ul>
<p><strong>ハミルトニアン:</strong></p>
<p>$$H = -\sum_{v} A_v - \sum_{f} B_f$$</p>
<ul>
<li>$A_v = \prod_{i \in \partial v} X_i$: 頂点 $v$ に接する辺のX積（Xスタビライザー）</li>
<li>$B_f = \prod_{i \in \partial f} Z_i$: 面 $f$ を囲む辺のZ積（Zスタビライザー）</li>
</ul>
<h3>シンドローム測定とデコーダー</h3>
<p><strong>エラー検出:</strong></p>
<ul>
<li>Zエラー → $A_v = -1$（頂点アニオン出現）</li>
<li>Xエラー → $B_f = -1$（面アニオン出現）</li>
</ul>
<p><strong>最小重みマッチング（MWPM）デコーダー:</strong></p>
<p>$$\text{correction} = \arg\min \sum_{\text{pairs}} d(\text{anyon}_i, \text{anyon}_j)$$</p>
<ul>
<li>シンドローム上の全アニオンをペアに分け、最短距離でマッチング</li>
<li>Blossom アルゴリズム（多項式時間）で効率的に解ける</li>
</ul>
<h3>論理演算子と符号距離</h3>
<p>$$\bar{X} = \prod_{i \in \gamma_X} X_i, \quad \bar{Z} = \prod_{i \in \gamma_Z} Z_i$$</p>
<ul>
<li>$\gamma_X$: 左境界から右境界を結ぶX演算子のチェーン</li>
<li>$\gamma_Z$: 上境界から下境界を結ぶZ演算子のチェーン</li>
<li>符号距離 $d$ = 論理エラーに必要な最小演算子数 = 格子サイズ $d$</li>
</ul>
<blockquote>
<p>📊 Fig. 4 参照（原論文）— 表面符号の格子・安定化子・論理演算子</p>
</blockquote>
<hr />

</details>

### 第5章: 耐障害性と閾値定理

<video controls width="100%" src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1907-11157/paper_1907.11157_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>耐障害性と閾値定理</h2>
<h3>耐障害性（Fault Tolerance）の概念</h3>
<ul>
<li><strong>問題</strong>: シンドローム測定回路自体にエラーが入る</li>
<li><strong>解決</strong>: 測定エラーが論理エラーに「増幅」されない回路設計</li>
<li><strong>条件</strong>: 任意のゲートで1エラーが2エラーに広がらない</li>
</ul>
<h3>フォルトトレラント量子計算の要素</h3>
<table>
<thead>
<tr>
<th>要素</th>
<th>実装方法</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td>メモリ</td>
<td>QEC サイクル</td>
<td>シンドロームを繰り返し測定</td>
</tr>
<tr>
<td>CliffordゲートCNOT</td>
<td>トランスバーサル</td>
<td>表面符号で実現可能</td>
</tr>
<tr>
<td>非Clifford（Tゲート）</td>
<td>マジック状態蒸留</td>
<td>特別な状態 $\|T\rangle$ を注入</td>
</tr>
</tbody>
</table>
<h3>マジック状態蒸留</h3>
<p>$$|T\rangle = \frac{|0\rangle + e^{i\pi/4}|1\rangle}{\sqrt{2}}$$</p>
<ul>
<li>Tゲートをトランスバーサルに実装不可 → 代わりに $\|T\rangle$ を使う</li>
<li>低品質な $\|T\rangle$ を多数用意 → 蒸留プロトコルで高品質に精製</li>
<li>オーバーヘッドが大きい（量子コンピュータの大部分はT蒸留に使われる）</li>
</ul>
<h3>閾値定理</h3>
<p><strong>物理エラー率 $p$ が閾値 $p_{th}$ を下回れば、コードサイズを増やして論理エラー率を指数的に下げられる：</strong></p>
<p>$$p_L \propto \left(\frac{p}{p_{th}}\right)^{\lceil d/2 \rceil}$$</p>
<ul>
<li>表面符号の閾値: $p_{th} \approx 1\%$（独立脱分極ノイズ）</li>
<li>Google Willow（2024）: 物理エラー率 $\sim 0.1\%$ → 閾値を下回る</li>
<li>IBM Eagle/Heron: 同様の水準に到達</li>
</ul>
<blockquote>
<p>📊 Fig. 5 参照（原論文）— 閾値定理の概念図・論理エラー率のスケーリング</p>
</blockquote>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
