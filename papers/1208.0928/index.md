---
title: "表面符号 ── 大規模量子コンピュータへの実践的アプローチ"
layout: default
---

# 表面符号 ── 大規模量子コンピュータへの実践的アプローチ

*Austin G. Fowler, Matteo Mariantoni, John M. Martinis, Andrew N. Cleland (2012)*

- arXiv: [1208.0928](https://arxiv.org/abs/1208.0928)
- Internet Archive: [lk-paper-1208-0928](https://archive.org/details/lk-paper-1208-0928)

---

## 概要

Fowler et al. 2012「Surface codes: Towards practical large-scale quantum computation」（arXiv:1208.0928）の第1章を深く読み解きます。量子ビットが脆い理由から、ショアのアルゴリズムに必要な物理量子ビット約400万個という試算まで、数式と対話で丁寧に解説。

▼ 第1章の内容
・なぜ量子エラー訂正が必要か（デコヒーレンス・ゲートエラー）
・古典エラー訂正が量子に使えない2つの理由（no-cloning定理・測定崩壊）
・X/Z/Yエラーの3種類と位相エラーの難しさ
・符号距離dと物理量子ビット数 n ≈ 2d² の関係
・論理エラー率の指数的スケーリング（d=25 で 10の-15乗）
・ショアのアルゴリズム実行に必要な物理量子ビット約400万個の試算
・1サイクル1マイクロ秒・実行時間数時間の試算
・表面符号の3つの強み：近傍のみ・閾値1%・スケーラブル
・現在の量子コンピュータ（Google Willow 105個）との比較

▼ 原論文（arXiv）
https://arxiv.org/abs/1208.0928 — 表面符号：大規模量子コンピュータへの実践的アプローチ

#量子コンピュータ #量子誤り訂正 #表面符号 #arxiv #論文解説 #ゆっくり解説 #ずんだもん #量子情報 #量子力学 #IBM #Google #フォールトトレラント #量子ビット #機械学習 #テクノロジー

---

## 章別動画・解説

### 第1章: Part 1: 導入と規模推計

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch01.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 1: 導入と規模推計

### なぜ量子エラー訂正が必要か（§I）

- 物理量子ビットは**デコヒーレンス**（環境との結合で量子状態が崩れる）と**ゲートエラー**の2種類の欠陥を持つ
- 現実のゲートエラー率：超伝導量子ビットで 0.1〜1%（古典コンピュータの $10^{18}$ 分の1に比べ 16桁悪い）
- **量子エラーの種類**：ビット反転 $X$、位相反転 $Z$、両方同時の $Y=iXZ$（古典の1種類に対し3種類）
- Shor のアルゴリズム（RSA-2048 の素因数分解）：$\approx 10^9$ ゲート操作が必要
- エラー率 0.1% で $10^9$ 回操作 → エラー **100 万回**：エラー訂正なしでは実用不可能

### 古典 vs 量子のエラー訂正

| | 古典 | 量子 |
|--|------|------|
| コピー | OK（繰り返し符号） | **不可**（no-cloning 定理） |
| 測定 | 状態を壊さない | **崩れる**（射影測定） |
| エラー種別 | ビット反転のみ | $X$（反転）＋$Z$（位相）＋$Y$ の 3種 |
| エラー検出法 | 直接読み出し | スタビライザー（状態を壊さずシンドロームだけ取得） |

### 規模の推計（§II）

> 📊 Fig. 1 参照（原論文）

**符号距離 $d$**：表面符号格子の一辺サイズ（同時に訂正できるエラー数 $\lfloor(d-1)/2\rfloor$）

$$n_{\text{phys}} \approx 2d^2 \quad (\text{1論理量子ビットあたり物理量子ビット数})$$

論理エラー率のスケーリング（物理エラー率 $p$ が閾値 $p_{\rm th} \approx 1\%$ 以下のとき）：

$$p_L \approx A \left(\frac{p}{p_{\rm th}}\right)^{\lceil d/2 \rceil}$$

- $d = 25$ のとき：$p_L \approx 10^{-15}$（$10^9$ ゲート操作に耐えられる）
- 必要な物理量子ビット：$2d^2 \approx 1{,}250$ 個（1論理量子ビットあたり）
- Shor（RSA-2048）：論理量子ビット $\approx 2{,}000$ 個 → 基本部 **250万個**
- マジック状態蒸留ファクトリー込みの総計：物理量子ビット **≈ 400 万個**

**実行時間の試算：**

- 1サイクル（スタビライザー測定一回）$\approx 1 \, \mu\text{s}$（ゲート 100 ns + 読み出し 900 ns）
- Shor 必要サイクル数：$\approx 10^9$ → 基本計算 **≈ 1000 秒**
- マジック状態蒸留込み実効時間：**≈ 数時間〜数日**（閾値・蒸留段数依存）

**現状（2024）との比較：**

| 実装 | 物理量子ビット数 |
|------|----------------|
| Google Willow (2024) | 105 個 |
| 必要 (Shor RSA-2048) | ≈ 400 万個 |
| スケールアップ倍率 | **≈ 40,000 倍** |

### 表面符号の 3 つの強み

| 強み | 内容 | 意義 |
|------|------|------|
| 近傍相互作用のみ | 隣接4量子ビット操作で完結 | 超伝導・中性原子等のプラットフォームで製造しやすい |
| 高い誤り閾値 | $p_{\rm th} \approx 1\%$（他の多くの符号より高い） | 現行の物理エラー率（0.1〜0.5%）はすでに閾値以下 |
| スケーラブル | $d$ を大きくするだけで論理エラーが指数的に改善 | 設計変更不要で規模拡大可能 |

---


</details>

### 第2章: Part 2: スタビライザーと表面符号

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch02.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 2: スタビライザーと表面符号

### パウリ演算子（§III）

$$
X = \begin{pmatrix}0&1\\1&0\end{pmatrix},\quad
Z = \begin{pmatrix}1&0\\0&-1\end{pmatrix},\quad
Y = iXZ = \begin{pmatrix}0&-i\\i&0\end{pmatrix}
$$

- $X$：ビット反転，$Z$：位相反転
- **反可換**：$XZ = -ZX$（この非可換性がエラー検出の鍵）
- パウリ群：$\{I, X, Y, Z\}^{\otimes n}$（$n$ 量子ビット系）

### スタビライザーの定義

量子状態 $|\psi\rangle$ を固有値 $+1$ で安定化する演算子 $S$：

$$S|\psi\rangle = +|\psi\rangle$$

エラー $E$ が起きると（$E$ が $S$ と反可換なら）：

$$S(E|\psi\rangle) = -E(S|\psi\rangle) = -(E|\psi\rangle)$$

固有値が $-1$ に反転 → **エラーを状態を崩さずに検出**

### 2量子ビットの例（§III）

$S_1 = ZZ$，$S_2 = XX$ でベル状態 $|\Phi^+\rangle = \frac{|00\rangle+|11\rangle}{\sqrt{2}}$ を安定化

- $X_1$ エラー → $S_1 = ZZ$ の測定値が $-1$ に → 検出！量子状態は破壊されない
- 量子情報は $Z_1Z_2$ と $X_1X_2$ の固有空間に「エンコード」されている

### 表面符号のスタビライザー（§IV）

> 📊 Fig. 2, 3 参照（原論文）

$d \times d$ 格子上に量子ビットを配置（辺上に1個ずつ）：

$$A_v = \prod_{i \in \partial v} X_i \qquad (\text{頂点プラケット：位相エラー検出})$$

$$B_p = \prod_{i \in \partial p} Z_i \qquad (\text{面プラケット：ビット反転エラー検出})$$

- $[A_v, B_p] = 0$（常に可換 → 同時測定可能、論理状態を壊さない）
- 正常状態：全プラケット測定値 $= +1$（シンドロームはすべて 0）

```
● ─X─ ● ─X─ ●
|      |      |
Z  Bp  Z  Bp  Z
|      |      |
● ─X─ ● ─X─ ●
```

---


</details>

### 第3章: Part 3: 欠陥と論理量子ビットの初期化・測定

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch03.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 3: 欠陥と論理量子ビットの初期化・測定

### 欠陥（Defect）とは（§V）

> 📊 Fig. 4, 5 参照（原論文）

格子上の一部のプラケット測定をあえて止めると「**欠陥（穴）**」が生まれる：

- **$d$タイプ欠陥**：$B_p$（$Z$プラケット）を止めた穴
- **$p$タイプ欠陥**：$A_v$（$X$プラケット）を止めた穴
- 同タイプの欠陥ペアで **論理量子ビット 1個** を定義

論理演算子：

$$\bar{X} = \prod_{i \in \text{欠陥間の鎖}} X_i, \qquad \bar{Z} = \prod_{i \in \text{欠陥周囲}} Z_i$$

### 論理量子ビットの初期化・測定（§VI）

> 📊 Fig. 6 参照（原論文）

| 操作 | 手順 |
|------|------|
| $|\bar{0}\rangle$ 初期化 | 全データ量子ビットを $|0\rangle$ にセット → スタビライザー測定 $d$ 回 |
| $|\bar{+}\rangle$ 初期化 | 全データ量子ビットを $|+\rangle$ にセット → スタビライザー測定 $d$ 回 |
| $\bar{Z}$ 測定 | $d$タイプ欠陥間のデータ量子ビットを $Z$ 測定（情報は消滅） |
| $\bar{X}$ 測定 | $p$タイプ欠陥を囲む量子ビットを $X$ 測定（情報は消滅） |

- 測定ノイズを考慮して **$d$ 回繰り返し測定**して多数決

---


</details>

### 第4章: Part 4: 論理量子ビットの移動とブレイド

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch04.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 4: 論理量子ビットの移動とブレイド

### 論理量子ビットの移動（§VII）

> 📊 Fig. 7, 8 参照（原論文）

欠陥を格子上で「滑らせる」ことで論理量子ビットを移動：

1. 移動先のプラケット測定を停止（穴を拡張）
2. 元の位置の測定を再開（穴を縮小）
3. 移動中もスタビライザー測定を継続 → **フォールトトレラント**

移動コスト：距離 $\ell$ の移動に $O(\ell \cdot d)$ サイクル

### ブレイドによる論理 CNOT（§VIII）

> 📊 Fig. 9, 10, 11 参照（原論文）

制御量子ビット（$d$型欠陥）を標的量子ビット（$p$型欠陥）の**周りを一周**させる：

$$|c\rangle|\psi\rangle \xrightarrow{\text{braid}} |c\rangle\, X^c|\psi\rangle \quad (\text{論理 CNOT})$$

- **位相的操作**：経路の細部が変わっても結果は不変（トポロジカル保護）
- 局所エラーに対して本質的に頑健
- ゲートコスト：$O(d^2)$ サイクル

---


</details>

### 第5章: Part 5: HゲートとSゲートとTゲート

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch05.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 5: HゲートとSゲートとTゲート

### Hadamard ゲート（§IX）

> 📊 Fig. 12 参照（原論文）

$$H = \frac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix}, \quad HXH^\dagger = Z,\quad HZH^\dagger = X$$

表面符号での実現：格子を **90°回転** → $X$プラケットと$Z$プラケットが入れ替わる（物理的には量子ビットの再ラベリング）

### $S$ ゲート（§X）

> 📊 Fig. 13 参照（原論文）

$$S = \begin{pmatrix}1&0\\0&i\end{pmatrix} = \sqrt{Z}$$

アンシラ量子ビットとの**測定ベース操作**で実現：アンシラ準備 → CNOT → $X$ 測定 → パウリ補正

### $T$ ゲート（§XI）

$$T = \begin{pmatrix}1&0\\0&e^{i\pi/4}\end{pmatrix} = \sqrt{S}$$

- **スタビライザー形式の外**にあるゲート → 直接フォールトトレラントに実現不可
- マジック状態を使った「状態注入（state injection）」で実現：

$$|T\rangle = T|+\rangle = \frac{|0\rangle + e^{i\pi/4}|1\rangle}{\sqrt{2}}$$

$|T\rangle$ を消費することで $T$ ゲートを 1 回適用できる

---


</details>

### 第6章: Part 6: マジック状態蒸留と物理実装

<video controls width="100%" src="https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp4"></video>

[Internet Archive で開く](https://archive.org/download/lk-paper-1208-0928/paper_1208.0928_ch06.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

## Part 6: マジック状態蒸留と物理実装

### マジック状態蒸留（§XII）

> 📊 Fig. 14, 15 参照（原論文）

低品質な $|T\rangle$（エラー率 $p_{\rm in}$）を多数消費して高品質な $|T\rangle$ を生成：

**15-to-1 蒸留プロトコル：**

$$p_{\rm out} \approx 35\, p_{\rm in}^3$$

- 15 個の低品質 $|T\rangle$ を消費して 1 個の高品質 $|T\rangle$ を出力
- エラー率が 3 乗で改善（$p_{\rm in} = 10^{-3}$ → $p_{\rm out} \approx 3.5 \times 10^{-8}$）
- 必要に応じて **多段蒸留**（第1段の出力を第2段の入力に使う）

### $\{H, S, T, \text{CNOT}\}$ = ユニバーサルゲートセット

| ゲート | 表面符号での実装 |
|--------|-----------------|
| CNOT | ブレイド変換（§VIII） |
| $H$ | 格子 90° 回転 |
| $S$ | 測定ベース操作 |
| $T$ | マジック状態注入 |

### 物理実装（§XIV）

> 📊 Fig. 16, 17 参照（原論文）

| プラットフォーム | 特徴 | 課題 |
|-----------------|------|------|
| 超伝導量子ビット | 高速（ns ゲート）、2次元格子が作りやすい | デコヒーレンス時間 $\sim 100\,\mu$s |
| トラップドイオン | 長いコヒーレンス時間、高忠実度 | 操作速度が遅い（$\mu$s ゲート）、スケールアップ困難 |
| 中性原子 | 光ピンセットで柔軟な配置 | 読み出し速度、真空技術が課題 |
| フォトニクス | 室温動作可能 | 決定論的2量子ビットゲートが困難 |

---


</details>

---

[← 論文一覧に戻る](../../)
