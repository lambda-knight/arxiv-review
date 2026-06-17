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

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>背景 — 断片化したロボット知能の課題</h2>
<h3>身体性 AI（Embodied AI）とは</h3>
<ul>
<li>ロボットの体を持ち、<strong>見て → 考えて → 動く</strong>を実世界でこなす AI</li>
<li>三要素: <strong>知覚（Perception）・推論（Reasoning）・行動（Action）</strong></li>
<li>単なるチャット AI と違い、カメラ・センサーで状況を読み取り、モーターを動かして物理的に行動する</li>
</ul>
<h3>主要タスクの種類</h3>
<table>
<thead>
<tr>
<th>タスク</th>
<th>内容</th>
<th>例</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>操作 (Manipulation)</strong></td>
<td>物体を掴む・動かす・組み立てる</td>
<td>カップを棚に置く、部品を組み付ける</td>
</tr>
<tr>
<td><strong>ナビゲーション (Navigation)</strong></td>
<td>指示に従って環境を移動する</td>
<td>「リビングのソファの前に行って」</td>
</tr>
<tr>
<td><strong>軌跡予測 (Trajectory)</strong></td>
<td>エージェントの移動経路を予測する</td>
<td>人・車の経路予測、経路計画</td>
</tr>
</tbody>
</table>
<h3>従来手法の「分断」問題</h3>
<table>
<thead>
<tr>
<th>代表的な既存モデル</th>
<th>得意</th>
<th>不得意</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>RT-2</strong> (Google, 2023)</td>
<td>ロボット操作</td>
<td>ナビゲーション不可</td>
</tr>
<tr>
<td><strong>π0</strong> (Physical Intelligence, 2024)</td>
<td>操作・多タスク</td>
<td>ナビ・軌跡不対応</td>
</tr>
<tr>
<td><strong>OpenVLA</strong> (UC Berkeley, 2024)</td>
<td>操作（VLM活用）</td>
<td>ナビ不可</td>
</tr>
<tr>
<td><strong>NaviLLM</strong> (2023)</td>
<td>VL ナビゲーション</td>
<td>操作不可</td>
</tr>
<tr>
<td><strong>VLN-BERT</strong> (2021)</td>
<td>ナビゲーション</td>
<td>操作不可</td>
</tr>
</tbody>
</table>
<p><strong>根本的な問題</strong>: モデルが分断→視覚理解・推論能力が共有されない→知識の転用ゼロ</p>
<h3>なぜ統一が難しかったか</h3>
<ol>
<li><strong>出力形式の違い</strong>: 操作は連続的な関節角度（6〜7次元）、ナビは離散的な方向、軌跡は2D座標列</li>
<li><strong>データ分布の乖離</strong>: ロボットアーム（テーブル上の小物）とナビ（室内全体のパノラマ）では視点・スケールが全く異なる</li>
<li><strong>エンボディメントの多様性</strong>: 片腕・双腕（ALOHA）・走行型ロボットで制御次元数が180度違う</li>
<li><strong>タスク間干渉の懸念</strong>: 異なるタスクを無理に混ぜると互いの精度が下がる「負の転移」の問題</li>
</ol>
<h3>Qwen-VLA の中心命題</h3>
<blockquote>
<p><strong>「操作・ナビゲーション・軌跡予測という異質な身体的意思決定を、単一の VLA モデルに統合できるか？」</strong></p>
</blockquote>
<p>答え: Yes — Qwen の VLM 基盤に DiT アクションデコーダを追加し、大規模な合同事前学習で実現した</p>
<hr />

</details>

