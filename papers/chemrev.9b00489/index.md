---
title: "ニトロゲナーゼ補因子の生合成"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

# ニトロゲナーゼ補因子の生合成

*Burén, Jiménez-Vicente, Echavarri-Erasun, Rubio*

- DOI: [10.1021/acs.chemrev.9b00489](https://doi.org/10.1021/acs.chemrev.9b00489)
- Internet Archive: [paper-explain-chemrev-9b00489](https://archive.org/details/paper-explain-chemrev-9b00489)

---

## 概要

Burén, Jiménez-Vicente, Echavarri-Erasun, Rubio「Biosynthesis of Nitrogenase Cofactors」（Chemical Reviews, 2020）を全10章で徹底解説！

空気中の窒素（N₂）を生物が使えるアンモニアに変える「ニトロゲナーゼ」。その心臓部にある3種の金属補因子（[4Fe-4S]・Pクラスター・FeMo-co）が、40年の研究を経てどこまで解明されたかをずんだもんと四国めたんがわかりやすく解説するのだ！

📄 対象論文：
・Biosynthesis of Nitrogenase Cofactors
  Stefan Burén, Emilio Jiménez-Vicente, Carlos Echavarri-Erasun, Luis M. Rubio
  Chemical Reviews 120, 4921–4968 (2020)
  DOI: 10.1021/acs.chemrev.9b00489

📚 チャプター構成：
Ch.01 窒素固定の全体像と生物的窒素固定の意義
Ch.02 ニトロゲナーゼの構成タンパク質と全体構造
Ch.03 [4Fe-4S]クラスター ── Feタンパクの補因子と酵素サイクル
Ch.04 Pクラスターの構造・状態変化・電子伝達
Ch.05 FeMo-coの構造と窒素還元の活性部位
Ch.06 NifS・NifU ── 鉄硫黄クラスター組立の基盤
Ch.07 Pクラスターの生合成 ── その場での酸化還元カップリング
Ch.08 FeMo-co生合成 前半 ── NifBのラジカルSAM反応
Ch.09 FeMo-co生合成 後半 ── NifEN足場と金属シャペロン
Ch.10 代替ニトロゲナーゼと窒素固定の応用展望

#論文解説 #ニトロゲナーゼ #窒素固定 #生化学 #ChemicalReviews #鉄硫黄クラスター #FeMoco #ラジカルSAM #数式でわかる #研究 #大学院

---

## 章別動画・解説

### 第1章: 窒素固定の全体像と生物的窒素固定の意義

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch01.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch01.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>窒素固定の全体像と生物的窒素固定の意義</h2>
<h3>窒素循環と「固定」の壁</h3>
<ul>
<li>大気の約78%はN₂（窒素分子）だが、生物が直接使えるのはNH₃やNO₃⁻などの「固定窒素」のみ</li>
<li>N≡N三重結合の結合エネルギー: <strong>945 kJ/mol</strong> ── 極めて安定で切断が困難</li>
</ul>
<p>$$\text{N}_2 + 8\text{H}^+ + 8e^- + 16\text{ATP} \xrightarrow{\text{ニトロゲナーゼ}} 2\text{NH}_3 + \text{H}_2 + 16\text{ADP} + 16P_i$$</p>
<ul>
<li>$8e^-$：N₂の還元に6電子、H₂生成に2電子（必須の副反応）</li>
<li>$16\text{ATP}$：巨大なエネルギーコスト → 生物的N₂固定がいかに難しいかを示す</li>
</ul>
<h3>工業的固定（ハーバー・ボッシュ法）との比較</h3>
<blockquote>
<p>📊 Fig. 1 参照（原論文）</p>
</blockquote>
<table>
<thead>
<tr>
<th></th>
<th>ハーバー・ボッシュ</th>
<th>生物的窒素固定</th>
</tr>
</thead>
<tbody>
<tr>
<td>触媒</td>
<td>Fe系金属触媒</td>
<td>ニトロゲナーゼ酵素</td>
</tr>
<tr>
<td>条件</td>
<td>150〜300気圧、400〜500℃</td>
<td>常温常圧</td>
</tr>
<tr>
<td>エネルギー源</td>
<td>化石燃料</td>
<td>ATP（光合成産物）</td>
</tr>
<tr>
<td>CO₂排出</td>
<td>多大</td>
<td>なし</td>
</tr>
<tr>
<td>年間規模</td>
<td>約1.5億トンNH₃</td>
<td>約1.4億トンN</td>
</tr>
</tbody>
</table>
<h3>生物的窒素固定を行う微生物</h3>
<ul>
<li><strong>独立栄養細菌</strong>: <em>Azotobacter vinelandii</em>、<em>Clostridium pasteurianum</em></li>
<li><strong>共生系</strong>: <em>Rhizobium</em> 属（マメ科植物根粒）、シアノバクテリア</li>
<li>nif（nitrogen fixation）遺伝子群がコード: <code>nifH</code>, <code>nifD</code>, <code>nifK</code>, <code>nifB</code>, <code>nifE</code>, <code>nifN</code>, ...</li>
<li>nif遺伝子は嫌気条件・窒素飢餓で誘導（O₂でニトロゲナーゼは不活性化）</li>
</ul>
<h3>3種類のニトロゲナーゼ</h3>
<table>
<thead>
<tr>
<th>型</th>
<th>活性中心</th>
<th>遺伝子</th>
<th>特徴</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mo型（主要）</td>
<td>FeMo-co</td>
<td>nifHDKBEN...</td>
<td>最も活性が高い</td>
</tr>
<tr>
<td>V型</td>
<td>VFe-co</td>
<td>vnfHDGK...</td>
<td>Mo欠乏時に発現</td>
</tr>
<tr>
<td>Fe型（Fe-only）</td>
<td>FeFe-co</td>
<td>anfHDGK...</td>
<td>Mo・V両欠乏時</td>
</tr>
</tbody>
</table>
<hr />

</details>

### 第2章: ニトロゲナーゼの構成タンパク質と全体構造

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch02.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch02.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>ニトロゲナーゼの構成タンパク質と全体構造</h2>
<h3>2つのコンポーネントタンパク質</h3>
<p>ニトロゲナーゼは<strong>2つの別個のタンパク質</strong>が複合体を形成して機能する：</p>
<blockquote>
<p>📊 Fig. 2, 3 参照（原論文）</p>
</blockquote>
<p><strong>① Feタンパク（NifH）── ジニトロゲナーゼリダクターゼ</strong></p>
<p>$$\text{NifH}_2 \cdot [\text{4Fe-4S}] \cdot \text{MgATP}_2$$</p>
<ul>
<li>同一サブユニット2量体（γ₂）</li>
<li>サブユニット間に[4Fe-4S]クラスター1個を架橋</li>
<li>MgATP 2分子を結合 → コンフォメーション変化 → MoFeタンパクへ電子転移</li>
<li>電子供与体: フェレドキシン or フラボドキシン（生体内）</li>
</ul>
<p><strong>② MoFeタンパク（NifDK）── ジニトロゲナーゼ</strong></p>
<p>$$(\alpha\beta)_2 \cdot [\text{2× P-cluster}] \cdot [\text{2× FeMo-co}]$$</p>
<ul>
<li>α₂β₂ ヘテロ四量体（α = NifD, β = NifK）</li>
<li>各αβペアに Pクラスター 1個＋FeMo-co 1個</li>
</ul>
<h3>電子伝達の流れ</h3>
<pre><code>還元剤（Fdx/Flav）
      ↓ e⁻
   [4Fe-4S]（Feタンパク）
      ↓ e⁻（ATP依存）
   Pクラスター（NifDK）
      ↓ e⁻
   FeMo-co（活性中心）
      ↓ e⁻ × 6〜8
   N₂ → 2NH₃
</code></pre>
<h3>Feタンパク–MoFeタンパク複合体</h3>
<blockquote>
<p>📊 Fig. 4 参照（原論文）</p>
</blockquote>
<ul>
<li>1分子のFeタンパクが1つのαβ界面に結合（非対称）</li>
<li>結合→ATP加水分解→電子転移→解離 のサイクルを繰り返す</li>
<li>速度律速段階: ADP解離（ADP結合状態では次の電子を受け取れない）</li>
</ul>
<hr />

</details>

### 第3章: [4Fe-4S]クラスター ── Feタンパクの補因子と酵素サイクル

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch03.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch03.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>[4Fe-4S]クラスター ── Feタンパクの補因子と酵素サイクル</h2>
<h3>[4Fe-4S]クラスターの構造</h3>
<p>Feタンパクの[4Fe-4S]クラスターは2つのサブユニット界面に位置：</p>
<blockquote>
<p>📊 Fig. 5 参照（原論文）</p>
</blockquote>
<p>$$[\text{4Fe-4S}]^{2+/1+} \quad E^0 \approx -300 \text{ mV (vs. NHE)}$$</p>
<ul>
<li>4個のFeと4個のS²⁻が立方体状に配置</li>
<li>各Fe原子は隣接するS²⁻に加えシステイン（Cys₉₇・Cys₁₃₂）配位</li>
<li>酸化還元: [4Fe-4S]²⁺ → [4Fe-4S]¹⁺（1電子還元）</li>
</ul>
<h3>MgATP結合によるコンフォメーション変化</h3>
<p>$$\Delta G_{\text{ATP}} \approx -30 \text{ kJ/mol（加水分解自由エネルギー）}$$</p>
<p>MgATP 2分子の結合により：
1. Feタンパクの形状が「開いた」→「閉じた」コンフォメーションへ変化
2. [4Fe-4S]クラスターの<strong>還元電位が約200 mV 負方向にシフト</strong>
3. MoFeタンパクへの電子転移が熱力学的に有利になる</p>
<blockquote>
<p>📊 Fig. 6 参照（原論文）</p>
</blockquote>
<h3>FeタンパクのATPaseサイクル</h3>
<ol>
<li><strong>還元型FeタンパクがMgATPを結合</strong>（コンフォメーション変化）</li>
<li><strong>MoFeタンパクと複合体形成</strong></li>
<li><strong>電子転移</strong>: [4Fe-4S]¹⁺ → Pクラスター</li>
<li><strong>ADP + Pᵢ の生成</strong>（2 ATP/電子）</li>
<li><strong>複合体解離</strong>（ADP解離が律速）</li>
<li>フェレドキシン等により再還元 → サイクル繰り返し</li>
</ol>
<h3>全体の触媒化学量論</h3>
<p>$$\text{N}_2 + 8\text{H}^+ + 8e^- + 16\text{ATP} \rightarrow 2\text{NH}_3 + \text{H}_2 + 16\text{ADP} + 16P_i$$</p>
<ul>
<li>最低8回のFeタンパクサイクルが必要</li>
<li>H₂生成（2e⁻分）は避けられない → 理論効率の上限は75%</li>
</ul>
<hr />

</details>

### 第4章: Pクラスターの構造・状態変化・電子伝達

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch04.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch04.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Pクラスターの構造・状態変化・電子伝達</h2>
<h3>Pクラスターの特異な構造</h3>
<blockquote>
<p>📊 Fig. 7, 8 参照（原論文）</p>
</blockquote>
<p>$$[\text{8Fe-7S}] \quad \text{P}^N \text{ 状態}$$</p>
<ul>
<li>8個のFeと7個のS²⁻から成る大型鉄硫黄クラスター</li>
<li>αサブユニットと βサブユニットを<strong>橋架け</strong>する位置に存在</li>
<li>Cys残基6本で固定（α側3本 + β側3本）</li>
</ul>
<h3>2つの酸化還元状態</h3>
<table>
<thead>
<tr>
<th>状態</th>
<th>電子数</th>
<th>構造的特徴</th>
</tr>
</thead>
<tbody>
<tr>
<td>P^N（還元型）</td>
<td>基底</td>
<td>立方体2個が中央S²⁻で融合した構造。Cys残基のみ配位</td>
</tr>
<tr>
<td>P^OX（酸化型）</td>
<td>2電子酸化</td>
<td>αのSer188・βのCys153 がFeに配位して安定化（構造大変化）</td>
</tr>
</tbody>
</table>
<p>$$\text{P}^N \xrightarrow{-2e^-} \text{P}^{OX}$$</p>
<h3>電子転移のゲート役</h3>
<blockquote>
<p>📊 Fig. 9 参照（原論文）</p>
</blockquote>
<ul>
<li>Feタンパクから電子を受け取る（P^N → 中間状態）</li>
<li>FeMo-coへ電子を渡す</li>
<li>P^OX → P^N への再還元がFMN等によって行われる可能性</li>
</ul>
<p><strong>なぜPクラスターが必要か？</strong>
- FeMo-coは直接Feタンパクと接触していない（空間的に離れている）
- Pクラスターが「中継ステーション」として電子を伝達する
- 2電子貯蔵能を持つ可能性（N₂還元に2電子単位が必要）</p>
<hr />

</details>

### 第5章: FeMo-coの構造と窒素還元の活性部位

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch05.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch05.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>FeMo-coの構造と窒素還元の活性部位</h2>
<h3>FeMo-coの構造 ── 自然界で最も複雑な金属クラスター</h3>
<blockquote>
<p>📊 Fig. 10, 11 参照（原論文）</p>
</blockquote>
<p>$$[\text{7Fe-9S-C-Mo-R-homocitrate}]$$</p>
<ul>
<li>7個のFe、9個のS²⁻、<strong>炭素原子1個（C）</strong>、Mo原子1個、ホモクエン酸1分子</li>
<li>1997年まで炭素の存在は不明だった（2011年にX線結晶構造で確定）</li>
</ul>
<p><strong>構造の詳細：</strong>
$$[\text{4Fe-4S}]^{\text{cubane}} - \text{C} - [\text{3Fe-3S}] - \text{Mo}(\text{homocitrate})$$</p>
<ul>
<li>[4Fe-4S]立方体と[3Fe-3S-Mo]部分が中央の炭素原子で結合</li>
<li>Moはヒスチジン（His442）とホモクエン酸で配位</li>
<li>Feの一方のコーナーはシステイン（Cys275）でタンパクに固定</li>
</ul>
<h3>中心炭素（炭化物）の役割</h3>
<p>$$\text{FeMo-co} = [\text{Mo-7Fe-9S-C}] + \text{homocitrate}$$</p>
<ul>
<li>炭素は6個のFe原子に配位した炭化物（carbide）</li>
<li>NifBのラジカルSAM反応でS-アデノシルメチオニン（SAM）から挿入</li>
<li>N₂が結合・還元される際の足場として機能する可能性</li>
</ul>
<h3>N₂還元の機構（未解明部分あり）</h3>
<blockquote>
<p>📊 Fig. 12 参照（原論文）</p>
</blockquote>
<p>提案されているN₂結合モデル：</p>
<p><strong>交互機構（Alternating mechanism）</strong>：
$$\text{N}_2 \rightarrow \text{N}_2\text{H}_2 \rightarrow \text{N}_2\text{H}_4 \rightarrow \text{NH}_3$$
両端のN原子が交互にプロトン化・還元される</p>
<p><strong>解離機構（Distal mechanism）</strong>：
$$\text{N}_2 \rightarrow \text{N-NH}_2 \rightarrow \text{N-NH}_3 \rightarrow \text{N} + \text{NH}_3 \rightarrow \text{NH}_3$$
遠位N原子が先にNH₃として解離</p>
<ul>
<li>現在も論争中。Feベルトの2-7位の鉄サイトが反応に関与する説が有力</li>
</ul>
<h3>FeMo-coとNifDKの相互作用</h3>
<ul>
<li>NifDのHis442・Cys275がFeMo-coをタンパクに固定</li>
<li>FeMo-co挿入部位（Nifα-Kα ドメイン）は空洞 → apo-NifDKへのFeMo-co挿入経路</li>
</ul>
<hr />

</details>

### 第6章: NifS・NifU ── 鉄硫黄クラスター組立の基盤

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch06.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch06.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>NifS・NifU ── 鉄硫黄クラスター組立の基盤</h2>
<h3>鉄硫黄クラスター（Fe-Sクラスター）の一般的な生合成</h3>
<p>すべてのFe-Sクラスターは主に2タンパクの協同で作られる：</p>
<blockquote>
<p>📊 Fig. 13 参照（原論文）</p>
</blockquote>
<p><strong>NifS（システインデスルフラーゼ）</strong>：
$$\text{Cys} + \text{NifS（PLP）} \rightarrow \text{Ala} + \text{NifS-SSH（ペルスルフィド）}$$</p>
<ul>
<li>ピリドキサールリン酸（PLP）依存酵素</li>
<li>システインのチオール基（-SH）を硫黄源として活性化</li>
<li>生成したペルスルフィド（-SSH）がNifUのFe-Sクラスター形成を担う</li>
</ul>
<p><strong>NifU（足場タンパク）</strong>：</p>
<p>$$[\text{2Fe-2S}] \xrightarrow{\text{還元・結合}} [\text{4Fe-4S}]$$</p>
<ul>
<li>U型ドメインに一時的に[2Fe-2S]クラスターを組立（labile site）</li>
<li>2つの[2Fe-2S]が縮合して[4Fe-4S]となり標的タンパクへ転送</li>
<li>N末端恒久的クラスター（permanent site）はNifU自身の機能に必要</li>
</ul>
<h3>NifU/NifSの構造</h3>
<blockquote>
<p>📊 Fig. 14 参照（原論文）</p>
</blockquote>
<p><strong>NifU</strong>の三機能的ドメイン：
1. <strong>N末端ドメイン</strong>: [2Fe-2S] 組立（足場）サイト（Cys35, Cys62, Cys106, Cys131）
2. <strong>中央ドメイン</strong>: 恒久的[4Fe-4S]クラスター
3. <strong>C末端ドメイン</strong>: Thioredoxin様ドメイン（還元電位調整？）</p>
<h3>他の鉄硫黄クラスター生合成系との比較</h3>
<table>
<thead>
<tr>
<th>系</th>
<th>生物</th>
<th>主要タンパク</th>
</tr>
</thead>
<tbody>
<tr>
<td>NIF</td>
<td>窒素固定菌（ニトロゲナーゼ専用）</td>
<td>NifU, NifS</td>
</tr>
<tr>
<td>ISC</td>
<td>ほぼ全真核生物・多くの細菌（ミトコンドリア）</td>
<td>IscU, IscS</td>
</tr>
<tr>
<td>SUF</td>
<td>酸化ストレス・Fe欠乏条件の細菌</td>
<td>SufBCDE, SufS</td>
</tr>
<tr>
<td>CIA</td>
<td>真核生物細胞質</td>
<td>CIA標的化経路</td>
</tr>
</tbody>
</table>
<p>$$\text{NifU/NifS} \rightarrow \text{[4Fe-4S] for NifH, NifB, NifU}_{\text{自身}}$$</p>
<hr />

</details>

### 第7章: Pクラスターの生合成 ── その場での酸化還元カップリング

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch07.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch07.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>Pクラスターの生合成 ── その場での酸化還元カップリング</h2>
<h3>Pクラスター生合成の最大の謎</h3>
<p>Pクラスターは[8Fe-7S]という巨大クラスターだが、<strong>前駆体は2つの[4Fe-4S]クラスター</strong>と考えられている：</p>
<blockquote>
<p>📊 Fig. 15, 16 参照（原論文）</p>
</blockquote>
<p>$$2 \times [\text{4Fe-4S}] \xrightarrow{\text{NifH＋ATP}} [\text{8Fe-7S}](\text{P-cluster})$$</p>
<ul>
<li>この変換はMoFeタンパクの<strong>α-β界面でその場（in situ）</strong>で起きる</li>
<li>外部の足場タンパクを必要としない</li>
</ul>
<h3>apo-NifDKとPクラスター組立</h3>
<p><strong>apo-NifDK（Pクラスター未形成の前駆体）</strong>：
- [4Fe-4S]^3+状態の前駆体クラスターをα・βサブユニットそれぞれに持つ
- X線構造解析で「P^∗クラスター」として確認
- α側3Cys＋β側3Cysで各[4Fe-4S]を固定</p>
<h3>NifHによるPクラスター成熟化</h3>
<blockquote>
<p>📊 Fig. 17 参照（原論文）</p>
</blockquote>
<ol>
<li>apo-NifDKにNifH（ATP付き）が結合</li>
<li>NifHが電子を供与 → 前駆体クラスターが還元</li>
<li><strong>2つの[4Fe-4S]が1個の硫黄を共有して融合</strong> → [8Fe-7S] P^Nクラスター形成</li>
<li>NifHが解離</li>
</ol>
<p><strong>還元電位とエネルギー論</strong>：
$$\Delta G_{\text{カップリング}} < 0 \text{（ATP加水分解でエネルギー供給）}$$</p>
<h3>なぜその場合成なのか</h3>
<ul>
<li>Pクラスターの[8Fe-7S]は α・β 両サブユニットに架橋 → 単独では形成不可</li>
<li>αβ界面の閉じた空間でのみ正確な幾何学配置が可能</li>
<li>NifHの存在下でのみ成熟化 → 「品質管理」の役割も担う</li>
</ul>
<hr />

</details>

### 第8章: FeMo-co生合成 前半 ── NifBのラジカルSAM反応

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch08.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch08.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>FeMo-co生合成 前半 ── NifBのラジカルSAM反応</h2>
<h3>FeMo-coの生合成経路全体像</h3>
<blockquote>
<p>📊 Fig. 18 参照（原論文）</p>
</blockquote>
<pre><code>NifU/NifS → [4Fe-4S] building blocks
                    ↓
               NifB (radical SAM)
                    ↓
              NifB-co [8Fe-9S-C] ← SAMから炭素挿入
                    ↓
         NifEN scaffold (holo-NifEN)
                    ↓
         Mo + homocitrate 挿入
                    ↓
         FeMo-co [7Fe-9S-C-Mo-homocitrate]
                    ↓
      金属シャペロン (NifX/NafY/NifY) で搬送
                    ↓
          apo-NifDKへ挿入 → holo-NifDK
</code></pre>
<h3>NifB ── ラジカルSAM酵素</h3>
<p>$$\text{SAM} + e^- \rightarrow \text{5'-dAdo}^\bullet + \text{Met}$$</p>
<ul>
<li>S-アデノシルメチオニン（SAM）が[4Fe-4S]クラスターから1電子を受け取り開裂</li>
<li>生成した<strong>5'-デオキシアデノシルラジカル（Ado•）</strong>が炭素原子を引き抜く反応を開始</li>
</ul>
<blockquote>
<p>📊 Fig. 19, 20 参照（原論文）</p>
</blockquote>
<h3>NifBの独特なドメイン構造</h3>
<p>NifBは複数のドメインを持つ複合機能タンパク：</p>
<table>
<thead>
<tr>
<th>ドメイン</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr>
<td>SAMドメイン</td>
<td>ラジカルSAM反応（炭素源のSAMを活性化）</td>
</tr>
<tr>
<td>Kドメイン（NifB-K）</td>
<td>[4Fe-4S]クラスター2つを保持→融合</td>
</tr>
<tr>
<td>NifXドメイン（融合型）</td>
<td>生成したNifB-coを保持・転送</td>
</tr>
</tbody>
</table>
<h3>NifB-coの形成ステップ</h3>
<blockquote>
<p>📊 Fig. 21 参照（原論文）</p>
</blockquote>
<ol>
<li><strong>NifUからの[4Fe-4S]取り込み</strong>: Kドメインに[4Fe-4S]を2個配置</li>
<li><strong>SAMによるメチル基転移</strong>: 第1のSAMがメチル基をKドメインのS²⁻に転移（-SCH₃中間体）</li>
<li><strong>ラジカル反応による炭素挿入</strong>: 第2のSAMのAdo•がC-Hを引き抜き、炭素原子が[4Fe-4S]クラスターに挿入</li>
<li><strong>クラスター融合</strong>: 2つの[4Fe-4S]が炭化物（C⁴⁻）を中心に融合 → <strong>NifB-co [8Fe-9S-C]</strong></li>
</ol>
<p>$$[\text{4Fe-4S}]_1 + [\text{4Fe-4S}]_2 + \text{SAM(C)} \rightarrow [\text{8Fe-9S-C}] \text{(NifB-co)}$$</p>
<h3>ラジカルSAM反応の化学</h3>
<p>$$\text{5'-dAdo}^\bullet + \text{SAM}_{2} \rightarrow \text{SAM}^\bullet \rightarrow \text{carbanion at S-CH}_3 \rightarrow \text{carbide}$$</p>
<ul>
<li>この反応は前例のない炭化物挿入経路</li>
<li>炭化物（C⁴⁻）は完全に還元された炭素原子</li>
<li>生成物NifB-coはFeMo-coより1Fe少ない（後でMo置換時に1Feが失われる説あり）</li>
</ul>
<hr />

</details>

### 第9章: FeMo-co生合成 後半 ── NifEN足場と金属シャペロン

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch09.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch09.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>FeMo-co生合成 後半 ── NifEN足場と金属シャペロン</h2>
<h3>NifEN ── NifDKの構造的ホモログ</h3>
<blockquote>
<p>📊 Fig. 22 参照（原論文）</p>
</blockquote>
<p>$$\text{NifE} \approx \text{NifD（配列同一性 ≈ 23\%）}, \quad \text{NifN} \approx \text{NifK（≈ 28\%）}$$</p>
<ul>
<li>NifENはNifDKと同じα₂β₂構造をとる</li>
<li><strong>NifB-coの成熟化足場</strong>として機能</li>
<li>NifDKがFeMo-coを使って窒素固定するのに対し、NifENはFeMo-co生合成用プラットフォーム</li>
</ul>
<h3>NifENでのFeMo-co成熟化ステップ</h3>
<p><strong>Step 1: NifB-coのNifENへの転送</strong>
$$\text{NifB-co} \xrightarrow{\text{NifX}} \text{NifEN（apo）} \rightarrow \text{holo-NifEN}$$</p>
<ul>
<li>NifXがNifB-coを受け取り、NifENの特定サイト（αサブユニット）へ挿入</li>
<li>NifENとNifDKの活性部位残基の違い → NifENはFeMo-coを「触媒」せず「加工」する</li>
</ul>
<p><strong>Step 2: Moとホモクエン酸の挿入</strong></p>
<blockquote>
<p>📊 Fig. 23 参照（原論文）</p>
</blockquote>
<p>$$[\text{8Fe-9S-C}] + \text{Mo}^{6+} + \text{homocitrate} \xrightarrow{\text{NifEN, NifV?, NifQ?}} [\text{7Fe-9S-C-Mo-homocitrate}]$$</p>
<ul>
<li><strong>ホモクエン酸合成酵素（NifV）</strong>: 2-オキソグルタル酸からホモクエン酸を合成</li>
<li><strong>NifQ</strong>: Moの取り込みとプロセシング（Mo輸送体との相互作用）</li>
<li>1FeBの喪失？またはNifB-coの9S中の1Sが除去？→詳細は議論中</li>
</ul>
<p><strong>Step 3: FeMo-coの完成とNifENからの解離</strong>
- holo-NifENからFeMo-coが解離
- NafYがFeMo-coを受け取り、apo-NifDKへ輸送</p>
<h3>金属シャペロンの役割</h3>
<blockquote>
<p>📊 Fig. 24, 25 参照（原論文）</p>
</blockquote>
<table>
<thead>
<tr>
<th>タンパク</th>
<th>機能</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>NifX</strong></td>
<td>NifB-co を NifEN へ転送。Fe-Sクラスター輸送シャペロン</td>
</tr>
<tr>
<td><strong>NafY（NifY）</strong></td>
<td>FeMo-co を NifEN から apo-NifDK へ輸送。挿入シャペロン</td>
</tr>
<tr>
<td><strong>NifQ</strong></td>
<td>Moのプロセシング・転送（NifBとの相互作用）</td>
</tr>
</tbody>
</table>
<p><strong>NafYの働き</strong>：
$$\text{NafY} + \text{FeMo-co} \rightarrow \text{NafY-FeMo-co} \xrightarrow{\text{apo-NifDK}} \text{holo-NifDK} + \text{NafY}$$</p>
<ul>
<li>NafYのγドメインがFeMo-coを非共有結合的に保持</li>
<li>apo-NifDKのNifα-K挿入口（His442周辺）に特異的に結合して挿入を仲介</li>
</ul>
<h3>FeMo-co挿入と完全活性NifDKの形成</h3>
<ul>
<li>apo-NifDKはFeMo-coを持たず、窒素固定活性ゼロ</li>
<li>NafYとの複合体形成後、FeMo-coが挿入されてコンフォメーション変化</li>
<li>holo-NifDKはFeタンパクと複合体を形成して触媒機能を発揮</li>
</ul>
<hr />

</details>

### 第10章: 代替ニトロゲナーゼと窒素固定の応用展望

<video controls width="100%" src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch10.mp4"></video>

<audio controls src="https://archive.org/download/paper-explain-chemrev-9b00489/paper_chemrev.9b00489_ch10.mp3" style="width:100%;margin-top:4px"></audio>

<details>
<summary>解説スライド（クリックで展開）</summary>

<h2>代替ニトロゲナーゼと窒素固定の応用展望</h2>
<h3>V型ニトロゲナーゼ（VFe-co含有）</h3>
<blockquote>
<p>📊 Fig. 26 参照（原論文）</p>
</blockquote>
<p>$$[\text{VFe-co}] = [\text{7Fe-8S-C-V-homocitrate}]$$</p>
<ul>
<li>MoをVanadium（V）で置換した活性中心</li>
<li>FeMo-coと比較して<strong>1S²⁻ が多く（8S vs 9S）</strong>、1FeO（δ-カーボキシル？）が追加</li>
<li>V型ニトロゲナーゼ特異的なサブユニット VnfG（δサブユニット）が存在</li>
<li><strong>CO₂をCOに還元できる</strong>点がFeMo-co型と異なる（工業的に注目）</li>
</ul>
<p>$$\text{CO}_2 + 2\text{H}^+ + 2e^- \xrightarrow{\text{VFe型}} \text{CO} + \text{H}_2\text{O}$$</p>
<h3>Fe型ニトロゲナーゼ（FeFe-co含有）</h3>
<p>$$[\text{FeFe-co}] = [\text{8Fe-8S-C-homocitrate}] \text{（推定）}$$</p>
<ul>
<li>Mo・V両方が欠乏する極端条件でのみ発現</li>
<li>Fe型は3種の中で最も活性が低い</li>
<li>詳細構造はまだ不明な部分が多い</li>
</ul>
<h3>3種ニトロゲナーゼの比較</h3>
<table>
<thead>
<tr>
<th></th>
<th>Mo型</th>
<th>V型</th>
<th>Fe型</th>
</tr>
</thead>
<tbody>
<tr>
<td>活性中心金属</td>
<td>Mo</td>
<td>V</td>
<td>Fe（のみ）</td>
</tr>
<tr>
<td>N₂還元活性</td>
<td>+++（最高）</td>
<td>++</td>
<td>+（最低）</td>
</tr>
<tr>
<td>H₂生成</td>
<td>少</td>
<td>多</td>
<td>最多</td>
</tr>
<tr>
<td>CO₂還元</td>
<td>×</td>
<td>○</td>
<td>△</td>
</tr>
<tr>
<td>発現誘導</td>
<td>Mo欠乏時を除き常時</td>
<td>Mo欠乏時</td>
<td>Mo・V両欠乏時</td>
</tr>
</tbody>
</table>
<h3>農業・工業への応用展望</h3>
<blockquote>
<p>📊 Fig. 27, 28 参照（原論文）</p>
</blockquote>
<p><strong>植物への窒素固定能付与（夢のシナリオ）</strong>：
- nif遺伝子群を植物（またはその共生体）に導入
- 課題: ① O₂感受性（嫌気条件の確保）、② 16ATP/N₂の巨大コスト、③ 多数のnif遺伝子の協調発現
- <em>Rhizobium</em> 共生の改良や非マメ科植物への共生導入研究が進行中</p>
<p><strong>人工的窒素固定触媒の設計指針</strong>：</p>
<p>$$[\text{7Fe-9S-C-Mo}] \rightarrow \text{均一系・不均一系触媒への応用}$$</p>
<ul>
<li>FeMo-coの構造をモデルとしたN₂還元触媒の合成</li>
<li>炭化物の役割の解明が常温常圧N₂固定への鍵</li>
</ul>
<p><strong>ハーバー・ボッシュ法の代替</strong>：
- 世界の天然ガス消費の約1〜2%をハーバー・ボッシュ法が占める
- 生物的窒素固定のメカニズム解明 → より温和な条件での化学触媒設計へ</p>
<h3>まとめ：40年の研究が示すもの</h3>
<ol>
<li>FeMo-coは自然界で最も精巧に設計された金属クラスターの1つ</li>
<li>その生合成には<strong>NifB（炭化物挿入）→ NifEN（足場）→ NifX/NafY（輸送）</strong>という複数ステップが必要</li>
<li>Pクラスターの「その場合成」はα-β界面という固有の環境で実現</li>
<li>代替ニトロゲナーゼ（V型・Fe型）が多様な環境適応戦略を示す</li>
<li>常温常圧でN₂を固定する酵素機構の解明は人類の持続可能な農業・エネルギー問題への回答に直結</li>
</ol>
<h3>参考</h3>
<ul>
<li>Burén S, Jiménez-Vicente E, Echavarri-Erasun C, Rubio LM. <em>Chem. Rev.</em> <strong>120</strong>, 4921–4968 (2020).
  DOI: 10.1021/acs.chemrev.9b00489</li>
</ul>

</details>

---

[← 論文一覧に戻る](../../)
