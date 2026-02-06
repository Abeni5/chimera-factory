Agent Skills Directory
Skills are runtime capabilities for Chimera Workers. Each skill:

Has strict Pydantic I/O contracts (specs/technical.md)
Called via MCP Tools (no direct APIs)
Stateless, async, idempotent
3 Critical Skills (TDD-ready):

trend_fetcher/ - Fetch platform trends + relevance score
content_generator/ - Multimodal content (text/image/video) w/ persona lock
social_publisher/ - Platform-agnostic posting w/ AI disclosure
EOF