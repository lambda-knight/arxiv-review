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

## 章別動画

### 第1章: 背景 — 断片化したロボット知能の課題

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch01.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch01.mp4){:target="_blank"}

### 第2章: Qwen-VLA の全体像とアーキテクチャ

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch02.mp4){:target="_blank"}

### 第3章: DiT アクションデコーダ — 拡散過程で動きを生成

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch03.mp4){:target="_blank"}

### 第4章: 大規模学習データとエンボディメント対応

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch04.mp4){:target="_blank"}

### 第5章: 実験結果・限界・今後の展望

<video controls width="100%" src="https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4"></video>

[Internet Archive で開く](https://archive.org/download/paper-explain-2605-30280/paper_2605.30280_ch05.mp4){:target="_blank"}

---

[← 論文一覧に戻る](../../)
