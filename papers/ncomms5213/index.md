---
title: "フォトニック量子プロセッサ上の変分固有値ソルバー（VQE）"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

### 第1章: 導入：量子固有値問題と既存手法の限界

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>導入：量子固有値問題と既存手法の限界</h2>
<h3>なぜ固有値問題が重要か</h3>
<ul>
<li>原子・分子の性質はシュレーディンガー方程式の固有値（エネルギー）を解くことで決まる</li>
<li>系の規模が指数関数的に拡大 → 古典コンピュータでは2〜3原子以上は厳密解が困難</li>
<li>量子化学以外でも、検索エンジン最適化・新材料設計・創薬にも固有値問題が現れる</li>
</ul>
<h3>既存の量子アプローチ：QPE（量子位相推定）の問題点</h3>
<ul>
<li>QPE（量子位相推定）は固有値を指数的高速で計算できる</li>
<li>しかし精度 $p$ を得るためには $O(1/p)$ 回の $e^{-i\mathcal{H}t}$ 演算が必要</li>
<li>実用的な4×4行列でも最低12個のCNOTゲートが必要</li>
<li>現在のデバイスでは数十〜数百ゲートが限界 → QPEは近未来には非現実的</li>
</ul>
<h3>本論文の提案：VQE（変分量子固有値ソルバー）</h3>
<p>2つのアルゴリズムの組み合わせ：</p>
<table>
<thead>
<tr>
<th>アルゴリズム</th>
<th>担当</th>
<th>計算の場所</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Algorithm 1</strong>: 量子期待値推定</td>
<td>$\langle\mathcal{H}\rangle$ の計算</td>
<td>量子プロセッサ（QPU）</td>
</tr>
<tr>
<td><strong>Algorithm 2</strong>: 量子変分固有値ソルバー</td>
<td>パラメータ最適化</td>
<td>古典プロセッサ（CPU）</td>
</tr>
</tbody>
</table>
<ul>
<li>QPEの「長いコヒーレント発展」をなくし、<strong>短いコヒーレント発展を多数回繰り返す</strong>方式に変換</li>
<li>今日・近未来の量子デバイスで実現可能</li>
</ul>
<blockquote>
<p>📊 Fig. 1 参照（原論文）— QPUとCPUのハイブリッドアーキテクチャ</p>
</blockquote>
<hr />

</details>

### 第2章: Algorithm 1：ハミルトニアン期待値の効率的な計算

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Algorithm 1：ハミルトニアン期待値の効率的な計算</h2>
<h3>ハミルトニアンのパウリ分解</h3>
<p>任意のハミルトニアンはパウリ演算子の積の和として書ける（式1）：</p>
<p>$$\mathcal{H} = \sum_{i\alpha} h^i_\alpha \sigma_\alpha^i + \sum_{ij\alpha\beta} h^{ij}_{\alpha\beta} \sigma_\alpha^i \sigma_\beta^j + \cdots$$</p>
<ul>
<li>ローマ字インデックス $i, j$：演算子が作用する部分空間</li>
<li>ギリシャ字インデックス $\alpha, \beta$：パウリ演算子の種類（$x, y, z$）</li>
<li>係数 $h^i_\alpha, h^{ij}_{\alpha\beta}$ は実数</li>
</ul>
<p>期待値の線形性により（式2）：</p>
<p>$$\langle\mathcal{H}\rangle = \sum_{i\alpha} h^i_\alpha \langle\sigma_\alpha^i\rangle + \sum_{ij\alpha\beta} h^{ij}_{\alpha\beta} \langle\sigma_\alpha^i \sigma_\beta^j\rangle + \cdots$$</p>
<h3>なぜ量子コンピュータが効率的か</h3>
<ul>
<li>量子ハードウェアはパウリ積の期待値を一定時間で測定できる</li>
<li>必要な繰り返し回数は $O(|h|^2/p^2)$（$p$ は精度）</li>
<li><strong>コヒーレンス時間は $O(1)$（1回の測定で十分）</strong>：QPEの $O(1/p)$ と対照的</li>
<li>指数的な量子優位性を保ちながら、コヒーレンス要件を劇的に削減</li>
</ul>
<h3>古典計算との比較</h3>
<table>
<thead>
<tr>
<th></th>
<th>量子（このアルゴリズム）</th>
<th>古典</th>
</tr>
</thead>
<tbody>
<tr>
<td>状態保持</td>
<td>$n$ 量子ビット</td>
<td>$2^n$ 複素数</td>
</tr>
<tr>
<td>期待値計算</td>
<td>$O(|h|^2 M/p^2)$ 繰り返し</td>
<td>$O(2^n)$ 浮動小数点演算</td>
</tr>
<tr>
<td>規模依存</td>
<td>多項式</td>
<td>指数的</td>
</tr>
</tbody>
</table>
<ul>
<li>$n$ 量子ビットで $2^n \times 2^n$ のハミルトニアン期待値を効率計算</li>
<li>N-表現可能性問題（NP困難）が量子ハードウェアでは自然に回避される</li>
</ul>
<hr />

