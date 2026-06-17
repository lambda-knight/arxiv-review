---
title: "Qwen-VLA — 一つのモデルで「見る・考える・動く」を統一する"
layout: default
---

# Qwen-VLA — 一つのモデルで「見る・考える・動く」を統一する

*Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments*

- arXiv: [2605.30280](https://arxiv.org/abs/2605.30280)
- Internet Archive: [paper-explain-2605-30280](https://archive.org/details/paper-explain-2605-30280)

---

## 概要

今回解説する論文:
Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments
arXiv: https://arxiv.org/abs/2605.30280
著者: Qiuyue Wang, Mingsheng Li, Jian Guan ほか（Qwen チーム / Alibaba）

■ 動画の内容
これまでのロボット研究では、「物を掴む操作」「室内ナビゲーション」「軌跡予測」はそれぞれ別々の専用モデルで解かれてきました。Qwen-VLA はこの「断片化」を解決するため、Qwen の視覚-言語モデルに DiT（Diffusion Transformer）アクションデコーダを追加し、一つのモデルで三つのタスクをこなします。

拡散モデルをロボット制御に使う理由、前向き過程の数式（ノイズ付加）・訓練目標（ノイズ予測）・ポリシーの定式化まで、数式を画面に表示しながら丁寧に解説します。

■ 章構成（各章独立した動画）
第1章：背景 — 断片化したロボット知能の課題
第2章：Qwen-VLA の全体像とアーキテクチャ
第3章：DiT アクションデコーダ — 拡散過程で動きを生成
第4章：大規模学習データとエンボディメント対応
第5章：実験結果・限界・今後の展望

■ 主要結果
・LIBERO（操作シミュ）: 97.9%
・RoboTwin-Hard（操作）: 87.2%
・実世界 ALOHA（双腕ロボット OOD）: 76.9%
・R2R ナビゲーション: 69.0% OSR
・DOMINO ゼロショット: 26.6%

■ ずんだもん＋四国めたんが軽快テンポで数式まで踏み込んで解説！

#論文解説 #arxiv #数式でわかる #ロボット #身体性AI #ディープラーニング #拡散モデル #強化学習 #大規模言語モデル #VLA #Robotics #EmbodiedAI

---

## 章別動画・解説

### 第1章: 背景 — 断片化したロボット知能の課題

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch01.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch01.mp4){:target="_blank"}

<details markdown="1">
<summary>解説スライド（クリックで展開）</summary>

## 背景 — 断片化したロボット知能の課題

### 身体性 AI（Embodied AI）とは
- ロボットの体を持ち、**見て → 考えて → 動く**を実世界でこなす AI
- 三要素: **知覚（Perception）・推論（Reasoning）・行動（Action）**
- 単なるチャット AI と違い、カメラ・センサーで状況を読み取り、モーターを動かして物理的に行動する

### 主要タスクの種類
| タスク | 内容 | 例 |
|--------|------|----|
| **操作 (Manipulation)** | 物体を掴む・動かす・組み立てる | カップを棚に置く、部品を組み付ける |
| **ナビゲーション (Navigation)** | 指示に従って環境を移動する | 「リビングのソファの前に行って」 |
| **軌跡予測 (Trajectory)** | エージェントの移動経路を予測する | 人・車の経路予測、経路計画 |

### 従来手法の「分断」問題
| 代表的な既存モデル | 得意 | 不得意 |
|-------------------|------|--------|
| **RT-2** (Google, 2023) | ロボット操作 | ナビゲーション不可 |
| **π0** (Physical Intelligence, 2024) | 操作・多タスク | ナビ・軌跡不対応 |
| **OpenVLA** (UC Berkeley, 2024) | 操作（VLM活用） | ナビ不可 |
| **NaviLLM** (2023) | VL ナビゲーション | 操作不可 |
| **VLN-BERT** (2021) | ナビゲーション | 操作不可 |

**根本的な問題**: モデルが分断→視覚理解・推論能力が共有されない→知識の転用ゼロ

### なぜ統一が難しかったか
1. **出力形式の違い**: 操作は連続的な関節角度（6〜7次元）、ナビは離散的な方向、軌跡は2D座標列
2. **データ分布の乖離**: ロボットアーム（テーブル上の小物）とナビ（室内全体のパノラマ）では視点・スケールが全く異なる
3. **エンボディメントの多様性**: 片腕・双腕（ALOHA）・走行型ロボットで制御次元数が180度違う
4. **タスク間干渉の懸念**: 異なるタスクを無理に混ぜると互いの精度が下がる「負の転移」の問題

### Qwen-VLA の中心命題
> **「操作・ナビゲーション・軌跡予測という異質な身体的意思決定を、単一の VLA モデルに統合できるか？」**

答え: Yes — Qwen の VLM 基盤に DiT アクションデコーダを追加し、大規模な合同事前学習で実現した

---


</details>

### 第2章: Qwen-VLA の全体像とアーキテクチャ

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4){:target="_blank"}

