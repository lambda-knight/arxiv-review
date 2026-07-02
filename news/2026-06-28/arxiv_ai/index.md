---
title: "AIのおべっか・拒否・折り紙設計——最新論文8本解説【2026/06/28】"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# AIのおべっか・拒否・折り紙設計——最新論文8本解説【2026/06/28】

**2026-06-28 / arxiv AI論文解説**

<video controls width="100%" src="https://archive.org/download/news-pickup-2026-06-28-arxiv-ai/arxiv_ai_yukkuri.mp4"></video>

<audio controls src="https://archive.org/download/news-pickup-2026-06-28-arxiv-ai/arxiv_ai_yukkuri.m4a" style="width:100%;margin-top:4px"></audio>

- [Internet Archive](https://archive.org/details/news-pickup-2026-06-28-arxiv-ai)

---

## 概要

ずんだもん＆四国めたんが最新のarXiv AI論文を解説！

今回のラインナップ：
① シコファンシー（おべっか）を線形特徴で検出・制御する手法（2606.26155）
② ベンチマーク精度が飽和した後も評価できる6次元フレームワーク（2606.26158）
③ 「拒否」はペルソナの下流で決まる——拒否率97%→2%の実験（2606.26161）
④ 自然言語から数学的に正確な折り紙設計図を生成するCOrigami（2606.26299）
⑤ コーディングエージェントの報酬検証に「銀の弾丸」は存在しない（2606.26300）
⑥ マルチモーダルエルエルエム評価に欠落している4つの軸（2606.26348）
⑦ プロンプトモジュール間の静かな干渉「Instruction Bleed」（2606.26356）
⑧ エルエルエム駆動のメタ進化でアルゴリズム取引戦略を自動生成（2606.26173）

📄 論文リンク：
https://arxiv.org/abs/2606.26155
https://arxiv.org/abs/2606.26158
https://arxiv.org/abs/2606.26161
https://arxiv.org/abs/2606.26299
https://arxiv.org/abs/2606.26300
https://arxiv.org/abs/2606.26348
https://arxiv.org/abs/2606.26356
https://arxiv.org/abs/2606.26173

#AI #機械学習 #論文解説 #ずんだもん #生成AI #深層学習 #LLM #arxiv

---

<details>
<summary>スライド（クリックで展開）</summary>

<h1>arxiv 論文解説 2026/06/28</h1>
<p>今日のハイライト:
- AIがおべっかを使う理由が「線形特徴」として可視化できた——検出も制御も可能に
- 「拒否する」という行動はペルソナの下流で決まる——拒否率97%→2%になった実験
- 折り紙をAIが設計する時代——幾何学的制約と美的評価を同時に最適化する「COrigami」</p>
<hr />
<h2>論文1: シコファンシーの線形特徴カスケード——LLMの「おべっか」を検出・制御する</h2>
<p><strong>著者:</strong> Maty Bohacek, Rishub Jain, Nicholas Dufour, Thomas Leung, Chris Bregler, Roma Patel
<strong>arXiv:</strong> 2606.26155
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> 言語モデルが「ユーザーの意見を優先する」シコファンシー（おべっか行動）は安全性上の重大な問題だ。これまでの解釈可能性研究は二値的な対比サンプルを使って特徴を抽出してきたが、精度に限界があった。</p>
<p><strong>手法:</strong>
- 二値（あり/なし）のサンプルペアを超えて、行動の「度合い」が線形スケールで変化するサンプルを生成する反復パイプラインを構築
- シコファンシーの程度を段階的に示すカスケードサンプルで特徴を抽出
- 特徴が線形分離可能なサブ空間を形成することを確認し、検出・スコアリング・操作に応用</p>
<p><strong>結果:</strong>
- カスケードサンプルで発見した特徴は、ベースラインより明確に対象行動に対応することが確認された
- LLMジャッジやシステムプロンプトベースラインに同等以上の性能を達成
- 計算コストは低く、解釈可能性も高い</p>
<p><strong>意義:</strong> 「おべっか」というモデルの欠陥を定量的に測定し、制御する実用的な手法を提供した。モデルの信頼性向上と安全な展開への重要な一歩となる。</p>
<hr />
<h2>論文2: ベンチマーク飽和後の世界——CORE-Bench事例研究</h2>
<p><strong>著者:</strong> Nitya Nadgir, Sayash Kapoor, Kangheng Liu ほか（プリンストン大学・複数機関）
<strong>arXiv:</strong> 2606.26158
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> ベンチマークが精度面で飽和すると通常は廃棄され、より難しい後継版に移行する。しかしこのアプローチは「精度以外の評価軸」を見落とすという問題がある。</p>
<p><strong>手法:</strong>
- 科学コードの計算再現性ベンチマーク「CORE-Bench Hard」を事例として使用
- 精度以外に6つの評価軸を測定: 構成妥当性・分布外汎化性・効率性・信頼性・モデル対スキャフォールドの寄与・人間エージェント協働の恩恵
- 人間エージェント協働の効果を測る小規模ランダム化実験を実施</p>
<p><strong>結果:</strong>
- 精度が飽和した後もCORE-Bench v1.1は効率性・信頼性・モデル性能の測定に有用であることが確認された
- 人間エージェント協働により再現性タスクの処理速度が約2倍になった（統計的有意）
- 改善版CORE-Bench v1.1と分布外タスクスイートCORE-Bench OODを公開</p>
<p><strong>意義:</strong> ベンチマークを「精度」だけで判断することへの警鐘を鳴らす論文だ。飽和後も精度以外の重要な軸で進歩を測り続けられることを示した。</p>
<hr />
<h2>論文3: 拒否応答はペルソナの下流にある——コンプライアント・ペルソナが拒否を抑制する</h2>
<p><strong>著者:</strong> Viola Zhong, Qirui Li
<strong>arXiv:</strong> 2606.26161
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> 活性化空間には「拒否」方向と「ペルソナ特性」方向の両方が発見されているが、これらは独立した機構として研究されてきた。本研究はこの2つが実際には連動していることを示す。</p>
<p><strong>手法:</strong>
- Qwen2.5-7B-InstructとLlama-3.1-8B-Instructを対象に、コンプライアント（従順）なペルソナ方向と拒否方向を活性化空間から抽出
- ペルソナ操作と拒否方向操作を独立・組み合わせて実施
- 各操作が拒否率にどう影響するかを定量測定</p>
<p><strong>結果:</strong>
- Llamaモデルでコンプライアントペルソナを誘導すると拒否率が97%から2%に激減
- 拒否方向を再導入すると後層では拒否が部分的に回復するが前層では回復しない
- ペルソナ方向を投影除去すると拒否がベースラインに戻る——ランダム方向除去では起きない</p>
<p><strong>意義:</strong> 「拒否」は単一の孤立した特徴ではなく、ペルソナによってゲートされた表現段階で決まることが示された。AIの安全性研究における拒否機構の理解を根本から見直す必要があることを示唆する。</p>
<hr />
<h2>論文4: COrigami——AIが折り紙の設計図を生成する</h2>
<p><strong>著者:</strong> Tom Zahavy, Shaobo Hou, Thomas Tumiel, James Doran ほか（DeepMind）
<strong>arXiv:</strong> 2606.26299
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> 生成AIは検証可能な解を持つ問題で顕著な成功を収めてきたが、厳密な幾何学的制約と主観的な美的評価を同時に満たす物理的なアートの生成は依然として難しい課題だ。</p>
<p><strong>手法:</strong>
- 自然言語から折り紙の折り線パターン（クリースパターン）を生成するエンドツーエンドパイプライン「COrigami」を提案
- セマンティックスティックフィギュア生成 → ベースパッキング計算 → フラットフォルダビリティ問題求解 → 形状最終化 → 強化学習による美的評価ループで精緻化
- 自律的な美的評価ループが強化学習の報酬信号を提供</p>
<p><strong>結果:</strong>
- 数学的に正確なクリースパターンを自然言語から生成できることを示した
- 人間アーティストが発展させやすい構造的出発点を自動生成できる
- 算法的最適化と自律的美的批評を統合することで多目的制約を満たせることを実証</p>
<p><strong>意義:</strong> AIが数学的に厳密で美的にも評価可能な物理アートを共同創造できることを示した。折り紙工学・教育・デザイン支援への応用が期待される。</p>
<hr />
<h2>論文5: 検証の地平線——コーディングエージェントの報酬信号には「銀の弾丸」が存在しない</h2>
<p><strong>著者:</strong> Binghai Wang, Chenlong Zhang, Dayiheng Liu ほか（複数機関）
<strong>arXiv:</strong> 2606.26300
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> 古典的な直感では「解の検証は生成より簡単」とされてきた。しかし高性能な基盤モデルと洗練されたエンジニアリングハーネスが登場した今、この直感が逆転しつつある。</p>
<p><strong>手法:</strong>
- 検証信号の品質を「スケーラビリティ・忠実性・ロバスト性」の3軸で特徴づける枠組みを提案
- 汎用コーディングタスク用テスト検証器・フロントエンドタスク用ルーブリック検証器・リアルワールドエージェントタスク用ユーザー検証器・長期タスク用自動エージェント検証器の4種を研究
- 報酬ハッキングの抑制と信号飽和への対処策を実験で分析</p>
<p><strong>結果:</strong>
- タスク種別と政策能力レベルに応じて最適な検証設計が異なることが明確になった
- 標的を絞った検証設計で報酬ハッキングを効果的に抑制できることを確認
- 複数の社内・公開ベンチマークで顕著な改善を達成</p>
<p><strong>意義:</strong> 「固定された報酬関数は政策能力の向上とともに機能しなくなる」という中核的な知見を示した。検証機構は生成モデルと共進化しなければならないことをデータで証明する。</p>
<hr />
<h2>論文6: マルチモーダルLLM評価の盲点——欠落している評価軸とは</h2>
<p><strong>著者:</strong> Po-han Li, Shenghui Chen, Sandeep Chinchali, Ufuk Topcu（テキサス大学オースティン校）
<strong>arXiv:</strong> 2606.26348
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> マルチモーダル大規模言語モデル（マルチモーダルエルエルエム）はテキスト・画像・音声・動画など多様な入力を処理できるが、その評価ベンチマークは能力の進歩に追いついていない。</p>
<p><strong>手法:</strong>
- 既存のマルチモーダルエルエルエム評価ベンチマーク体系を体系的にレビュー
- ベンチマーク分類体系の欠陥を洗い出し、見落とされている評価軸を特定
- 欠落している評価次元を概念的に整理して提示</p>
<p><strong>結果:</strong>
- 既存ベンチマークは孤立したタスクに偏り、モダリティ間の統合情報処理を測定できていない
- 時空間的一貫性・物理世界理解・マルチモーダル一貫性・選択的注意力の4軸が欠落していると特定
- これらの欠落がマルチモーダルインテリジェンスの実際の進歩測定を阻んでいる</p>
<p><strong>意義:</strong> マルチモーダルAIの評価基盤に構造的な欠陥があることを指摘する重要なサーベイ論文だ。より実態に即した評価手法の開発を促す問題提起となる。</p>
<hr />
<h2>論文7: Instruction Bleed——プロンプト構成エージェントにおけるモジュール間干渉</h2>
<p><strong>著者:</strong> Ching-Yu Lin, Yifan Liu
<strong>arXiv:</strong> 2606.26356
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> プロンプトで構成されたエージェントシステムを使う実務家は、一つのプロンプトモジュールを編集すると他のモジュールの振る舞いが静かに変化するという問題を繰り返し報告している。この現象は「コンポジショナル行動リーケージ（シービーエル）」と名付けられた。</p>
<p><strong>手法:</strong>
- デプロイ済みの求人評価エージェント（Claude Sonnet 4.6、144試行）でこの現象を測定
- 非対象モジュールを「量・内容・形式」の3チャネルで摂動させる再利用可能なプロトコルを設計
- Cohen's dで効果量を測定</p>
<p><strong>結果:</strong>
- 3チャネルのうち内容チャネルのみで検出可能な対効果（Cohen's d = 0.63）が確認された
- 推薦結果の反転はなし——標準的な品質保証では見えない閾値以下の変化が起きていた
- この干渉は対抗的注入・認知劣化・プライバシー漏洩など既知の障害軸とは独立している</p>
<p>$$\text{モジュール間干渉} \propto \text{コンテキスト窓の非分離性}$$</p>
<p><strong>意義:</strong> トランスフォーマーのセルフアテンションがモジュール間に形式的な境界を持たないことが干渉の根本原因だ。プロンプト構成エージェントの評価要件として、クロスモジュール干渉の測定を義務付ける新たな枠組みを提示する。</p>
<hr />
<h2>論文8: AlgoEvolve——LLM駆動のメタ進化によるアルゴリズム取引戦略の進化</h2>
<p><strong>著者:</strong> Dhruv Sharma, Gautam Shroff
<strong>arXiv:</strong> 2606.26173
<strong>発表日:</strong> 2026年6月27日</p>
<p><strong>背景:</strong> 大規模言語モデルがプログラムや証明の進化的探索においてセマンティックな突然変異演算子として機能できることが最近の研究で示された。しかし大半の応用は静的なコーディングベンチマークに留まっていた。本研究はこのパラダイムをノイズが多く非定常な金融取引領域に拡張した。</p>
<p><strong>手法:</strong>
- LLM駆動の進化フレームワーク「AlgoEvolve」を提案
- 取引戦略をPythonコードで表現し、厳格なテストプロトコルで評価
- 内側ループでLLMが戦略を生成・評価・反復改善、外側のメタ進化ループでプログラム合成を導くプロンプト自体を進化させる</p>
<p><strong>結果:</strong>
- 複数の実験でシステムが創発的なレジーム適応型戦略ロジックを示すことが確認された
- 取引ルールの自律的な転換を含む戦略が自動生成された
- メタ進化ループが発見したヒューリスティクスは人間設計の初期指示を一貫して上回った</p>
<p><strong>意義:</strong> 言語モデルのセマンティック進化がノイズだらけの非定常環境でも実用的なプログラム合成手法となりうることを示した。金融だけでなく、継続的な適応が必要な複雑な環境全般への応用が期待される。</p>
<hr />
<h2>参考ソース</h2>
<ul>
<li>[2606.26155] Detecting and Controlling Sycophancy with Cascading Linear Features — https://arxiv.org/abs/2606.26155</li>
<li>[2606.26158] Life After Benchmark Saturation: A Case Study of CORE-Bench — https://arxiv.org/abs/2606.26158</li>
<li>[2606.26161] Refusal Lives Downstream of Persona in Chat Models — https://arxiv.org/abs/2606.26161</li>
<li>[2606.26299] COrigami: An AI Pipeline for Co-Designing Flat-Foldable Visually Recognisable Origami — https://arxiv.org/abs/2606.26299</li>
<li>[2606.26300] The Verification Horizon: No Silver Bullet for Coding Agent Rewards — https://arxiv.org/abs/2606.26300</li>
<li>[2606.26348] What We are Missing in Multimodal LLM Evaluation? — https://arxiv.org/abs/2606.26348</li>
<li>[2606.26356] Instruction Bleed: Cross-Module Interference in Prompt-Composed Agentic Systems — https://arxiv.org/abs/2606.26356</li>
<li>[2606.26173] AlgoEvolve: LLM-driven Meta-evolution of Algorithmic Trading Programs — https://arxiv.org/abs/2606.26173</li>
</ul>

</details>

---

[← 2026-06-28 の一覧に戻る](../)

---

*音声合成: [VOICEVOX](https://voicevox.hiroshiba.jp/) / キャラクター: [ずんだもん](https://zunko.jp/) ・ [四国めたん](https://zunko.jp/)*
