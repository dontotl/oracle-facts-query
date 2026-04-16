---
name: oracle-facts-query
description: Query Oracle latest facts with citations from the Oracle Facts notebook, or add new web sources, documents, and Google Drive files to keep it updated. Use this skill whenever the user asks Oracle-related questions, needs current Oracle information, or wants to contribute new Oracle sources to the shared knowledge base.
compatibility: Requires NotebookLM MCP (notebooklm-mcp) with authentication configured
---

# Oracle Facts Query & Source Manager

Manage and query the Oracle latest facts knowledge base with full source attribution. This skill combines query capabilities with source management to maintain an up-to-date, cited repository of Oracle information.

## Overview

This skill provides two complementary functions:

1. **Query Mode**: Search the Oracle Facts notebook and return answers with proper source citations
2. **Add Source Mode**: Contribute new sources (web URLs, documents, Google Drive files, or raw text) to enrich the knowledge base

All responses in Query Mode include source citations in the format `[1] Source Title - Description`, making it easy to trace information back to its origin.

---

## Features

### 1. Query Mode

**What it does**: Answers questions about Oracle products, services, pricing, and strategy using only information from the Oracle Facts notebook.

**When to use**:
- "What's Oracle AI Database 26ai?"
- "How much cheaper is OCI compared to AWS?"
- "What are the latest Oracle GoldenGate features?"
- "Compare Oracle's multicloud offerings"
- Any Oracle-related question where you need cited facts

**Output format**:
\`\`\`
[Answer paragraph with inline citations using numbers]

## Sources
[1] Source Title - Brief description or quote
[2] Another Source Title - Brief description or quote
\`\`\`

---

### 2. Add Source Mode

**What it does**: Adds new sources to the Oracle Facts notebook to keep the knowledge base current and comprehensive.

**Supported source types**:
- **Web URLs**: Any publicly accessible webpage or article
- **Document Files**: PDF, text files, or other supported documents
- **Google Drive**: Google Docs, Sheets, Slides, or PDFs in your Drive
- **Raw Text**: Paste content directly (useful for email excerpts, internal docs, etc.)

**When to use**:
- User provides a URL: "Add this to the Oracle notebook: https://..."
- User uploads a file: "Here's a PDF about Oracle, add it to the facts notebook"
- User shares a Google Drive link: "Share this Google Doc with the notebook"
- User pastes content: "Add this article excerpt to Oracle facts"

---

## How to Use

### Query Mode

The user simply asks an Oracle-related question. You:

1. Extract the notebook ID: `e55f93ec-71d0-4540-bf16-15fcac8d73e6`
2. Call `notebook_query` with the user's question
3. Format the response with source citations:
   - Use the returned citations to build the `## Sources` section
   - Format each source as `[N] Source Title - description`
   - Number citations sequentially `[1]`, `[2]`, etc.

**Example interaction**:

User: "Tell me about Oracle 26ai's pricing advantages"

