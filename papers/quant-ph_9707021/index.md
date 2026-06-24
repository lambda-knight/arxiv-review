---
title: "Kitaev「アニオンによる耐障害性量子計算」(quant-ph/9707021, 1997)"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# Kitaev「アニオンによる耐障害性量子計算」(quant-ph/9707021, 1997)

*著者**: A. Yu. Kitaev (L.D. Landau Institute for Theoretical Physics)*

- ID: quant-ph_9707021
- Internet Archive: [paper-explain-quant-ph-9707021](https://archive.org/details/paper-explain-quant-ph-9707021)

---

## 章別動画・解説

### 第1章: トーリックコードTOR(k) ── 定義と保護空間

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>トーリックコードTOR(k) ── 定義と保護空間</h2>
<ul>
<li>$k \times k$ 正方格子をトーラス上に描く。量子ビットは辺に配置（計 $n = 2k^2$ 個）</li>
<li><strong>頂点演算子</strong>（Section 1, 式1）
$$A_s = \prod_{j \in \mathrm{star}(s)} \sigma_x^j$$</li>
<li><strong>面演算子</strong>（Section 1, 式1）
$$B_p = \prod_{j \in \mathrm{boundary}(p)} \sigma_z^j$$</li>
<li>$[A_s, B_p] = 0$：star(s)とboundary(p)が辺を0または2本共有するため</li>
<li><strong>保護部分空間</strong>（式2）: $L = \{|\xi\rangle : A_s|\xi\rangle = |\xi\rangle,\ B_p|\xi\rangle = |\xi\rangle\ \forall s,p\}$</li>
<li>$\dim L = 4$（トーラス上）：独立安定化演算子は $m = 2k^2 - 2$ 個、$2^{n-m} = 4$</li>
<li>論理演算子: $Z_1, Z_2$（非収縮ループ沿いのZ積）、$X_1, X_2$（双対格子のX積）</li>
<li>明示的基底（式3）:
$$|\xi_{v_1,v_2}\rangle = 2^{-(k^2-1)/2} \sum_{\substack{z_1,\ldots,z_n \\ \sum_{j\in c_{z1}} z_j = v_1,\ \sum_{j\in c_{z2}} z_j = v_2}} |z_1,\ldots,z_n\rangle$$</li>
</ul>

</details>

### 第2章: コードの誤り訂正能力とハミルトニアンH₀

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>コードの誤り訂正能力とハミルトニアンH₀</h2>
<ul>
<li>TOR(k)は $k-1$ 個のエラーを検出、$\lfloor(k-1)/2\rfloor$ 個を訂正</li>
<li>証明: 非検出エラー $E \in G \setminus F$ のサポートは非収縮ループを含む → 最低 $k$ 辺必要</li>
<li>一定エラー率での回復不能確率 $\to 0$ as $\exp(-ak)$（式後半）</li>
<li>局所チェックコードの性質: ①各演算子は最大4量子ビット ②各量子ビットは最大4演算子 ③訂正数に上限なし</li>
<li><strong>ハミルトニアン</strong>（式4）:
$$H_0 = -\sum_s A_s - \sum_p B_p$$</li>
<li>基底状態 = 保護空間 $L$（エネルギーゼロ）、エネルギーギャップ $\Delta E \geq 2$</li>
<li><strong>摂動安定性</strong>: 分裂は $\exp(-aL)$ で消える（$L$ = 格子の最小次元）</li>
<li>仮想粒子のトンネル振幅 $b_{\alpha i} \sim \exp(-a_\alpha L_i)$、$a_\alpha \sim \sqrt{2m\Delta E}$</li>
</ul>

</details>

### 第3章: アーベルアニオン ── 電荷と磁気渦の統計

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>アーベルアニオン ── 電荷と磁気渦の統計</h2>
<ul>
<li><strong>z型粒子（電荷, electric charges）</strong>: $A_s = -1$ の頂点に現れる</li>
<li><strong>x型粒子（磁気渦, magnetic vortices）</strong>: $B_p = -1$ の面に現れる</li>
<li><strong>ひも演算子</strong>（式5）:
$$S_z(t) = \prod_{j \in t} \sigma_z^j, \quad S_x(t') = \prod_{j \in t'} \sigma_x^j$$</li>
<li>粒子は必ずペアで生まれる（$\prod_s A_s = 1$、$\prod_p B_p = 1$ から単独粒子は不可）</li>
<li><strong>アニオン統計</strong>: x型粒子がz型粒子を一周すると
$$|Ψ_{\mathrm{final}}\rangle = S_x(c)S_z(t)|\psi_x(q)\rangle = -|Ψ_{\mathrm{initial}}\rangle$$
  → 波動関数が $-1$ 倍（$S_x(c)$ と $S_z(t)$ は反可換、$S_x(c)|\psi_x(q)\rangle = |\psi_x(q)\rangle$）</li>
<li>アーベルアニオン = ブレイド群の非自明な1次元表現を実現する粒子</li>
<li>アハロノフ・ボーム効果として解釈可能</li>
<li>分数量子ホール効果（フィリング $p/q$）: 一周で $\exp(2\pi i/q)$ の位相</li>
<li>"Too few things can be done by moving abelian anyons"（論文原文）</li>
</ul>

</details>

### 第4章: 量子二重体D(G) ── 非アーベルアニオンの代数的基盤

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>量子二重体D(G) ── 非アーベルアニオンの代数的基盤</h2>
<ul>
<li>$G$: 有限群（一般に非アーベル）; $H = \mathbb{C}[G]$: 群代数（次元 $N = |G|$）</li>
<li><strong>4種類の演算子</strong>（式9）:
$$L_+^g|z\rangle = |gz\rangle,\quad L_-^g|z\rangle = |zg^{-1}\rangle$$
$$T_+^h|z\rangle = \delta_{h,z}|z\rangle,\quad T_-^h|z\rangle = \delta_{h^{-1},z}|z\rangle$$</li>
<li><strong>交換関係</strong>（式10）: $L_+^g T_+^h = T_{gh}^+ L_+^g$、$L_+^g T_-^h = T_{hg^{-1}}^- L_+^g$、等</li>
<li><strong>ゲージ・磁荷演算子</strong>（式11）:
$$A^g(s,p) = \prod_{j \in \mathrm{star}(s)} L^g(j,s), \quad B^h(s,p) = \sum_{h_1\cdots h_k = h} \prod_{m=1}^k T^{h_m}(j_m, p)$$</li>
<li><strong>対称化</strong>（式12）: $A(s) = N^{-1}\sum_{g \in G} A^g(s)$、$B(p) = B^1(s,p)$</li>
<li>$\{A^g(s,p), B^h(s,p)\}$ が生成する代数 = <strong>Drinfeld量子二重体 $D(G)$</strong></li>
<li><strong>ハミルトニアン</strong>（式13）:
$$H_0 = \sum_s (1 - A(s)) + \sum_p (1 - B(p))$$</li>
<li>粒子の型: $D(G)$ の既約表現 $(C, \chi)$（共役類 $C$ × 中心化群の既約表現 $\chi$）</li>
<li>$n$粒子励起空間 $L(x_1,\ldots,x_n)$ の次元 $= N^{2(n-1)}$</li>
</ul>

</details>

### 第5章: リボン演算子とホップ代数 ── 粒子対の生成と代数構造

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>リボン演算子とホップ代数 ── 粒子対の生成と代数構造</h2>
<ul>
<li>リボン $t$（格子上の帯）に対して $N^2$ 個のリボン演算子 $F^{(h,g)}(t)$（$g,h \in G$）（式24）</li>
<li>第1性質: $A(r), B(l)$（$r \neq s,s'$、$l \neq p,p'$）と可換</li>
<li>第2性質: 多粒子励起空間 $L(x_1,\ldots,x_n)$ への作用はリボンの位相類にのみ依存</li>
<li><strong>代数の積</strong>（式25）: $F^m(t)F^n(t) = \Lambda^k_{mn} F^k(t)$</li>
<li><strong>余積（comultiplication）</strong>（式26）:
$$F^k(t_1 t_2) = \Omega^k_{mn} F^m(t_1) F^n(t_2)$$</li>
<li>$D$ の余積（式27）: $\Delta(D^k) = \Lambda^{mn}_k D^m \otimes D^n$</li>
<li>$D$ と $F$ は互いに双対なホップ代数</li>
<li><strong>R行列</strong>（式39）:
$$R^{(h,g)}_{(v,u)} = \delta_{h,u}\,\delta_{g,1}$$</li>
<li>交換関係（式38）: $F^{(h,g)}(t_1)F^{(v,u)}(q_1) = F^{(v,u)}(q_1)F^{(v^{-1}hv,\,v^{-1}g)}(t_1)$</li>
</ul>

</details>

### 第6章: ブレイディングと融合 ── Section 6の位相的演算子

<video controls width="100%" src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch06.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-quant-ph-9707021/paper_quant-ph_9707021_ch06.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>ブレイディングと融合 ── Section 6の位相的演算子</h2>
<ul>
<li><strong>位相的演算子</strong>: すべての $D(x_j)$ と可換な $L(x_1,\ldots,x_n)$ 上の演算子</li>
<li><strong>反時計回りブレイディング演算子</strong>（式57）:
$$R^{\circlearrowleft} = R^{ji}(D'_i \otimes D'_j)\sigma$$</li>
<li><strong>磁気渦のブレイディング</strong>（式58）:
$$R^{\circlearrowleft}|v_1, v_2\rangle = |v_1 v_2 v_1^{-1},\, v_1\rangle$$</li>
<li><strong>融合は余積 $\Delta$ で記述</strong>（式59）:
$$\Delta(D'_{(h,g)})|v, v^{-1}\rangle = \delta_{h,1}|gvg^{-1},\, gv^{-1}g^{-1}\rangle$$
  反対の磁気渦が融合 → 磁荷なし・電荷あり（型 $(C,\chi)$ で $C=\{1\}$、$\chi$ = 随伴表現）</li>
</ul>

</details>

---

[← 論文一覧に戻る](../../)
