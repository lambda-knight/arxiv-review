---
title: "Gemini Robotics ── AIを物理世界に持ち込む"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# Gemini Robotics ── AIを物理世界に持ち込む

*Google DeepMind (2025)*

- arXiv: [2503.20020](https://arxiv.org/abs/2503.20020)
- Internet Archive: [paper-explain-2503-20020](https://archive.org/details/paper-explain-2503-20020)

---

## 概要

Google DeepMindが発表した「Gemini Robotics: Bringing AI into the Physical World」（2025）を全5章で徹底解説！

Gemini 2.0を基盤に構築されたロボット専用AIファミリー。身体化推論モデル（Gemini Robotics-ER）とVLAモデル（Gemini Robotics）の2本柱で、物理世界の難問に挑みます。ずんだもんと四国めたんが数式も交えてわかりやすく解説するのだ！

📄 対象論文：
・Gemini Robotics: Bringing AI into the Physical World
  Google DeepMind (2025)
  https://arxiv.org/abs/2503.20020

📚 チャプター構成：
Ch.1 背景と全体像 ── ロボットAIの4つの壁とGemini Roboticsの戦略
Ch.2 Gemini Robotics-ER ── 身体化推論：物体検出・軌跡予測・グラスプ予測・3D BB
Ch.3 Gemini Robotics ── VLAモデルのアーキテクチャ・チャンク予測・学習データ
Ch.4 特化訓練と汎化性能 ── 少数ショット・長期タスク・新規エンボディメント適応
Ch.5 安全性・実験結果・今後の展望 ── 4リスク・ベンチマーク・5つの課題

#論文解説 #arxiv #ロボットAI #Gemini #VLA #機械学習 #ディープラーニング #ロボティクス #生成AI #研究 #大学院

---

## 章別動画・解説

### 第1章: 背景と全体像 ── ロボットAIの壁

<video controls width="100%" src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch01_manim_ch01.mp3" style="width:100%;margin-top:4px"></audio>

[Internet Archive で開く](https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch01.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>背景と全体像 ── ロボットAIの壁</h2>
<h3>デジタルから物理世界へ</h3>
<ul>
<li>大規模マルチモーダルモデルはデジタル領域では驚異的な汎用能力を発揮</li>
<li>しかしロボットなどの<strong>物理エージェントへの転換は依然として大きな課題</strong></li>
<li>本論文は Gemini 2.0 を基盤とした<strong>ロボット専用AIモデルファミリー</strong>を発表</li>
</ul>
<h3>2つのモデル</h3>
<table>
<thead>
<tr>
<th>モデル</th>
<th>役割</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Gemini Robotics-ER</strong></td>
<td>Embodied Reasoning（身体化推論）。空間・時間的理解を強化した知覚モデル</td>
</tr>
<tr>
<td><strong>Gemini Robotics</strong></td>
<td>VLA（Vision-Language-Action）。ロボットを直接制御する汎用アクションモデル</td>
</tr>
</tbody>
</table>
<h3>なぜロボットは難しいのか</h3>
<blockquote>
<p>📊 Fig. 1 参照（原論文）</p>
</blockquote>
<ol>
<li><strong>物理世界のリアルタイム性</strong> ── デジタルと違い「やり直し」が効かない</li>
<li><strong>多様なロボット形態（エンボディメント）</strong> ── アームの自由度・センサが機体ごとに異なる</li>
<li><strong>長期的タスク</strong> ── 数十ステップ先を見越した計画が必要</li>
<li><strong>安全性</strong> ── 誤動作が物理的危険を招く</li>
</ol>
<h3>Gemini Robotics の主要能力</h3>
<ul>
<li>滑らかでリアクティブな動作生成</li>
<li>多様な物体・未知環境への汎化</li>
<li>オープン語彙の指示への対応</li>
<li>100デモ程度の少数ショット学習で新タスクに特化</li>
</ul>
<hr />

</details>

### 第2章: Gemini Robotics-ER ── 身体化推論の仕組み

<video controls width="100%" src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch02.mp3" style="width:100%;margin-top:4px"></audio>

[Internet Archive で開く](https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch02.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Gemini Robotics-ER ── 身体化推論の仕組み</h2>
<h3>ER（Embodied Reasoning）とは</h3>
<p>Gemini のマルチモーダル推論能力を物理世界に拡張：</p>
<blockquote>
<p>📊 Fig. 2, 3 参照（原論文）</p>
</blockquote>
<ul>
<li><strong>空間理解</strong>：物体の位置・形状・向きを3次元で把握</li>
<li><strong>時間的理解</strong>：動作の時系列・因果関係を追跡</li>
<li><strong>ロボティクス固有タスク</strong>：以下の4能力を実現</li>
</ul>
<h3>4つのロボティクス知覚能力</h3>
<p><strong>① 物体検出・ポインティング</strong></p>
<p>$$\text{query} \xrightarrow{\text{Gemini-ER}} \{(x_i, y_i, \text{label}_i)\}_i$$</p>
<ul>
<li>自然言語クエリから物体の2D座標を返す</li>
<li>例：「赤いカップの取っ手はどこ？」→ 画像上の点を出力</li>
</ul>
<p><strong>② 軌跡予測</strong></p>
<ul>
<li>ロボットの手先が通るべき経路を画像上の点列として予測</li>
<li>操作開始前の「計画」として利用</li>
</ul>
<blockquote>
<p>📊 Fig. 4 参照（原論文）</p>
</blockquote>
<p><strong>③ グラスプ予測</strong></p>
<p>$$\text{grasp} = (x, y, z, \theta_{\text{roll}}, \theta_{\text{pitch}}, \theta_{\text{yaw}})$$</p>
<ul>
<li>物体をどの姿勢で把持するかを6自由度で予測</li>
<li>素材・形状を考慮した把持点を提案</li>
</ul>
<p><strong>④ マルチビュー対応と3D Bounding Box</strong></p>
<ul>
<li>複数カメラ視点から3次元物体位置を推定</li>
<li>3D bounding box で物体の位置・サイズを特定</li>
</ul>
<h3>なぜERモデルを分離するのか</h3>
<ul>
<li>知覚モジュールを独立させることで<strong>多様なロボットアプリに再利用</strong>可能</li>
<li>ERモデルは大規模な視覚言語データで事前学習 → ファインチューニングなしで未知物体に対応</li>
</ul>
<hr />

</details>

### 第3章: Gemini Robotics ── VLAモデルのアーキテクチャと学習

<video controls width="100%" src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch03.mp3" style="width:100%;margin-top:4px"></audio>

[Internet Archive で開く](https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch03.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Gemini Robotics ── VLAモデルのアーキテクチャと学習</h2>
<h3>システム全体のアーキテクチャ</h3>
<blockquote>
<p>📊 Fig. 5, 6 参照（原論文）</p>
</blockquote>
<pre><code>カメラ画像 ─┐
タスク指示  ─┤→ Gemini Robotics-ER → コンテキスト特徴 c
エンボディメント記述 ─┘
                              ↓
                   Gemini Robotics（VLA）
                              ↓
                   アクション a_t（関節角度ベクトル）
</code></pre>
<h3>アクション生成の仕組み</h3>
<p><strong>チャンク予測</strong>：1ステップずつでなく、複数ステップを一括予測：</p>
<p>$$\mathbf{a}_{t:t+H} = \pi_\theta(\mathbf{o}_t, \mathbf{c})$$</p>
<ul>
<li>$H$：予測ホライズン（例：16ステップ）</li>
<li>$\mathbf{o}_t$：現在の観測（画像＋状態）</li>
<li>$\mathbf{c}$：タスク指示と環境のコンテキスト</li>
</ul>
<h3>学習データ</h3>
<blockquote>
<p>📊 Fig. 7 参照（原論文）</p>
</blockquote>
<table>
<thead>
<tr>
<th>データ種別</th>
<th>内容</th>
</tr>
</thead>
<tbody>
<tr>
<td>ロボット操作デモ</td>
<td>多様なロボット・タスクのテレオペ軌跡</td>
</tr>
<tr>
<td>人間の動作映像</td>
<td>一人称視点の手作業映像（暗黙知の学習）</td>
</tr>
<tr>
<td>合成シミュレーション</td>
<td>IsaacSim 等で自動生成</td>
</tr>
<tr>
<td>補助VLデータ</td>
<td>キャプション・VQA（破壊的忘却防止）</td>
</tr>
</tbody>
</table>
<h3>ゼロショット汎化の仕組み</h3>
<ul>
<li><strong>自然言語によるエンボディメント記述</strong>：ロボットの仕様をテキストで渡す</li>
<li>例：「7自由度アーム、エンドエフェクタ位置xyz＋姿勢＋グリッパー開閉」</li>
<li>言語モデルの推論能力で未学習のロボット記述から類推</li>
<li><strong>マルチタスク学習</strong>による正の転移</li>
</ul>
<hr />

</details>

### 第4章: 特化訓練と汎化性能

<video controls width="100%" src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch04.mp3" style="width:100%;margin-top:4px"></audio>

[Internet Archive で開く](https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch04.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>特化訓練と汎化性能</h2>
<h3>3つの特化シナリオ</h3>
<blockquote>
<p>📊 Fig. 8, 9, 10 参照（原論文）</p>
</blockquote>
<p><strong>① 長期・高精度タスクへの特化</strong></p>
<ul>
<li>例：多段階の料理タスク、複雑な組み立て</li>
<li>ファインチューニングで数十ステップ先を見越した計画を学習</li>
<li>ERモデルの軌跡予測と組み合わせて精度向上</li>
</ul>
<p><strong>② 少数ショット学習（Few-shot）</strong></p>
<p>$$\mathcal{D}_{\text{new}} = \{(\mathbf{o}_i, \mathbf{a}_i)\}_{i=1}^{N}, \quad N \approx 100$$</p>
<ul>
<li>100デモ程度で新タスクを習得</li>
<li>基盤モデルの事前知識を活用するため少量のデモで収束</li>
<li>比較：ゼロから学習する場合は数千〜数万デモが必要</li>
</ul>
<p><strong>③ 新規ロボット形態への適応</strong></p>
<ul>
<li>学習時に見ていないロボット（新しいアーム・二足歩行ロボット等）に転移</li>
<li>エンボディメント記述テキストを変えるだけで動作</li>
<li>ゼロショット・または少量データでの迅速な適応</li>
</ul>
<h3>汎化性能の評価</h3>
<blockquote>
<p>📊 Fig. 11, 12 参照（原論文）</p>
</blockquote>
<ul>
<li><strong>物体バリエーション</strong>：未知の色・素材・形状の物体への対応率</li>
<li><strong>環境バリエーション</strong>：照明・背景が変わった場合の成功率</li>
<li><strong>指示バリエーション</strong>：表現が異なる同義の指示への対応</li>
</ul>
<p><strong>DROID ベンチマーク（多様ロボット操作）</strong>での成績が示される</p>
<hr />

</details>

### 第5章: 安全性・実験結果・今後の展望

<video controls width="100%" src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch05.mp3" style="width:100%;margin-top:4px"></audio>

[Internet Archive で開く](https://archive.org/download/paper-explain-2503-20020/paper_2503.20020_ch05.mp4){:target="_blank"}

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>安全性・実験結果・今後の展望</h2>
<h3>安全性の考慮（重要）</h3>
<blockquote>
<p>📊 Fig. 13 参照（原論文）</p>
</blockquote>
<p>ロボット基盤モデルの安全性は通常のLLMと異なる課題を持つ：</p>
<table>
<thead>
<tr>
<th>リスク</th>
<th>対策</th>
</tr>
</thead>
<tbody>
<tr>
<td>物理的危害</td>
<td>動作速度・力の上限設定、異常検知</td>
</tr>
<tr>
<td>意図しない行動</td>
<td>タスク外の動作拒否メカニズム</td>
</tr>
<tr>
<td>悪用</td>
<td>エンボディメント記述の検証</td>
</tr>
<tr>
<td>データバイアス</td>
<td>多様なデモデータの収集</td>
</tr>
</tbody>
</table>
<p><strong>安全フィルタリング</strong>：
- 危険な動作パターンを学習データから除外
- 実行前の動作計画の安全性チェック</p>
<h3>実験結果</h3>
<blockquote>
<p>📊 Fig. 14, 15, 16 参照（原論文）</p>
</blockquote>
<p><strong>ゼロショット操作タスク</strong>：
- 多様な物体把持・配置タスクで高い成功率
- 未知物体・環境でもロバストに動作</p>
<p><strong>長期タスク</strong>：
- 10ステップ以上の複合タスクで従来手法を上回る成功率
- ERモデルの事前計画が精度に大きく貢献</p>
<p><strong>少数ショット適応</strong>：
- 100デモで新タスクに適応（ベースラインの3〜5倍の成功率）
- 1000デモでほぼ飽和（従来手法は数千〜数万必要）</p>
<h3>Qwen-VLA との比較</h3>
<table>
<thead>
<tr>
<th></th>
<th>Gemini Robotics</th>
<th>Qwen-VLA</th>
</tr>
</thead>
<tbody>
<tr>
<td>基盤モデル</td>
<td>Gemini 2.0</td>
<td>Qwen VLM</td>
</tr>
<tr>
<td>特徴</td>
<td>ERモデルを分離独立</td>
<td>DiT拡散デコーダ</td>
</tr>
<tr>
<td>データ規模</td>
<td>大規模（非公開）</td>
<td>大規模（一部公開）</td>
</tr>
<tr>
<td>ゼロショット</td>
<td>◎</td>
<td>◎</td>
</tr>
</tbody>
</table>
<h3>今後の展望</h3>
<ol>
<li><strong>より長期的な計画</strong> ── 数百ステップ規模のタスク</li>
<li><strong>触覚・力覚センサの統合</strong> ── 繊細な操作</li>
<li><strong>オンライン学習</strong> ── 実機での失敗から自動改善</li>
<li><strong>マルチロボット協調</strong> ── 複数ロボットの連携</li>
<li><strong>安全性の強化</strong> ── より堅牢な安全保証の確立</li>
</ol>
<h3>参考</h3>
<ul>
<li>Google DeepMind, "Gemini Robotics: Bringing AI into the Physical World," arXiv:2503.20020 (2025)</li>
<li>https://arxiv.org/abs/2503.20020</li>
</ul>

</details>

---

[← 論文一覧に戻る](../../)
