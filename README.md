# Trello Loader

A tool for loading Trello boards and converting them to structured Markdown files for AI agents.

## Features

- Loads Trello boards via the official API
- Converts Trello lists and cards into structured Markdown files
- Preserves important information such as descriptions, checklists, labels, and due dates
- Formats tasks as Markdown ToDo lists, ideal for AI agents

## Installation with uv

This project is managed with [uv](https://github.com/astral-sh/uv), an ultra-fast Python package manager.

If you don't have uv installed yet, you can install it with the following command:

```bash
curl -sSf https://install.astronomer.dev | sh
```

Or on Windows with:

```powershell
powershell -c "irm https://install.astronomer.dev | iex"
```

### Project Installation

1. Clone the repository
2. Change to the project directory
3. Install dependencies with uv:

```bash
uv pip install -e .
```

## Configuration

1. Create a `.env` file in the project's root directory
2. Add your Trello API keys (see `.env.example`)

To obtain Trello API keys:
1. Visit https://trello.com/app-key
2. Log in with your Trello account
3. Copy your API key
4. Generate a token with appropriate permissions

## Usage

### List all boards

```bash
uv run trello-to-md list-boards
```

### Convert a board

```bash
uv run trello-to-md convert BOARD_ID
```

Where `BOARD_ID` is the ID of the Trello board, which you can find using `list-boards`.

#### Options

- `--output` / `-o`: Path to the output Markdown file
- `--archived` / `-a`: Include archived cards

### Example

```bash
trello-to-md convert abc123 -o my_tasks.md
```

## Output Format

The generated Markdown file is structured as follows:

```markdown
# Board Name

Board description, if available

*Created on: YYYY-MM-DD HH:MM*

*Board ID: abc123*

---

## List 1

- [ ] **Card name**
  Card description
  - Checklists:
    - Checklist 1
      - [ ] Item 1
      - [x] Item 2
  - Tags: `Tag1`, `Tag2`
  - Due: YYYY-MM-DD HH:MM
  - [Go to card](https://trello.com/...)

## List 2

- [ ] **Card name 2**
  ...
```

## Publishing to PyPI

If you want to publish this package to PyPI:

1. Update the version in `pyproject.toml` and `trello_loader/__init__.py`
2. Install the required build tools:
   ```bash
   uv pip install build twine
   ```
3. Build the package:
   ```bash
   uv run -m build
   ```
4. Upload to PyPI:
   ```bash
   uv run -m twine upload dist/*
   ```

You'll need PyPI credentials to publish the package.

## Installation from PyPI

Once published, the package can be installed with:

```bash
uv pip install trello-loader
```

## License

MIT