### 第2章: Qwen-VLA の全体像とアーキテクチャ

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Qwen-VLA の全体像とアーキテクチャ</h2>
<h3>アーキテクチャの鳥瞰図</h3>
<pre><code>┌─────────────────────────────────┐
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
</code></pre>
<h3>統一された出力フレームワーク</h3>
<ul>
<li>操作・ナビ・軌跡を<strong>すべてアクション＋軌跡予測</strong>として定式化</li>
<li>操作 → 連続アクションチャンクとして予測</li>
<li>ナビゲーション → 候補候補視点の選択（離散アクション）として予測</li>
<li>軌跡 → 2D 座標列として予測</li>
</ul>
<h3>Qwen VL バックボーンの役割</h3>
<ul>
<li><strong>視覚エンコーダ</strong>: ViT 系、入力画像をトークン列に変換</li>
<li><strong>言語モデル（Qwen LLM）</strong>: テキスト指示・エンボディメント記述を処理</li>
<li><strong>クロスアテンション</strong>: 視覚と言語の特徴を融合</li>
<li>出力: 条件ベクトル $\mathbf{c}$（DiT デコーダへの入力）</li>
</ul>
<h3>エンボディメント対応プロンプト条件付け</h3>
<ul>
<li>モデルに<strong>「今どのロボット体を動かすか」をテキストで伝える</strong></li>
</ul>
<pre><code>[WidowX アームの場合]
&quot;You are controlling a WidowX 250s robot arm with 6 degrees of 
 freedom. Each action is a 6-dimensional vector [j1,j2,j3,j4,j5,j6]
 representing joint angles. The gripper state is appended as a binary.&quot;

[ALOHA 双腕の場合]
&quot;You are controlling an ALOHA bimanual robot with two 6-DOF arms.
 Each action is a 14-dimensional vector [left_arm×6, right_arm×6, grippers×2].&quot;

[ナビゲーションの場合]
&quot;You are a navigation agent. Select the next viewpoint from candidates.&quot;
</code></pre>
<ul>
<li>同一パラメータのまま、プロンプトを変えるだけで異なるロボットに適応</li>
</ul>
<hr />

</details>

