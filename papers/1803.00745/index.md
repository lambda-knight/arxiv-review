---
title: "量子回路学習（Quantum Circuit Learning）"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 量子回路学習（Quantum Circuit Learning）

*Quantum Circuit Learning*

- arXiv: [1803.00745](https://arxiv.org/abs/1803.00745)
- Internet Archive: [paper-explain-1803-00745](https://archive.org/details/paper-explain-1803-00745)

---

## 概要

大阪大学・京都大学の御手洗恭三・根来誠・北川拓也・藤井啓祐チームによる2018年論文を徹底解説します。パラメータ付き量子回路を機械学習モデルとして使う「量子回路学習（QCL）」の5ステップアルゴリズム、±π/2シフトで勾配を計算するパラメータシフト則の原形、そして量子力学のユニタリ性が過学習を防ぐ仕組みまで、フルテキストから数式を使って解説します。

▼ 今日の論文
・Quantum Circuit Learning — K. Mitarai, M. Negoro, M. Kitagawa（大阪大学）, K. Fujii（京都大学）
  Physical Review A 98, 032309 (2018) — arXiv:1803.00745

▼ 参考論文（arXiv）
https://arxiv.org/abs/1803.00745  — Quantum Circuit Learning

#量子コンピュータ #量子機械学習 #パラメータシフト則 #変分量子回路 #NISQ #arxiv #論文解説 #ゆっくり解説 #ずんだもん

---

## 章別動画・解説

### 第1章: 導入：量子機械学習の夜明け

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>導入：量子機械学習の夜明け</h2>
<h3>背景：なぜ量子コンピュータで機械学習か</h3>
<ul>
<li>2017〜2018年：機械学習ブームと量子コンピュータの実用化機運が重なった時代</li>
<li>量子コンピュータは一部の問題で指数的高速化が可能（ショアのアルゴリズム等）</li>
<li>量子物理・材料科学・創薬でも機械学習の応用が注目されていた</li>
</ul>
<h3>既存の量子機械学習の問題点</h3>
<table>
<thead>
<tr>
<th>手法</th>
<th>原理</th>
<th>欠点</th>
</tr>
</thead>
<tbody>
<tr>
<td>HHLベース (Schuld et al., Rebentrost et al.)</td>
<td>行列演算を量子で実行</td>
<td><strong>高深度回路が必要</strong> → NISQ非現実的</td>
</tr>
<tr>
<td>量子位相推定 (QPE)</td>
<td>固有値を直接読み出し</td>
<td><strong>長いコヒーレント発展</strong>が必要</td>
</tr>
</tbody>
</table>
<h3>本論文の提案：QCL（量子回路学習）</h3>
<ul>
<li><strong>低深度</strong>パラメータ付き量子回路を機械学習モデルとして用いる</li>
<li>量子回路でデータ変換 → 古典コンピュータでパラメータを最適化するハイブリッド手法</li>
<li>NISQデバイスで<strong>今すぐ実現可能</strong></li>
</ul>
<h3>関連手法との比較（論文 Fig. 1）</h3>
<table>
<thead>
<tr>
<th>手法</th>
<th>回路の調整</th>
<th>入力データ変換</th>
<th>最適化対象</th>
</tr>
</thead>
<tbody>
<tr>
<td>QRC（量子リザバー）</td>
<td>なし（固定）</td>
<td>なし</td>
<td>出力の線形重み $\boldsymbol{w}$</td>
</tr>
<tr>
<td>QVE/QAOA</td>
<td>θ を調整</td>
<td>なし（重みに符号化）</td>
<td>期待値 $\boldsymbol{w}_{\rm fixed}\cdot\langle\boldsymbol{B}(\boldsymbol{\theta})\rangle$</td>
</tr>
<tr>
<td><strong>QCL（本論文）</strong></td>
<td>θ を調整</td>
<td><strong>量子回路</strong> $U(\boldsymbol{x})$ で変換</td>
<td>コスト関数 $L$</td>
</tr>
</tbody>
</table>
<blockquote>
<p>📊 Fig. 1 参照（原論文）— QCL・QRC・QVEの比較図</p>
</blockquote>
<hr />

</details>

### 第2章: QCLアルゴリズム：5ステップの詳細

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>QCLアルゴリズム：5ステップの詳細</h2>
<h3>アルゴリズムの全体像</h3>
<p>$N$ 量子ビット回路でのQCL手順：</p>
<p>$$|\psi_{\rm out}(\boldsymbol{x}_i, \boldsymbol{\theta})\rangle = U(\boldsymbol{\theta})\,|\psi_{\rm in}(\boldsymbol{x}_i)\rangle = U(\boldsymbol{\theta})\,U(\boldsymbol{x}_i)\,|0\rangle$$</p>
<p>$$y(\boldsymbol{x}_i, \boldsymbol{\theta}) \equiv F\!\left(\{\langle B_j(\boldsymbol{x}_i, \boldsymbol{\theta})\rangle\}\right)$$</p>
<ul>
<li>$U(\boldsymbol{x}_i)$：入力ゲート（データを量子状態にエンコード）</li>
<li>$U(\boldsymbol{\theta})$：学習可能なパラメータ付きユニタリ</li>
<li>$B_j \in \{I, X, Y, Z\}^{\otimes N}$：測定するパウリオブザーバブル</li>
<li>$F$：出力関数（測定値から予測値を計算）</li>
</ul>
<h3>ステップ1：入力エンコーディング</h3>
<p>$$|\psi_{\rm in}(\boldsymbol{x}_i)\rangle = U(\boldsymbol{x}_i)\,|0\rangle$$</p>
<ul>
<li>古典データ $\boldsymbol{x}_i$ を量子状態に変換</li>
<li>例（論文の1次元デモ）：
$$U_{\rm in}(x) = \prod_j R_j^Z(\cos^{-1} x^2)\,R_j^Y(\sin^{-1} x)$$</li>
<li>テンソル積構造が自動的に $x^N$ 次の多項式を含む状態を生成</li>
</ul>
<h3>ステップ2：パラメータ付きユニタリ変換</h3>
<p>$$|\psi_{\rm out}\rangle = U(\boldsymbol{\theta})\,|\psi_{\rm in}\rangle, \quad U(\boldsymbol{\theta}) = \prod_{j=1}^l U_j(\theta_j)$$</p>
<ul>
<li>数値実験では1量子ビット任意回転 $U(\theta_j^{(i)}) = R_j^X(\theta_{j1}^{(i)})R_j^Z(\theta_{j2}^{(i)})R_j^X(\theta_{j3}^{(i)})$ を使用</li>
<li>回路にはイジングハミルトニアンによる時間発展も含む（絡み合いを生成）</li>
</ul>
<h3>ステップ3：測定と出力</h3>
<p>コスト関数（回帰問題）：</p>
<p>$$L(\boldsymbol{\theta}) = \sum_i \|f(\boldsymbol{x}_i) - y(\boldsymbol{x}_i, \boldsymbol{\theta})\|^2$$</p>
<p>分類問題ではクロスエントロピーを使用：</p>
<p>$$L = \sum_i \sum_{k \in \{0,1\}} \bigl(f(\boldsymbol{x}_i)\bigr)_k \log y_{ik}$$</p>
<ul>
<li>$f(\boldsymbol{x}_i)$：教師データ（正解ラベル）</li>
<li>$y_i$：量子回路の出力</li>
<li>コストを最小化するように $\boldsymbol{\theta}$ を反復更新</li>
</ul>
<blockquote>
<p>📊 Fig. 2 参照（原論文）— 数値実験で使用した量子回路の構造</p>
</blockquote>
<hr />

</details>

### 第3章: 理論的基礎：関数近似能力と勾配計算

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>理論的基礎：関数近似能力と勾配計算</h2>
<h3>テンソル積構造と関数近似</h3>
<p>入力状態のテンソル積構造（$N$ 量子ビット）：</p>
<p>$$\rho_{\rm in}(x) = \frac{1}{2^N}\bigotimes_{i=1}^N \bigl[I + x X_i + \sqrt{1-x^2}\,Z_i\bigr]$$</p>
<ul>
<li>$N$ 量子ビットが $x, x^2, \ldots, x^N$ までの高次項を自動的に含む</li>
<li>任意のユニタリ変換後の期待値は <strong>任意の $N$ 次多項式</strong>を表現できる</li>
<li>解析関数であれば原理的に QCL で近似可能（量子版・普遍近似定理）</li>
</ul>
<h3>ユニタリ条件と量子優位性の可能性</h3>
<ul>
<li>出力は各行ベクトル $\boldsymbol{u}_i$ のノルムがユニタリ条件で $\|\boldsymbol{u}_i\| = 1$ に固定される</li>
<li>量子回路は指数的に大きい特徴空間を多項式の回路サイズで活用できる</li>
<li>QCLが表現できる関数を古典ニューラルネットで学習するには万能量子計算機の模倣が必要 → 古典的に非効率</li>
</ul>
<h3>勾配計算：パラメータシフト則の原形</h3>
<p>パウリ積生成のゲート $U_j(\theta_j) = \exp(-i\theta_j P_j/2)$ に対する勾配：</p>
<p>$$\frac{\partial \langle B\rangle}{\partial \theta_j} = \frac{\langle B\rangle_j^+ - \langle B\rangle_j^-}{2}$$</p>
<p>$$\langle B\rangle_j^\pm: \theta_j \text{ を } \pm\frac{\pi}{2} \text{ シフトしたときの期待値}$$</p>
<ul>
<li>$\pm\pi/2$ 回転を挿入した2つの回路を実行するだけで<strong>厳密な勾配</strong>が得られる</li>
<li>量子ハードウェア上でそのまま実行可能（シミュレーション不要）</li>
<li>Li et al. (2017) の制御パルス最適化と同様のアプローチ</li>
<li>これが後の「<strong>パラメータシフト則</strong>」（Mitarai et al. 2019）の基礎</li>
</ul>
<hr />

</details>

### 第4章: 数値実験：関数フィッティング

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>数値実験：関数フィッティング</h2>
<h3>実験設定（共通）</h3>
<ul>
<li><strong>量子ビット数</strong>: $N = 6$、<strong>回路深さ</strong>: $D = 6$</li>
<li>ハミルトニアン（完全結合横磁場イジング型、式4）：</li>
</ul>
<p>$$H = \sum_{j=1}^N a_j X_j + \sum_{j=1}^N \sum_{k=1}^{j-1} J_{jk} Z_j Z_k$$</p>
<ul>
<li>$a_j$, $J_{jk}$ は $[-1,1]$ 上の一様乱数</li>
<li>進化時間 $T = 10$、最適化は BFGS 法（SciPy）</li>
<li>サンプリングノイズを模擬するガウスノイズを付加</li>
</ul>
<h3>1次元関数フィッティング（100サンプル）</h3>
<p>対象関数：$f(x) = x^2,\ e^x,\ \sin x,\ |x|$</p>
<ul>
<li>入力エンコーディング: $U_{\rm in}(x) = \prod_j R_j^Z(\cos^{-1} x^2) R_j^Y(\sin^{-1} x)$</li>
<li>出力: 第1量子ビットの $Z$ 期待値（定数 $a$ も同時最適化）</li>
<li><strong>結果</strong>: $x^2$、$e^x$、$\sin x$ はよく近似できた</li>
</ul>
<blockquote>
<p>📊 Fig. 3 参照（原論文）— 各関数のフィッティング結果</p>
</blockquote>
<ul>
<li>$|x|$ の近似精度は比較的低い：$x=0$ での非解析性（微分不連続）が原因</li>
<li>改善策として Legendre 多項式などの異なる入力関数を使う可能性を論文は指摘</li>
</ul>
<hr />

</details>

### 第5章: 数値実験：分類と多体ダイナミクス

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>数値実験：分類と多体ダイナミクス</h2>
<h3>2次元分類タスク（200サンプル）</h3>
<ul>
<li>訓練データ: 2次元入力 $\boldsymbol{x}_i = (x_{i,0}, x_{i,1})$、2クラス（100サンプル/クラス）</li>
<li>教師: クラス0→$(1,0)$、クラス1→$(0,1)$</li>
<li>出力: 第1・第2量子ビットの $Z$ 期待値をソフトマックス変換
$$\boldsymbol{y}_i = \boldsymbol{F}\!\left(\langle Z_1\rangle, \langle Z_2\rangle\right), \quad F_k(\boldsymbol{q}) = \frac{e^{q_k}}{\sum_i e^{q_i}}$$</li>
<li>損失関数: クロスエントロピー</li>
<li><strong>結果</strong>: 非線形な決定境界を正確に学習した</li>
</ul>
<blockquote>
<p>📊 Fig. 4 参照（原論文）— 訓練データと最適化後の出力</p>
</blockquote>
<h3>量子多体ダイナミクスのフィッティング</h3>
<p>10スピン完全結合横磁場イジング系のダイナミクスを6量子ビット回路で近似：</p>
<ul>
<li>教師データ: 10スピン系（$a_j$, $J_{jk}$ は回路とは独立の乱数）の $Z$ 期待値</li>
<li>初期状態 $|0\rangle^{\otimes 10}$、過渡応答時間 $T_{\rm transient} = 300$ を除いた $t \in [300, 308]$</li>
<li>$t$ を $x \in [-1, 1]$ に線形マッピングして入力</li>
<li><strong>学習対象</strong>: 最初の3スピンの $Z$ 期待値を6量子ビット回路の最初の3量子ビット出力で近似</li>
<li><strong>結果</strong>: 6量子ビット回路（64次元）が10スピン系（1024次元）の3つのオブザーバブルを同時に再現</li>
</ul>
<blockquote>
<p>📊 Fig. 5 参照（原論文）— 多体ダイナミクスのフィッティング結果</p>
</blockquote>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
