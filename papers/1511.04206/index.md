---
title: "量子アルゴリズム概観【Montanaro 2016 解説】"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 量子アルゴリズム概観【Montanaro 2016 解説】

*> 本文HTMLは未取得のため、abstract および本論文の既知の内容をもとに解説しています*

- arXiv: [1511.04206](https://arxiv.org/abs/1511.04206)
- Internet Archive: [paper-explain-1511-04206](https://archive.org/details/paper-explain-1511-04206)

---

## 概要

量子コンピュータで使われる主要アルゴリズムの全体像を4章に分けて完全解説。Ashley Montanaroの「Quantum algorithms: an overview」（npj Quantum Information 2016）をベースに、ずんだもん＆四国めたんが量子フーリエ変換・振幅増幅・ハミルトニアンシミュレーション・HHLを数式とともに丁寧に説明します。

▼ 章別動画ラインナップ
・量子アルゴリズムとは何か — 重ね合わせ・もつれ・干渉・計算複雑性の基礎
・暗号解読：ショアのアルゴリズム — 素因数分解・量子フーリエ変換・耐量子暗号
・探索と最適化：グローバーとその発展 — 振幅増幅・量子ウォーク・QAOA
・量子系のシミュレーション — トロッター分解・VQE・FeMoCo・量子化学
・線形方程式系とNISQ時代 — HHL・細字条件・誤り訂正・量子優位性の現状

▼ 参考文献
https://arxiv.org/abs/1511.04206 — Ashley Montanaro, "Quantum algorithms: an overview", npj Quantum Information 2, 15023 (2016)

#量子コンピュータ #量子アルゴリズム #ショアのアルゴリズム #グローバー #HHL #量子フーリエ変換 #振幅増幅 #VQE #量子化学 #論文解説 #ゆっくり解説 #ずんだもん #NISQ #数式でわかる

---

## 章別動画・解説

### 第1章: 量子アルゴリズムとは何か

<video controls width="100%" src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子アルゴリズムとは何か</h2>
<ul>
<li>量子コンピュータは<strong>重ね合わせ・量子もつれ・干渉</strong>を利用して古典計算を超える</li>
<li>量子優位性のある主要領域: 暗号解読・探索と最適化・量子シミュレーション・線形方程式系</li>
</ul>
<p>$n$ 量子ビットの状態空間は $2^n$ 次元:
$$|\psi\rangle = \sum_{x \in \{0,1\}^n} \alpha_x |x\rangle, \quad \sum_x |\alpha_x|^2 = 1$$</p>
<ul>
<li>$|\psi\rangle$: $n$ 量子ビットの純粋状態</li>
<li>$\alpha_x$: 基底 $|x\rangle$ の確率振幅（複素数）</li>
<li>測定確率: $|\alpha_x|^2$</li>
</ul>
<p><strong>量子優位性の源泉:</strong>
1. <strong>重ね合わせ</strong>: $n$ 量子ビットで $2^n$ の状態を同時表現
2. <strong>量子もつれ</strong>: 複数量子ビット間の非古典的相関
3. <strong>干渉</strong>: 正しい答えへの振幅を強め、誤りを打ち消す</p>
<p><strong>計算複雑性による優位性の分類:</strong>
- クエリ複雑性: オラクルへの問い合わせ回数
- ゲート複雑性: 量子ゲートの総数（実行時間に近い）</p>

</details>

### 第2章: 暗号解読：ショアのアルゴリズム

<video controls width="100%" src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>暗号解読：ショアのアルゴリズム</h2>
<ul>
<li><strong>ショアのアルゴリズム（1994）</strong>: 整数の素因数分解を多項式時間で解く</li>
<li>古典最速（数体篩法）: $e^{O(N^{1/3})}$（指数時間）</li>
<li>量子（ショア）: $O((\log N)^3)$（多項式時間）— <strong>指数的高速化</strong></li>
</ul>
<p>位数発見の核心:
$$a^r \equiv 1 \pmod{N}, \quad \gcd\!\left(a^{r/2} \pm 1, N\right) = \text{素因数}$$</p>
<ul>
<li>$N$: 分解したい整数、$a$: $N$ と互いに素なランダム整数</li>
<li>量子フーリエ変換（QFT）で周期 $r$（位数）を効率よく取り出す</li>
<li>$r$ が偶数のとき、$a^{r/2} \pm 1$ と $N$ の最大公約数が因数</li>
</ul>
<p><strong>影響を受ける暗号:</strong>
| 暗号 | 困難問題 | 量子への対処 |
|------|---------|------------|
| RSA | 素因数分解 | 破られる |
| 楕円曲線暗号 | 離散対数 | 破られる |
| AES | 総当たり（Grover二次加速） | 鍵長2倍で対応可 |</p>
<p><strong>耐量子暗号（PQC）</strong>: NIST が 2024 年に格子ベース等の標準を確定</p>

</details>

### 第3章: 探索と最適化：グローバーとその発展

<video controls width="100%" src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>探索と最適化：グローバーとその発展</h2>
<ul>
<li><strong>グローバーのアルゴリズム（1996）</strong>: $N$ 件の非構造化探索を $O(\sqrt{N})$ で解く（古典 $O(N)$）</li>
<li>最適性証明: $\Omega(\sqrt{N})$ が量子クエリ複雑性の下限</li>
</ul>
<p>振幅増幅の1ステップ:
$$|\psi\rangle \xrightarrow{O} \text{正解に位相反転} \xrightarrow{D} \text{平均周りに反転}$$</p>
<ul>
<li>正解の確率振幅を毎回 $O(1/\sqrt{N})$ ずつ増幅</li>
<li>約 $\frac{\pi}{4}\sqrt{N}$ 回の反復で確率 $\approx 1$</li>
</ul>
<p><strong>量子ウォーク（Quantum Walk）:</strong>
- グラフ上の量子版ランダムウォーク
- マルコフ連鎖のスペクトルギャップ $\delta$ を二次改善: $\delta_Q \approx \sqrt{\delta_C}$
- 三角形探索: 古典 $O(N^2)$ → 量子 $O(N^{4/3})$</p>
<p><strong>QAOA（量子近似最適化アルゴリズム）:</strong>
$$|\gamma, \beta\rangle = \prod_{p=1}^{P} e^{-i\beta_p B} e^{-i\gamma_p C} |+\rangle^{\otimes n}$$</p>
<ul>
<li>$C$: コスト演算子（目的関数）、$B$: ミキサー演算子</li>
<li>NISQ デバイス向け変分アルゴリズム; 組み合わせ最適化に適用</li>
</ul>

</details>

### 第4章: 量子系のシミュレーション

<video controls width="100%" src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子系のシミュレーション</h2>
<ul>
<li>ファインマン提案（1982）: 量子系のシミュレーションには量子コンピュータが自然</li>
<li>$n$ 粒子系は $2^n$ 次元 → 古典では指数的メモリ・時間が必要</li>
</ul>
<p>ハミルトニアン時間発展（積公式/トロッター分解）:
$$e^{-iHt} \approx \left(\prod_k e^{-iH_k t/r}\right)^r, \quad H = \sum_k H_k$$</p>
<ul>
<li>$H_k$: 各項のハミルトニアン（局所的・スパース）</li>
<li>1次トロッター誤差 $O(t^2/r)$; 高次公式で精度向上</li>
<li>必要ゲート数は時間 $t$ と精度 $\epsilon$ に多項式</li>
</ul>
<p><strong>変分量子固有値ソルバー（VQE）:</strong>
$$E_0 \leq \langle\psi(\theta)|H|\psi(\theta)\rangle$$</p>
<ul>
<li>$|\psi(\theta)\rangle$: パラメータ $\theta$ の変分量子回路（アンザッツ）</li>
<li>古典最適化で $\theta$ を更新し基底エネルギー $E_0$ に接近</li>
<li>NISQ デバイスで量子化学計算に使用</li>
</ul>
<p><strong>応用例:</strong>
- FeMoCo（鉄モリブデンコファクター）: 窒素固定触媒の電子構造計算
- 高温超伝導体・ペロブスカイト材料の設計
- 創薬: タンパク質-薬分子相互作用のシミュレーション</p>

</details>

### 第5章: 線形方程式系とNISQ時代

<video controls width="100%" src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-1511-04206/paper_1511.04206_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>線形方程式系とNISQ時代</h2>
<p><strong>HHL アルゴリズム（Harrow-Hassidim-Lloyd 2009）:</strong></p>
<p>$$Ax = b \quad \Rightarrow \quad |x\rangle \propto A^{-1}|b\rangle$$</p>
<table>
<thead>
<tr>
<th></th>
<th>計算量</th>
<th>$N$ 依存性</th>
</tr>
</thead>
<tbody>
<tr>
<td>古典（共役勾配法）</td>
<td>$O(N\kappa\log(1/\epsilon))$</td>
<td>$N$ に比例</td>
</tr>
<tr>
<td>量子（HHL）</td>
<td>$O(\kappa^2 \log N / \epsilon^2)$</td>
<td>$\log N$ — 指数的高速化</td>
</tr>
</tbody>
</table>
<ul>
<li>$\kappa$: 条件数（最大/最小固有値比）</li>
<li><strong>制約（細字条件）</strong>: 解を全て読み出すと $O(N)$ かかる</li>
<li>有効な用途: 内積・期待値計算、量子系のアウトプット</li>
</ul>
<p><strong>NISQ 時代の現状:</strong>
- 物理ゲートエラー率: 0.1〜1%（深い回路では誤差蓄積）
- Google（2023）表面符号で「しきい値定理」を実証
  - 物理量子ビット増加 → 論理エラー指数的減少を確認
- 論理量子ビット1つに物理量子ビット数千が必要</p>
<p><strong>量子優位性の厳密な実証は現在も進行中:</strong>
- VQE/QAOA: NISQ デバイスで実行可能だが古典との差が不明確
- 脱量子化（dequantization）: 量子機械学習の一部は古典でも同等と判明
- 量子化学シミュレーションが「最初の実用的量子優位性」の最有力候補</p>
<p><strong>近未来のロードマップ:</strong>
- 2020年代後半: フォールトトレラント量子コンピュータの初期実証
- 2030年代以降: 実用規模での量子化学・材料設計への応用</p>

</details>

---

[← 論文一覧に戻る](../../)
