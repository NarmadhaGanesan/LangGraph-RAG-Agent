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
├── notebooks/
│   └── langgraph_chatbot.ipynb    # Main implementation notebook
│
├── requirements.txt               # Project dependencies
├── README.md                      # This file
└── graph.png                      # Generated graph visualization
```

## 🔧 Implementation Details

### Core Components

#### 1. **ChatBot with Memory**
```python
class State(TypedDict):
    '''State for our Chatbot - holds conversation history'''
    messages: Annotated[list[BaseMessage], add_messages]
```

#### 2. **Two-Node Agent System**
```python
class AgentState(TypedDict):
    '''State for our two-node agent'''
    messages: Annotated[list[BaseMessage], add_messages]
```

#### 3. **Tool Definitions**
```python
@tool
def calculator(expression: str) -> str:
    '''Calculate mathematical expressions'''
    return f"The result of {expression} is {eval(expression)}"

search_tool = DuckDuckGoSearchRun()
```

### Graph Workflow

1. **User Input** → Chatbot Node
2. **Chatbot Analysis** → Decide to use tools or respond directly
3. **Tool Execution** (if needed) → Process calculations or web search
4. **Response Generation** → Return final answer to user

## 🚀 Usage Examples

### Basic Chatbot
```python
# Initialize the graph
graph = build_basic_chatbot()

# Test conversation
test_chatbot("Hello, my name is Narmadha")
test_chatbot("Do you remember my name?")
```

### Advanced Agent with Tools
```python
# Initialize the agent with tools
app = build_agent_with_tools()

# Interactive chat session
chat_with_agent("What's 25 * 4 + 17?", thread_id="thread-1")
chat_with_agent("Search for recent news about AI", thread_id="thread-1")
```

## 💻 Code Examples

### 1. **Running the Chatbot**
```python
def test_chatbot(message: str):
    '''Helper function to test our chatbot'''
    print(f"\n👤 User: {message}")
    initial_state = {"messages": [HumanMessage(content=message)]}
    result = graph.invoke(initial_state)
    ai_response = result['messages'][-1].content
    print(f"🤖 Assistant: {ai_response}")
    return result
```

### 2. **Agent with Memory**
```python
def chat_with_memory(message: str, thread_id: str):
    '''Chat function with memory'''
    config = {'configurable': {'thread_id': thread_id}}
    initial_state = {"messages": [HumanMessage(content=message)]}
    result = graph_with_memory.invoke(initial_state, config)
    return result
```

## 📊 Graph Visualization

The system generates a visual representation of the workflow:

```
START → Chatbot Node → Conditional Routing
                    ↘
                    [Has tool calls?] → Yes → Tool Node → Chatbot Node
                    ↗
                    No → END
```

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

## 🧪 Testing Scenarios

```python
# Test cases demonstrating different capabilities
test_cases = [
    "Hello, my name is Narmadha",
    "What's 15% of 240?",
    "What's the latest news about artificial intelligence?",
    "Can you tell me more about that?"
]

for test_message in test_cases:
    chat_with_agent(test_message, thread_id="test-thread")
```

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

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [LangChain](https://github.com/langchain-ai/langchain) for the framework
- [OpenAI](https://openai.com/) for GPT models
- [LangGraph](https://github.com/langchain-ai/langgraph) for graph-based workflows

## 📞 Support

For issues, questions, or contributions:
1. Open an issue in the GitHub repository
2. Check existing documentation
3. Review the LangChain community forums

---

**Note**: This is a demonstration project. For production use, consider:
- Adding proper error handling
- Implementing rate limiting
- Adding authentication
- Setting up monitoring and logging
- Following security best practices