<details markdown="1">
<summary>解説スライド（クリックで展開）</summary>

## Qwen-VLA の全体像とアーキテクチャ

### アーキテクチャの鳥瞰図
```
┌─────────────────────────────────┐
│           入  力                  │
│  カメラ画像  + タスク指示          │
│           + エンボディメント記述   │
└─────────────────────────────────┘
              ↓
┌─────────────────────────────────┐
│       Qwen VL Backbone           │
│  ・視覚エンコーダ（ViT 系）        │
│  ・言語モデル（Qwen LLM）          │
│  → 視覚・言語の統合特徴ベクトル c  │
└─────────────────────────────────┘
              ↓
┌─────────────────────────────────┐
│    DiT-based Action Decoder       │
│  ・拡散過程でノイズ→アクションへ  │
│  ・条件: c（VL 特徴）             │
└─────────────────────────────────┘
              ↓
┌─────────────────────────────────┐
│          出  力                   │
│  操作: 関節角度ベクトル（6〜7次元）│
│  ナビ: 候補視点への離散選択        │
│  軌跡: 2D 座標点列               │
└─────────────────────────────────┘
```

### 統一された出力フレームワーク
- 操作・ナビ・軌跡を**すべてアクション＋軌跡予測**として定式化
- 操作 → 連続アクションチャンクとして予測
- ナビゲーション → 候補候補視点の選択（離散アクション）として予測
- 軌跡 → 2D 座標列として予測

### Qwen VL バックボーンの役割
- **視覚エンコーダ**: ViT 系、入力画像をトークン列に変換
- **言語モデル（Qwen LLM）**: テキスト指示・エンボディメント記述を処理
- **クロスアテンション**: 視覚と言語の特徴を融合
- 出力: 条件ベクトル $\mathbf{c}$（DiT デコーダへの入力）

### エンボディメント対応プロンプト条件付け
- モデルに**「今どのロボット体を動かすか」をテキストで伝える**

```
[WidowX アームの場合]
"You are controlling a WidowX 250s robot arm with 6 degrees of 
 freedom. Each action is a 6-dimensional vector [j1,j2,j3,j4,j5,j6]
 representing joint angles. The gripper state is appended as a binary."

[ALOHA 双腕の場合]
"You are controlling an ALOHA bimanual robot with two 6-DOF arms.
 Each action is a 14-dimensional vector [left_arm×6, right_arm×6, grippers×2]."

[ナビゲーションの場合]
"You are a navigation agent. Select the next viewpoint from candidates."
```

- 同一パラメータのまま、プロンプトを変えるだけで異なるロボットに適応

---


</details>

### 第3章: DiT アクションデコーダ — 拡散過程で動きを生成

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4){:target="_blank"}

<details markdown="1">
<summary>解説スライド（クリックで展開）</summary>

## DiT アクションデコーダ — 拡散過程で動きを生成

### なぜ拡散モデル（Diffusion Model）か？

ロボット動作は本質的に**多峰的（multimodal）**: 「コップを取る」という指示に対して最適な手の軌道は無数にある。

| アプローチ | 問題 |
|-----------|------|
| MSE 回帰（平均的解） | 複数の最適解の「平均」を出力→ぎこちない中間的な動き |
| 離散化 | 連続アクションを量子化→精度が粗くなる |
| **拡散モデル** | ノイズから目標分布を学習→自然で多様な動きを生成 ✓ |

### 前向き過程（ノイズ付加）— 学習時

$$\mathbf{a}_t = \sqrt{\bar{\alpha}_t}\,\mathbf{a}_0 + \sqrt{1 - \bar{\alpha}_t}\,\boldsymbol{\epsilon}$$

- $\mathbf{a}_0$: ノイズなしの正解アクション（教師データ）
- $\mathbf{a}_t$: タイムステップ $t$ でノイズを加えたアクション
- $\bar{\alpha}_t = \prod_{s=1}^{t}(1-\beta_s)$: 累積ノイズスケジュール（$t \to T$ で $\bar{\alpha}_t \to 0$）
- $\boldsymbol{\epsilon} \sim \mathcal{N}(0, \mathbf{I})$: 加えるガウスノイズ

**直感**: $t=0$ は元のアクション、$t=T$ は完全なランダムノイズ。その中間状態を学習する。

### 訓練目標（ノイズ予測）

$$\mathcal{L}_{\text{DiT}} = \mathbb{E}_{t,\,\mathbf{a}_0,\,\boldsymbol{\epsilon}} \left[ \left\| \boldsymbol{\epsilon} - \boldsymbol{\epsilon}_\theta\!\left(\mathbf{a}_t,\, t,\, \mathbf{c}\right) \right\|^2 \right]$$

