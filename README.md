# discourse-rpg-sheet

Generate RPG character sheets from Discourse forum activity using [term-llm](https://github.com/juftin/term-llm) and the [Discourse MCP server](https://github.com/discourse/discourse-mcp).

## Setup

### Prerequisites

- Ruby 3.x
- Node.js / npm (for `npx`)
- [term-llm](https://github.com/juftin/term-llm)
- An OpenAI-compatible inference endpoint
- Optional: 1Password CLI (`op`) for secret management

### Configuration

Copy the example config and fill in your provider details:

```bash
cp config.example.json config.json
```

The script looks for config in this order:
1. `./config.json` (current directory)
2. `./.discourse-rpg-sheet.json`
3. `~/.config/discourse-rpg-sheet/config.json`
4. Explicit `--config PATH`

See `config.example.json` for the format, or run:

```bash
bin/discourse-rpg-sheet --example-config
```

### API key resolution

The script resolves the LLM API key in order:
1. Environment variable named in `provider.api_key_env`
2. 1Password reference in `provider.api_key_op` (using `provider.op_account`)

### Discourse MCP auth

By default, the script generates a fresh Discourse User API key each run using `@discourse/mcp generate-user-api-key`. You approve the key in your browser, paste the encrypted payload, and it's used only for that run.

## Usage

```bash
bin/discourse-rpg-sheet USERNAME [SITE_URL] [TIMEFRAME]
```

If `SITE_URL` is omitted, uses `discourse.default_site` from config.

Interactive by default: after data gathering and analysis, the script uses `ask_user` to let you choose/remix identity, stats, abilities, debuffs, and inventory before generating output.

### Examples

```bash
# Interactive (default)
bin/discourse-rpg-sheet USERNAME

# Specify site and timeframe
bin/discourse-rpg-sheet USERNAME https://your-discourse.com "last year"

# Batch mode: model decides everything
bin/discourse-rpg-sheet USERNAME --batch

# Custom output directory
bin/discourse-rpg-sheet USERNAME -o ./sheets

# Override model from CLI
bin/discourse-rpg-sheet USERNAME --model "different-model-name"

# Public read-only, no user API key
bin/discourse-rpg-sheet USERNAME https://your-discourse.com "last 30 days" --no-user-api-key
```

### Output

Two files in the output directory:
- `{username}-character-sheet.md`
- `{username}-character-sheet.html`

The HTML is self-contained (inline CSS/JS) and references an optional portrait at `{username}-character-portrait.png`.

## Debugging

```bash
DEBUG=1 bin/discourse-rpg-sheet USERNAME
bin/discourse-rpg-sheet USERNAME --keep-temp
```

## All options

```bash
bin/discourse-rpg-sheet --help
```
