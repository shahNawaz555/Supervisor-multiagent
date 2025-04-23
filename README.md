Multi-Agent Workflow with LangGraph and LangChain
This project implements a multi-agent workflow using LangGraph and LangChain, designed to handle tasks like coding and research through specialized agents (Researcher and Coder) managed by a supervisor. The system leverages a stateful graph for dynamic task routing, persistence for interruption handling, and robust error management. It is optimized for modularity, scalability, and debugging with LangSmith integration.
Features

Agent Specialization:
Researcher: Uses Tavily Search to gather information from the web.
Coder: Executes Python code safely using a REPL tool.


Supervisor:
Dynamically routes tasks to the appropriate agent or signals completion (FINISH).
Uses structured output for reliable decision-making.


State Management:
Explicit state schema with annotated message sequences and private agent states.
Persistence via MemorySaver for resuming workflows.


Error Handling:
Safe code execution with try-catch blocks.
API key validation and fallback mechanisms.


Debugging:
Integrated with LangSmith for tracing and visualization.
Graph visualization support using Mermaid diagrams.


Modularity:
Reusable agent and tool creation functions.
Separated configuration for easy extension.



Requirements

Python 3.8+

Dependencies (install via pip):
pip install langchain langchain-openai langgraph langchain-community python-dotenv pydantic


API Keys (set in .env):

OpenAI API (OPENAI_API_KEY) for GPT-4o.
Tavily API (TAVILY_API_KEY) for search.
LangChain API (LANGCHAIN_API_KEY) for tracing.


Environment Variables:
export LANGCHAIN_TRACING_V2="true"
export LANGCHAIN_ENDPOINT="https://api.smith.langchain.com"



Installation

Clone the repository:
git clone https://github.com/your-username/multi-agent-workflow.git
cd multi-agent-workflow


Install dependencies:
pip install -r requirements.txt


Set up environment variables in a .env file:
OPENAI_API_KEY=your-openai-api-key
TAVILY_API_KEY=your-tavily-api-key
LANGCHAIN_API_KEY=your-langchain-api-key


Load environment variables:
from dotenv import load_dotenv
load_dotenv()



Usage
Run the main script to execute tasks like coding or research:
python main.py

Example Inputs
from graph import graph

# Example 1: Coding task
for s in graph.stream(
    {
        "messages": [
            HumanMessage(content="Code hello world and print it to the terminal")
        ]
    },
    {"recursion_limit": 100},
):
    if "__end__" not in s:
        print(s)
        print("----")

# Example 2: Research task
for s in graph.stream(
    {
        "messages": [
            HumanMessage(content="Write a brief research report on pikas.")
        ]
    },
    {"recursion_limit": 100},
):
    if "__end__" not in s:
        print(s)
        print("----")

Output

Console Output: Displays the workflow steps (supervisor decisions, agent outputs) and final results.
Trace Logs: Available via LangSmith for debugging.
Graph Visualization: Optional Mermaid diagram output for workflow inspection.