Response:
\`\`\`
Oracle AI Database 26ai emphasizes integrated AI capabilities at no additional cost. 
Unlike competitors, Oracle includes AI Vector Search, AI for Database Management, and 
other advanced features in the base license [1]. 

Additionally, Oracle Cloud Infrastructure (OCI) offers substantially lower compute costs 
than AWS, with pricing 50% lower for comparable compute resources [2]. This extends 
across the entire infrastructure stack - block storage is 70% cheaper, and networking 
data egress is 80% cheaper than AWS [3].

## Sources
[1] Oracle AI Database 26ai Technical Blog - Advanced features included in base license
[2] OCI Pricing Comparison Study - Compute cost comparison vs AWS
[3] Oracle Cloud Infrastructure Pricing Guide - Storage and networking cost analysis
\`\`\`

---

### Add Source Mode

The user wants to add a new source. Identify the source type and call the appropriate method:

#### Web URL
\`\`\`
User: "Can you add this URL to the Oracle facts notebook? https://example.com/oracle-news"

Response: "Adding that URL to the Oracle Facts notebook..."
[Call source_add with source_type="url" and the URL]
"✓ Added! The notebook will process and index this source shortly."
\`\`\`

#### Local File (PDF, text, audio)
\`\`\`
User: [uploads a PDF file about Oracle]

Response: "Adding this PDF to the Oracle Facts notebook..."
[Call source_add with source_type="file" and file_path]
"✓ Added! Processing your document now."
\`\`\`

#### Google Drive Document
\`\`\`
User: "Add this Google Doc to the Oracle notebook: https://docs.google.com/document/d/..."

Response: "Adding that Google Doc..."
[Extract document_id from URL or use the provided ID]
[Call source_add with source_type="drive", document_id, and doc_type]
"✓ Added! The notebook now has access to this document."
\`\`\`

#### Raw Text
\`\`\`
User: "Add this excerpt to the Oracle facts: [pastes text]"

Response: "Adding that text to the Oracle Facts notebook..."
[Call source_add with source_type="text" and the text content]
"✓ Added! This content is now part of the knowledge base."
\`\`\`

---

## Implementation Details

### Required Tools

- `mcp__notebooklm-mcp__notebook_query` - Query the notebook with a question
- `mcp__notebooklm-mcp__source_add` - Add sources to the notebook

### Notebook Reference

**Notebook ID**: `e55f93ec-71d0-4540-bf16-15fcac8d73e6`  
**Name**: Oracle latest facts  
**Current Sources**: 82+ (as of April 2026)  
**Coverage**: Oracle 26ai, OCI pricing, multicloud strategy, GoldenGate, competitive analysis, AI capabilities

### Source Citation Format

Always use this format for sources:
\`\`\`
[N] Source Title - Brief description/context
\`\`\`

Numbers should be sequential starting from 1. If the API returns citations with numbers, use those directly. If not, assign numbers based on the order sources appear in the response.

### Error Handling

**Query returns no results**:
\`\`\`
I searched the Oracle Facts notebook but didn't find specific information 
about [topic]. The notebook currently focuses on Oracle 26ai, OCI services, 
and recent competitive strategy. If you have sources about this topic, 
we can add them!
\`\`\`

**Source add fails**:
\`\`\`
I had trouble adding that source. Please verify:
- The URL is accessible and public
- The file format is supported (PDF, text, audio)
- The Google Drive document is accessible to your account

Try again or upload a different source.
\`\`\`

---

## Best Practices

### For Query Mode

- **Be precise with citations**: Always trace quoted facts back to sources
- **Combine multiple sources**: If multiple sources cover a topic, cite all relevant ones
- **Indicate confidence**: If information seems incomplete, suggest the user add more sources
- **Stay in scope**: Only answer questions that relate to Oracle facts in the notebook

### For Add Source Mode

- **Provide context**: When adding a source, briefly explain why it's relevant
- **Check for duplicates**: Ask if the source seems similar to existing content in the notebook
- **Verify accessibility**: Confirm URLs are public and files are in supported formats
- **Encourage updates**: If a source is outdated, suggest finding a newer version

---

## Example Workflows

### Workflow 1: Answer + Add Followup Source
\`\`\`
User: "What's the latest on Oracle's cloud pricing?"
You: [Query notebook, return answer with sources]
User: "Here's an updated pricing page I found: https://..."
You: [Add URL to notebook]
"Great! I've added that to keep our Oracle facts current."
\`\`\`

### Workflow 2: Contribute New Research
\`\`\`
User: "I just read a great article about Oracle 26ai. Here it is: [file upload]"
You: "Adding this to the Oracle Facts notebook..."
[Add file source]
"✓ Added! This is now part of our Oracle knowledge base, available for queries."
\`\`\`

### Workflow 3: Multi-Source Query
\`\`\`
User: "Compare OCI and AWS costs across regions"
You: [Query notebook for pricing comparisons]
[Return answer citing multiple regional pricing sources]
"The notebook has pricing data for X regions. Want me to add more regional comparisons?"
\`\`\`

---

## GitHub Deployment Notes

When deploying to GitHub:

1. **Authentication**: Users must have NotebookLM MCP configured locally
   - Requires `nlm login` to be run beforehand
   - Credentials stored in `~/.notebooklm-mcp-cli/`

2. **Notebook ID**: Hardcoded to `e55f93ec-71d0-4540-bf16-15fcac8d73e6`
   - This is the shared "Oracle latest facts" notebook
   - Can be modified in deployment for custom notebooks

3. **Sharing Across Projects**: 
   - Works seamlessly in codex, antigravity, and other projects
   - Each invocation enriches the same shared knowledge base
   - All contributors see accumulated sources

4. **README for Users**: Include installation notes explaining:
   - NotebookLM MCP must be installed and authenticated
   - How to run `nlm login` if not already done
   - That the skill maintains a shared Oracle knowledge base
   - How to contribute sources via the Add Source mode
