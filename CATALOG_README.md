# Prompt Catalog Documentation

This document describes the structure and usage of `prompt_catalog.json`, a comprehensive metadata catalog of 410 system prompts from various AI providers.

## Overview

The `prompt_catalog.json` file is an automatically generated catalog that provides structured metadata for all system prompts in the repository. It enables programmatic access to prompt information without needing to read individual markdown files.

## File Statistics

- **Total prompts cataloged**: 410
- **Total tokens**: 2,660,614
- **Last generated**: 2026-07-23T02:29:24.207794

## Structure

The JSON file contains two main sections:

### 1. Metadata Section

```json
{
  "metadata": {
    "generated_at": "2026-07-23T02:29:24.207794",
    "total_files": 410,
    "total_tokens": 2660614,
    "categories": { ... },
    "providers": { ... }
  }
}
```

#### Categories Distribution

| Category | Count | Description |
|----------|-------|-------------|
| `skill_definition` | 126 | Claude Code bundled skills |
| `general_assistant` | 55 | General-purpose AI assistants |
| `system_prompt` | 41 | Core system prompts |
| `legacy_prompt` | 36 | Older/deprecated prompts |
| `coding_assistant` | 34 | Code generation/editing assistants |
| `official_model_prompt` | 34 | Official published prompts |
| `agent_prompt` | 11 | Autonomous agent configurations |
| `slash_command` | 9 | Claude Code slash commands |
| `injected_reminder` | 8 | Runtime-injected instructions |
| `research_assistant` | 8 | Research-focused assistants |
| `documentation` | 7 | Documentation/metadata files |
| `api_prompt` | 7 | API-specific prompts |
| `document_assistant` | 6 | Document processing assistants |
| `mcp_server` | 5 | Model Context Protocol servers |
| `personality_prompt` | 5 | Personality/role configurations |
| `raw_capture` | 4 | Verbatim captures |
| `voice_assistant` | 4 | Voice interface assistants |
| `design_assistant` | 3 | Design-focused assistants |
| `browser_assistant` | 3 | Browser extension assistants |
| `image_assistant` | 2 | Image processing assistants |
| `tool_prompt` | 1 | Tool-specific prompts |
| `memory_assistant` | 1 | Memory/context management |

#### Providers Distribution

| Provider | Count | Products Included |
|----------|-------|-------------------|
| `anthropic` | 240 | Claude, Claude Code, Claude Design, Claude Cowork |
| `openai` | 84 | ChatGPT, GPT-5.x, Codex, o-series |
| `misc` | 24 | Various third-party products |
| `google` | 22 | Gemini, AI Studio, Jules |
| `xai` | 11 | Grok models |
| `microsoft` | 5 | GitHub Copilot, VS Code Copilot |
| `perplexity` | 5 | Perplexity AI, Deep Research |
| `kimi` | 2 | Kimi K2.6 |
| `meta` | 2 | Meta AI Muse Spark |
| `mistral` | 2 | Mistral Medium, Mistral Code |
| `cursor` | 1 | Cursor IDE |
| `deepseek` | 1 | DeepSeek Chat |
| `glm` | 1 | GLM (Z.ai) |
| `notion` | 1 | Notion AI |
| `opencode` | 1 | OpenCode |
| `pi` | 1 | Pi (Inflection) |
| `qwen` | 1 | Qwen 3.6 Plus |

### 2. Prompts Array

```json
{
  "prompts": [
    {
      "id": "path/to/file.md",
      "title": "Prompt Title",
      "provider": "anthropic",
      "category": "system_prompt",
      "subcategory": "general",
      "persona": "",
      "tools_or_integrations": [],
      "guardrails_and_constraints": [],
      "best_fit_scenarios": [],
      "is_documentation": false,
      "size_bytes": 10711,
      "size_tokens": 2677,
      "source_hash": "7984C5193FA257B04EE9D12F83A2DB94",
      "confidence": "high",
      "purpose_summary": "Description of the prompt's purpose",
      "key_capabilities": [],
      "output_format_hint": ""
    }
  ]
}
```

## Field Descriptions

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Relative path to the prompt file (e.g., `Anthropic/claude-opus-4.8.md`) |
| `title` | string | Human-readable name of the prompt |
| `provider` | string | Company/provider identifier (lowercase) |
| `category` | string | Primary classification (see Categories Distribution) |
| `subcategory` | string | Secondary classification (e.g., `general`, `coding`, `voice`) |
| `is_documentation` | boolean | Whether this is documentation vs. actual prompt content |
| `size_bytes` | integer | File size in bytes |
| `size_tokens` | integer | Approximate token count |
| `source_hash` | string | MD5 hash for change detection |
| `confidence` | string | Extraction confidence: `high`, `medium`, or `low` |