### 第3章: DiT アクションデコーダ — 拡散過程で動きを生成

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>DiT アクションデコーダ — 拡散過程で動きを生成</h2>
<h3>なぜ拡散モデル（Diffusion Model）か？</h3>
<p>ロボット動作は本質的に<strong>多峰的（multimodal）</strong>: 「コップを取る」という指示に対して最適な手の軌道は無数にある。</p>
<table>
<thead>
<tr>
<th>アプローチ</th>
<th>問題</th>
</tr>
</thead>
<tbody>
<tr>
<td>MSE 回帰（平均的解）</td>
<td>複数の最適解の「平均」を出力→ぎこちない中間的な動き</td>
</tr>
<tr>
<td>離散化</td>
<td>連続アクションを量子化→精度が粗くなる</td>
</tr>
<tr>
<td><strong>拡散モデル</strong></td>
<td>ノイズから目標分布を学習→自然で多様な動きを生成 ✓</td>
</tr>
</tbody>
</table>
<h3>前向き過程（ノイズ付加）— 学習時</h3>
<p>$$\mathbf{a}_t = \sqrt{\bar{\alpha}_t}\,\mathbf{a}_0 + \sqrt{1 - \bar{\alpha}_t}\,\boldsymbol{\epsilon}$$</p>
<ul>
<li>$\mathbf{a}_0$: ノイズなしの正解アクション（教師データ）</li>
<li>$\mathbf{a}_t$: タイムステップ $t$ でノイズを加えたアクション</li>
<li>$\bar{\alpha}<em>t = \prod</em>{s=1}^{t}(1-\beta_s)$: 累積ノイズスケジュール（$t \to T$ で $\bar{\alpha}_t \to 0$）</li>
<li>$\boldsymbol{\epsilon} \sim \mathcal{N}(0, \mathbf{I})$: 加えるガウスノイズ</li>
</ul>
<p><strong>直感</strong>: $t=0$ は元のアクション、$t=T$ は完全なランダムノイズ。その中間状態を学習する。</p>
<h3>訓練目標（ノイズ予測）</h3>
<p>$$\mathcal{L}<em>{\text{DiT}} = \mathbb{E}</em>{t,\,\mathbf{a}<em>0,\,\boldsymbol{\epsilon}} \left[ \left| \boldsymbol{\epsilon} - \boldsymbol{\epsilon}</em>\theta!\left(\mathbf{a}_t,\, t,\, \mathbf{c}\right) \right|^2 \right]$$</p>
<ul>
<li>$\boldsymbol{\epsilon}_\theta(\cdot)$: DiT が予測する「加えられたノイズ」（パラメータ $\theta$）</li>
<li>$\mathbf{c}$: 条件ベクトル（Qwen VL が生成した視覚・言語・エンボディメント特徴）</li>
<li><strong>最小化する量</strong>: 予測ノイズ $\boldsymbol{\epsilon}_\theta$ と実際に加えたノイズ $\boldsymbol{\epsilon}$ の二乗誤差（MSE）</li>
</ul>
<p>記号の意味:
- $\boldsymbol{\epsilon}_\theta$: DiT ネットワーク（パラメータ $\theta$）
- $t$: 拡散タイムステップ（1〜T）
- $\mathbf{c}$: VL 特徴条件（=「状況・指示の要約」）</p>
<h3>ポリシーとしての拡散モデル</h3>
<p>$$\pi_\theta!\left(\mathbf{a} \mid \mathbf{o},\, \ell_{\text{task}},\, \ell_{\text{body}}\right) = p_\theta!\left(\mathbf{a}<em>0 \;\Big|\; \mathbf{a}_T \sim \mathcal{N}(0, \mathbf{I}),\;\; \mathbf{c} = f</em>\phi(\mathbf{o},\, \ell_{\text{task}},\, \ell_{\text{body}})\right)$$</p>
<ul>
<li>$\mathbf{o}$: カメラ画像（観測）</li>
<li>$\ell_{\text{task}}$: タスク指示文（例: "pick up the red cup"）</li>
<li>$\ell_{\text{body}}$: エンボディメント記述（ロボットの体・制御仕様）</li>
<li>$f_\phi$: Qwen VL エンコーダ（視覚×言語→条件ベクトル $\mathbf{c}$）</li>
<li>推論時: $\mathbf{a}_T$（ランダムノイズ）から始め $T$ ステップかけてノイズ除去 → $\mathbf{a}_0$ を得る</li>
</ul>
<h3>DiT（Diffusion Transformer）の内部構造</h3>
<ul>
<li><strong>Transformer ブロック</strong>を拡散ステップ $t$ と条件 $\mathbf{c}$ で条件付け</li>
<li>条件付け手法: <strong>AdaLN（Adaptive Layer Normalization）</strong></li>
</ul>
<p>$$\text{AdaLN}(h, t, \mathbf{c}) = \gamma(t, \mathbf{c}) \cdot \frac{h - \mu}{\sigma} + \beta(t, \mathbf{c})$$</p>
<ul>
<li>$\gamma, \beta$: ステップ $t$ と条件 $\mathbf{c}$ から MLP で生成されるスケール・シフト係数</li>
<li>自己回帰でなく<strong>並列デコーディング</strong>→ チャンク単位の高速アクション生成</li>
</ul>
<h3>推論手順（逆拡散）</h3>
<ol>
<li>$\mathbf{a}_T \sim \mathcal{N}(0, \mathbf{I})$ をサンプル（完全ノイズ）</li>
<li>$t = T, T-1, \ldots, 1$ のループ:</li>
<li>$\boldsymbol{\epsilon}_\theta(\mathbf{a}_t, t, \mathbf{c})$ を DiT で推論</li>
<li>DDPM スケジューラで $\mathbf{a}<em>t \to \mathbf{a}</em>{t-1}$ に更新</li>
<li>$\mathbf{a}_0$ をロボットに送信（関節角度 / 方向 / 座標列）</li>
</ol>
<hr />

</details>

