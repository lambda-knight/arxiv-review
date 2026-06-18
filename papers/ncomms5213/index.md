---
title: "フォトニック量子プロセッサ上の変分固有値ソルバー（VQE）"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# フォトニック量子プロセッサ上の変分固有値ソルバー（VQE）

*Peruzzo et al., *Nature Communications* 5, 4213 (2014)*

- ID: ncomms5213
- Internet Archive: [paper-explain-ncomms5213](https://archive.org/details/paper-explain-ncomms5213)

---

## 章別動画・解説

### 第1章: イントロダクション

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>イントロダクション</h2>
<h3>量子化学の壁：指数的爆発</h3>
<ul>
<li>量子系のシュレーディンガー方程式は<strong>原理的には解ける</strong></li>
<li>問題：系のサイズ N に対して、状態空間は <strong>2^N</strong> で指数的に増大</li>
<li>原子2〜3個を超えると古典計算機では厳密解が不可能</li>
<li>量子固有値問題の応用例:</li>
<li>量子化学: 分子の基底状態エネルギー・反応経路</li>
<li>材料設計・創薬</li>
<li>PageRank などの大規模固有値問題</li>
</ul>
<h3>量子位相推定（QPE）の限界</h3>
<table>
<thead>
<tr>
<th>項目</th>
<th>QPE</th>
<th>VQE（本論文）</th>
</tr>
</thead>
<tbody>
<tr>
<td>量子ゲート数</td>
<td>O(1/p)（精度 p）</td>
<td>少数</td>
</tr>
<tr>
<td>コヒーレンス時間</td>
<td>数百万〜数十億ゲート</td>
<td><strong>O(1)</strong></td>
</tr>
<tr>
<td>現在の量子デバイス</td>
<td>非現実的</td>
<td><strong>実現可能</strong></td>
</tr>
</tbody>
</table>
<ul>
<li>QPE は指数的高速化を約束するが<strong>完全なコヒーレント発展</strong>が必要</li>
<li>現在実現できる量子ゲート数は数十〜数百</li>
<li><strong>本論文はコヒーレンス要件を劇的に緩和する代替手法を提案</strong></li>
</ul>
<hr />

</details>

### 第2章: 量子期待値推定

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子期待値推定</h2>
<h3>ハミルトニアンのパウリ分解</h3>
<p>任意のエルミートハミルトニアンは次のように展開できる：</p>
<p>$$\mathcal{H} = \sum_{\alpha} h_\alpha \bigotimes_i P^i_\alpha$$</p>
<ul>
<li>$h_\alpha$: 実係数</li>
<li>$P^i_\alpha$: $i$ 番目の部分空間に作用するパウリ演算子（$I, X, Y, Z$）</li>
<li>量子化学・イジングモデル・ハイゼンベルクモデルなど幅広い系に適用可能</li>
</ul>
<h3>期待値の線形性を利用</h3>
<p>$$\langle \mathcal{H} \rangle = \sum_\alpha h_\alpha \left\langle \bigotimes_i P^i_\alpha \right\rangle$$</p>
<ul>
<li>テンソル積パウリ演算子の期待値は<strong>定数時間で測定可能</strong></li>
<li>M 項の和 → M 回の独立測定</li>
<li>精度 p の推定コスト: $O\left(|h_\text{max}|^2 M / p^2\right)$ 回の繰り返し</li>
</ul>
<h3>鍵となる利点</h3>
<ul>
<li>1回の測定あたりのコヒーレンス時間は <strong>O(1)</strong></li>
<li>QPE（長いコヒーレント発展）vs 本手法（短い測定の多数繰り返し）</li>
<li>N-表現可能性問題（古典・量子コンピュータ双方で難解）を回避</li>
<li>量子ハードウェアが指数的少ないリソースで大域的量子状態を保持するため</li>
</ul>
<blockquote>
<p>📊 Fig. 1（p.2）参照（原論文）— Algorithm 1 &amp; 2 の関係図</p>
</blockquote>
<hr />

</details>

### 第3章: 量子変分固有値ソルバー

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子変分固有値ソルバー</h2>
<h3>レイリー・リッツ変分原理</h3>
<p>最小固有値は次の最小化問題として書き直せる：</p>
<p>$$\lambda_{\min} = \min_{|\psi\rangle} \frac{\langle \psi | \mathcal{H} | \psi \rangle}{\langle \psi | \psi \rangle}$$</p>
<ul>
<li><strong>VQE のアイデア</strong>: 量子デバイスで $\langle \mathcal{H} \rangle$ を計算しながら、古典最適化で $|\psi\rangle$ のパラメータを更新</li>
</ul>
<h3>アンザッツ状態（Ansatz）</h3>
<p>状態 $|\psi(\theta)\rangle$ を多項式個のパラメータ $\theta$ で記述：</p>
<p>$$|\psi(\theta)\rangle = e^{T(\theta) - T^\dagger(\theta)} |\Phi_\text{ref}\rangle$$</p>
<ul>
<li><strong>ユニタリ結合クラスター（UCC）アンザッツ</strong></li>
<li>$T$: クラスター演算子（励起の重ね合わせ）</li>
<li>$|\Phi_\text{ref}\rangle$: ハートリー・フォック基底状態</li>
<li>UCC は量子化学の「ゴールドスタンダード」とされる非ユニタリ版より優れた結果が期待される</li>
</ul>
<h3>VQEのループ</h3>
<pre><code>① 量子デバイス: |ψ(θ)⟩ を準備 → ⟨H⟩ を測定
② 古典コンピュータ: θ を更新（Nelder-Mead 等）
③ 収束するまで繰り返す
</code></pre>
<ul>
<li>量子部分のコヒーレンス時間は状態準備と1回の測定のみ</li>
<li>探索空間は多項式次元 → 古典最適化が効率的</li>
</ul>
<blockquote>
<p>📊 Fig. 1（p.2）参照（原論文）— QPU + CPU ハイブリッドループ</p>
</blockquote>
<hr />

</details>

### 第4章: プロトタイプ実証

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>プロトタイプ実証</h2>
<h3>フォトニック量子プロセッサ</h3>
<ul>
<li>集積量子フォトニクス技術による再構成可能な導波路チップ</li>
<li><strong>8個の電圧駆動位相シフタ</strong>で任意の2量子ビット純粋状態を準備</li>
<li>平均統計忠実度 $F > 99\%$（Shadbolt et al. 2011）</li>
<li>シリコン単光子検出器でフォトン計数</li>
</ul>
<blockquote>
<p>📊 Fig. 2（p.3）参照（原論文）— フォトニックチップの模式図</p>
</blockquote>
<h3>HeH⁺分子の結合解離曲線</h3>
<p>検証に選んだ問題: <strong>ヘリウム水素化物イオン（HeH⁺）</strong> の基底状態エネルギー</p>
<p>4×4 の全配置間相互作用（FCI）ハミルトニアン：</p>
<p>$$\mathcal{H}(R) = \sum_\alpha h^i_\alpha(R) \sigma^i_\alpha + \sum_{\alpha\beta} h^{ij}_{\alpha\beta}(R) \sigma^i_\alpha \sigma^j_\beta$$</p>
<ul>
<li>$R$: 原子核間距離</li>
<li>係数は PSI3 量子化学パッケージで計算</li>
</ul>
<h3>実験結果</h3>
<ul>
<li>核間距離 $R$ を変えながら基底状態エネルギーを計算</li>
<li><strong>化学精度（chemical accuracy: 1.6 mHa）以内で一致</strong></li>
<li>最適化の収束を実験的に実証</li>
</ul>
<blockquote>
<p>📊 Fig. 3（p.4）参照（原論文）— エネルギー収束の実証
📊 Fig. 4（p.4）参照（原論文）— HeH⁺ 結合解離曲線</p>
</blockquote>
<hr />

</details>

### 第5章: 考察と展望

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>考察と展望</h2>
<h3>VQE の位置づけ</h3>
<table>
<thead>
<tr>
<th>特性</th>
<th>QPE</th>
<th>VQE</th>
</tr>
</thead>
<tbody>
<tr>
<td>理論的コスト</td>
<td>指数的高速（精度保証）</td>
<td>変分近似（精度は ansatz 依存）</td>
</tr>
<tr>
<td>コヒーレンス要件</td>
<td>非常に高い</td>
<td><strong>大幅緩和</strong></td>
</tr>
<tr>
<td>現在の実装可能性</td>
<td>困難</td>
<td><strong>NISQ デバイスで実現可能</strong></td>
</tr>
<tr>
<td>スケーラビリティ</td>
<td>完全量子が必要</td>
<td>ハイブリッド量子古典</td>
</tr>
</tbody>
</table>
<ul>
<li><strong>NISQ（Noisy Intermediate-Scale Quantum）時代の代表的アルゴリズム</strong></li>
<li>今日の量子リソースを最大活用する実用的な道筋を示した</li>
</ul>
<h3>今後の課題と展望</h3>
<ul>
<li>より大きな分子への拡張: 多くの qubit とアンザッツが必要</li>
<li>ノイズへの耐性: NISQ デバイスではエラーが蓄積</li>
<li>最適化の難しさ: バレン高原（barren plateau）問題</li>
<li>ハードウェア効率的アンザッツ: UCC の代わりに回路に合ったアンザッツ</li>
<li><strong>本論文は量子古典ハイブリッドアルゴリズムの出発点となった</strong>（被引用数 6000+ ）</li>
</ul>
<h3>まとめ</h3>
<ul>
<li><strong>量子期待値推定</strong>: H をパウリ分解 → 多数の短い測定</li>
<li><strong>VQE</strong>: 変分原理 + アンザッツ + 古典最適化</li>
<li><strong>実証</strong>: フォトニックチップで HeH⁺ の基底状態エネルギーを化学精度で再現</li>
<li><strong>意義</strong>: NISQ 時代の量子化学計算の扉を開いた歴史的論文</li>
</ul>
<hr />

</details>

---

[← 論文一覧に戻る](../../)
