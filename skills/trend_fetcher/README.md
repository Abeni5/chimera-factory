Skill: trend_fetcher
Purpose: Fetch real-time trends for Planner (e.g. Twitter, TikTok via MCP)

Input Contract (Pydantic)
class TrendInput(BaseModel):
    persona_id: str          # "chimera.eth.fashion"
    niche: str              # "summer.ethiopia"
    platforms: List[str]    # ["twitter", "tiktok"]
    max_results: int = 10
Output Contract
class TrendOutput(BaseModel):
    trends: List[TrendData]
    relevance_scores: Dict[str, float]  # 0.0-1.0 per trend
    timestamp: datetime

class TrendData(BaseModel):
    keyword: str
    volume: int
    sentiment: float  # -1 to +1
    platform: str
Failing Test: tests/test_trend_fetcher.py
EOF