- $\boldsymbol{\epsilon}_\theta(\cdot)$: DiT が予測する「加えられたノイズ」（パラメータ $\theta$）
- $\mathbf{c}$: 条件ベクトル（Qwen VL が生成した視覚・言語・エンボディメント特徴）
- **最小化する量**: 予測ノイズ $\boldsymbol{\epsilon}_\theta$ と実際に加えたノイズ $\boldsymbol{\epsilon}$ の二乗誤差（MSE）

記号の意味:
- $\boldsymbol{\epsilon}_\theta$: DiT ネットワーク（パラメータ $\theta$）
- $t$: 拡散タイムステップ（1〜T）
- $\mathbf{c}$: VL 特徴条件（=「状況・指示の要約」）

### ポリシーとしての拡散モデル

$$\pi_\theta\!\left(\mathbf{a} \mid \mathbf{o},\, \ell_{\text{task}},\, \ell_{\text{body}}\right) = p_\theta\!\left(\mathbf{a}_0 \;\Big|\; \mathbf{a}_T \sim \mathcal{N}(0, \mathbf{I}),\;\; \mathbf{c} = f_\phi(\mathbf{o},\, \ell_{\text{task}},\, \ell_{\text{body}})\right)$$

- $\mathbf{o}$: カメラ画像（観測）
- $\ell_{\text{task}}$: タスク指示文（例: "pick up the red cup"）
- $\ell_{\text{body}}$: エンボディメント記述（ロボットの体・制御仕様）
- $f_\phi$: Qwen VL エンコーダ（視覚×言語→条件ベクトル $\mathbf{c}$）
- 推論時: $\mathbf{a}_T$（ランダムノイズ）から始め $T$ ステップかけてノイズ除去 → $\mathbf{a}_0$ を得る

### DiT（Diffusion Transformer）の内部構造
- **Transformer ブロック**を拡散ステップ $t$ と条件 $\mathbf{c}$ で条件付け
- 条件付け手法: **AdaLN（Adaptive Layer Normalization）**

$$\text{AdaLN}(h, t, \mathbf{c}) = \gamma(t, \mathbf{c}) \cdot \frac{h - \mu}{\sigma} + \beta(t, \mathbf{c})$$

- $\gamma, \beta$: ステップ $t$ と条件 $\mathbf{c}$ から MLP で生成されるスケール・シフト係数
- 自己回帰でなく**並列デコーディング**→ チャンク単位の高速アクション生成

### 推論手順（逆拡散）
1. $\mathbf{a}_T \sim \mathcal{N}(0, \mathbf{I})$ をサンプル（完全ノイズ）
2. $t = T, T-1, \ldots, 1$ のループ:
   - $\boldsymbol{\epsilon}_\theta(\mathbf{a}_t, t, \mathbf{c})$ を DiT で推論
   - DDPM スケジューラで $\mathbf{a}_t \to \mathbf{a}_{t-1}$ に更新
3. $\mathbf{a}_0$ をロボットに送信（関節角度 / 方向 / 座標列）

---


</details>

### 第4章: 大規模学習データとエンボディメント対応

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4){:target="_blank"}

<details markdown="1">
<summary>解説スライド（クリックで展開）</summary>

## 大規模学習データとエンボディメント対応

### 6 つのデータソース

| データ種別 | 代表データセット | 役割 |
|-----------|----------------|------|
| **ロボット操作軌跡** | Open X-Embodiment, LEROBOT, RoboTwin | アクション生成の基礎訓練 |
| **人間の一人称映像** | EPIC-Kitchens, Ego4D | 物体操作の暗黙知・手の動き |
| **合成シミュレーション** | Isaac Sim / MuJoCo 生成データ | データ量・環境多様性の補完 |
| **VL ナビゲーション** | R2R, RxR データセット | 空間推論・言語接地 |
| **軌跡中心監督** | 俯瞰軌跡 + アノテーション | 軌跡予測能力の習得 |
| **補助 VL データ** | VQA, image captioning | 視覚・言語理解能力の維持 |

### データの役割分担
- **操作・シミュ**: アクション生成の精度向上
- **一人称映像**: VLM の物体・動作理解を実世界にアンカー
- **ナビゲーション**: 空間的推論・指示に基づく行動計画
- **補助 VL**: 合同訓練による VLM 能力の劣化を防ぐ（catastrophic forgetting 対策）

### エンボディメント対応プロンプト — 詳細

ロボット記述はシステムプロンプトとして入力:
```
System: <embodiment>
  Robot: Franka Panda
  DOF: 7
  Control: End-Effector Pose (xyz + quaternion + gripper)
  Action dimension: 7
</embodiment>
```

