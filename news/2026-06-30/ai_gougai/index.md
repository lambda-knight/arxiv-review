---
title: "生成AI号外 2026-06-30"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# 生成AI号外 2026-06-30

**2026-06-30 / 生成AI号外**

<audio controls src="https://archive.org/download/news-pickup-2026-06-30-ai-gougai/ai_gougai_yukkuri.m4a" style="width:100%;margin-top:4px"></audio>

- [Internet Archive](https://archive.org/details/news-pickup-2026-06-30-ai-gougai)

---

<details>
<summary>スライド（クリックで展開）</summary>

<h1>量子コンピュータ 号外 2026/06/30</h1>
<p>今日は2本の重大ニュースを詳しくお届けします。</p>
<h2>QuEra「Libra」— 100万量子演算の耐故障性QPUが2028年にAmazon Braketへ</h2>
<p>AWSと{QuEra|キュエラ} Computing（ハーバード系スピンオフ）が2026年6月に戦略的協業拡大を発表。2028年を目標に、フォールトトレラント量子コンピュータ <strong>Libra</strong> を Amazon Braket クラウドで提供開始する。</p>
<h3>QuEraとは何者か</h3>
<ul>
<li>2019年創業。ハーバード大学の量子物理学者 {Mikhail Lukin|ミハイル・ルーキン} 教授らのスピンオフ企業</li>
<li>中性原子方式の量子コンピュータ開発でトップを走るスタートアップ</li>
<li>AWSとの提携は2023年から段階的に拡大</li>
</ul>
<h3>Libraの主要仕様</h3>
<table>
<thead>
<tr>
<th>項目</th>
<th>仕様</th>
</tr>
</thead>
<tbody>
<tr>
<td>量子演算規模</td>
<td>Megaquop（100万論理量子演算）</td>
</tr>
<tr>
<td>論理量子ビット</td>
<td>256以上</td>
</tr>
<tr>
<td>論理エラー率</td>
<td>10⁻⁶（100万分の1）</td>
</tr>
<tr>
<td>技術基盤</td>
<td>中性原子（ライドバーグ原子）+ 光ピンセット</td>
</tr>
<tr>
<td>接続性</td>
<td>全対全（All-to-all）接続</td>
</tr>
<tr>
<td>拡張性</td>
<td>単一モジュールで10,000〜100,000+ 物理量子ビット</td>
</tr>
</tbody>
</table>
<h3>なぜ中性原子か？</h3>
<table>
<thead>
<tr>
<th>特徴</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>光ピンセット</strong></td>
<td>レーザー光で個々の原子を浮かせ・移動。量子ビットを動的に再配置できる</td>
</tr>
<tr>
<td><strong>全対全接続</strong></td>
<td>任意の量子ビット同士を直接つなげる。超伝導方式（IBM・Google）は隣接のみ</td>
</tr>
<tr>
<td><strong>ライドバーグ原子</strong></td>
<td>高励起状態の原子。強い相互作用で量子ゲートを高精度に実装</td>
</tr>
<tr>
<td><strong>スケーラビリティ</strong></td>
<td>1モジュールで1万〜10万量子ビットへの拡張が理論上可能</td>
</tr>
</tbody>
</table>
<h3>NISQ と耐故障性の違い</h3>
<ul>
<li><strong>NISQ（ノイジー中規模量子コンピュータ）</strong>: 数百〜数千のゲート操作で誤りが蓄積し崩壊</li>
<li>物理エラー率 ≈ 10⁻³（千回に1回ミス）</li>
<li><strong>論理量子ビット</strong>: 複数の物理量子ビットで誤りを訂正した「本物の」量子ビット</li>
<li>Libraの論理エラー率 ≈ 10⁻⁶（100万回に1回ミス）= NISQの <strong>1000倍</strong> 精度</li>
</ul>
<h3>qLDPCとの相性が抜群な理由</h3>
<ul>
<li><strong>qLDPC</strong>（量子低密度パリティ検査符号）は非局所な接続——遠くの量子ビット間のゲート——を必要とする最新の誤り訂正符号</li>
<li>光ピンセットで原子を動かせる中性原子はこの要件に完璧にマッチ</li>
<li>超伝導方式では実装が非常に困難</li>
</ul>
<h3>2028年に何ができるのか</h3>
<ul>
<li><strong>量子化学シミュレーション</strong>: 新薬候補分子・触媒・新素材の高精度計算</li>
<li><strong>高エネルギー物理</strong>: 格子QCDのシミュレーション</li>
<li><strong>最適化問題</strong>: 物流・金融ポートフォリオ・スケジューリング</li>
<li><strong>ハイブリッドワークフロー</strong>: Amazon BraketでHPC・AI・量子を組み合わせた計算</li>
</ul>
<hr />
<h2>10,000量子ビットでRSA/ECC暗号が破られる？ショアのアルゴリズム新推定</h2>
<p>{Oratomic|オラトミック}・{Caltech|カルテック}・{UC Berkeley|ユーシー バークレー}の研究チームが発表した論文で、高レートqLDPC符号を使うと従来推定の50分の1以下の量子ビット数でRSA-2048・ECC-256の解読が可能になることが示された。</p>
<h3>ショアのアルゴリズムとは</h3>
<ul>
<li>1994年、{MIT|エムアイティー}の {Peter Shor|ピーター・ショア} 教授が考案した量子アルゴリズム</li>
<li><strong>大きな数の素因数分解</strong>を古典コンピュータの指数倍の速度で解ける</li>
<li>{RSA|アールエスエー}暗号・{ECC|イーシーシー}（楕円曲線暗号）はこの素因数分解の困難さに安全性を依存している</li>
</ul>
<h3>推定値の変化：どれだけ下がったか</h3>
<table>
<thead>
<tr>
<th>推定時期</th>
<th>ECC-256に必要な量子ビット数</th>
</tr>
</thead>
<tbody>
<tr>
<td>Google（2021年・表面符号ベース）</td>
<td>約 500,000 物理量子ビット</td>
</tr>
<tr>
<td>新推定（2026年・qLDPCベース）</td>
<td><strong>10,000〜26,000</strong> 物理量子ビット</td>
</tr>
</tbody>
</table>
<p>→ <strong>50分の1以下に激減</strong></p>
<h3>なぜこんなに少ない量子ビットで済むのか</h3>
<p>$$\text{表面符号: } 100 \text{ 物理量子ビット} \to 4 \text{ 論理量子ビット（符号化率 4\%）}$$</p>
<p>$$\text{qLDPC (lp}_{24}\text{)}: 5{,}278 \text{ 物理量子ビット} \to 1{,}480 \text{ 論理量子ビット（符号化率 28\%）}$$</p>
<ul>
<li>符号化率の比較: 表面符号 ≈ 4% vs qLDPC ≈ 30%（<strong>7.5倍の効率</strong>）</li>
<li>誤り訂正のオーバーヘッドが劇的に削減されるため、必要な物理量子ビット数が大幅に減少</li>
</ul>
<h3>暗号解読に必要な量子ビット数（新推定）</h3>
<table>
<thead>
<tr>
<th>暗号方式</th>
<th>物理量子ビット数</th>
<th>実行時間（1msサイクルタイム想定）</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>ECC-256</strong></td>
<td>10,000〜26,000</td>
<td>10〜264日</td>
</tr>
<tr>
<td><strong>RSA-2048</strong></td>
<td>11,000〜102,000</td>
<td>数ヶ月〜数年</td>
</tr>
</tbody>
</table>
<h3>暗号資産への影響</h3>
<ul>
<li><strong>ビットコインP2PKアドレス</strong>: 旧アドレスは公開鍵がブロックチェーンに露出</li>
<li>理論的な対象: 約 170万 BTC（サトシ・ナカモト時代の眠れる資産含む）</li>
<li><strong>イーサリアム</strong>: 上位1,000アカウントが保有する約 2,050万 ETH が理論的対象</li>
<li><strong>攻撃は数日〜数週間かかる</strong>: ライブ取引への即時攻撃には向かない。休止中の古い資産が主な標的</li>
</ul>
<h3>現時点での重要な留保</h3>
<ol>
<li>1万量子ビットの中性原子コンピュータは<strong>現時点では存在しない</strong></li>
<li>1ミリ秒サイクルタイムはまだ達成されていない（現在は数ミリ秒）</li>
<li>あくまで理論研究——ただし <strong>推定値の急速な低下</strong>というトレンドは明確</li>
</ol>
<h3>今すぐ始めるべき対策：耐量子暗号（PQC）</h3>
<ul>
<li><strong>「今収集して後で解読する」攻撃</strong>: 今の暗号通信を録音・収集し、将来量子コンピュータで解読する手法</li>
<li><strong>{NIST|エヌアイエスティー}が2024年に確定したPQC標準</strong>:</li>
<li>{CRYSTALS-Kyber|クリスタルズ・カイバー}（鍵交換）</li>
<li>{CRYSTALS-Dilithium|クリスタルズ・ディリシウム}（デジタル署名）</li>
<li>企業・政府システムの移行には <strong>5〜10年</strong> かかると予測——今すぐ開始が必須</li>
</ul>
<hr />
<h2>まとめ</h2>
<p>QuEraのLibraは2028年に耐故障性量子コンピューティングをクラウドで実現しようとしている。
qLDPC研究は量子コンピュータが暗号を破るために必要な量子ビット数を50分の1に下げる可能性を示した。
中性原子テクノロジーがこの2つを結ぶキーテクノロジー——光ピンセットで全対全接続を実現してqLDPCを効率よく動かせる。
技術は確実に進んでいる。企業も個人も、ポスト量子暗号への移行を本気で考え始める時期に来ている。</p>
<h2>参考ソース</h2>
<ul>
<li>https://www.quera.com/press-releases/quera-announces-2028-fault-tolerant-quantum-computer-and-expanded-multi-year-strategic-collaboration-with-aws</li>
<li>https://aws.amazon.com/blogs/quantum-computing/aws-deepens-strategic-collaboration-with-quera-to-bring-fault-tolerant-quantum-computing-to-amazon-braket/</li>
<li>https://postquantum.com/security-pqc/10000-qubits-shors/</li>
<li>https://nist.gov/pqcrypto</li>
</ul>

</details>

---

[← 2026-06-30 の一覧に戻る](../)

---

*音声合成: [VOICEVOX](https://voicevox.hiroshiba.jp/) / キャラクター: [ずんだもん](https://zunko.jp/) ・ [四国めたん](https://zunko.jp/)*
