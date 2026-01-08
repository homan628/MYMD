# MyMD — Personal Knowledge Database

<div align="center">

![MyMD System](https://img.shields.io/badge/MyMD-v1.0.0-blue)
![AI Ready](https://img.shields.io/badge/AI-Native-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

**把你的人生數據，變成 AI 能精準讀取的知識庫**

[English](#english) | [中文](#chinese) | [日本語](#japanese)

</div>

---

<a name="english"></a>

## English

### The Problem

Traditional AI chatbots read your entire conversation history every time you ask a question:
- 🔥 **Token waste** — Rereading thousands of messages
- 👻 **Hallucinations** — AI gets confused by too much context
- 🎯 **Imprecise answers** — Important details buried in noise

### The Solution: MyMD

MyMD is an **AI-Native Personal Knowledge Database** that splits your life data into **independent MD files**. Each file is self-contained — AI reads only what it needs, precisely.

> "Who is Alex?" → AI reads only `alex.md`  
> "What camera do I own?" → AI reads only `sony-a7iv.md`  
> **No digging through full context. Precise retrieval.**

### ✨ Core Philosophy

| Concept | What It Means |
|---------|---------------|
| **Independent MD Files** | Each entity (person, project, place) = one file |
| **Self-Contained** | Every file has summary + history. No need to read other files. |
| **Precise Retrieval** | AI reads only the relevant file, not the whole database |

MyMD combines:
- 📝 **Zettelkasten** — Atomic notes
- 🧠 **Second Brain** — Externalized memory  
- 🔍 **RAG Best Practices** — On-demand retrieval

### 📂 Structure

```
MYMD/
├── me.md                    # Your profile & index
├── relationships/           # People, pets, communities
├── work/                    # Career, projects, clients
├── experiences/             # Places, food, content consumed
├── assets/                  # Gear, digital assets
├── knowledge/               # Skills, credentials, notes
├── health/                  # Medical, habits
├── values/                  # Goals, preferences
├── timeline/                # Daily diary (source of truth)
└── _system/                 # System core (AI reads this first)
    ├── _metadata.md         # Main operating manual
    ├── _templates/          # Entity templates
    ├── _tags.md             # Controlled vocabulary
    ├── _logs/               # AI operation logs
    └── _onboarding.md       # New user questionnaire
```

### 🚀 How It Works

#### 1. Dump Your Data
Throw messy data at the AI:
- Resumes, CVs
- Chatbot exports (ChatGPT, Claude)
- Diaries, notes

#### 2. AI Organizes
AI follows rules in `_system/_metadata.md` to:
1. **Analyze** — Identify entities (Person, Project, Place...)
2. **Split** — Create independent MD files
3. **Link** — Build bidirectional connections

#### 3. Precise Retrieval
Each file contains:
- **Attributes** — Flat YAML for quick parsing
- **Description** — AI-generated summary
- **History Log** — Self-contained context
- **Links** — Related entities and timeline entries

### ⚡️ Setup

Works with **Cursor**, **VS Code + Copilot**, **Obsidian**, or any AI editor.

1. AI reads `_system/_metadata.md` for rules
2. `.cursorrules` at root guides AI behavior
3. Each folder has `[folder]_overview.md` for indexing

### 🆕 Getting Started

1. Copy `_system/_onboarding.md` and fill in your info
2. Tell AI: *"Process my onboarding and update me.md"*
3. Start dumping data — AI handles the rest!

---

<a name="chinese"></a>

## 中文

### 問題

傳統 AI 聊天機器人每次回答問題，都要重讀整段對話記錄：
- 🔥 **浪費 Tokens** — 重複讀取成千上萬的訊息
- 👻 **容易幻覺** — 上下文太多，AI 容易混亂
- 🎯 **回答不精準** — 重要細節被淹沒在雜訊中

### 解決方案：MyMD

MyMD 是一個 **AI 原生的個人知識庫**，把你的人生數據拆分成**獨立 MD 檔案**。每個檔案自成一體，AI 只讀需要的那一個，精準讀取。

> 「Alex 是誰？」→ AI 只讀 `alex.md`  
> 「我有什麼相機？」→ AI 只讀 `sony-a7iv.md`  
> **無需翻找全部上下文，精準讀取。**

### ✨ 核心理念

| 概念 | 含義 |
|-----|------|
| **獨立 MD 檔案** | 每個實體（人物、專案、地點）= 一個獨立檔案 |
| **檔案自成一體** | 每個檔案都有摘要 + 歷史記錄，無需讀其他檔案 |
| **精準讀取** | AI 只讀相關檔案，不用掃全庫 |

MyMD 結合了：
- 📝 **Zettelkasten** — 原子化筆記
- 🧠 **第二大腦** — 外部化記憶
- 🔍 **RAG 最佳實踐** — 按需檢索

### 📂 結構

```
MYMD/
├── me.md                    # 個人檔案與索引
├── relationships/           # 人際關係
├── work/                    # 工作、專案
├── experiences/             # 體驗（地點、美食、影視）
├── assets/                  # 資產（設備、數位資產）
├── knowledge/               # 知識（技能、證照、筆記）
├── health/                  # 健康
├── values/                  # 價值觀、目標
├── timeline/                # 日記（資料來源）
└── _system/                 # 系統核心
    ├── _metadata.md         # 規則手冊
    ├── _templates/          # 模板
    ├── _tags.md             # 標籤詞彙
    ├── _logs/               # 操作日誌
    └── _onboarding.md       # 新手問卷
```

### 🚀 運作方式

#### 1. 傾倒數據
把雜亂的資料丟給 AI：
- 履歷表、CV
- 對話記錄（ChatGPT、Claude 匯出）
- 日記、筆記

#### 2. AI 自動整理
AI 依照 `_system/_metadata.md` 規則：
1. **分析** — 辨識實體（人物、專案、地點⋯）
2. **拆分** — 建立獨立 MD 檔案
3. **連結** — 建立雙向關聯

#### 3. 精準讀取
每個檔案包含：
- **屬性** — 扁平化 YAML，方便解析
- **Description** — AI 生成的摘要
- **歷史記錄** — 檔案內的上下文
- **連結** — 關聯的實體與時間軸

### ⚡️ 環境設定

支援 **Cursor**、**VS Code + Copilot**、**Obsidian** 等 AI 編輯器。

1. AI 讀取 `_system/_metadata.md` 了解規則
2. 根目錄 `.cursorrules` 指引 AI 行為
3. 每個資料夾有 `[folder]_overview.md` 作為索引

### 🆕 開始使用

1. 複製 `_system/_onboarding.md` 填寫基本資料
2. 告訴 AI：「處理我的 onboarding 並更新 me.md」
3. 開始傾倒數據，AI 會自動處理！

---

<a name="japanese"></a>

## 日本語

### 問題

従来のAIチャットボットは、質問のたびに全会話履歴を読み直します：
- 🔥 **トークンの無駄** — 数千のメッセージを再読み込み
- 👻 **ハルシネーション** — コンテキストが多すぎてAIが混乱
- 🎯 **回答が不正確** — 重要な詳細がノイズに埋もれる

### 解決策：MyMD

MyMDは **AIネイティブな個人知識データベース** です。人生のデータを**独立したMDファイル**に分割。各ファイルは自己完結型 — AIは必要なものだけを的確に読み取ります。

> 「Alexって誰？」→ AIは `alex.md` だけを読む  
> 「持ってるカメラは？」→ AIは `sony-a7iv.md` だけを読む  
> **全コンテキストを探す必要なし。的確な検索。**

### ✨ 核心理念

| コンセプト | 意味 |
|-----------|------|
| **独立MDファイル** | 各エンティティ（人物、プロジェクト、場所）= 1ファイル |
| **自己完結型** | 各ファイルにサマリー＋履歴を含む。他ファイル不要 |
| **的確な検索** | AIは関連ファイルのみ読み取り、DB全体をスキャンしない |

MyMDは以下を統合：
- 📝 **Zettelkasten** — アトミックノート
- 🧠 **セカンドブレイン** — 外部化された記憶
- 🔍 **RAGベストプラクティス** — オンデマンド検索

### 📂 構成

```
MYMD/
├── me.md                    # プロフィール＆インデックス
├── relationships/           # 人間関係
├── work/                    # 仕事、プロジェクト
├── experiences/             # 体験（場所、グルメ、コンテンツ）
├── assets/                  # 資産（機材、デジタル）
├── knowledge/               # 知識（スキル、資格、ノート）
├── health/                  # 健康
├── values/                  # 価値観、目標
├── timeline/                # 日記（データソース）
└── _system/                 # システムコア
    ├── _metadata.md         # 操作マニュアル
    ├── _templates/          # テンプレート
    ├── _tags.md             # タグ語彙
    ├── _logs/               # 操作ログ
    └── _onboarding.md       # 新規ユーザー質問票
```

### 🚀 仕組み

#### 1. データを投入
雑多なデータをAIに渡す：
- 履歴書、CV
- チャットログ（ChatGPT、Claudeからエクスポート）
- 日記、メモ

#### 2. AIが自動整理
AIは `_system/_metadata.md` のルールに従って：
1. **分析** — エンティティを特定（人物、プロジェクト、場所...）
2. **分割** — 独立したMDファイルを作成
3. **リンク** — 双方向の関連を構築

#### 3. 的確な検索
各ファイルに含まれる：
- **属性** — フラットなYAML（解析しやすい）
- **Description** — AI生成のサマリー
- **履歴ログ** — ファイル内のコンテキスト
- **リンク** — 関連エンティティとタイムライン

### ⚡️ セットアップ

**Cursor**、**VS Code + Copilot**、**Obsidian** 等のAIエディタで動作。

1. AIが `_system/_metadata.md` でルールを把握
2. ルートの `.cursorrules` がAI動作を誘導
3. 各フォルダに `[folder]_overview.md` でインデックス

### 🆕 はじめに

1. `_system/_onboarding.md` をコピーして基本情報を入力
2. AIに「onboardingを処理してme.mdを更新して」と伝える
3. データを投入 — 後はAIにお任せ！

---

<div align="center">

**MyMD** — Your life, organized for AI ❤️

</div>