</details>

### 第3章: Algorithm 2：変分最適化によるアンザッツ状態の準備

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Algorithm 2：変分最適化によるアンザッツ状態の準備</h2>
<h3>変分原理の活用</h3>
<p>レイリー・リッツ商の最小化（式3）：</p>
<p>$$\min_{|\psi\rangle} \frac{\langle\psi|\mathcal{H}|\psi\rangle}{\langle\psi|\psi\rangle}$$</p>
<ul>
<li>最小値を与える $|\psi\rangle$ が基底状態</li>
<li>実験パラメータ $\{\theta_i\}$ で $|\psi(\{\theta_i\})\rangle$ を準備 → Algorithm 1 で期待値計算 → CPUで最小化</li>
</ul>
<h3>ユニタリ連結クラスター（UCC）アンザッツ（式4）</h3>
<p>$$|\Psi\rangle = e^{T - T^\dagger}|\Phi\rangle_{\rm ref}$$</p>
<ul>
<li>$|\Phi\rangle_{\rm ref}$：参照状態（通常はハートリー・フォック基底状態）</li>
<li>$T = T_1 + T_2 + \cdots + T_N$：クラスター演算子</li>
<li>$T_1 = \sum_{pr} t_p^r \hat{a}_p^\dagger \hat{a}_r$（1粒子励起）</li>
<li>$T_2 = \sum_{pqrs} t_{pq}^{rs} \hat{a}_p^\dagger \hat{a}_q^\dagger \hat{a}_r \hat{a}_s$（2粒子励起）</li>
<li>$(T - T^\dagger)$ は反エルミート → $e^{T-T^\dagger}$ はユニタリ</li>
<li>古典コンピュータでは効率的アルゴリズムが知られていない → 量子優位性の具体例</li>
</ul>
<h3>アルゴリズムのループ</h3>
<ol>
<li>量子回路パラメータ $\{\theta_i^n\}$ で状態 $|\psi^n\rangle$ を準備</li>
<li>Algorithm 1 で $\langle\mathcal{H}\rangle = f(\{\theta_i^n\})$ を計算</li>
<li>CPUの最小化アルゴリズム（Nelder-Mead 単体法）が次のパラメータ $\{\theta_i^{n+1}\}$ を決定</li>
<li>収束まで繰り返す</li>
</ol>
<blockquote>
<p>📊 Fig. 2 参照（原論文）— 実験装置（フォトニックチップ）の模式図と写真</p>
</blockquote>
<hr />

</details>

