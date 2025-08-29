# Python Monorepo Example

A Python monorepo example demonstrating LangGraph agents with shared packages, similar to the JavaScript version in `../isaac-js-graph`.

## Structure

```
python-monorepo-example/
├── libs/
│   ├── shared/                 # Real package with pyproject.toml
│   │   ├── pyproject.toml
│   │   └── src/shared/
│   │       ├── __init__.py
│   │       └── utils.py        # get_dummy_message(), get_shared_timestamp()
│   └── common/                 # Faux package (no pyproject.toml)
│       ├── __init__.py
│       └── helpers.py          # get_common_prefix()
├── apps/
│   ├── agent1/
│   │   ├── langgraph.json      # deps: ["../../libs/shared", "../../libs/common"]
│   │   ├── pyproject.toml
│   │   └── src/agent1/
│   │       ├── __init__.py
│   │       ├── state.py
│   │       └── graph.py        # Simple single-node LangGraph
│   └── agent2/
│       ├── langgraph.json      # deps: ["../../libs/shared", "../../libs/common"]
│       ├── pyproject.toml
│       └── src/agent2/
│           ├── __init__.py
│           ├── state.py
│           └── graph.py        # Simple single-node LangGraph
├── pyproject.toml              # Root project with shared dependencies
├── .gitignore
└── README.md
```

## Key Features

### Shared Packages
- **`libs/shared/`**: Real Python package with `pyproject.toml`, containing utility functions
- **`libs/common/`**: Faux package (directory with Python files, no `pyproject.toml`)

### Agent Configuration
- Each agent has `langgraph.json` with `"dependencies": ["../../libs/shared", "../../libs/common"]`
- This mirrors the JS monorepo pattern where shared packages are referenced via configuration rather than individual package dependencies
- Each agent has its own `pyproject.toml` for LangGraph-specific dependencies

### LangGraph Implementation
- Simple single-node graphs that demonstrate importing from both shared packages
- Each agent outputs: `"[COMMON] Agent1/2 says: Hello from shared library! (timestamp)"`
- Follows the same pattern as the JS example but using Python/LangGraph

## Dependencies

The root `pyproject.toml` contains shared dependencies:
- `langgraph>=0.6.0,<0.7.0`
- `langchain-core>=0.2.14`

Each agent's `langgraph.json` specifies the shared package dependencies using relative paths, allowing the LangGraph CLI to properly resolve the imports.

## Usage

Each agent can be run independently using the LangGraph CLI, and both will have access to the shared utility functions via the dependency configuration.