### 第4章: 大規模学習データとエンボディメント対応

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>大規模学習データとエンボディメント対応</h2>
<h3>6 つのデータソース</h3>
<table>
<thead>
<tr>
<th>データ種別</th>
<th>代表データセット</th>
<th>役割</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>ロボット操作軌跡</strong></td>
<td>Open X-Embodiment, LEROBOT, RoboTwin</td>
<td>アクション生成の基礎訓練</td>
</tr>
<tr>
<td><strong>人間の一人称映像</strong></td>
<td>EPIC-Kitchens, Ego4D</td>
<td>物体操作の暗黙知・手の動き</td>
</tr>
<tr>
<td><strong>合成シミュレーション</strong></td>
<td>Isaac Sim / MuJoCo 生成データ</td>
<td>データ量・環境多様性の補完</td>
</tr>
<tr>
<td><strong>VL ナビゲーション</strong></td>
<td>R2R, RxR データセット</td>
<td>空間推論・言語接地</td>
</tr>
<tr>
<td><strong>軌跡中心監督</strong></td>
<td>俯瞰軌跡 + アノテーション</td>
<td>軌跡予測能力の習得</td>
</tr>
<tr>
<td><strong>補助 VL データ</strong></td>
<td>VQA, image captioning</td>
<td>視覚・言語理解能力の維持</td>
</tr>
</tbody>
</table>
<h3>データの役割分担</h3>
<ul>
<li><strong>操作・シミュ</strong>: アクション生成の精度向上</li>
<li><strong>一人称映像</strong>: VLM の物体・動作理解を実世界にアンカー</li>
<li><strong>ナビゲーション</strong>: 空間的推論・指示に基づく行動計画</li>
<li><strong>補助 VL</strong>: 合同訓練による VLM 能力の劣化を防ぐ（catastrophic forgetting 対策）</li>
</ul>
<h3>エンボディメント対応プロンプト — 詳細</h3>
<p>ロボット記述はシステムプロンプトとして入力:</p>
<pre><code>System: &lt;embodiment&gt;
  Robot: Franka Panda
  DOF: 7
  Control: End-Effector Pose (xyz + quaternion + gripper)
  Action dimension: 7
&lt;/embodiment&gt;
</code></pre>
<ul>
<li><strong>制御空間の記述</strong>: 関節角度制御か、手先位置制御かを明示</li>
<li><strong>アクション次元</strong>: 出力ベクトルの次元数を DiT デコーダに伝える</li>
<li><strong>グリッパー仕様</strong>: バイナリ（開閉2値）か連続値かを明示</li>
</ul>
<h3>なぜ言語でエンボディメントを指定できるか</h3>
<ul>
<li>Qwen LLM が持つ<strong>零射学習（zero-shot）能力</strong>を活用</li>
<li>「7次元のベクトル」「手先位置」といった記述を自然言語として理解</li>
<li>訓練時に見たことのないロボット記述でも<strong>構造的に類似した制御を推論</strong></li>
</ul>
<h3>転移学習の仕組み — なぜ汎化するか</h3>
<ul>
<li><strong>視覚エンコーダ</strong>: Qwen VL が多様な画像で学習済み→ロボット視点にも適応</li>
<li><strong>言語接地</strong>: タスク記述の意味的理解が実環境・シミュ環境を越えて共有</li>
<li><strong>DiT デコーダ</strong>: 「どんな次元の連続アクション」でも条件付き生成が可能</li>
<li><strong>合同学習の効果</strong>: 操作データとナビデータが互いの視覚推論を強化</li>
</ul>
<hr />

</details>

