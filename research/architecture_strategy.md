# Chimera Domain Architecture Strategy

## Agent Pattern: Hierarchical FastRender Swarm
**Choice**: Planner → Task Queue → Worker Swarm → Review Queue → Judge  
**Why**: 
- Parallelism: 50+ Workers for high-velocity tasks (comments, trends)
- Quality: Judge enforces persona consistency + confidence scoring
- Self-healing: OCC prevents race conditions, rejects invalid state
- Scale: Stateless Workers auto-scale to 1,000+ agents (SRS NFR 3.0)

## Human-in-the-Loop Placement
**Where**: Judge layer (post-Worker, pre-publish)  
**Logic** (SRS NFR 1.1):
- >0.90 confidence → Auto-approve
- 0.70-0.90 → Async HITL queue (Dashboard)
- <0.70 or sensitive (politics/health/finance) → Mandatory human review
**Why**: Balances velocity + safety without blocking high-confidence flow

## Database Strategy
**Primary**: Weaviate (vector DB) + Redis (cache/queues)  
**Why** (high-velocity video metadata):
- **Weaviate**: Semantic RAG memory (persona evolution, long-term recall) + hybrid search
- **Redis**: Episodic cache (1hr window) + Task/Review queues (Celery/BullMQ)
- **PostgreSQL**: Tenant configs + operational logs (low-velocity)
- **NoSQL over SQL**: 10x faster writes for social bursts, vector-native for RAG

## System Diagram
```mermaid
graph TD
    A[Human Orchestrator<br/>Dashboard] -->|Campaign Goals| B[Planner Agent]
    B -->|DAG Tasks| C[Redis Task Queue]
    C --> D[Worker Swarm<br/>Stateless Containers]
    D -->|Results| E[Redis Review Queue]
    E --> F[Judge Agent<br/>OCC + Confidence]
    F -->|Approve >0.90| G[GlobalState<br/>Publish via MCP]
    F -->|Reject| B
    F -->|0.70-0.90| H[HITL Queue]
    F -->|Low/Sensitive| A
    subgraph "MCP Layer (External)"
        I[mcp-server-twitter]
        J[mcp-server-weaviate]
        K[mcp-server-coinbase]
        L[mcp-server-runway]
    end
    D -.-> I & J & K & L
    style A fill:#ff9999
    style F fill:#ffcc99
EOF