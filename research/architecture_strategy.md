# Chimera Architecture Strategy

**Agent Pattern**: Hierarchical FastRender Swarm (Planner → Workers → Judge)  
Why: Parallelism, error recovery, quality control via Judge (SRS 3.1).

**Human-in-the-Loop**: Judge escalates <0.70 confidence or sensitive topics to dashboard.

**Database**: Weaviate (semantic memory) + Redis (queues/cache)  
Why: High-velocity metadata, vector search for RAG.

## Diagram
```mermaid
graph TD
    A[Orchestrator] --> B[Planner]
    B --> C[Redis Tasks]
    C --> D[Workers]
    D --> E[Redis Review]
    E --> F[Judge]
    F -->|Approve| G[Publish]
    F -->|Reject| B
    F -->|Escalate| A[HITL]