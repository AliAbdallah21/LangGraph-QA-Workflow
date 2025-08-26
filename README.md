# LangGraph Q&A Workflow: Intelligent Context-Aware Question Answering

A comprehensive tutorial demonstrating how to build intelligent question-answering systems using LangGraph with conditional context handling and OpenAI GPT integration.

## Links

- **Author**: Ali Abdallah
- **Email**: Aliabdalla2110@gmail.com
- **GitHub**: [AliAbdallah21](https://github.com/AliAbdallah21/LangGraph-QA-Workflow)
- **LinkedIn**: [Ali Abdallah](https://linkedin.com/in/ali-abdallah-b5ba792b6/)

## Overview

This project demonstrates how to create a sophisticated Q&A workflow using LangGraph that intelligently determines whether questions are relevant to a specific domain (the guided project) and provides contextual responses accordingly. The system seamlessly integrates OpenAI's GPT-3.5 model through LangChain for natural language processing.

## What You'll Learn

### Core Concepts
- **Stateful Q&A Design**: Building question-answering systems that maintain context
- **Input Validation**: Implementing robust question validation and preprocessing
- **Conditional Context**: Creating smart context detection for domain-specific queries
- **LLM Integration**: Seamlessly incorporating OpenAI models into workflows
- **Error Handling**: Building resilient systems with graceful fallback responses

### Technical Skills
- LangGraph workflow construction and state management
- OpenAI API integration through LangChain
- TypedDict state structures for type safety
- Conditional routing based on content analysis
- Production-ready error handling patterns

## Architecture

The Q&A workflow follows a linear processing pattern with intelligent context switching:

```
[InputValidation] → [ContextProvider] → [LLM_QA] → END
```

### Workflow Components

1. **Input Validation Node**
   - Validates user input for completeness and format
   - Handles empty or invalid questions gracefully
   - Ensures downstream nodes receive clean input

2. **Context Provider Node**
   - Analyzes questions for project relevance
   - Provides detailed context for LangGraph-related queries
   - Returns null context for unrelated questions

3. **LLM Q&A Node**
   - Processes questions using OpenAI GPT-3.5
   - Generates informed responses when context is available
   - Provides clear messaging when context is insufficient

## Getting Started

### Prerequisites

- Python 3.8+
- OpenAI API Key
- Google Colab (recommended) or local Jupyter environment

### Installation

1. Clone the repository:
```bash
git clone https://github.com/AliAbdallah21/LangGraph-QA-Workflow.git
cd LangGraph-QA-Workflow
```

2. Install required packages:
```bash
pip install langgraph langchain-openai
```

3. Set up your OpenAI API key:
   - For Google Colab: Add `OPENAI_API_KEY` to your secrets
   - For local development: Set as environment variable

### Running the Tutorial

Open `LangGraph_QA_Workflow.ipynb` and execute the cells sequentially. The notebook includes detailed explanations and working examples.

## State Management

The system uses a clean TypedDict structure for state management:

```python
class QAState(TypedDict):
    question: Optional[str]
    context: Optional[str] 
    answer: Optional[str]
```

This structure provides:
- Type safety for all state transitions
- Clear data flow between nodes
- Optional fields for flexible processing

## Key Features

### Intelligent Context Detection
The system automatically detects whether questions relate to the guided project:

```python
def context_provider_node(state):
    question = state.get("question", "").lower()
    if "langgraph" in question or "guided project" in question:
        context = (
            "This guided project is about using LangGraph, a Python library to design state-based workflows. "
            "LangGraph simplifies building complex applications by connecting modular nodes with conditional edges."
        )
        return {"context": context}
    return {"context": None}
```

### Robust Error Handling
Multiple layers of validation ensure system reliability:
- Input validation prevents empty questions
- Context checking handles domain relevance
- LLM integration includes exception handling

### Seamless LLM Integration
OpenAI GPT-3.5 integration through LangChain:

```python
def llm_qa_node(state):
    question = state.get("question", "")
    context = state.get("context", None)
    
    if not context:
        return {"answer": "I don't have enough context to answer your question."}
    
    prompt = f"Context: {context}\nQuestion: {question}\nAnswer the question based on the provided context."
    response = llm.invoke(prompt)
    return {"answer": response.content.strip()}
```

## Example Usage

### Project-Related Questions
```python
# Input: "What is LangGraph?"
# Output: Detailed explanation based on provided context
```

### Unrelated Questions
```python
# Input: "What is the weather today?"
# Output: "I don't have enough context to answer your question."
```

## Workflow Execution Examples

The notebook demonstrates various scenarios:

1. **Valid project questions**: Receive contextual, informed responses
2. **Invalid/empty questions**: Handled with appropriate error messages
3. **Off-topic questions**: Clear communication about scope limitations

## Customization Options

### Extending Context Detection
Add new keywords or topics:

```python
if "langgraph" in question or "guided project" in question or "your_keyword" in question:
    # Provide relevant context
```

### Enhanced Context Provision
Expand the context database:

```python
context_database = {
    "langgraph": "LangGraph context...",
    "python": "Python-specific context...",
    "workflow": "Workflow-specific context..."
}
```

### Alternative LLM Models
Switch between different models:

```python
llm = ChatOpenAI(model='gpt-4', openai_api_key=api_key)
```

## Best Practices Demonstrated

- **Clean State Management**: Using TypedDict for structured data flow
- **Error Boundaries**: Proper exception handling at each processing stage
- **Context Awareness**: Smart routing based on content analysis
- **User Experience**: Clear messaging for both valid and invalid scenarios
- **Modularity**: Each node has a single, well-defined responsibility

## Technical Implementation Details

### Node Design Pattern
Each node follows a consistent pattern:
- Extract relevant data from state
- Process the data
- Return updated state dictionary
- Handle edge cases gracefully

### State Transitions
The workflow maintains state integrity through:
- Immutable state updates
- Clear data flow between nodes
- Optional field handling

### Integration Points
The system demonstrates integration with:
- OpenAI API through LangChain
- Google Colab secrets management
- LangGraph workflow engine

## Future Enhancements

Potential extensions include:
- Multi-domain context handling
- Conversation history tracking
- Advanced NLP for better context detection
- Integration with vector databases
- Real-time learning capabilities

## Troubleshooting

Common issues and solutions:

1. **API Key Issues**: Ensure OPENAI_API_KEY is properly set
2. **Package Conflicts**: Use fresh virtual environment
3. **Model Timeouts**: Implement retry logic for API calls
4. **Context Mismatches**: Review keyword detection logic

## Contributing

Contributions are welcome! Areas for improvement:

1. Enhanced context detection algorithms
2. Additional domain-specific contexts
3. Performance optimizations
4. Extended error handling
5. Documentation improvements

## License

This project is open source and available under the MIT License.

## Support

For questions or support:

- **Email**: Aliabdalla2110@gmail.com
- **LinkedIn**: [Connect with me](https://linkedin.com/in/ali-abdallah-b5ba792b6/)
- **Issues**: [GitHub Issues](https://github.com/AliAbdallah21/LangGraph-QA-Workflow/issues)

## Acknowledgments

This tutorial builds upon the foundations of LangGraph and demonstrates practical applications of state-based workflow design in AI systems. Special thanks to the LangChain and OpenAI communities for their excellent tools and documentation.

---

**Ready to build intelligent Q&A systems?** Clone the repository and start experimenting with context-aware workflows!
