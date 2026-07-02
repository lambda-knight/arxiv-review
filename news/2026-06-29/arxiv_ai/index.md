---
title: "「確率が高い=正しい」はなぜ間違い？ AIエージェントの欠陥解剖ほか生成AI論文8本【2026/06/29】"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 「確率が高い=正しい」はなぜ間違い？ AIエージェントの欠陥解剖ほか生成AI論文8本【2026/06/29】

**2026-06-29 / arxiv AI論文解説**

<video controls width="100%" src="https://archive.org/download/news-pickup-2026-06-29-arxiv-ai/arxiv_ai_yukkuri.mp4"></video>

<audio controls src="https://archive.org/download/news-pickup-2026-06-29-arxiv-ai/arxiv_ai_yukkuri.m4a" style="width:100%;margin-top:4px"></audio>

- [Internet Archive](https://archive.org/details/news-pickup-2026-06-29-arxiv-ai)

---

## 概要

マルチモーダルモデルの「視覚無視」問題・デコード戦略の根本的誤解・ジェイルブレイク自動最適化の警告など、今週の生成AI論文8本をずんだもん＆四国めたんが解説します。

▼ 今日の論文ラインナップ
・VISE: 自己進化型マルチモーダルモデルの視覚無視問題を修正（ECCV 2026採択）— モハメッド・ビン・ザイード人工知能大学（arXiv:2606.27373）
・確率が高い回答=正しい回答は成立しない — デコード戦略の根本前提を検証（arXiv:2606.27359）
・エージェントAIの完全ガイド — 基礎から本番デプロイまで（arXiv:2606.24937）
・タスク無感覚性: エージェントが指示を無視する構造的欠陥の特定と修正（arXiv:2606.26918）
・意味的早期停止: 反復エージェントループのトークンを38%削減（arXiv:2606.27009）
・バンディットによるジェイルブレイク自動最適化 — 97%成功率の警告（arXiv:2606.26936）
・ViQ: テキスト整合型視覚量子化で訓練を20〜70%高速化（arXiv:2606.27313）
・LLMによる量子実験制御＋ハードウェア安全ゲート（デューク大学）（arXiv:2606.27231）

▼ 参考論文（arXiv）
https://arxiv.org/abs/2606.27373  — VISE: 自己進化型マルチモーダルモデルの視覚無視問題を修正
https://arxiv.org/abs/2606.27359  — 確率と正解の罠
https://arxiv.org/abs/2606.24937  — エージェントAIのヒッチハイカーズガイド
https://arxiv.org/abs/2606.26918  — タスク無感覚性: エージェントが指示を無視する構造的欠陥
https://arxiv.org/abs/2606.27009  — 意味的早期停止
https://arxiv.org/abs/2606.26936  — バンディットによるジェイルブレイク自動最適化
https://arxiv.org/abs/2606.27313  — ViQ: テキスト整合型視覚量子化
https://arxiv.org/abs/2606.27231  — LLMによる量子実験制御

#生成AI #ChatGPT #Claude #LLM #AI #人工知能 #arxiv #論文解説 #ゆっくり解説 #ずんだもん #OpenAI #Anthropic #AIエージェント #機械学習 #ディープラーニング

---

<details>
<summary>スライド（クリックで展開）</summary>

<h1>arxiv 論文解説 2026/06/29</h1>
<p>今日のハイライト:
- マルチモーダルモデルが「画像を見ていない」問題を自己進化で解決——VISEが視覚注意を強制する
- 確率が高い回答=正しい回答とは限らない——デコード戦略の根本的な誤解を検証
- AIエージェントが「タスクを無視する」欠陥のメカニズムと修正法
- バンディットアルゴリズムでジェイルブレイクを自動最適化——97%の成功率という警告</p>
<hr />
<h2>論文1: VISE——自己進化型マルチモーダルモデルの「視覚無視」問題を修正する</h2>
<p><strong>著者:</strong> Shravan Venkatraman, Ritesh Thawkar, Omkar Thawakar, Rao Muhammad Anwer, Hisham Cholakkal, Salman Khan, Fahad Khan（モハメッド・ビン・ザイード人工知能大学ほか）
<strong>arXiv:</strong> 2606.27373
<strong>発表日:</strong> 2026年6月28日</p>
<p><strong>背景:</strong> 自己進化型マルチモーダルモデルは回答一貫性を最適化するが、デコーダが実際に画像を「見て」いることを保証しない。その結果、言語パターンに頼った「視覚的アンダーコンディショニング」という欠陥が生じる。</p>
<p><strong>手法:</strong>
- 純粋な教師なし自己進化フレームワーク「VISE（Visual Invariance Self-Evolution）」を提案
- 幾何学的不変性報酬（画像の幾何変換後も同じ回答が得られるか）とセマンティック不変性報酬の2軸で視覚注意を正則化
- 単一モデルで完結し、外部アノテーションも専門家役割分担も不要
- ラベルなし画像のみで学習</p>
<p><strong>結果:</strong>
- Qwen3-VL-2Bをベースとして、COCO画像キャプションで+16.85 CIDEr、TextCapsで+19.66 CIDErの大幅改善
- オブジェクト幻覚を低減
- 複数モデルアーキテクチャとスケールで汎化を確認
- ECCV 2026採択</p>
<p><strong>意義:</strong> マルチモーダルモデルが「画像を見ているふりをしている」という根本的な問題を自己改善ループで解決した。外部ラベル不要という実用的なアプローチは、大規模デプロイにおける重要な一歩となる。</p>
<hr />
<h2>論文2: 確率と正解の罠——エルエルエムにおける「確率が高い=正しい」は成立しない</h2>
<p><strong>著者:</strong> Johannes Zenn, Jonas Geiping（所属機関はarXivに非掲載）
<strong>arXiv:</strong> 2606.27359
<strong>発表日:</strong> 2026年6月28日</p>
<p><strong>背景:</strong> デコード戦略の改善でLLMの精度を向上させようとする研究は「確率の高い回答が正しい」という前提に立っている。この前提が実際に成立するか否かを系統的に検証した。</p>
<p><strong>手法:</strong>
- シーケンス確率と正解率の関係を複数の分析レベルで調査
- データセット間での「確率と正解の相関」を測定
- ハイパーパラメータ調整でシーケンス確率を意図的に変化させ、精度への影響を分析
- 同一プロンプトに対する複数の回答間でも比較検証</p>
<p><strong>結果:</strong>
- データセット全体での比較では確率が高い回答のほうが正解率が高い傾向は確認された
- しかしハイパーパラメータ変更でシーケンス確率を上げると精度は向上しない
- 同一プロンプトへの複数回答間での確率は正解の識別に信頼できない</p>
<p><strong>意義:</strong> 「確率を上げれば賢くなる」という直感に反する知見を提供した。デコード最適化・自己一貫性手法・検証器なし自己改善技術の設計思想を見直す必要があることを示す。</p>
<hr />
<h2>論文3: エージェントAIの完全ガイド——基礎からシステム構築まで</h2>
<p><strong>著者:</strong> Haggai Roitman（所属機関はarXivに非掲載）
<strong>arXiv:</strong> 2606.24937
<strong>発表日:</strong> 2026年6月22日</p>
<p><strong>背景:</strong> AIエージェントのスタック全体——トランスフォーマー基盤からマルチエージェント協調まで——を実務的観点から体系化した参考文献が不足していた。本論文はその包括的なガイドを提供する。</p>
<p><strong>手法（カバー範囲）:</strong>
- 基盤エルエルエム: トランスフォーマーアーキテクチャ・GPU最適化・LoRA・エムオーイー・推論最適化
- アライメントと推論: RLHF・PPO・DPO・テストタイムスケーリング
- エージェント技術: ラグ（RAG）・メモリ（インコンテキスト/外部/エピソード/セマンティック）・ツール使用
- マルチエージェント協調: モデルコンテキストプロトコル（エムシーピー）・A2A通信・中央集権/分散/階層トポロジー
- プロダクション: 評価・UI設計・デプロイ戦略</p>
<p><strong>意義:</strong> エージェントAI開発に携わる実務家にとって体系的な一冊。理論と実装の両方に踏み込んだ設計が特徴で、急速に変化する分野の現時点でのまとめとして参照価値が高い。</p>
<hr />
<h2>論文4: タスク無感覚症候群——エージェントが「指示を無視する」根本原因と治療法</h2>
<p><strong>著者:</strong> Jingyu Liu, Xiaopeng Wu, Kehan Chen, Chuan Yu, Yong Liu（所属機関はarXivに非掲載）
<strong>arXiv:</strong> 2606.26918
<strong>発表日:</strong> 2026年6月25日</p>
<p><strong>背景:</strong> エルエルエムをエージェントとして使うと、分布外タスクで失敗するケースが繰り返し報告されている。本研究はその根本原因として「タスク無感覚性」を特定した。</p>
<p><strong>手法:</strong>
- モデルが訓練パターンを適用し、手元のタスクを「解かない」失敗パターン（タスク無感覚性）を定義
- タスク説明を意味的に破壊しても、モデルが同一の出力を返すことを実験で確認
- アテンションパターンを分析し、訓練中にタスクトークンへの注意が局所的な観察へとドリフトすることを発見
- 「タスク摂動負の対数尤度最適化（Task-Perturbed NLL Optimization）」という軽量なコントラスト正則化項を提案</p>
<p><strong>結果:</strong>
- タスク感度の向上と分布外汎化の改善を確認
- タスクトークンへのアテンションが安定して維持されるようになった</p>
<p><strong>意義:</strong> エージェントのOOD失敗を「確率的なエラー」ではなく「構造的な欠陥」として捉え直した。軽量な修正で根本原因に対処できることを示した点が重要だ。</p>
<hr />
<h2>論文5: 意味的早期停止——エルエルエムエージェントループのトークン消費を38%削減</h2>
<p><strong>著者:</strong> Sahil Shrivastava（所属機関はarXivに非掲載）
<strong>arXiv:</strong> 2606.27009
<strong>発表日:</strong> 2026年6月25日</p>
<p><strong>背景:</strong> ライター・クリティックのような反復型マルチエージェントループは通常、固定の最大反復回数で打ち切られる。しかし「これ以上改善しない」という判断を動的にできれば、大幅なコスト削減が可能だ。</p>
<p><strong>手法:</strong>
- 連続する草稿の埋め込みがコサイン距離で収束し、かつ回答の品質が向上しなくなった時点で終了する「意味的早期停止」を提案
- 埋め込みベースの収束検出と「我慢窓（patience window）」を組み合わせる
- 決定論的終了と well-definiteness の理論的保証を機械検証済み証明で提供
- HotpotQAを使ったエルエルエムジャッジキャッシュプロトコルで公平な評価</p>
<p><strong>結果:</strong>
- 同等品質を維持しつつ演算トークンを38%削減（Δ-IS = -0.004、p = 0.81）
- オラクル（最適ラウンド選択）がすべての実用的ポリシーを上回ることを確認
- 問題は「いつ止めるか」ではなく「どのラウンドが最善か」だと再定義</p>
<p><strong>意義:</strong> 推論コストが急増するマルチエージェント時代に、計算予算を大幅に節約できる実用的な手法を提供した。理論保証付きという点も実務信頼性の面で重要だ。</p>
<hr />
<h2>論文6: バンディットでジェイルブレイクを自動最適化——素人でも97%成功率</h2>
<p><strong>著者:</strong> Prarabdh Shukla, Ritik, Suhas Rao, Arpit Agarwal, Arjun Bhagoji（所属機関はarXivに非掲載）
<strong>arXiv:</strong> 2606.26936
<strong>発表日:</strong> 2026年6月28日</p>
<p><strong>背景:</strong> エルエルエムのジェイルブレイク攻撃は専門知識なしには難しいとされてきた。しかし自動化されたバンディットアルゴリズムを使えば、非専門家でも最適なジェイルブレイク手法を効率よく発見できるのではないか。</p>
<p><strong>手法:</strong>
- 多腕バンディットフレームワークを使い、大量の選択肢から「ノイジーな探索」で最適ジェイルブレイクを学習する手法を提案
- FrankensteinBench: 11,279件の悪意あるクエリを技術的難易度別にカテゴリ分けしたベンチマークを構築
- クエリ複雑度を自動増加させる仕組みを組み込む
- 15本のオープンウェイトエルエルエムで評価</p>
<p><strong>結果:</strong>
- 最大97%の攻撃成功率を達成
- クエリ複雑度の増加で攻撃成功率が平均26%向上
- 専門知識なしでも実用的な攻撃が可能</p>
<p><strong>意義:</strong> AIセーフティへの実践的な脅威を示した重要な警告論文だ。攻撃の自動化と低コスト化が進んでいることを示し、オープンウェイトモデルの安全対策強化の必要性を訴える。</p>
<hr />
<h2>論文7: ViQ——マルチモーダル視覚量子化で訓練を20〜70%高速化</h2>
<p><strong>著者:</strong> Xuanyuan Yu, Zuyan Liu, Zhenyu Yang, Yuhao Dong, Shengsheng Qian, Jiwen Lu, Han Hu, Yongming Rao（清華大学・マイクロソフトリサーチほか）
<strong>arXiv:</strong> 2606.27313
<strong>発表日:</strong> 2026年6月28日</p>
<p><strong>背景:</strong> マルチモーダルモデルの訓練では「意味的な詳細」と「視覚的な細部」の両方を量子化表現に収める必要がある。これらは通常トレードオフにあり、解像度依存の問題もある。</p>
<p><strong>手法:</strong>
- テキスト整合型視覚量子化表現「ViQ（Visual Quantized Representations）」を提案
- 意味と視覚細部のバランスを保ちながら、任意解像度に対応するネイティブ解像度サポートを実現
- マルチモーダル訓練に統合することで推論の効率化を実証</p>
<p><strong>結果:</strong>
- マルチモーダル訓練において20〜70%の高速化を達成
- 意味と細部の両立を確認</p>
<p><strong>意義:</strong> 大規模マルチモーダルモデルの訓練コストを大幅に削減する実用的な手法。視覚トークン効率化研究の重要な前進となる。</p>
<hr />
<h2>論文8: エルエルエムで量子実験を制御——安全ゲートで人間の監督を形式的に保証</h2>
<p><strong>著者:</strong> Duanyang Wang, Lu Qi, Yuanheng Xie, Norbert M. Linke, Kenneth R. Brown（デューク大学）
<strong>arXiv:</strong> 2606.27231
<strong>発表日:</strong> 2026年6月28日</p>
<p><strong>背景:</strong> トラップイオン型量子コンピュータの制御には専門的なプログラミングが必要で、エルエルエムによる自律制御が検討されている。しかし量子実験の制御コードを誤ると機器破損や実験失敗につながるため、安全性保証が不可欠だ。</p>
<p><strong>手法:</strong>
- ハードウェア安全性ゲートを組み込んだシステムを設計
- エルエルエムが書いたARTIQネイティブ制御コードを人間が承認する形式的な認可境界を設定
- 人間監督とエージェント決定の間に明確な境界線を引く</p>
<p><strong>結果:</strong>
- エルエルエム生成コードが量子実験制御で動作することを実証
- 形式的な安全境界により、人間の監督なしにエージェントが危険な操作をできない構造を実現</p>
<p><strong>意義:</strong> 科学実験制御という高リスク領域への自律AIエージェント適用に対して、安全性の形式的保証を提供するフレームワークを示した。量子コンピューティング研究の自動化加速への重要な布石となる。</p>
<hr />
<h2>参考ソース</h2>
<ul>
<li>[2606.27373] Paying More Attention to Visual Tokens in Self-Evolving Large Multimodal Models — https://arxiv.org/abs/2606.27373</li>
<li>[2606.27359] When are likely answers right? On Sequence Probability and Correctness in LLMs — https://arxiv.org/abs/2606.27359</li>
<li>[2606.24937] The Hitchhiker's Guide to Agentic AI: From Foundations to Systems — https://arxiv.org/abs/2606.24937</li>
<li>[2606.26918] Diagnosing Task Insensitivity in Language Agents — https://arxiv.org/abs/2606.26918</li>
<li>[2606.27009] Semantic Early-Stopping for Iterative LLM Agent Loops — https://arxiv.org/abs/2606.27009</li>
<li>[2606.26936] Jailbreaking for the Average Jane: Choosing Optimal Jailbreaks via Bandit Algorithms — https://arxiv.org/abs/2606.26936</li>
<li>[2606.27313] ViQ: Text-Aligned Visual Quantized Representations at Any Resolution — https://arxiv.org/abs/2606.27313</li>
<li>[2606.27231] A hardware-safety-gated system for LLM-written native ARTIQ control code on trapped-ion platform — https://arxiv.org/abs/2606.27231</li>
</ul>

</details>

---

[← 2026-06-29 の一覧に戻る](../)

---

*音声合成: [VOICEVOX](https://voicevox.hiroshiba.jp/) / キャラクター: [ずんだもん](https://zunko.jp/) ・ [四国めたん](https://zunko.jp/)*
