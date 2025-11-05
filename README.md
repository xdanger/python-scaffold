# Python Project Scaffold

Python project scaffold for rapid cold start.

## Features

- Python 3.14 support
- Pre-commit hooks configured
- Ruff linter + formatter for Python
- Prettier formatter for Markdown/YAML/JSON/TOML
- AutoCorrect for Chinese copywriting
- Mise for unified tool management
- CI/CD with GitHub Actions

## Quick Start

### Option 1: With mise (Recommended)

[mise](https://mise.jdx.dev) automatically installs all required tools including Python, AutoCorrect, etc.

```bash
# Clone this repository
git clone <your-repo-url>
cd python-scaffold

# Install mise (if not already installed)
# macOS/Linux:
curl https://mise.run | sh
# or: brew install mise

# One-command setup (installs all tools + dependencies + hooks)
mise run setup
```

### Option 2: Manual setup

```bash
# Clone this repository
git clone <your-repo-url>
cd python-scaffold

# Install Python 3.14 and UV
# (mise does this automatically)

# Install AutoCorrect
brew install autocorrect  # macOS
# or see https://github.com/huacnlee/autocorrect/releases

# Install dependencies
uv sync --group dev

# Install pre-commit hooks
uv run pre-commit install
```

## Pre-commit Hooks

The following hooks run automatically on `git commit`:

1. **Ruff**: Lint and format Python code
2. **Prettier**: Format Markdown, YAML, JSON, TOML files
3. **AutoCorrect**: Format Chinese/CJK copywriting

## Manual Formatting

```bash
# Run all formatters at once (mise task)
mise run lint

# Or run individually:
uv run ruff check --fix .
uv run ruff format .
uv run pre-commit run prettier --all-files
autocorrect --fix .
```

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── lint.yml             # CI workflow
├── .vscode/
│   ├── settings.json            # VSCode editor settings
│   └── extensions.json          # Recommended extensions
├── .mise.toml                   # Tool version management
├── .pre-commit-config.yaml      # Pre-commit hooks configuration
├── .prettierrc                  # Prettier configuration
├── .prettierignore              # Prettier ignore rules
├── .autocorrectrc               # AutoCorrect configuration
├── .python-version              # Python version
├── pyproject.toml               # Project metadata and dependencies
├── main.py                      # Entry point
└── README.md                    # This file
```

## CI/CD

The project includes a GitHub Actions workflow (`.github/workflows/lint.yml`) that:

- Installs all tools via mise
- Runs all pre-commit hooks
- Ensures code quality on every push/PR

## VSCode Setup

The project includes VSCode configuration for optimal development experience.

### Recommended Extensions

When you open this project in VSCode, you'll be prompted to install recommended extensions:

- **Ruff** (`charliermarsh.ruff`) - Python linter & formatter
- **Prettier** (`esbenp.prettier-vscode`) - Markdown/JSON/YAML formatter
- **AutoCorrect** (`huacnlee.autocorrect`) - Chinese copywriting formatter
- **Even Better TOML** (`tamasfe.even-better-toml`) - TOML file support
- **Python** (`ms-python.python`) - Python language support

### Features

- **Format on Save**: Automatically formats code when saving files
- **Organize Imports**: Auto-organizes Python imports on save
- **Linting**: Real-time linting with Ruff
- **Chinese Formatting**: Auto-formats Chinese text with proper spacing

### Personal Settings

To override settings locally without committing, create `.vscode/settings.local.json` (already in `.gitignore`).

## Configuration

### Mise

Edit `.mise.toml` to manage tool versions:

```toml
[tools]
python = { path = ".python-version" }
"cargo:autocorrect" = "latest"
```

### Ruff

Edit `pyproject.toml`:

```toml
[tool.ruff]
line-length = 100
target-version = "py314"
```

### Prettier

Edit `.prettierrc`:

```json
{
  "printWidth": 100,
  "tabWidth": 2
}
```

### AutoCorrect

Edit `.autocorrectrc`:

```yaml
rules:
  space-word: 1
  space-punctuation: 1
```

## License

MIT
