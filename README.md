# LangGraph Chatbot with Tool Integration

A comprehensive conversational AI system built with LangGraph that combines language models, web search, and calculation tools in an interactive agent.

## 🚀 Features

- **Conversational AI Agent**: Multi-turn chatbot with memory and context retention
- **Tool Integration**: 
  - Web search using DuckDuckGo
  - Mathematical calculations
- **Graph-Based Architecture**: Visual workflow using LangGraph
- **State Management**: Conversation history and tool usage tracking
- **Memory System**: Persistent chat memory across sessions

## 📋 Prerequisites

- Python 3.8+
- OpenAI API key
- LangSmith API key (optional, for tracing)

## 🛠️ Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd langgraph-chatbot
```

2. Install required packages:
```bash
pip install langchain langchain-openai langchain-community langchain-core langgraph duckduckgo-search
```

3. Set up environment variables:
```python
import os
os.environ["OPENAI_API_KEY"] = "your-openai-api-key"
os.environ["LANGSMITH_TRACING"] = "true"  # Optional
os.environ["LANGSMITH_API_KEY"] = "your-langsmith-key"  # Optional
os.environ["LANGSMITH_PROJECT"] = "langgraph-rag"  # Optional
```

## 🏗️ Architecture

The system is built using LangGraph with the following components:

### 1. **State Management**
- `AgentState`: Tracks conversation history with annotated message lists
- Memory persistence using `MemorySaver`

### 2. **Graph Nodes**
- **Chatbot Node**: Processes messages and decides when to use tools
- **Tool Node**: Executes calculator and web search tools
- **Routing Logic**: Conditionally routes between chatbot responses and tool usage

### 3. **Tool System**
- `calculator`: Evaluates mathematical expressions
- `duckduckgo_search`: Performs web searches for real-time information

## 📁 Project Structure

```
langgraph-chatbot/
│
├── langgraph_chatbot.ipynb    # Main implementation notebook
├── requirements.txt               # Project dependencies
├── README.md                      # This file
```



### Graph Workflow

1. **User Input** → Chatbot Node
2. **Chatbot Analysis** → Decide to use tools or respond directly
3. **Tool Execution** (if needed) → Process calculations or web search
4. **Response Generation** → Return final answer to user


## 🔍 Tool Usage Guidelines

The agent intelligently decides when to use tools based on:

### **Use Web Search When:**
- Asked about current events or news
- Need specific facts or real-time data
- Querying weather, stock prices, etc.

### **Use Calculator When:**
- Performing mathematical calculations
- Solving math problems

### **Direct Response When:**
- General knowledge questions
- Conversational queries


## 📈 Performance Features

- **Context Retention**: Remembers user information across sessions
- **Tool Chaining**: Can use multiple tools in sequence
- **Error Handling**: Graceful handling of tool failures
- **Conversation Flow**: Maintains natural dialogue flow

## 🛡️ Error Handling

The system includes robust error handling for:
- Invalid mathematical expressions
- Network failures during web search
- Empty or irrelevant search results
- Memory retrieval failures

## 🔮 Future Enhancements

1. **Additional Tools**:
   - Database querying
   - File system operations
   - API integrations

2. **Advanced Features**:
   - Multi-modal capabilities
   - Voice interaction
   - Custom tool development

3. **Performance Improvements**:
   - Async tool execution
   - Caching mechanisms
   - Load balancing

## 📚 Dependencies

```txt
langchain>=0.3.0
langchain-openai>=0.3.0
langchain-community>=0.3.0
langchain-core>=0.3.0
langgraph>=0.0.0
duckduckgo-search>=8.0.0
openai>=1.0.0
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request


## 🙏 Acknowledgments

- [LangChain](https://github.com/langchain-ai/langchain) for the framework
- [OpenAI](https://openai.com/) for GPT models
- [LangGraph](https://github.com/langchain-ai/langgraph) for graph-based workflows

---

