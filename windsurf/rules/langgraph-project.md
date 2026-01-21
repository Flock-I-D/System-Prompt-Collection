# LangGraph Project Rules

## 1. State Management

### 1.1. State Definition
- **Rule:** Use `TypedDict` with type annotations
- **Reducers:** `operator.add` for lists, default overwrite for single values
- **Separation:** Isolate `messages`, `artifacts`, and orchestration metadata

### 1.2. Memory Management
- **Rule:** Prune messages to 10-20 recent entries, summarize older content
- **Persistence:** Use `SqliteSaver` with unique `thread_id` for concurrent executions

## 2. Graph Architecture

### 2.1. Node Design
- **Rule:** Single responsibility per node (planning, execution, validation, coordination)
- **Routing:** Use `add_conditional_edges` for orchestration decisions, static edges only for guaranteed transitions
- **Termination:** All paths must reach `END`, implement explicit termination conditions
- **Limits:** Set `recursion_limit` based on complexity (50-150 simple, 200+ complex)

## 3. Multi-Agent Coordination

### 3.1. Lead-Subagent Pattern
- **Rule:** Lead agent orchestrates only, subagents execute specialized tasks without decision authority
- **Decomposition:** Break tasks into independent subtasks with clear boundaries
- **Concurrency:** Limit parallel subagents to 3-5 to prevent resource exhaustion
- **Aggregation:** Lead agent consolidates results, implements conflict resolution

## 4. Data Handling

### 4.1. Serialization
- **Rule:** Use `.model_dump_json()` for Pydantic models in messages, store originals in `artifacts`
- **Metadata:** Include only orchestration-relevant data in message history
- **Compression:** Summarize non-essential information between agents

## 5. Tools

### 5.1. Integration
- **Rule:** Use `.bind_tools()` with validated Pydantic schemas
- **Execution:** Use `ToolNode` with try-catch and retry logic
- **Validation:** Validate outputs before state updates, implement fallback strategies

## 6. Production

### 6.1. Configuration
- **Rule:** Externalize all parameters (models, keys, timeouts, limits)
- **Singleton:** Compile graphs once at startup, use dependency injection
- **Fault Tolerance:** Circuit breakers for external dependencies, exponential backoff
- **Thread Safety:** Unique `thread_id` per execution context

## 7. Advanced Patterns

### 7.1. Message Types
- **SystemMessage:** Orchestration instructions and roles
- **HumanMessage:** External inputs and tasks
- **AIMessage:** Agent outputs and responses

### 7.2. Human-in-Loop
- **Rule:** Use `interrupt_before` for critical decision points

### 7.3. Streaming
- **Rule:** Use `astream_events()` for monitoring, implement event filtering for production

### 7.4. Metrics
- **Rule:** Track task decomposition success, subagent execution times, result aggregation accuracy, orchestration efficiency

## 8. Observability

### 8.1. Monitoring
- **Rule:** Log orchestration decisions with correlation IDs
- **Performance:** Track overhead vs single-agent baselines
- **Quality:** Automated checks comparing multi-agent vs single-agent outputs