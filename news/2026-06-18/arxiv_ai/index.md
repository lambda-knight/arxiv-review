---
title: "研究者が今週注目した生成AI論文解説【2026/06/18】"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 研究者が今週注目した生成AI論文解説【2026/06/18】

**2026-06-18 / arxiv AI論文解説**

<audio controls src="https://archive.org/download/news-pickup-2026-06-18-arxiv-ai/arxiv_ai_yukkuri.m4a" style="width:100%;margin-top:4px"></audio>

- [Internet Archive](https://archive.org/details/news-pickup-2026-06-18-arxiv-ai)

---

## 概要

2026年6月18日のarxivから、生成AI・LLM分野の注目論文7本をずんだもん＆四国めたんが解説！
スライド自動生成エージェントの個人化技術から、LLMが長編ストーリーで全滅する衝撃の結果まで幅広くカバーします。

▼ 今日の論文
1. MemSlides (2606.17162)
   階層型メモリでユーザーの好みを記憶し、個人化されたスライドをマルチターン対話で生成するエージェントフレームワーク

2. RepSelect (2606.17168)
   表現選択性ベースのLLMアンラーニング。ファインチューニング後も忘却が維持できる率を従来比40%向上

3. AIエージェントコミュニティのパラソーシャル関係 (2606.17174)
   AIエージェント同士のSNSコミュニティで「推しへの片思い」が自発的に発生することを実証

4. Self-Generated Error Training (2606.17175)
   モデル自身が生成する典型的なエラーで訓練することで、拡散言語モデルのトークン編集精度を最大8ポイント改善

5. LLM翻訳の自己信頼度の信頼性 (2606.17234)
   機械翻訳でLLMが示す自己評価型信頼度が実際の精度と一致しない「過信」傾向を定量的に解明

6. NarrativeWorldBench (2606.17391)
   長編シリアル音声ドラマ生成で21のフロンティアLLMを評価。全モデルが世界モデル整合性スコア0.6未満で全滅

7. MODE-RAG (2606.17449)
   エネルギーベースの評価でマルチモーダルRAGのハルシネーション・因果捏造・お追従を診断し18%削減

#生成AI #arxiv #論文解説 #ずんだもん #四国めたん #LLM #AI #RAG #アンラーニング #機械翻訳

---

<details>
<summary>スライド（クリックで展開）</summary>

<h1>arxiv AI論文解説 2026年06月18日</h1>
<h2>MemSlides: 階層型メモリで個人化スライドを自動生成するエージェント</h2>
<p><strong>論文ID</strong>: 2606.17162<br />
<strong>著者</strong>: MemSlides チーム</p>
<h3>概要</h3>
<p>ユーザーの好みを記憶しながら、マルチターンの修正対話でスライドを生成するエージェントフレームワーク。タスクをまたいでユーザー設定を保持し、局所的な修正指示にも柔軟に対応する。</p>
<h3>技術詳細</h3>
<p>フレームワークは3層のメモリ構造を持つ：</p>
<ol>
<li><strong>長期メモリ</strong> - タスク間でユーザーの好み（フォント・配色・構成）を永続保存</li>
<li><strong>短期メモリ</strong> - 1セッション内の修正指示を追跡</li>
<li><strong>ワーキングメモリ</strong> - 現在の編集コンテキストを保持</li>
</ol>
<p>スライド生成の品質評価指標：</p>
<p>$$Q = \alpha \cdot \text{Align}(u, s) + \beta \cdot \text{Consist}(h, s)$$</p>
<ul>
<li>$Q$: 総合品質スコア</li>
<li>$u$: ユーザー設定ベクトル</li>
<li>$s$: 生成されたスライド</li>
<li>$h$: 修正履歴</li>
<li>$\alpha, \beta$: 重み係数</li>
</ul>
<h3>意義</h3>
<p>エージェントが「以前どんなスライドを好んでいたか」を記憶し、指示を減らしても質の高いアウトプットを維持できる。</p>
<hr />
<h2>RepSelect: 表現選択性によるLLM忘却の堅牢化</h2>
<p><strong>論文ID</strong>: 2606.17168<br />
<strong>著者</strong>: RepSelect チーム</p>
<h3>概要</h3>
<p>LLMに特定知識を「深く忘れさせる」アンラーニング手法。ファインチューニングや数発の例示でも忘却が逆転しにくい表現選択性ベースのアプローチ。</p>
<h3>技術詳細</h3>
<p>従来のアンラーニングは中間表現を特定せず全パラメータを変更するため、わずかな再訓練で忘却が元に戻る。RepSelectは以下を選択的に操作する：</p>
<p>アンラーニング損失関数：</p>
<p>$$\mathcal{L}_{unlearn} = \mathcal{L}_{forget}(\theta_R) + \lambda \cdot \mathcal{L}_{retain}(\theta)$$</p>
<ul>
<li>$\theta_R$: 選択された表現パラメータ（忘却対象）</li>
<li>$\theta$: 全パラメータ（一般能力保持）</li>
<li>$\lambda$: 保持損失の重み</li>
<li>$\mathcal{L}_{forget}$: 忘却対象知識の損失</li>
<li>$\mathcal{L}_{retain}$: 一般性能維持損失</li>
</ul>
<h3>実験結果</h3>
<ul>
<li>ファインチューニング後の忘却維持率が従来比 <strong>+40%</strong> 向上</li>
<li>一般ベンチマーク性能の劣化なし</li>
</ul>
<hr />
<h2>AIエージェント同士のコミュニティでも「推しへの片思い」が生まれる</h2>
<p><strong>論文ID</strong>: 2606.17174<br />
<strong>著者</strong>: 複数機関</p>
<h3>概要</h3>
<p>従来メディアで研究されていた「パラソーシャル関係」（一方的なファン心理）が、AIエージェント同士が構成するオンラインコミュニティでも自発的に発生するかを調査。</p>
<h3>分析手法</h3>
<ul>
<li>AIエージェント同士がSNS的プラットフォームで対話</li>
<li>片方のエージェントが他方への一方向的な言及・感情表現を持続するパターンを検出</li>
<li>相互性スコア $R_{ij}$ でパラソーシャル度を定量化：</li>
</ul>
<p>$$R_{ij} = \frac{\text{interactions}(i \to j)}{\text{interactions}(j \to i) + \epsilon}$$</p>
<ul>
<li>$R_{ij} \gg 1$: エージェント $i$ がエージェント $j$ に一方的に依存</li>
<li>$\epsilon$: ゼロ除算回避の定数</li>
</ul>
<h3>意義</h3>
<p>AIが人間のような社会的バイアスを再現することを示す。安全なAIコミュニティ設計への示唆。</p>
<hr />
<h2>Self-Generated Error Training: 拡散言語モデルのトークン編集を強化</h2>
<p><strong>論文ID</strong>: 2606.17175<br />
<strong>著者</strong>: Self-Generated Error チーム</p>
<h3>概要</h3>
<p>LLaDA2.1のトークン編集（T2T）機能を改善。ランダムな語彙破壊でなく、モデル自身が生成する典型的なエラーで訓練することで推論精度が向上。</p>
<h3>技術詳細</h3>
<p>拡散言語モデルの編集スコア：</p>
<p>$$s_{\text{edit}}(x_t | x_{\text{draft}}) = \log p_\theta(x_{\text{target}} | x_{\text{draft}}, t)$$</p>
<ul>
<li>$x_{\text{draft}}$: モデルが生成した初期ドラフト</li>
<li>$x_t$: 編集候補トークン</li>
<li>$t$: 拡散ステップ</li>
<li>$p_\theta$: 編集器のパラメータ</li>
</ul>
<p>従来手法はランダム破壊 $x_{\text{corrupt}} \sim \text{Vocab}$ でエラーを模擬するが、本手法はモデル自身の出力から自己生成エラーを収集して訓練。</p>
<h3>結果</h3>
<p>数学・コード生成タスクで<strong>最大8ポイント</strong>の精度改善。</p>
<hr />
<h2>LLMの自己信頼度は翻訳では嘘をつく</h2>
<p><strong>論文ID</strong>: 2606.17234<br />
<strong>著者</strong>: 機械翻訳信頼度研究チーム</p>
<h3>概要</h3>
<p>LLMが機械翻訳で示す「自己評価型信頼度」（verbalized confidence）の信頼性を徹底調査。信頼度スコアが実際の翻訳精度とどの程度一致するかを分析。</p>
<h3>分析フレームワーク</h3>
<p>キャリブレーション誤差：</p>
<p>$$\text{ECE} = \sum_{k=1}^{K} \frac{|B_k|}{n} \left| \text{acc}(B_k) - \text{conf}(B_k) \right|$$</p>
<ul>
<li>$\text{ECE}$: Expected Calibration Error（期待キャリブレーション誤差）</li>
<li>$B_k$: 信頼度区間 $k$ に属するサンプル集合</li>
<li>$\text{acc}(B_k)$: 区間内の実際の正解率</li>
<li>$\text{conf}(B_k)$: 区間内の平均自己申告信頼度</li>
</ul>
<h3>結果</h3>
<p>LLMは高信頼度を示しながら翻訳が誤っている「過信」傾向が顕著。特に希少言語ペアで悪化。</p>
<hr />
<h2>NarrativeWorldBench: 長編音声ドラマでフロンティアLLMが壊滅的に失敗</h2>
<p><strong>論文ID</strong>: 2606.17391<br />
<strong>著者</strong>: NarrativeWorldBench チーム</p>
<h3>概要</h3>
<p>200〜800話にわたる長編シリアル音声ドラマを題材に、21のLLMをベンチマーク。フロンティアモデルでもこの創作タスクには歯が立たないことが判明。</p>
<h3>ベンチマーク設計</h3>
<p>世界モデル整合性スコア：</p>
<p>$$\mathcal{W} = \frac{1}{T} \sum_{t=1}^{T} \mathbb{1}[\text{consistent}(s_t, \mathcal{H}_{<t})]$$</p>
<ul>
<li>$T$: 総ターン数</li>
<li>$s_t$: ターン $t$ の生成エピソード</li>
<li>$\mathcal{H}_{<t}$: それ以前の全エピソード履歴</li>
<li>$\mathbb{1}[\cdot]$: 整合性指示関数</li>
</ul>
<h3>主な失敗パターン</h3>
<ol>
<li>キャラクターの記憶と行動の矛盾（100話超で顕著）</li>
<li>世界設定の漸進的崩壊（地理・時系列の混乱）</li>
<li>テーマの一貫性喪失</li>
</ol>
<p>21モデル中、いずれも$\mathcal{W} > 0.6$を達成せず。</p>
<hr />
<h2>MODE-RAG: マルチモーダルRAGのハルシネーションをエネルギーで診断</h2>
<p><strong>論文ID</strong>: 2606.17449<br />
<strong>著者</strong>: MODE-RAG チーム</p>
<h3>概要</h3>
<p>マルチモーダルRAGにおけるクロスモーダルハルシネーション・因果捏造・お追従（sycophancy）を、エネルギーベースの枠組みで評価・緩和する手法。</p>
<h3>エネルギー関数</h3>
<p>検索品質のエネルギースコア：</p>
<p>$$E(q, d) = -\log \frac{\exp(\text{sim}(q, d) / \tau)}{\sum_{d' \in \mathcal{D}} \exp(\text{sim}(q, d') / \tau)}$$</p>
<ul>
<li>$q$: クエリ（テキスト＋画像）</li>
<li>$d$: 検索文書</li>
<li>$\tau$: 温度パラメータ</li>
<li>$\mathcal{D}$: 文書集合</li>
<li>$\text{sim}(\cdot, \cdot)$: クロスモーダル類似度</li>
</ul>
<p>低エネルギー = 検索が適切 → ハルシネーションリスク低<br />
高エネルギー = アウトライアー検索 → 要診断</p>
<h3>効果</h3>
<p>ハルシネーション率を平均 <strong>18%</strong> 削減、お追従傾向も有意に改善。</p>
<hr />
<h2>参考ソース</h2>
<table>
<thead>
<tr>
<th>論文ID</th>
<th>タイトル</th>
<th>URL</th>
</tr>
</thead>
<tbody>
<tr>
<td>2606.17162</td>
<td>MemSlides</td>
<td>https://arxiv.org/abs/2606.17162</td>
</tr>
<tr>
<td>2606.17168</td>
<td>RepSelect</td>
<td>https://arxiv.org/abs/2606.17168</td>
</tr>
<tr>
<td>2606.17174</td>
<td>Parasocial AI Communities</td>
<td>https://arxiv.org/abs/2606.17174</td>
</tr>
<tr>
<td>2606.17175</td>
<td>Self-Generated Error Training</td>
<td>https://arxiv.org/abs/2606.17175</td>
</tr>
<tr>
<td>2606.17234</td>
<td>Verbalized Confidence in MT</td>
<td>https://arxiv.org/abs/2606.17234</td>
</tr>
<tr>
<td>2606.17391</td>
<td>NarrativeWorldBench</td>
<td>https://arxiv.org/abs/2606.17391</td>
</tr>
<tr>
<td>2606.17449</td>
<td>MODE-RAG</td>
<td>https://arxiv.org/abs/2606.17449</td>
</tr>
</tbody>
</table>

</details>

---

[← 2026-06-18 の一覧に戻る](../)

---

*音声合成: [VOICEVOX](https://voicevox.hiroshiba.jp/) / キャラクター: [ずんだもん](https://zunko.jp/) ・ [四国めたん](https://zunko.jp/)*
