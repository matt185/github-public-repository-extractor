# GitHub Public Repository Extrator

こちらのプロジェクトでは、指定した GitHub ユーザーのすべての公開リポジトリのデータを、tap-github エクストラクターを使用して抽出し、target-sqlite ローダーを使用してローカルの SQLite データベースに保存することができます。

---

## 必要条件

- Python >=3.9
- Meltano
- GitHub Personal Access Token

---

## セットアップ方法

### 1. **セットアップ Environment Variable**

**Windows**:

```bash
$env:PYTHONIOENCODING = "utf-8"
```

**Mac/Linux**:

```bash
export PYTHONIOENCODING=utf-8
```

### 2. **Meltano のインストール**

```bash
pip install meltano
```

または、プロジェクトで指定されたバージョンをインストールする場合：

```bash
pip install -r requiremets.txt
```

### 3.**プロジェクトの依存関係をインストールする**:

プロジェクトの依存関係を以下のコマンドでインストールします:

`bash meltano install `

##tap-github エクストラクターの設定

### 1.GitHub トークンを追加する

プロジェクトのルートに .env ファイルを作成し、GitHub トークンを追加してください：

```bash
TAP_GITHUB_AUTH_TOKEN='ここにあなたのGitHubトークンを追加してください`
```

### 2.ターゲット GitHub ユーザーを設定する

\<USERNAME\> を、データを抽出したい GitHub ユーザー名に置き換えてください：

```bash
meltano config tap-github set searches '[{\"search_type\": \"search_repos\", \"name\": \"public_repos\", \"query\": \"user:<USERNAME> is:public\"}]'
```

例:

```bash
meltano config tap-github set searches '[{\"search_type\": \"search_repos\", \"name\": \"public_repos\", \"query\": \"user:torvalds is:public\"}]'
```

### 3.抽出するデータを選択する

抽出するリポジトリのフィールドを指定します。例えば、リポジトリ名のみを取得するには：

```bash
meltano select tap-github repositories name
```

利用可能なすべてのフィールドを表示するには：

```bash
meltano select tap-github --list --all
```

## Pipeline を実行する

このコマンドは既存の SQLite データベースを削除し、output/ フォルダに新しいデータベースを生成します：

**Windows**:

```bash
Remove-Item .\output\database.db
meltano run --full-refresh tap-github target-sqlite
```

**Mac/Linux**:

```bash
rm output\database.db
meltano run --full-refresh tap-github target-sqlite
```

## 追加のリソース

- [Meltano](https://meltano.com/)
- [tap-github GitHub Repository](https://github.com/MeltanoLabs/tap-github)
- [tap-github on Meltano Hub](https://hub.meltano.com/extractors/tap-github/)
- [GitHub Docs](https://docs.github.com/en/search-github/searching-on-github/searching-for-repositories)
- [target-sqlite on Meltano Hub](https://hub.meltano.com/loaders/target-sqlite/)
