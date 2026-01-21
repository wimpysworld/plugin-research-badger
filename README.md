# Research Badger 🦡

Relentlessly dig through online sources to uncover comprehensive insights on any topic. Research Badger compiles thorough reports by drafting research plans, searching the web, and reading web pages with tenacious attention to detail.

This plugin was forked from [TypingMind Deep Research](https://github.com/TypingMind/plugin-deep-research) and uses [**Jina AI**](https://jina.ai/) for both web search and content extraction. You only need a single Jina AI API key to start using it.

## Installation

### Method 1: Import via URL (Recommended)

1. Open **TypingMind** and navigate to **Plugins**
2. Click **Import plugins** button
3. Paste this URL into the import field:
   ```
   https://github.com/wimpysworld/plugin-research-badger
   ```
4. Click **Import** to add Research Badger to your TypingMind instance

### Method 2: Import via JSON

1. Download the `plugin.json` file from this repository
2. Open **TypingMind** → **Plugins** → **Create Plugin**
3. Select **Import plugin from JSON**
4. Upload the downloaded `plugin.json` file

### Configuration

After installation, you'll need to configure the plugin with your API key:

1. Open **TypingMind** → **Plugins**
2. Find **Research Badger** and click **Settings**
3. Enter your **Jina AI API Key**: Get your free key at [jina.ai/?sui=apikey](https://jina.ai/?sui=apikey)
4. Select your preferred **Digging Intensity** (see below)
5. Save your settings

**Note**: Jina AI offers a generous free tier suitable for testing and moderate use.

## Digging Intensity

- **Snuffle**: Research Badger will attempt to extract data from online sources using the extract tool from Jina AI Reader, which saves tokens at a cost of reduced data accuracy. This is the default mode.
- **Burrow**: Research Badger will read the full content of the online sources to determine the final answer. If the web pages have a lot of content, it can risk consuming a lot of tokens, which is expensive and may exceed the model's context length limit.
- **Instinct**: Research Badger will run in Snuffle mode by default, but may opt in to read full web page content when absolutely needed to get the most accurate answer.

### Customisable

The Research Badger plugin is customisable. You can duplicate this plugin and add your own tools to enhance the quality of the final report. The system instructions and prompts are also available in the plugin source.

By default, the Research Badger plugin comes with 3 tools: Research Plan, Search Web, and Read Web Page. Depending on your specific needs, you can add more tools like reading from a tweet, searching from a private database, or controlling a browser. The TypingMind plugin system allows you to add multiple tools to the Research Badger plugin and supports various ways to implement your tools using JavaScript, HTTP requests, or MCP.

[Learn how to develop TypingMind plugins here](https://www.typingmind.com/plugins-docs).

## Token Usage

This plugin may use multiple tools in multiple turns. A deep research task can run for up to 2 minutes. Please monitor the token usage closely to avoid consuming too many tokens. You can also modify the plugin to make it more token-efficient by adding your own tools to perform web searches and read web pages.

### Example Usage

> Compare the current latest EV cars and their prices available for purchase in the EU.
