---
title: "アニオンで計算する ── Kitaev のトポロジカル量子計算"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# アニオンで計算する ── Kitaev のトポロジカル量子計算

*A. Yu. Kitaev（ランダウ理論物理学研究所）*

- DOI: [10.1016/S0003-4916(02)00018-0](https://doi.org/10.1016/S0003-4916(02)00018-0)
- Internet Archive: [paper-explain-quant-ph-9707021](https://archive.org/details/paper-explain-quant-ph-9707021)

---

## 概要

Kitaev「Fault-tolerant quantum computation by anyons」（1997）── トポロジカル量子計算の原典を全5章で徹底解説！

2次元の量子系に現れる「アニオン」という特殊な粒子を使えば、物理的に耐障害性を持つ量子コンピュータが実現できる。このビジョンを初めて数学的に定式化したKitaevの伝説的論文を、ずんだもんと四国めたんがトーリックコード・ブレイディング・融合規則まで踏み込んで解説するのだ！

📄 対象論文：
・Fault-tolerant quantum computation by anyons
  A. Yu. Kitaev
  arXiv: quant-ph/9707021 (1997)
  Annals of Physics 303, 2–30 (2003)
  DOI: 10.1016/S0003-4916(02)00018-0

📚 チャプター構成：
Ch.01 アニオンとは何か ── 位相統計と量子コンピューティングの接点
Ch.02 アニオンの代数的理論 ── 融合規則とF行列・R行列
Ch.03 Z₂トーリックコード ── 格子ゲージ理論と安定化符号
Ch.04 ブレイディングによる量子ゲート ── ユニタリ変換の位相的実装
Ch.05 測定と誤り訂正 ── 融合プロトコルと障害耐性のまとめ

#論文解説 #量子コンピュータ #トポロジカル量子計算 #Kitaev #アニオン #トーリックコード #表面符号 #量子誤り訂正 #数式でわかる #研究 #大学院 #物理

---

## 章別動画・解説

### 第1章: アニオンとは何か ── 位相統計と量子コンピューティングの接点

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>アニオンとは何か ── 位相統計と量子コンピューティングの接点</h2>
<h3>粒子の統計：ボゾン・フェルミオン・アニオン</h3>
<p>3次元空間では、同種粒子を交換すると波動関数は 2 通りの変化しかしない：</p>
<p>$$|\psi\rangle \to e^{i\theta} |\psi\rangle, \quad \theta = 0 \text{（ボゾン）または } \pi \text{（フェルミオン）}$$</p>
<p><strong>2次元空間（平面）では交換が「絡み合い」を生む：</strong></p>
<p>$$|\psi\rangle \to e^{i\theta} |\psi\rangle, \quad \theta \in [0, 2\pi) \text{（任意の位相が許される）}$$</p>
<ul>
<li>3次元: 2点入れ替えを2回繰り返すと元に戻る（対称群 $S_n$）</li>
<li>2次元: 経路に「向き」があり、時計回り ≠ 反時計回り（ブレイド群 $B_n$）</li>
<li><strong>アニオン（anyons）</strong>: $\theta$ が 0 でも $\pi$ でもない粒子。2次元系にのみ存在</li>
</ul>
<h3>Aharonov-Bohm 効果との対応</h3>
<blockquote>
<p>📊 Fig. 1 参照（原論文）</p>
</blockquote>
<p>磁束 $\Phi$ の管のまわりを電荷 $q$ の粒子が一周すると：</p>
<p>$$e^{i\theta} = e^{iq\Phi/\hbar}$$</p>
<ul>
<li>電気的励起（e粒子）と磁気的励起（m粒子）のペアがアニオンを作る</li>
<li>互いのまわりを一周すると位相 $e^{i\pi} = -1$ を獲得 → <strong>自明でないブレイディング</strong></li>
</ul>
<h3>なぜ位相的量子計算が耐障害性を持つか</h3>
<p>量子情報が<strong>グローバルな位相的性質</strong>にエンコードされる：</p>
<ul>
<li>局所的な摂動（ノイズ）は位相的情報を変えない</li>
<li>情報を壊すには「ひも」を格子全体に渡すほどの大域操作が必要</li>
<li>エラーは短い「ひも」として現れ、検出・訂正できる</li>
</ul>
<p>$$P_{\text{error}} \propto e^{-d/\xi}$$</p>
<ul>
<li>$d$: コードの距離（格子サイズに比例）</li>
<li>$\xi$: 相関長（有限温度でも十分小さければ誤り訂正可能）</li>
</ul>
<hr />

</details>

### 第2章: アニオンの代数的理論 ── 融合規則とF行列・R行列

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>アニオンの代数的理論 ── 融合規則とF行列・R行列</h2>
<h3>融合規則</h3>
<p>異なる型のアニオンを「合体」させると何が生まれるかを記述：</p>
<p>$$a \times b = \sum_c N_{ab}^c \, c$$</p>
<ul>
<li>$N_{ab}^c \in \mathbb{Z}_{\geq 0}$: 融合多重度</li>
<li>Z₂アニオン（トーリックコード）の場合：</li>
</ul>
<p>$$e \times e = 1, \quad m \times m = 1, \quad e \times m = \epsilon, \quad \epsilon \times \epsilon = 1$$</p>
<ul>
<li>$e$: 電気的励起（electric anyon）</li>
<li>$m$: 磁気的励起（magnetic anyon）  </li>
<li>$\epsilon = e \times m$: フェルミオン的複合励起</li>
<li>$1$: 真空（アニオンなし）</li>
</ul>
<h3>F行列（Fシンボル）── 結合の変換</h3>
<p>3体融合に2通りの括弧の付け方があるとき、変換行列を F行列という：</p>
<p>$$\sum_e [F^{abc}_d]_{ec} \, (ab \to e, ec \to d) = \sum_f [F^{abc}_d]_{fc} \, (bc \to f, af \to d)$$</p>
<ul>
<li>トーリックコードでは $F$ 行列はすべて $1\times1$（多重度なし）で自明</li>
<li>より複り複雑なアニオン（フィボナッチアニオンなど）では非自明な行列になる</li>
</ul>
<h3>R行列（Rシンボル）── ブレイディング位相</h3>
<p>2体のアニオン $a, b$ を交換（時計回り）すると：</p>
<p>$$|\text{fused to } c\rangle \to R^{ab}_c \, |\text{fused to } c\rangle$$</p>
<p>Z₂アニオンのRシンボル（ブレイディング位相）：</p>
<table>
<thead>
<tr>
<th>交換</th>
<th>位相 $R^{ab}_c$</th>
</tr>
</thead>
<tbody>
<tr>
<td>$e, e \to 1$</td>
<td>$+1$</td>
</tr>
<tr>
<td>$m, m \to 1$</td>
<td>$+1$</td>
</tr>
<tr>
<td>$e, m \to \epsilon$</td>
<td>$+i$</td>
</tr>
<tr>
<td>$m, e \to \epsilon$</td>
<td>$-i$</td>
</tr>
</tbody>
</table>
<h3>ペンタゴン方程式とヘキサゴン方程式</h3>
<p>整合条件（F行列とR行列が矛盾しない条件）：</p>
<p><strong>ペンタゴン方程式</strong>（5辺の五角形ダイアグラム）：
$$\sum_f [F^{fcd}_e]_{gl} [F^{abl}_e]_{fc} = \sum_k [F^{abc}_k]_{jl} [F^{akd}_e]_{jm} [F^{bcd}_m]_{kl}$$</p>
<p><strong>ヘキサゴン方程式</strong>（6辺の六角形ダイアグラム）：
$$R^{ac}_e [F^{acb}_d]_{ef} R^{bc}_f = \sum_g [F^{cab}_d]_{eg} R^{gc}_d [F^{abc}_d]_{gf}$$</p>
<p>これらを満たす $(F, R)$ の組が<strong>アニオンモデル</strong>を定義する。</p>
<hr />

</details>

### 第3章: Z₂トーリックコード ── 格子ゲージ理論と安定化符号

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Z₂トーリックコード ── 格子ゲージ理論と安定化符号</h2>
<h3>格子の定義</h3>
<blockquote>
<p>📊 Fig. 2 参照（原論文）</p>
</blockquote>
<p>正方格子（$L \times L$）をトーラス上に置く（周期境界条件）：
- <strong>辺（edge）</strong>: 量子ビットを置く場所 → $2L^2$ 量子ビット
- <strong>頂点（vertex / star）</strong>: $s$
- <strong>面（plaquette）</strong>: $p$</p>
<h3>ハミルトニアン</h3>
<p>$$H = -\sum_{s} A_s - \sum_{p} B_p$$</p>
<p>$$A_s = \prod_{j \in \text{star}(s)} \sigma_j^x, \qquad B_p = \prod_{j \in \partial p} \sigma_j^z$$</p>
<ul>
<li>$A_s$: 頂点 $s$ に接する4辺のパウリX積</li>
<li>$B_p$: 面 $p$ の境界4辺のパウリZ積</li>
<li>$[A_s, B_p] = 0$ → すべての $A_s$, $B_p$ が同時対角化可能</li>
</ul>
<h3>基底状態の構造</h3>
<p>基底状態 $|G\rangle$ は：
$$A_s |G\rangle = +|G\rangle \quad \forall s, \qquad B_p |G\rangle = +|G\rangle \quad \forall p$$</p>
<p>トーラス上では基底状態が <strong>4重に縮退</strong>（位相的縮退）：</p>
<p>$$\dim(\mathcal{H}_{\text{ground}}) = 4 = 2^{2g}, \quad g=1 \text{（トーラスの種数）}$$</p>
<p>一般の種数 $g$ の曲面では $2^{2g}$ 重縮退 → <strong>位相的量子ビット</strong></p>
<h3>アニオン的励起</h3>
<p>$A_s = -1$ となる頂点 $s$ に <strong>電気的励起（e粒子）</strong> が生成：</p>
<p>$$Z(t) = \prod_{j \in t} \sigma_j^z \quad \text{（ひもの端点に e 粒子が対で生成）}$$</p>
<p>$B_p = -1$ となる面 $p$ に <strong>磁気的励起（m粒子）</strong> が生成：</p>
<p>$$X(s) = \prod_{j \in s} \sigma_j^x \quad \text{（双対ひもの端点に m 粒子が対で生成）}$$</p>
<blockquote>
<p>📊 Fig. 3 参照（原論文）</p>
</blockquote>
<h3>符号距離と位相的保護</h3>
<p>論理演算子（基底状態を変える最小演算子）の重さ = <strong>格子サイズ $L$</strong>：</p>
<p>$$d = L$$</p>
<ul>
<li>ランダムノイズがコードを壊すには $O(L)$ 個のエラーが必要</li>
<li>熱的安定性：有限温度では $O(e^{-2J/T})$ の確率でエラー（4次元では安定）</li>
</ul>
<hr />

</details>

### 第4章: ブレイディングによる量子ゲート ── ユニタリ変換の位相的実装

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>ブレイディングによる量子ゲート ── ユニタリ変換の位相的実装</h2>
<h3>アニオン対の生成と移動</h3>
<p>基底状態から励起を生成し、ひもを伸ばして移動：</p>
<ol>
<li>隣接辺にパウリ Z を作用 → e粒子対を生成（2頂点に1個ずつ）</li>
<li>さらに辺を続けて作用 → 1つの e粒子を格子上で「移動」</li>
<li>対を再合体させて消滅</li>
</ol>
<p>$$Z(t_{AB}) = \prod_{j \in t_{AB}} \sigma_j^z \quad \text{（A→B の経路 $t_{AB}$ に沿った e粒子移動）}$$</p>
<h3>ブレイディング：eをmのまわりで一周</h3>
<blockquote>
<p>📊 Fig. 4 参照（原論文）</p>
</blockquote>
<p>e粒子が m粒子のまわりを一周すると：</p>
<p>$$U_{\text{braid}} = e^{i\pi} = -1$$</p>
<p>これは Aharonov-Bohm 効果の位相 $e^{i q \Phi/\hbar}$ に相当（$q=1, \Phi=\pi$）。</p>
<p>この位相は：
- <strong>局所的な操作に依存しない</strong>（経路の細部によらずトポロジーのみ）
- <strong>ノイズ・環境揺らぎで破壊されない</strong></p>
<h3>論理ゲートの実装（トーラス上）</h3>
<p>トーラス上の2本の非自明サイクル $\gamma_1, \gamma_2$（縦・横方向）に沿ったひも演算子：</p>
<p>$$\bar{X}_1 = \prod_{j \in \gamma_1} \sigma_j^x, \quad \bar{Z}_1 = \prod_{j \in \gamma_1^*} \sigma_j^z$$</p>
<p>これらは <strong>論理量子ビットのパウリ演算子</strong>：
$$\bar{X}_1 \bar{Z}_1 = -\bar{Z}_1 \bar{X}_1, \quad [\bar{X}_1, \bar{X}_2] = 0, \quad [\bar{Z}_1, \bar{Z}_2] = 0$$</p>
<p>4重縮退した基底状態空間が <strong>2論理量子ビット</strong> を符号化。</p>
<h3>位相的耐障害性の本質</h3>
<table>
<thead>
<tr>
<th>操作</th>
<th>物理実装</th>
<th>位相的理由</th>
</tr>
</thead>
<tbody>
<tr>
<td>量子情報の保存</td>
<td>4重縮退基底状態</td>
<td>局所操作で区別不可</td>
</tr>
<tr>
<td>論理Xゲート</td>
<td>格子全体を渡るひも演算子</td>
<td>局所エラーは短いひもに留まる</td>
</tr>
<tr>
<td>論理Zゲート</td>
<td>双対格子の全域ひも</td>
<td>同上</td>
</tr>
<tr>
<td>誤り検出</td>
<td>頂点・面の測定</td>
<td>アニオンの端点検出</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第5章: 測定と誤り訂正 ── 融合プロトコルと障害耐性のまとめ

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>測定と誤り訂正 ── 融合プロトコルと障害耐性のまとめ</h2>
<h3>アニオン対の融合と測定</h3>
<p>2つのアニオンを「合体」させると融合規則に従った結果が観測される：</p>
<p>$$e + e \to 1 \quad \text{（アニオンが対消滅 = 真空へ）}$$
$$e + e \to \epsilon \quad \text{（別の型への変換）}$$</p>
<p>トーリックコードでは：
- 同種アニオン（e+e または m+m）の融合 → 常に真空（$1$）に戻る
- 測定結果は決定論的（確率的でない）</p>
<h3>シンドローム抽出</h3>
<p>誤りの「場所」を特定する測定（符号量子ビットを壊さない）：</p>
<p>$$s_v = \langle A_v \rangle \in \{+1, -1\}, \quad s_p = \langle B_p \rangle \in \{+1, -1\}$$</p>
<ul>
<li>$s_v = -1$: 頂点 $v$ に e粒子あり（Xエラーの端点）</li>
<li>$s_p = -1$: 面 $p$ に m粒子あり（Zエラーの端点）</li>
<li>シンドロームはペア（偶数個のアニオン）として現れる</li>
</ul>
<h3>誤り訂正プロトコル</h3>
<blockquote>
<p>📊 Fig. 5 参照（原論文）</p>
</blockquote>
<ol>
<li><strong>シンドローム測定</strong>: 全頂点・全面の $A_v, B_p$ を測定 → アニオン位置を特定</li>
<li><strong>マッチング</strong>: シンドロームアニオンをペアにする（最小重みマッチング）</li>
<li><strong>訂正操作</strong>: 各ペアを結ぶ最短経路に沿ってパウリ演算子を適用</li>
</ol>
<p><strong>閾値定理（Threshold Theorem）</strong>:</p>
<p>$$p_{\text{physical}} < p_{\text{th}} \approx 1\% \Rightarrow p_{\text{logical}} \to 0 \text{ (格子サイズ } L \to \infty \text{ で)}$$</p>
<h3>トーリックコードと表面符号の関係</h3>
<p>Kitaev のトーリックコード（1997）→ Dennis et al. の表面符号（2002）→ Fowler et al. の実装提案（2012）</p>
<table>
<thead>
<tr>
<th></th>
<th>トーリックコード</th>
<th>表面符号</th>
</tr>
</thead>
<tbody>
<tr>
<td>境界条件</td>
<td>周期境界（トーラス）</td>
<td>開境界</td>
</tr>
<tr>
<td>論理量子ビット数</td>
<td>$2g$（種数 $g$）</td>
<td>1</td>
</tr>
<tr>
<td>符号距離</td>
<td>$L$</td>
<td>$d$</td>
</tr>
<tr>
<td>実装容易性</td>
<td>難しい（トーラス形状）</td>
<td>容易（平面）</td>
</tr>
</tbody>
</table>
<h3>アニオン計算の完全性と展望</h3>
<p>Z₂アニオン（トーリックコード）だけでは <strong>普遍量子計算ができない</strong>：</p>
<p>$$\text{Clifford group（ブレイド）} \subsetneq \text{普遍量子計算}$$</p>
<p>普遍計算には非アーベルアニオンが必要：
- <strong>フィボナッチアニオン</strong>: ブレイディングだけで普遍計算可能
- <strong>イジングアニオン</strong>: ブレイドはCliffordのみ、マジック状態蒸留と組み合わせで普遍に
- <strong>マヨラナフェルミオン</strong>: 固体物理での実験実装が期待される</p>
<p>$$\text{位相的量子計算} = \text{ハードウェアレベルでの誤り訂正}$$</p>
<p>Kitaev の1997年のビジョンは、現代のトポロジカル量子コンピュータ開発の指針となっている。</p>
<hr />
<hr />

</details>

### 第6章: 付録：アニオンの代数理論の完全定式化とアニオンモデルの例

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch06.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>付録：アニオンの代数理論の完全定式化とアニオンモデルの例</h2>
<h3>Appendix A: 位相的スピン・S行列・量子次元</h3>
<p>ペンタゴン方程式・ヘキサゴン方程式を満たす $(F, R)$ から導かれる量：</p>
<p><strong>位相的スピン（topological spin）</strong>:</p>
<p>$$\theta_a = R^{aa}_1$$</p>
<p>アニオン $a$ を $2\pi$ 回転させたときの位相。フェルミオンは $\theta = -1$、ボゾンは $\theta = +1$。</p>
<p><strong>リボン構造</strong>: 融合後のスピンは</p>
<p>$$\theta_c = \theta_a \theta_b R^{ab}_c R^{ba}_c$$</p>
<p><strong>量子次元（quantum dimension）</strong>: 融合規則の最大固有値から定まるスカラー</p>
<p>$$d_a \geq 1, \quad d_a d_b = \sum_c N^c_{ab} d_c$$</p>
<p>Z₂トーリックコード: $d_e = d_m = d_\epsilon = 1$（アーベルアニオン）。</p>
<p>フィボナッチアニオン: $d_\tau = \varphi = \frac{1+\sqrt{5}}{2}$（黄金比）。</p>
<p><strong>総量子次元</strong>:</p>
<p>$$\mathcal{D} = \sqrt{\sum_a d_a^2}$$</p>
<p><strong>S行列（モジュラーデータ）</strong>:</p>
<p>$$S_{ab} = \frac{1}{\mathcal{D}} \sum_c N^c_{ab} \frac{\theta_c}{\theta_a \theta_b} d_c$$</p>
<p>S行列は「アニオン $a$ と $b$ を互いのまわりで一周させたときの振幅」を符号化する。これがフェルリンデ公式（Verlinde formula）と結びつく：</p>
<p>$$N^c_{ab} = \sum_x \frac{S_{ax} S_{bx} S_{cx}^*}{S_{0x}}$$</p>
<h3>Appendix B: アニオンモデルの例</h3>
<h4>Z₂理論（トーリックコード）</h4>
<table>
<thead>
<tr>
<th>アニオン</th>
<th>量子次元 $d$</th>
<th>位相的スピン $\theta$</th>
</tr>
</thead>
<tbody>
<tr>
<td>$1$（真空）</td>
<td>1</td>
<td>+1</td>
</tr>
<tr>
<td>$e$</td>
<td>1</td>
<td>+1</td>
</tr>
<tr>
<td>$m$</td>
<td>1</td>
<td>+1</td>
</tr>
<tr>
<td>$\epsilon = e \times m$</td>
<td>1</td>
<td>−1（フェルミオン）</td>
</tr>
</tbody>
</table>
<p>全アニオンがアーベル（次元1）→ ブレイディングは位相のみ。<strong>普遍量子計算には不十分</strong>。</p>
<h4>イジングアニオン</h4>
<p>融合規則: $\sigma \times \sigma = 1 + \psi$, $\sigma \times \psi = \sigma$, $\psi \times \psi = 1$</p>
<table>
<thead>
<tr>
<th>アニオン</th>
<th>量子次元</th>
<th>位相的スピン</th>
</tr>
</thead>
<tbody>
<tr>
<td>$1$</td>
<td>1</td>
<td>+1</td>
</tr>
<tr>
<td>$\sigma$</td>
<td>$\sqrt{2}$</td>
<td>$e^{i\pi/8}$</td>
</tr>
<tr>
<td>$\psi$</td>
<td>1</td>
<td>−1</td>
</tr>
</tbody>
</table>
<p>$\sigma$ は非アーベルアニオン（$d_\sigma = \sqrt{2} > 1$）。マヨラナフェルミオンのゼロモードとして固体物理で実現可能。イジングアニオンのブレイディングはクリフォード群のみ → <strong>単独では普遍計算不可能</strong>。</p>
<h4>フィボナッチアニオン</h4>
<p>融合規則: $\tau \times \tau = 1 + \tau$（これだけ）</p>
<p>$$d_\tau = \varphi = \frac{1+\sqrt{5}}{2} \approx 1.618$$</p>
<p>ペンタゴン方程式を解くと F行列の要素に黄金比が現れる：</p>
<p>$$[F^{\tau\tau\tau}_\tau]_{11} = \varphi^{-1}, \quad [F^{\tau\tau\tau}_\tau]_{1\tau} = \varphi^{-1/2}$$</p>
<p>フィボナッチアニオンのブレイディング群は<strong>SU(2)に稠密</strong> → ブレイディングのみで任意のユニタリ変換に任意精度で近づける。</p>
<p>$$\text{フィボナッチアニオンのブレイド} \xrightarrow{\text{稠密}} \text{普遍量子計算}$$</p>
<blockquote>
<p>📊 Fig. A1 参照（原論文）— ペンタゴン方程式の図的表現</p>
</blockquote>
<h4>アニオンモデルの比較</h4>
<table>
<thead>
<tr>
<th>モデル</th>
<th>アーベル？</th>
<th>普遍計算</th>
<th>固体物理実装候補</th>
</tr>
</thead>
<tbody>
<tr>
<td>Z₂（トーリック）</td>
<td>○</td>
<td>✗</td>
<td>量子スピン液体</td>
</tr>
<tr>
<td>イジング</td>
<td>✗</td>
<td>✗（Cliffordのみ）</td>
<td>マヨラナ準粒子</td>
</tr>
<tr>
<td>フィボナッチ</td>
<td>✗</td>
<td>✓</td>
<td>ν=12/5 分数量子ホール</td>
</tr>
</tbody>
</table>
<p>フィボナッチアニオンの物理的実現として最も有力な候補は充填率 $\nu = 12/5$ の分数量子ホール状態。ただし実験的確認はまだ途上。</p>
<hr />
<p><em>参考: arXiv: quant-ph/9707021 (https://arxiv.org/abs/quant-ph/9707021)</em></p>

</details>

---

[← 論文一覧に戻る](../../)