- **制御空間の記述**: 関節角度制御か、手先位置制御かを明示
- **アクション次元**: 出力ベクトルの次元数を DiT デコーダに伝える
- **グリッパー仕様**: バイナリ（開閉2値）か連続値かを明示

### なぜ言語でエンボディメントを指定できるか
- Qwen LLM が持つ**零射学習（zero-shot）能力**を活用
- 「7次元のベクトル」「手先位置」といった記述を自然言語として理解
- 訓練時に見たことのないロボット記述でも**構造的に類似した制御を推論**

### 転移学習の仕組み — なぜ汎化するか
- **視覚エンコーダ**: Qwen VL が多様な画像で学習済み→ロボット視点にも適応
- **言語接地**: タスク記述の意味的理解が実環境・シミュ環境を越えて共有
- **DiT デコーダ**: 「どんな次元の連続アクション」でも条件付き生成が可能
- **合同学習の効果**: 操作データとナビデータが互いの視覚推論を強化

---


</details>

### 第5章: 実験結果・限界・今後の展望

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4){:target="_blank"}

<details markdown="1">
<summary>解説スライド（クリックで展開）</summary>

## 実験結果・限界・今後の展望

### ベンチマーク — 操作系

#### シミュレーション
| ベンチマーク | 評価内容 | Qwen-VLA | 比較手法 |
|-------------|---------|---------|---------|
| **LIBERO** | 4タスク×50エピソード（把持・整理等） | **97.9%** | RT-2: ~65% / OpenVLA: ~79% |
| **Simpler-WidowX** | WidowX アームでの把持タスク | **73.7%** | OpenVLA: ~56% |
| **RoboTwin-Easy** | ランダム配置・簡易 | **86.1%** | π0: ~78% |
| **RoboTwin-Hard** | ランダム配置・高難度 | **87.2%** | π0: ~71% |

#### 実世界実験（ALOHA 双腕ロボット）
- **平均 OOD 成功率: 76.9%**
- OOD 条件: シーンレイアウト変更・背景変更・照明変更・物体配置変更・ロボット本体変更
- 汎化が最も難しい「ロボット本体変更」でも高い成功率を維持

### ベンチマーク — ナビゲーション系

| ベンチマーク | 指標 | 内容 | Qwen-VLA |
|-------------|------|------|---------|
| **R2R** (Room-to-Room) | OSR (Off-path Success Rate) | 英語指示で室内ナビ | **69.0%** |
| **RxR** (Room-across-Room) | SR (Success Rate) | 多言語指示ナビ | **59.6%** |

- 操作モデルとナビモデルが**完全に共有されたパラメータ**でこれだけの性能

### ベンチマーク — 軌跡予測・ゼロショット

| ベンチマーク | 内容 | 結果 |
|-------------|------|------|
| **DOMINO** | 動的操作・ゼロショット（未訓練タスク） | **26.6% SR** |

- ゼロショット（事前にタスクを見ていない）での26.6%は特筆すべき性能
- 操作データとナビデータの合同学習が軌跡予測にも汎化した証拠

### OOD 汎化の分析
- **シーン変化**（背景・照明・物体配置）: 最大 -8% 程度の精度低下に抑制
- **エンボディメント変化**: プロンプト変更のみで対応、再訓練不要
- **言語指示の多様性**: 同じ操作でも異なる言語表現に対応（RxR 多言語で確認）

### 限界（Limitations）
1. **推論速度**: DiT のデノイジングは複数ステップ（T=10〜50）→リアルタイム制約のある高速タスクに課題
2. **長期依存タスク**: 10+ ステップの長い計画（ロングホライズン）は未解決
3. **触覚・力覚フィードバック**: 現状は視覚のみ→柔軟物の把持・繊細な組み立てに限界
4. **実ロボットデータの量**: シミュレーション依存が大きく、実ロボット軌跡の絶対量は少ない
5. **エンボディメント記述の品質依存**: テキスト記述が不適切だと性能が大幅低下する可能性

### 今後の展望
- **マルチモーダル拡張**: 触覚・力覚センサーとの統合（接触情報をフィードバック）
- **オンライン学習**: 実環境での継続的な自己改善（reinforcement learning from interaction）
- **計算効率の改善**: Consistency Models など少ステップ拡散への移行（10ステップ→1〜3ステップ）
- **世界モデルとの統合**: 行動結果を予測しながら計画立案（モデルベース RL との融合）
- **ロングホライズン**: タスクを部分目標に分解し、VLM の推論能力を活かした階層計画

---

**参考ソース**
- arXiv: https://arxiv.org/abs/2605.30280
- Qwen チーム / Alibaba — 2026年5月
- カテゴリ: cs.RO, cs.AI, cs.CL

</details>

---

[← 論文一覧に戻る](../../)