### 第4章: 実験実装：フォトニック量子回路

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>実験実装：フォトニック量子回路</h2>
<h3>量子プロセッサの構成</h3>
<ul>
<li><strong>集積フォトニクス技術</strong>（ブリストル大学・O'Brienグループ）</li>
<li>自発パラメトリック下方変換で光子対を生成、導波路に入射して $|00\rangle$ を準備</li>
<li>8個の電圧制御熱位相シフタ $\phi_{1-8}$ と1個のCNOTゲートで任意の2量子ビット純粋状態を準備</li>
<li>光子検出器 D1〜D4 の同時計数率をCPUへ送信</li>
<li>平均統計忠実度 $F \geq 99\%$（Shadbolt et al. 2011）</li>
</ul>
<h3>実験対象：He-H+ の結合解離曲線</h3>
<p>フルCI（完全配置間相互作用）ハミルトニアン（4次元 = 2量子ビット）（式5）：</p>
<p>$$\mathcal{H}(R) = \sum_{i\alpha} h^i_\alpha(R) \sigma_\alpha^i + \sum_{ij\alpha\beta} h^{ij}_{\alpha\beta}(R) \sigma_\alpha^i \sigma_\beta^j$$</p>
<ul>
<li>係数は PSI3 計算化学パッケージで算出（最小基底 STO-3G）</li>
<li>核間距離 $R$ をパラメータとして変化させ、各 $R$ での基底状態エネルギーを計算</li>
<li>QPEによる同等計算では最低12 CNOTゲートが必要 → 本手法では <strong>1 CNOT</strong> のみ</li>
</ul>
<h3>QPEとの計算コスト比較</h3>
<table>
<thead>
<tr>
<th></th>
<th>QPE</th>
<th>このアルゴリズム</th>
</tr>
</thead>
<tbody>
<tr>
<td>CNOT数</td>
<td>≥ 12</td>
<td><strong>1</strong></td>
</tr>
<tr>
<td>コヒーレンス要件</td>
<td>長時間（$O(1/p)$）</td>
<td>短時間×多数回</td>
</tr>
<tr>
<td>補助量子ビット</td>
<td>必要</td>
<td>不要</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第5章: 実験結果：化学精度での基底状態エネルギー計算

<video controls width="100%" src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-ncomms5213/paper_ncomms5213_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>実験結果：化学精度での基底状態エネルギー計算</h2>
<h3>代表的な最適化実行（$R = 90$ pm）</h3>
<ul>
<li>Algorithm 2 を実行し、$\langle\mathcal{H}(R)\rangle$ を最小化</li>
<li>最適化は基底状態エネルギーに収束</li>
<li>各ステップでのタングル（量子もつれの度合い）も追跡</li>
<li>基底状態は小さいがゼロでないタングルを持つ（量子もつれが必要）</li>
</ul>
<blockquote>
<p>📊 Fig. 3 参照（原論文）— エネルギー収束と重なり積分の最適化過程</p>
</blockquote>
<h3>結合解離曲線（$R = 80〜100$ pm の79点）</h3>
<p>測定された平衡結合距離と基底状態エネルギー：</p>
<p>$$R_{\rm eq} = 92.3 \pm 0.1 \text{ pm}, \quad E_0 = -2.865 \pm 0.008 \text{ MJ/mol}$$</p>
<ul>
<li><strong>96%以上のデータ点が化学精度内</strong>（理論値との誤差 &lt; 化学精度）</li>
<li>系統誤差 $\varepsilon = 50$ KJ/mol を補正済み</li>
<li>解の再現性：最適化終了後、実験パラメータから状態を効率的に再構築可能</li>
</ul>
<blockquote>
<p>📊 Fig. 4 参照（原論文）— He-H+ の結合解離曲線</p>
</blockquote>
<h3>誤差の原因（付録：実験詳細）</h3>
<table>
<thead>
<tr>
<th>誤差の種類</th>
<th>原因</th>
<th>将来の改善法</th>
</tr>
</thead>
<tbody>
<tr>
<td>統計誤差（$\sigma \approx 37$ KJ/mol）</td>
<td>光子のポアソン統計</td>
<td>測定回数増加で低減</td>
</tr>
<tr>
<td>系統誤差（$\varepsilon = 50$ KJ/mol）</td>
<td>① 光源の不純度（高次光子数項）<br>② チップ設計誤差<br>③ 結合効率のアンバランス</td>
<td>① 真の単一光子源<br>② 製造精度向上<br>③ ファイバー固定技術</td>
</tr>
</tbody>
</table>
<ul>
<li>平均同時計数率 2000〜4000 events/秒</li>
<li>全解離曲線測定に約158時間（冷却サイクルが律速、デューティサイクル〜5%）</li>
</ul>
<hr />

</details>

