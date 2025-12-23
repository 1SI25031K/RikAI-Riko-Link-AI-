# RikAI apollo for Slack (RikoLink Activity Intelligence) 

> **「活動を、価値に。」** > RikAIは、理工系学生の日常的な開発プロセスを定量化し、その「熱量」と「技術力」を正当な対価（ROI）へと変換する、RikoLink専用のインテリジェンス・エンジンです。

---

## 1. Introduction
理系学生サークル（ロボコン、競技プログラミング、開発チーム）において、SlackやDiscordでの議論、GitHubでのコミットは、単なるログではなく「無形の資産」です。

**RikAI**は、これらの活動ログをリアルタイムに収集・解析し、独自アルゴリズムによって**TechLeader Score**として可視化します。学生には「動けば評価される」体験を、企業には「データに基づく確信ある投資」を提供し、エンジニアリングの価値を再定義します。

---

## 2. Core Features
RikAIは、以下の3つのコア機能によって学生の活動を支援します。

* **@RikAI Weekly Summary Generation** 1週間の活動ログをGemini 1.5 Proが解析。「今週の技術的ブレイクスルー」や「チーム貢献」を自動要約し、ポートフォリオとして蓄積可能な形式で出力します。
* **TechLeader Score Reflection** 後述する評価式に基づき、実装力(TES)や貢献度(TCS)をリアルタイム更新。活動の偏りを防ぎ、バランスの取れた成長を促します。
* **Enterprise Report Export** 企業の採用担当者や投資家向けに、個人の技術スタックと成長曲線、活動実績をワンクリックで公式レポートとして送信。ES不要のマッチングを実現します。

---

## 3. Tech Stack
最新のクラウドネイティブな技術スタックを採用し、OCI上でのセキュアかつ高速な運用を実現しています。

* **Language:** Python 3.11+
* **Bot Framework:** Slack Bolt SDK
* **AI Engine:** Gemini 1.5 Flash / Pro (via Google AI SDK)
* **Infrastructure:** Oracle Cloud Infrastructure (OCI)
    * **Compute:** OCI Ampere A1 Compute (ARM)
    * **Functions:** OCI Functions (Serverless pipeline)
* **Database:** Oracle Autonomous JSON Database / Autonomous Data Warehouse (ADW)

---

## 4. Architecture
RikAIは、Slackerフレームワークの設計思想（モジュール化）を継承し、以下のパイプラインで動作します。

```text
[Slack Workspace] 
      │
      ▼ (Event Subscriptions / Webhook)
[OCI API Gateway]
      │
      ▼ (Triggers)
[OCI Functions (Listener/Filter)] ───▶ [Gemini 1.5 API (Analysis)]
      │                                       │
      ▼                                       ▼
[Oracle Autonomous DB] ◀────────── [OCI Functions (Scoring Engine)]
      │
      ▼ (Notification)
[Slack / Enterprise UI]

```
---

## 5. Evaluation Formula: TechLeader Score
学生の活動は、以下の多角的な指標によって算出されます。このスコアは、エンジニアの実装力だけでなく、チームへの貢献や成長速度を正当に評価するためのものです。

$$TechLeader Score = 0.4 \times TES + 0.3 \times PCS + 0.2 \times TCS + 0.1 \times TGS$$

| 指標 | 名称 | 定義 | データソース |
| :--- | :--- | :--- | :--- |
| **TES** | **実装力** (Technical Execution Score) | コードの品質、PR承認率、GitHubでのアクティビティ | GitHub API |
| **PCS** | **完遂力** (Project Completion Score) | マイルストーン達成率、納期遵守率、大会実績 | 実績データ |
| **TCS** | **貢献度** (Team Contribution Score) | Slackでのレビュー、レスポンス速度、ドキュメント作成 | Slack API |
| **TGS** | **成長率** (Technical Growth Score) | 新技術の習得数、コード品質の時系列改善度 | AI Analysis |

---

## 6. Getting Started

### 6.1 Prerequisites
* Python 3.11 以上
* OCI CLI のセットアップと認証情報の構成
* Slack App (Bot Token & Signing Secret) の取得

### 6.2 Setup Environment
プロジェクトのルートディレクトリに `.env` ファイルを作成し、必要なトークンとOCIの構成情報を設定してください。

```bash
# Slack Configuration
SLACK_BOT_TOKEN=xoxb-your-token
SLACK_SIGNING_SECRET=your-secret

# Gemini API
GEMINI_API_KEY=your-gemini-key

# Oracle DB (OCI) Configuration
OCI_USER_OCID=ocid1.user.oc1...
OCI_TENANCY_OCID=ocid1.tenancy.oc1...
OCI_KEY_FILE=./path/to/your/oci_api_key.pem
OCI_REGION=ap-tokyo-1

```

### 6.3 Installation & Run
依存関係をインストールし、リスナーサーバーを起動してBotを有効化します。ローカル環境でのテストには `ngrok` 等を利用して公開URLを取得し、Slack Appの設定画面（Event Subscriptions）に登録してください。

```bash
# 依存関係のインストール
pip install -r requirements.txt

# リスナーサーバーの起動 (Local Test)
# backend/f01_listener/server.py がエントリーポイントとなります
python -m backend.f01_listener.server

```

---

## 7. License
Copyright (c) 2025 RikoLink Project. All rights reserved.

本プロジェクトは、理工系学生の技術的貢献を正当に評価し、産業界との健全な架け橋となることを目的としています。無断転載および商用利用については、RikoLink運営事務局までお問い合わせください。

Developed with ❤️ by **Kosei Miyamoto** & **GEM (AI Architect)**.
