# LangChain Notebook Tutorial

This notebook demonstrates core concepts of LangChain for building LLM-powered applications using OpenAI's GPT-4o model via OpenRouter API.

## Overview

The notebook covers the following LangChain components and patterns:

1. **ChatOpenAI** - ChatOpenAI model from LangChain
2. **Basic** - Making simple LLM queries and processing responses
3. **Prompt Templates** - Creating structured prompts with variables for dynamic input
4. **Runnables** - Using LangChain's Runnable for composing LLM chains
5. **Chain Creation** - Building chains using the pipe operator (`|`) for sequential processing
6. **Output Parsing** - Extracting structured string output from LLM responses

## Prerequisites

- Python 3.7+
- OpenRouter API key (set in `.env` file as `OPENAI_API_KEY`)
- Required packages (see [requirements.txt](requirements.txt))

## Installation

```bash
pip install -r requirements.txt
```

Create a `.env` file in the project directory with your OpenRouter API credentials:

```
OPENAI_API_KEY=your_openrouter_api_key
```

## Notebook Sections

### 1. Setup
- Loads environment variables
- Initializes ChatOpenAI client with GPT-4o model
- Configures OpenRouter API endpoint

### 2. Basic Queries
- Simple question-answering (e.g., "What is India's national flower?")
- Demonstrates how to invoke the model and extract content

### 3. System Prompts
- Shows how to use system and user prompts together
- Example: System role as a Python developer, user query for function definition

### 4. Prompt Templates
- Creates reusable prompt templates with variable placeholders
- Demonstrates formatting messages with different parameter 
- Example: Language translation templates with `{language}` and `{query}` variables

### 5. Runnable Interface
- Uses the Runnable pattern for more flexible invocation
- Shows the difference between manual formatting and runnable chains

### 6. Chaining
- Demonstrates pipe operator (`|`) for chaining components
- Creates a pipeline: `prompts | lm`
- Makes code more readable and maintainable

### 7. Output Parsing
- Uses `StrOutputParser` to extract plain string content
- Creates a complete chain: `prompts | lm | out`
- Strips unnecessary metadata from LLM responses

## Key Examples

### Basic Query
```python
lm = ChatOpenAI(model="openai/gpt-4o", base_url="https://openrouter.ai/api/v1")
ans = lm.invoke("what is India's national flower")
print(ans.content)
```

### Prompt Template with Chaining
```python
prompts = ChatPromptTemplate.from_messages([
    {"role":"system","content":"translate given query into {language}"},
    {"role":"user","content":"{query}"}
])

chain = prompts | lm | StrOutputParser()
result = chain.invoke({"language": "hindi", "query": "I am a girl"})
print(result) 
```

## Outcomes

- How to set up and configure LangChain with OpenAI models
- How to create and use prompt templates for dynamic prompts
- How to compose LLM operations into reusable chains
- How to parse and format LLM outputs
- Best practices for structuring LLM applications

## Files

- `lang.ipynb` - Main tutorial notebook
- `requirements.txt` - Python dependencies
- `readme.md` - This documentation file

## References

- [LangChain Documentation](https://python.langchain.com/)
- [OpenRouter API](https://openrouter.ai/)
- [OpenAI GPT-4o Model](https://openai.com/gpt-4)

## Notes

- The notebook uses OpenRouter API for accessing OpenAI models
- Max tokens is set to 500 for response limits
- All examples for flexibility
- The pipe operator (`|`) is the recommended way to chain LangChain components

## Author

Created as a learning resource for LangChain fundamentals.