### 第5章: 実験結果・限界・今後の展望

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>実験結果・限界・今後の展望</h2>
<h3>ベンチマーク — 操作系</h3>
<h4>シミュレーション</h4>
<table>
<thead>
<tr>
<th>ベンチマーク</th>
<th>評価内容</th>
<th>Qwen-VLA</th>
<th>比較手法</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>LIBERO</strong></td>
<td>4タスク×50エピソード（把持・整理等）</td>
<td><strong>97.9%</strong></td>
<td>RT-2: ~65% / OpenVLA: ~79%</td>
</tr>
<tr>
<td><strong>Simpler-WidowX</strong></td>
<td>WidowX アームでの把持タスク</td>
<td><strong>73.7%</strong></td>
<td>OpenVLA: ~56%</td>
</tr>
<tr>
<td><strong>RoboTwin-Easy</strong></td>
<td>ランダム配置・簡易</td>
<td><strong>86.1%</strong></td>
<td>π0: ~78%</td>
</tr>
<tr>
<td><strong>RoboTwin-Hard</strong></td>
<td>ランダム配置・高難度</td>
<td><strong>87.2%</strong></td>
<td>π0: ~71%</td>
</tr>
</tbody>
</table>
<h4>実世界実験（ALOHA 双腕ロボット）</h4>
<ul>
<li><strong>平均 OOD 成功率: 76.9%</strong></li>
<li>OOD 条件: シーンレイアウト変更・背景変更・照明変更・物体配置変更・ロボット本体変更</li>
<li>汎化が最も難しい「ロボット本体変更」でも高い成功率を維持</li>
</ul>
<h3>ベンチマーク — ナビゲーション系</h3>
<table>
<thead>
<tr>
<th>ベンチマーク</th>
<th>指標</th>
<th>内容</th>
<th>Qwen-VLA</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>R2R</strong> (Room-to-Room)</td>
<td>OSR (Off-path Success Rate)</td>
<td>英語指示で室内ナビ</td>
<td><strong>69.0%</strong></td>
</tr>
<tr>
<td><strong>RxR</strong> (Room-across-Room)</td>
<td>SR (Success Rate)</td>
<td>多言語指示ナビ</td>
<td><strong>59.6%</strong></td>
</tr>
</tbody>
</table>
<ul>
<li>操作モデルとナビモデルが<strong>完全に共有されたパラメータ</strong>でこれだけの性能</li>
</ul>
<h3>ベンチマーク — 軌跡予測・ゼロショット</h3>
<table>
<thead>
<tr>
<th>ベンチマーク</th>
<th>内容</th>
<th>結果</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>DOMINO</strong></td>
<td>動的操作・ゼロショット（未訓練タスク）</td>
<td><strong>26.6% SR</strong></td>
</tr>
</tbody>
</table>
<ul>
<li>ゼロショット（事前にタスクを見ていない）での26.6%は特筆すべき性能</li>
<li>操作データとナビデータの合同学習が軌跡予測にも汎化した証拠</li>
</ul>
<h3>OOD 汎化の分析</h3>
<ul>
<li><strong>シーン変化</strong>（背景・照明・物体配置）: 最大 -8% 程度の精度低下に抑制</li>
<li><strong>エンボディメント変化</strong>: プロンプト変更のみで対応、再訓練不要</li>
<li><strong>言語指示の多様性</strong>: 同じ操作でも異なる言語表現に対応（RxR 多言語で確認）</li>
</ul>
<h3>限界（Limitations）</h3>
<ol>
<li><strong>推論速度</strong>: DiT のデノイジングは複数ステップ（T=10〜50）→リアルタイム制約のある高速タスクに課題</li>
<li><strong>長期依存タスク</strong>: 10+ ステップの長い計画（ロングホライズン）は未解決</li>
<li><strong>触覚・力覚フィードバック</strong>: 現状は視覚のみ→柔軟物の把持・繊細な組み立てに限界</li>
<li><strong>実ロボットデータの量</strong>: シミュレーション依存が大きく、実ロボット軌跡の絶対量は少ない</li>
<li><strong>エンボディメント記述の品質依存</strong>: テキスト記述が不適切だと性能が大幅低下する可能性</li>
</ol>
<h3>今後の展望</h3>
<ul>
<li><strong>マルチモーダル拡張</strong>: 触覚・力覚センサーとの統合（接触情報をフィードバック）</li>
<li><strong>オンライン学習</strong>: 実環境での継続的な自己改善（reinforcement learning from interaction）</li>
<li><strong>計算効率の改善</strong>: Consistency Models など少ステップ拡散への移行（10ステップ→1〜3ステップ）</li>
<li><strong>世界モデルとの統合</strong>: 行動結果を予測しながら計画立案（モデルベース RL との融合）</li>
<li><strong>ロングホライズン</strong>: タスクを部分目標に分解し、VLM の推論能力を活かした階層計画</li>
</ul>
<hr />
<p><strong>参考ソース</strong>
- arXiv: https://arxiv.org/abs/2605.30280
- Qwen チーム / Alibaba — 2026年5月
- カテゴリ: cs.RO, cs.AI, cs.CL</p>

</details>

---

[← 論文一覧に戻る](../../)
