---
title: "量子回路学習（Quantum Circuit Learning）"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 量子回路学習（Quantum Circuit Learning）

*Mitarai, Negoro, Kitagawa, Fujii — *Physical Review A* 98, 032309 (2018)*

- arXiv: [1803.00745](https://arxiv.org/abs/1803.00745)
- Internet Archive: [paper-explain-1803-00745](https://archive.org/details/paper-explain-1803-00745)

---

## 章別動画・解説

### 第1章: イントロダクション：量子機械学習の夜明け

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch01.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>イントロダクション：量子機械学習の夜明け</h2>
<h3>なぜ量子コンピュータで機械学習か？</h3>
<ul>
<li>機械学習は量子物理・材料科学・創薬でも注目を集めていた（2017年当時）</li>
<li>量子コンピュータは一部の問題で指数的高速化を約束（ショアのアルゴリズム等）</li>
<li>自然な疑問：<strong>機械学習タスクも量子コンピュータで改善できるか？</strong></li>
</ul>
<h3>既存の量子機械学習の問題点</h3>
<table>
<thead>
<tr>
<th>手法</th>
<th>原理</th>
<th>限界</th>
</tr>
</thead>
<tbody>
<tr>
<td>HHLベース (Schuld et al., Rebentrost et al.)</td>
<td>行列演算を量子で実行</td>
<td><strong>高深度回路が必要</strong> → NISQ非現実的</td>
</tr>
<tr>
<td>QPE（量子位相推定）</td>
<td>固有値を直接読み出し</td>
<td><strong>長いコヒーレント発展</strong>が必要</td>
</tr>
</tbody>
</table>
<h3>本論文の提案：QCL（量子回路学習）</h3>
<ul>
<li><strong>低深度回路</strong>で動作するハイブリッド量子古典アルゴリズム</li>
<li>量子回路でデータ変換 → 古典コンピュータでパラメータ最適化</li>
<li>NISQデバイスで<strong>今すぐ実現可能</strong></li>
</ul>
<h3>QCLの位置づけ（関連手法との比較）</h3>
<table>
<thead>
<tr>
<th>手法</th>
<th>量子回路</th>
<th>パラメータ最適化</th>
<th>入力データ変換</th>
</tr>
</thead>
<tbody>
<tr>
<td>QRC（量子リザバー）</td>
<td>固定</td>
<td>古典（出力のみ）</td>
<td>なし</td>
</tr>
<tr>
<td>QVE/QAOA</td>
<td>パラメータ付き</td>
<td>古典（期待値最小化）</td>
<td>なし</td>
</tr>
<tr>
<td><strong>QCL（本論文）</strong></td>
<td>パラメータ付き</td>
<td>古典（勾配法）</td>
<td><strong>量子回路で変換</strong></td>
</tr>
</tbody>
</table>
<ul>
<li>QCLはQRCとQVEを統合した、より一般的なフレームワーク</li>
</ul>
<blockquote>
<p>📊 Fig. 1（p.2）参照（原論文）— QCLの概念図</p>
</blockquote>
<hr />

</details>

### 第2章: QCLアルゴリズム：3ステップで理解するパラメータ付き量子回路

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch02.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>QCLアルゴリズム：3ステップで理解するパラメータ付き量子回路</h2>
<h3>アルゴリズムの全体像</h3>
<p>$N$ 量子ビット回路上でのQCLアルゴリズム：</p>
<p>$$|\psi_{\rm out}(\boldsymbol{x}_i, \boldsymbol{\theta})\rangle = U(\boldsymbol{\theta})\, U(\boldsymbol{x}_i)\, |0\rangle$$</p>
<p>$$y(\boldsymbol{x}_i, \boldsymbol{\theta}) \equiv F\!\left(\{\langle B_j(\boldsymbol{x}_i, \boldsymbol{\theta})\rangle\}\right)$$</p>
<ul>
<li>$U(\boldsymbol{x}_i)$: 入力ゲート（データをエンコード）</li>
<li>$U(\boldsymbol{\theta})$: 学習可能ゲート（パラメータ $\boldsymbol{\theta}$ を調整）</li>
<li>$B_j \in \{I, X, Y, Z\}^{\otimes N}$: 測定するパウリオブザーバブル</li>
<li>$F$: 出力関数（測定値から予測値を計算）</li>
</ul>
<h3>ステップ1：入力エンコーディング</h3>
<p>$$|\psi_{\rm in}(\boldsymbol{x}_i)\rangle = U(\boldsymbol{x}_i)|0\rangle$$</p>
<ul>
<li>古典データ $\boldsymbol{x}_i$ を量子状態に変換</li>
<li>例：$x$ を回転角 $\theta = x$ として $R_Y(x)|0\rangle = \cos(x/2)|0\rangle + \sin(x/2)|1\rangle$</li>
<li>入力エンコーディングの設計は問題依存（重要な自由度）</li>
</ul>
<h3>ステップ2：パラメータ付きユニタリ変換</h3>
<p>$$|\psi_{\rm out}\rangle = U(\boldsymbol{\theta})|\psi_{\rm in}\rangle$$</p>
<ul>
<li>$U(\boldsymbol{\theta})$: パラメータ化された量子ゲートの積</li>
<li>例：交互に配置されたCNOTゲートと回転ゲート $R_Y(\theta_k)$</li>
<li>$\boldsymbol{\theta}$ が学習パラメータ（アナログ的に連続値）</li>
</ul>
<h3>ステップ3：測定と出力</h3>
<p>コスト関数（回帰問題の場合）：</p>
<p>$$L(\boldsymbol{\theta}) = \sum_i \|f(\boldsymbol{x}_i) - y(\boldsymbol{x}_i, \boldsymbol{\theta})\|^2$$</p>
<ul>
<li>$f(\boldsymbol{x}_i)$: 教師データ（正解ラベル）</li>
<li>$y(\boldsymbol{x}_i, \boldsymbol{\theta})$: 量子回路の出力</li>
<li>$L$ を最小化するように $\boldsymbol{\theta}$ を更新 → 学習！</li>
</ul>
<blockquote>
<p>📊 Fig. 2（p.3）参照（原論文）— 回路の具体的な構造</p>
</blockquote>
<hr />

</details>

### 第3章: 理論的基礎：近似能力・量子優位性・勾配計算

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch03.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>理論的基礎：近似能力・量子優位性・勾配計算</h2>
<h3>量子回路の汎用近似定理</h3>
<p><strong>定理（直感的表現）</strong>: 十分な量子ビット数があれば、QCLは<strong>任意の解析関数</strong>を近似できる。</p>
<ul>
<li>古典ニューラルネットワークの「普遍近似定理」の量子版</li>
<li>入力 $\boldsymbol{x}$ を $|\psi_{\rm in}(\boldsymbol{x})\rangle$ にエンコードすると、出力は三角多項式の重み付き和</li>
<li>量子ビット数 $N$ を増やすと近似できる関数のクラスが拡大</li>
</ul>
<p><strong>なぜ量子回路が非線形関数を表現できるか？</strong>
- 入力エンコーディング $U(\boldsymbol{x})$ が非線形変換を担う
- $\langle B_j \rangle$ の計算では $\sin$ や $\cos$ の積が現れる
- 回路の深さ・幅によって表現力が変化</p>
<h3>量子優位性の可能性</h3>
<table>
<thead>
<tr>
<th>観点</th>
<th>内容</th>
</tr>
</thead>
<tbody>
<tr>
<td>特徴空間</td>
<td>指数的に大きい量子特徴空間を活用できる</td>
</tr>
<tr>
<td>絡み合い</td>
<td>量子もつれが複雑な相関を効率的に表現</td>
</tr>
<tr>
<td>量子データ</td>
<td>量子系から来るデータは量子回路で自然に処理</td>
</tr>
</tbody>
</table>
<ul>
<li>ただし古典計算機に対する<strong>明確な量子優位性の証明はまだない</strong>（2018年当時）</li>
<li>「量子リザバー計算」との比較：QCLは全パラメータを学習（表現力が高い）</li>
</ul>
<h3>勾配の計算：パラメータシフト則の原形</h3>
<p>$$\frac{\partial \langle B_j \rangle}{\partial \theta_k} = \frac{1}{2}\left[\langle B_j \rangle\!\left(\theta_k + \frac{\pi}{2}\right) - \langle B_j \rangle\!\left(\theta_k - \frac{\pi}{2}\right)\right]$$</p>
<ul>
<li>回転ゲート $R(\theta_k) = e^{-i\theta_k P/2}$（$P$: パウリ演算子）の微分</li>
<li>$\theta_k$ を $\pm\pi/2$ シフトした回路の測定値の差で勾配を計算</li>
<li><strong>量子ハードウェア上でそのまま実行できる</strong>（シミュレーション不要）</li>
<li>これが後に「<strong>パラメータシフト則</strong>」として体系化（Mitarai et al. 2019）</li>
</ul>
<blockquote>
<p>📊 Fig. 3（p.4）参照（原論文）— 勾配計算の模式図</p>
</blockquote>
<hr />

</details>

### 第4章: 数値実験：関数回帰・分類・量子スピン系シミュレーション

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch04.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>数値実験：関数回帰・分類・量子スピン系シミュレーション</h2>
<h3>実験1：非線形関数の学習</h3>
<p><strong>設定</strong>: 1次元関数 $f(x) = x^3 + x^2 + x$ を量子回路で学習</p>
<ul>
<li>4量子ビット回路を使用</li>
<li>入力エンコーディング: $U(x) = R_Y(x)^{\otimes N}$</li>
<li>学習可能層: $d$ 層の交互ゲート構造</li>
</ul>
<p><strong>結果</strong>:
- QCLは非線形関数 $x^3 + x^2 + x$ を正確に学習できた
- 古典ニューラルネットワーク（同規模）と同等の精度
- 過学習は起きていない（後述の理論的裏付けあり）</p>
<h3>実験2：分類タスク</h3>
<p><strong>設定</strong>: 2次元平面上の2クラス分類</p>
<ul>
<li>$f(x_1, x_2) = x_1 \cdot x_2$（XORに類似した非線形境界）</li>
<li>4量子ビット回路 + 勾配降下法</li>
</ul>
<p><strong>結果</strong>:
- 非線形な決定境界を正確に学習
- 量子回路が古典的なロジスティック回帰では学習できないパターンを捉えた</p>
<h3>実験3：量子スピン系のダイナミクス予測</h3>
<p><strong>設定</strong>: 10スピン系のダイナミクスから3スピンの振る舞いを予測</p>
<p>$$H = \sum_{i<j} J_{ij} Z_i Z_j + \sum_i h_i X_i$$</p>
<p>（完全結合イジングハミルトニアン）</p>
<ul>
<li><strong>6量子ビット</strong>回路で学習</li>
<li>全体のヒルベルト空間は $2^{10} = 1024$ 次元</li>
<li>6量子ビット（$2^6 = 64$ 次元）で10スピン系を<strong>圧縮近似</strong></li>
</ul>
<p><strong>結果</strong>:
- 6量子ビットQCLが10スピン系の3スピン観測量のダイナミクスを再現
- 同サイズの古典ニューラルネットワークより高い精度
- 量子系のデータに量子回路が「相性が良い」ことを示唆</p>
<blockquote>
<p>📊 Fig. 4, 5, 6（p.5-6）参照（原論文）— 各実験の学習曲線</p>
</blockquote>
<hr />

</details>

### 第5章: 考察と結論：QCLが開いた新時代

<video controls width="100%" src="https://archive.org/download/paper-explain-1803-00745/paper_1803.00745_ch05.mp4"></video>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>考察と結論：QCLが開いた新時代</h2>
<h3>ユニタリ性がオーバーフィッティングを防ぐ（付録A）</h3>
<p><strong>重要な理論的洞察</strong>:</p>
<p>量子回路がユニタリ（$U^\dagger U = I$）であるという制約が、暗黙的な正則化として機能する：</p>
<p>$$\text{Tr}[(\rho_{\rm out})^2] = \text{Tr}[(\rho_{\rm in})^2]$$</p>
<ul>
<li>純粋状態の純粋度（purity）はユニタリ発展で保存される</li>
<li>これにより<strong>表現できる関数のクラスが制限</strong>される → 過学習を抑制</li>
<li>古典NNのL2正則化（weight decay）に対応する量子的メカニズム</li>
</ul>
<h3>QCLの限界と今後の課題</h3>
<table>
<thead>
<tr>
<th>課題</th>
<th>詳細</th>
</tr>
</thead>
<tbody>
<tr>
<td>バレンプラトー問題</td>
<td>量子ビット数が増えると勾配が指数的に消える（後に大きな研究分野に）</td>
</tr>
<tr>
<td>量子優位性の証明</td>
<td>古典計算に対する明確な優位性はまだ示されていない</td>
</tr>
<tr>
<td>スケーラビリティ</td>
<td>現状のNISQデバイスでは大規模タスクに限界</td>
</tr>
<tr>
<td>エラー耐性</td>
<td>ノイズが最適化を妨げる（エラー軽減法が必要）</td>
</tr>
</tbody>
</table>
<h3>QCLが開いた研究の流れ</h3>
<pre><code>QCL (2018) ← 本論文
    ├─ パラメータシフト則 (Mitarai et al. 2019)
    ├─ 変分量子固有値ソルバー（VQE）への応用拡大
    ├─ 量子カーネル法 (Havlicek et al. 2019)
    ├─ バレンプラトー問題の理論解析 (McClean et al. 2018)
    └─ ハードウェア効率的アンザッツ (Kandala et al. 2017)
</code></pre>
<h3>まとめ</h3>
<ul>
<li><strong>量子回路を機械学習モデルとして使う</strong>QCLフレームワークを提案</li>
<li>低深度回路でOK → <strong>NISQデバイスで実現可能</strong></li>
<li>任意の解析関数を近似できる（普遍近似定理の量子版）</li>
<li>数値実験で非線形関数学習・分類・量子系シミュレーションを実証</li>
<li>ユニタリ性が暗黙的正則化として機能 → 過学習を自然に抑制</li>
<li><strong>量子機械学習研究の基礎を確立した歴史的論文</strong>（被引用数1000件超）</li>
</ul>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
