---
title: "Qwen-VLA: タスク・環境・ロボット形態を超えた統一VLA"
layout: default
---

<script>
MathJax = { tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']], processEscapes: true } };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js" async></script>

- arXiv: [2605.30280](https://arxiv.org/abs/2605.30280)
- Internet Archive: [paper-explain-2605-30280](https://archive.org/details/paper-explain-2605-30280)

---

## 概要

アリババQwenチームが発表したQwen-VLA論文を徹底解説します。Qwen3.5-4BバックボーンとDiTベースのフローマッチングデコーダを組み合わせ、ロボット操作・ナビゲーション・自我視点データを単一モデルで統一。4段階学習レシピ（T2A→CPT→SFT→RL）と大規模ジョイント事前学習の詳細を、数式を交えてわかりやすく解説します。LIBERO 97.9%・RoboTwin Hard 87.2%・実世界ALOHA OOD 76.9%の最先端成果も紹介。

▼ 今日の論文
・Qwen-VLA: Unifying Vision-Language-Action Modeling across Tasks, Environments, and Robot Embodiments — Qwen Team (arXiv:2605.30280)

▼ 目次
00:00 研究の背景と課題
02:30 統一モデルの定式化
05:00 モデルアーキテクチャ（DiT・1.15Bパラメータ）
09:30 エンボディメント対応プロンプト
12:00 統一アクション表現と学習目標（フローマッチング）
16:00 4段階学習レシピ
20:30 大規模ロボット操作データ（10,000時間以上）
25:00 自我視点・合成・ナビゲーションデータ
29:00 ポスト訓練：SFTと強化学習（PPO）
33:30 シミュレーション操作実験
37:00 実世界実験（ALOHA）
40:00 ナビゲーション実験
42:30 アブレーション分析
45:00 まとめ

▼ 参考論文（arXiv）
https://arxiv.org/abs/2605.30280  — Qwen-VLA: Unifying Vision-Language-Action Modeling

#論文解説 #ロボット #生成AI #Alibaba #QwenVLA #VLA #ずんだもん #ゆっくり解説 #arxiv #人工知能 #機械学習 #強化学習 #フローマッチング

---

---

[← 論文一覧に戻る](../../)
