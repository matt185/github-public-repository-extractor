# GitHub Public Repository Extrator

This project allows you to extract the data of all the public repostitory of a specified GitHub user using `tap-github` extractor and stores the data in a local **SQLite** using `target-sqlite` loader.

---

## Prerequisites

- Python >=3.9
- Meltano
- GitHub Personal Access Token

---

## Project Setup

### 1. **Install Meltano**

To install the latest version:

```bash
pip install meltano
```

Or, to install the version specified in this project:

```bash
pip install -r requiremets.txt
```

### 2.**Install project dependency**:

Install project dependencies using:

`bash meltano install `

## Configure `tap-github` Extractor

### 1.Add GitHub Token

Create a .env file in the project root and add your GitHub token:

```bash
TAP_GITHUB_AUTH_TOKEN='Add Your GitHub Token here`
```

### 2.Set the target GitHub User

Replace **\<USERNAME\>** with the GitHub username you want to extract data for:

```bash
meltano config tap-github set searches '[{\"search_type\": \"search_repos\", \"name\": \"public_repos\", \"query\": \"user:<USERNAME> is:public\"}]'
```

Example:

```bash
meltano config tap-github set searches '[{\"search_type\": \"search_repos\", \"name\": \"public_repos\", \"query\": \"user:torvalds is:public\"}]'
```

### 3.Select Data to Extract

Specify which repository fields to extract. For example, to get just the repository names:

```bash
meltano select tap-github repositories name
```

To see all available fields:

```bash
meltano select tap-github --list --all
```

## Run the Pipeline

This command will delete the existing SQLite database and generate a new one in the output/ folder:

On **Windows (PowerShell)**:

```bash
Remove-Item .\output\database.db
meltano run --full-refresh tap-github target-sqlite
```

On **Mac/Linux (Bash)**:

```bash
rm output\database.db
meltano run --full-refresh tap-github target-sqlite
```

## Additional Resources

- [Meltano](https://meltano.com/)
- [tap-github GitHub Repository](https://github.com/MeltanoLabs/tap-github)
- [tap-github on Meltano Hub](https://hub.meltano.com/extractors/tap-github/)
- [GitHub Docs](https://docs.github.com/en/search-github/searching-on-github/searching-for-repositories)
- [target-sqlite on Meltano Hub](https://hub.meltano.com/loaders/target-sqlite/)