### Content Analysis Fields

| Field | Type | Description |
|-------|------|-------------|
| `persona` | string | Role/persona the AI adopts (empty if none) |
| `tools_or_integrations` | string[] | Tools, APIs, or integrations mentioned |
| `guardrails_and_constraints` | string[] | Safety rules, restrictions, or behavioral constraints |
| `best_fit_scenarios` | string[] | Recommended use cases |
| `purpose_summary` | string | Brief description of what the prompt does |
| `key_capabilities` | string[] | Notable features or abilities |
| `output_format_hint` | string | Expected output format (if specified) |

## Usage Examples

### Filtering by Provider

```javascript
const catalog = require('./prompt_catalog.json');

// Get all Anthropic prompts
const anthropicPrompts = catalog.prompts.filter(p => p.provider === 'anthropic');

// Get all OpenAI prompts
const openaiPrompts = catalog.prompts.filter(p => p.provider === 'openai');
```

### Filtering by Category

```javascript
// Get all system prompts
const systemPrompts = catalog.prompts.filter(p => p.category === 'system_prompt');

// Get all coding assistants
const codingAssistants = catalog.prompts.filter(p => p.category === 'coding_assistant');

// Get all skill definitions
const skills = catalog.prompts.filter(p => p.category === 'skill_definition');
```

### Finding Prompts with Specific Tools

```javascript
// Find prompts that use web search
const webSearchPrompts = catalog.prompts.filter(p => 
  p.tools_or_integrations.some(t => t.toLowerCase().includes('web'))
);

// Find prompts with file operations
const filePrompts = catalog.prompts.filter(p => 
  p.tools_or_integrations.some(t => 
    t.toLowerCase().includes('file') || t.toLowerCase().includes('read')
  )
);
```

### Analyzing Guardrails

```javascript
// Find prompts with safety constraints
const safePrompts = catalog.prompts.filter(p => 
  p.guardrails_and_constraints.length > 0
);

// Find prompts with content restrictions
const restrictedPrompts = catalog.prompts.filter(p => 
  p.guardrails_and_constraints.some(g => 
    g.toLowerCase().includes('never') || g.toLowerCase().includes('refuse')
  )
);
```

### Size Analysis

```javascript
// Find largest prompts by token count
const largestPrompts = [...catalog.prompts]
  .sort((a, b) => b.size_tokens - a.size_tokens)
  .slice(0, 10);

// Find smallest prompts
const smallestPrompts = [...catalog.prompts]
  .sort((a, b) => a.size_tokens - b.size_tokens)
  .slice(0, 10);
```

### Confidence Filtering

```javascript
// Only high-confidence extractions
const highConfidence = catalog.prompts.filter(p => p.confidence === 'high');

// Low confidence (may need review)
const lowConfidence = catalog.prompts.filter(p => p.confidence === 'low');
```

## Data Quality Notes

### Confidence Levels

- **high**: Prompt was clearly extracted with minimal parsing issues
- **medium**: Some parsing challenges but content is reliable
- **low**: Significant parsing issues; manual review recommended

### Common Issues

1. **Truncated fields**: Some `purpose_summary` and `key_capabilities` fields may be truncated due to extraction limits
2. **Partial tool extraction**: `tools_or_integrations` may contain partial matches or noise
3. **Persona detection**: Empty `persona` field doesn't mean no persona exists; it may not have been detected

## Regenerating the Catalog

The catalog is generated by scanning all `.md` files in the repository. To regenerate:

1. Ensure all prompt files are in their correct directories
2. Run the catalog generation script (if available)
3. The `generated_at` timestamp will update automatically

## Contributing

When adding new prompts to the repository:

1. Place the file in the appropriate provider directory
2. Use a descriptive filename matching the model/product
3. Include the raw, unedited system prompt
4. The catalog will be regenerated on the next build

For more details, see [CONTRIBUTING.md](.github/CONTRIBUTING.md).

## Example Queries

### Find all Claude Code skills
```bash
# Using jq
jq '.prompts[] | select(.provider == "anthropic" and .category == "skill_definition") | .title' prompt_catalog.json
```

### Count prompts per provider
```bash
jq '.metadata.providers | to_entries | sort_by(.value) | reverse' prompt_catalog.json
```

### List prompts with voice capabilities
```bash
jq '.prompts[] | select(.subcategory == "voice") | {id, title, provider}' prompt_catalog.json
```

### Export to CSV
```bash
jq -r '.prompts[] | [.id, .title, .provider, .category, .size_tokens] | @csv' prompt_catalog.json > prompts.csv
```

## License

This catalog is part of the [System Prompts Leaks](https://github.com/asgeirtj/system_prompts_leaks) repository. See the repository for license information.
