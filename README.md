# discourse-rpg-sheet

Generate RPG character sheets from Discourse forum activity using [term-llm](https://github.com/juftin/term-llm) and the [Discourse MCP server](https://github.com/discourse/discourse-mcp).

The model gathers forum posts, analyzes patterns, and translates them into a fantasy RPG character sheet complete with stats, abilities, debuffs, quests, and an origin story. Everything is named in RPG language, not workplace language.

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

### Interaction modes

By default, the model asks you to pick your character's name, family, trade, and temper, then generates everything else automatically.

- `--review` adds a full sheet preview before output, with the option to re-roll sections
- `--batch` skips all interaction; the model decides everything
- `--reroll` skips data gathering and reuses the analysis from a previous run

### Examples

```bash
# Interactive (default): pick identity, auto-generate the rest
bin/discourse-rpg-sheet USERNAME

# With full review before output
bin/discourse-rpg-sheet USERNAME --review

# Re-roll: reuse gathered data, pick new identity and regenerate
bin/discourse-rpg-sheet USERNAME --reroll

# Batch mode: fully automatic, no interaction
bin/discourse-rpg-sheet USERNAME --batch

# Specify site and timeframe
bin/discourse-rpg-sheet USERNAME https://your-discourse.com "last year"

# Custom output directory
bin/discourse-rpg-sheet USERNAME -o ./sheets

# Public read-only, no user API key
bin/discourse-rpg-sheet USERNAME --no-user-api-key
```

### Output

Three files in the output directory:
- `{username}-analysis.md` — cached analysis data (reused by `--reroll`)
- `{username}-character-sheet.md` — the character sheet in markdown
- `{username}-character-sheet.json` — structured character data

The script renders HTML automatically from the JSON using an ERB template. The HTML page is written to `{username}-character-sheet.html` and references an optional portrait at `{username}-character-portrait.png`.

A portrait generation prompt is printed at the end of each run.

## Debugging

```bash
DEBUG=1 bin/discourse-rpg-sheet USERNAME
bin/discourse-rpg-sheet USERNAME --keep-temp
```

## All options

```bash
bin/discourse-rpg-sheet --help
```
