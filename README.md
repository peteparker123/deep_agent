# Deep Agents Research Report Generator

A research agent powered by Google Gemini that conducts internet searches and automatically saves reports as markdown files using deep agents.

## Features

- **Autonomous Research**: Agent uses DuckDuckGo search to gather information
- **Automatic File Saving**: Uses `write_file` tool to save reports to disk
- **Rate-Limited**: Capped at 2 searches per query to reduce API usage
- **Real Filesystem Access**: FilesystemBackend saves files to the current directory

## Setup

```bash
pip install -qU deepagents langchain-google-genai langchain_community ddgs
```

## Configuration

Set your Gemini API key in the code:
```python
api_key="your-gemini-api-key"
```

Or use environment variable:
```python
api_key=os.environ["GOOGLE_API_KEY"]
```

## Usage

Run the notebook. The agent will:
1. Receive a research question
2. Search the web (max 2 queries)
3. Synthesize findings into a markdown report
4. Save to `report.md` in the current directory

```python
# The agent is asked to research LangGraph
agent.stream({
    "messages": [{
        "role": "user",
        "content": "What is LangGraph? Save your final report to report.md."
    }]
})
```

## Output

- **report.md** — Generated markdown report saved by the agent

## Key Components

| Component | Purpose |
|-----------|---------|
| `ChatGoogleGenerativeAI` | LLM model (Gemini 3.5 Flash) |
| `DuckDuckGoSearchResults` | Web search tool |
| `FilesystemBackend` | Enables file writing on disk |
| `create_deep_agent()` | Creates the research agent with tools |

## Customization

**Change the research question:**
```python
"content": "Your research question here?"
```

**Adjust search limit:**
```python
max_results: int = 2,  # Change this value
```

**Change output filename:**
```python
"write_file tool to save... to a file named `your_filename.md`"
```

## Notes

- Free tier Gemini API has a 20 requests/day limit
- Each research run typically uses 5-10 API calls
- For higher limits, upgrade to a paid Gemini plan
- The agent's available tools include: `internet_search`, `write_file`, `read_file`, `ls`, `edit_file`, `glob`, `grep`
- The problem i faced was api exhausted error 
