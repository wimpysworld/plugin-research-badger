# Research Badger - TypingMind Plugin

## Project Overview

Research Badger is a TypingMind plugin that performs deep, relentless research by searching the web and extracting content from online sources. Forked from `plugin-deep-research` and rebranded to emphasise tenacious, thorough investigation.

## Technology Stack

- **Plugin Format**: TypingMind JSON plugin specification
- **Implementation**: JavaScript (ES6+) and HTTP requests
- **APIs**: Serp API (web search), Firecrawl API (content extraction)
- **Runtime**: TypingMind plugin environment (browser-based)

## Project Structure

```
plugin-research-badger/
├── plugin.json         # Plugin configuration and function definitions
├── README.md          # User-facing documentation
├── icon.png           # Plugin icon (PNG format)
└── icon.svg           # Plugin icon (SVG source)
```

## Plugin Architecture

### Core Components

**plugin.json structure:**
- `id/uuid`: Unique plugin identifier (`c98a694c-74c7-426f-8aaa-24b52f2a3942`)
- `userSettings`: API keys and digging intensity configuration
- `pluginFunctions`: Four research tools (see below)
- `dynamicContextEndpoints`: System instructions for AI behaviour

### Plugin Functions

1. **Research Plan** (`update_research_plan`) - JavaScript
   - Manages structured research task lists
   - Tracks progress with todo items (pending/in_progress/completed/cancelled)

2. **Search Web** (`badger_search_web`) - HTTP
   - Google search via Serp API
   - Returns snippets, titles, and URLs

3. **Extract Web Page** (`extract_web_page`) - JavaScript
   - Lightweight extraction using Firecrawl
   - Mode-aware (Scout Dig/Deep Burrow/Adaptive Dig)

4. **Read Full Web Page** (`read_full_web_page_content`) - JavaScript
   - Full content retrieval in Deep Burrow/Adaptive Dig modes
   - Returns complete page markdown

## Configuration

### Required API Keys

- **Serp API**: Sign up at [serpapi.com](https://serpapi.com)
- **Firecrawl API**: Get key at [firecrawl.dev/app/api-keys](https://www.firecrawl.dev/app/api-keys)

### Digging Intensity

- **Scout Dig** (default): Token-efficient extraction with reduced accuracy
- **Deep Burrow**: Full content retrieval, high token consumption
- **Adaptive Dig**: Starts with Scout Dig, upgrades to full reads when needed

## Development

### Testing Plugin Changes

1. **Validate JSON syntax:**
   ```bash
   jq empty plugin.json
   ```

2. **Extract function names:**
   ```bash
   jq -r '.pluginFunctions[].openaiSpec.name' plugin.json
   ```

3. **Verify user settings:**
   ```bash
   jq '.userSettings' plugin.json
   ```

4. **Test in TypingMind:**
   - Import `plugin.json` via TypingMind plugin manager
   - Configure API keys in plugin settings
   - Create test chat and enable Research Badger
   - Test with: "Research the latest developments in quantum computing"

### Modifying Functions

**JavaScript functions:**
- Located in `plugin.json` under `pluginFunctions[].code`
- Must match `openaiSpec.name` exactly
- Accept `(params, userSettings)` arguments
- Support async/await for API calls

**HTTP actions:**
- Defined in `pluginFunctions[].httpAction`
- Support variable interpolation: `{paramName}`, `{settingName}`
- GET/POST methods supported

### Adding New Tools

1. Add function object to `pluginFunctions` array
2. Include unique `id` (UUID)
3. Define `openaiSpec` with name, parameters, description
4. Implement via `code` (JavaScript) or `httpAction` (HTTP)
5. Set `outputType: "respond_to_ai"`
6. Update dynamic context if behaviour guidance needed

## Code Style

### JSON

- 2-space indentation
- No trailing commas
- Use double quotes
- Validate with `jq`

### JavaScript

- ES6+ syntax (async/await, arrow functions, template literals)
- Handle errors explicitly (try/catch for API calls)
- Validate user settings before API requests
- Return structured objects with clear keys

### Naming Conventions

- Functions: `snake_case` (OpenAI spec requirement)
- User settings: `camelCase`
- Plugin namespace: `badger_*` for unique functions

## Testing Guidelines

### Manual Testing Checklist

- [ ] Plugin loads without errors
- [ ] API keys validate correctly
- [ ] Research plan creates and updates todos
- [ ] Web search returns relevant results
- [ ] Extract web page works in Scout Dig mode
- [ ] Full page read works in Deep Burrow/Adaptive Dig modes
- [ ] Mode switching behaves correctly
- [ ] Token usage is reasonable

### Test Queries

```
Simple: "What is quantum computing?"
Comparative: "Compare React vs Vue in 2026"
Multi-step: "Research AI coding assistants: features, pricing, and user reviews"
```

## Security Considerations

- **API keys**: Stored as password type (masked in UI)
- **User settings**: Never log or expose in responses
- **External APIs**: Validate responses before processing
- **Error messages**: Don't leak sensitive configuration details

## Git Workflow

### Commit Messages

Follow conventional commits:
```
feat: add citation tracking to extract_web_page
fix: handle Firecrawl API errors gracefully
docs: update README with troubleshooting section
refactor: consolidate API error handling
```

### Branch Strategy

- `main`: Stable, production-ready plugin
- Feature branches: `feat/feature-name`
- Fixes: `fix/issue-description`

## Resources

- [TypingMind Plugin Documentation](https://docs.typingmind.com/plugins/build-a-typingmind-plugin)
- [Serp API Documentation](https://serpapi.com/docs)
- [Firecrawl API Documentation](https://docs.firecrawl.dev)
- [OpenAI Function Calling](https://platform.openai.com/docs/guides/function-calling)

## Known Limitations

- Research Plan tool has no persistent state (AI must track todos)
- Token consumption can be high in Deep Burrow mode
- Maximum research session: ~2 minutes
- Requires valid API keys for both Serp and Firecrawl
- Adaptive Dig mode relies on AI discretion for full reads
