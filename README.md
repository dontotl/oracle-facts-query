# Oracle Facts Query & Source Manager

A Claude Code skill for querying Oracle latest facts with proper source citations and adding new sources to enrich the knowledge base.

## Features

### 📖 Query Mode
Search the Oracle Facts notebook and get answers backed by citations.

**Supported Query Types:**
- Product features and capabilities
- Pricing comparisons
- Strategy and announcements
- Technical specifications
- Competitive analysis

### ➕ Add Source Mode
Contribute new sources to keep the Oracle knowledge base current.

**Supported Source Types:**
- 🌐 **Web URLs** - Blog posts, articles, news
- 📄 **Documents** - PDF, text files, audio
- 📊 **Google Drive** - Docs, Sheets, Slides, PDFs
- 📝 **Raw Text** - Direct text input

## Installation

### Prerequisites
- Claude Code with Skill support
- NotebookLM MCP installed and configured
- NotebookLM authentication via `nlm login`

### Quick Setup

1. **Install NotebookLM MCP** (if not already installed)
   ```bash
   pip install notebooklm-mcp
   ```

2. **Authenticate with NotebookLM**
   ```bash
   nlm login
   ```
   This saves credentials to `~/.notebooklm-mcp-cli/`

3. **Install this skill**
   - Clone this repository or download the skill files
   - Copy to your Claude Code skills folder

4. **Done!** The skill will appear in your Claude Code skill list

## Usage

### Query Examples

**Ask about Oracle products:**
```
"Tell me about Oracle 26ai's AI Vector Search capabilities"
"What are the differences between 23ai and 26ai?"
"How much cheaper is OCI compared to AWS?"
```

### Add Source Examples

**Add a web URL:**
```
"Add this to the Oracle facts notebook: https://example.com/oracle-news"
```

**Upload a document:**
```
[Upload PDF file]
"Add this PDF to the Oracle facts notebook"
```

## How It Works

### Query Mode
1. User asks an Oracle-related question
2. Skill queries the Oracle Facts notebook via NotebookLM MCP
3. Returns answer with source citations in `[1] Source Title` format

### Add Source Mode
1. User provides a source (URL, file, or text)
2. Skill adds it to the Oracle Facts notebook
3. NotebookLM processes and indexes the source

## Requirements

- **Claude Code**: Latest version with skill support
- **NotebookLM MCP**: Installed and authenticated
- **Internet Connection**: For web sources and NotebookLM API

## Notebook Details

- **Name**: Oracle latest facts
- **Sources**: 80+ articles, whitepapers, documentation
- **Coverage**: Oracle 26ai, OCI, multicloud, AI capabilities, pricing, strategy
- **Updated**: Regularly with community contributions

## Using Across Projects

This skill works seamlessly with:
- **codex** - Query Oracle facts in your coding workflows
- **antigravity** - Research Oracle capabilities before proposals
- **claude-code** - General Oracle knowledge management

## Contributing

Help improve the Oracle Facts knowledge base!

### Adding Sources
1. Find relevant Oracle information
2. Share the URL, document, or text with the skill
3. Skill adds it to the shared notebook
4. Your contribution helps others get better answers

## License

MIT License - See LICENSE file for details

## Support

For issues, questions, or contributions, please open an issue or create a pull request.

---

**Made with ❤️ for the Claude Code community**
