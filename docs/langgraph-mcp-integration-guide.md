# LangGraph와 MCP 서버 연동 가이드

## 개요

이 문서는 LangGraph에서 MCP(Model Context Protocol) 서버를 연동하는 방법을 설명합니다. MCP는 대규모 언어 모델(LLM)이 외부 데이터 소스와 도구에 접근할 수 있게 해주는 표준화된 프로토콜입니다.

## MCP란 무엇인가?

MCP(Model Context Protocol)는 Anthropic에서 개발한 오픈 프로토콜로, LLM 애플리케이션과 외부 데이터 소스 및 도구 간의 원활한 통합을 가능하게 합니다. MCP는 AI 애플리케이션을 위한 표준화된 인터페이스로 작동하여, 다양한 데이터 소스와 도구를 쉽게 연결할 수 있게 해줍니다.

```mermaid
graph TD
    A[LangGraph 애플리케이션] -->|MCP 클라이언트| B[MCP 프로토콜]
    B --> C[MCP 서버 1: Redis]
    B --> D[MCP 서버 2: PostgreSQL]
    B --> E[MCP 서버 3: 커스텀 도구]
```

## 필요한 패키지 설치

LangGraph에서 MCP 서버를 연동하기 위해서는 `langchain-mcp-adapters` 패키지가 필요합니다:

```bash
pip install langchain-mcp-adapters
```

## MCP 서버 연동 방법

### 1. 단일 MCP 서버 연동

아래는 단일 MCP 서버를 LangGraph와 연동하는 기본적인 예제입니다:

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
from langgraph.prebuilt import create_react_agent
from langchain_openai import ChatOpenAI
import asyncio

async def run_agent():
    # MCP 서버 연결 설정
    async with MultiServerMCPClient(
        {
            "postgres": {
                "command": "node",
                "args": ["/path/to/src/postgres/index.js", "postgresql://user:password@localhost:5432/dbname"],
                "transport": "stdio",
            }
        }
    ) as client:
        # LLM 모델 설정
        model = ChatOpenAI(model="gpt-4")
        
        # 에이전트 생성
        agent = create_react_agent(model, client.get_tools())
        
        # 에이전트 실행
        response = await agent.ainvoke({"messages": "users 테이블의 모든 레코드를 가져와줘"})
        return response

# 비동기 함수 실행
result = asyncio.run(run_agent())
print(result)
```

### 2. 여러 MCP 서버 연동

여러 MCP 서버를 동시에 연동하는 방법입니다:

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
from langgraph.prebuilt import create_react_agent
from langchain_openai import ChatOpenAI
import asyncio

async def run_multi_servers():
    # 여러 MCP 서버 연결 설정
    async with MultiServerMCPClient(
        {
            "postgres": {
                "command": "node",
                "args": ["/path/to/src/postgres/index.js", "postgresql://user:password@localhost:5432/dbname"],
                "transport": "stdio",
            },
            "redis": {
                "command": "node",
                "args": ["/path/to/src/redis/src/index.js", "redis://localhost:6379"],
                "transport": "stdio",
            }
        }
    ) as client:
        # LLM 모델 설정
        model = ChatOpenAI(model="gpt-4")
        
        # 에이전트 생성
        agent = create_react_agent(model, client.get_tools())
        
        # 에이전트 실행
        response = await agent.ainvoke({"messages": "Redis에 'user:1'이라는 키의 값을 가져와서 PostgreSQL의 users 테이블에서 해당 ID로 검색해줘"})
        return response

# 비동기 함수 실행
result = asyncio.run(run_multi_servers())
print(result)
```

## MCP 서버 구현 방법

### Python으로 간단한 MCP 서버 만들기

```python
# math_server.py
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("Math")

@mcp.tool()
def add(a: int, b: int) -> int:
    """두 숫자를 더합니다"""
    return a + b

@mcp.tool()
def multiply(a: int, b: int) -> int:
    """두 숫자를 곱합니다"""
    return a * b

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

### 이 서버를 LangGraph와 연동하기

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
from langgraph.prebuilt import create_react_agent
from langchain_openai import ChatOpenAI
import asyncio

async def run_math_agent():
    async with MultiServerMCPClient(
        {
            "math": {
                "command": "python",
                "args": ["math_server.py"],
                "transport": "stdio",
            }
        }
    ) as client:
        model = ChatOpenAI(model="gpt-4")
        agent = create_react_agent(model, client.get_tools())
        
        response = await agent.ainvoke({"messages": "3과 5를 더한 후 그 결과를 12와 곱하면 얼마인가요?"})
        return response

result = asyncio.run(run_math_agent())
print(result)
```

## LangGraph 그래프에 MCP 서버 통합하기

LangGraph의 그래프 구조에 MCP 도구를 통합하는 방법입니다:

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
from langchain_openai import ChatOpenAI
from langgraph.graph import StateGraph, END
from typing import TypedDict, List, Dict, Any
import asyncio

# 상태 정의
class AgentState(TypedDict):
    messages: List
    tools: List[Dict[str, Any]]

# 노드 함수 정의
async def agent_node(state: AgentState):
    model = ChatOpenAI(model="gpt-4")
    messages = state["messages"]
    tools = state["tools"]
    
    # 도구 사용을 위한 프롬프트
    prompt = f"""
    당신은 도구를 사용하여 사용자의 질문에 답변하는 AI 비서입니다.
    사용 가능한 도구: {tools}
    """
    
    # 모델 호출
    response = await model.ainvoke(
        messages + [{"role": "system", "content": prompt}]
    )
    
    # 메시지 업데이트
    return {"messages": messages + [response], "tools": tools}

# 메인 함수
async def run_graph():
    # MCP 클라이언트 설정
    async with MultiServerMCPClient(
        {
            "postgres": {
                "command": "node",
                "args": ["/path/to/src/postgres/index.js", "postgresql://user:password@localhost:5432/dbname"],
                "transport": "stdio",
            }
        }
    ) as client:
        # 도구 가져오기
        tools = client.get_tools()
        
        # 그래프 정의
        workflow = StateGraph(AgentState)
        workflow.add_node("agent", agent_node)
        workflow.set_entry_point("agent")
        workflow.add_edge("agent", END)
        
        # 그래프 컴파일
        graph = workflow.compile()
        
        # 초기 상태
        state = {
            "messages": [{"role": "user", "content": "users 테이블에서 모든 사용자의 이름과 이메일을 가져와줘"}],
            "tools": tools
        }
        
        # 그래프 실행
        result = await graph.ainvoke(state)
        return result

# 실행
result = asyncio.run(run_graph())
print(result)
```

## Redis MCP 서버 연동 예제

Redis MCP 서버를 LangGraph와 연동하는 구체적인 예제입니다:

```python
from langchain_mcp_adapters.client import MultiServerMCPClient
from langgraph.prebuilt import create_react_agent
from langchain_openai import ChatOpenAI
import asyncio

async def run_redis_agent():
    async with MultiServerMCPClient(
        {
            "redis": {
                "command": "node",
                "args": ["/path/to/src/redis/src/index.js", "redis://localhost:6379"],
                "transport": "stdio",
            }
        }
    ) as client:
        model = ChatOpenAI(model="gpt-4")
        agent = create_react_agent(model, client.get_tools())
        
        # Redis 관련 작업 수행
        response = await agent.ainvoke({
            "messages": "Redis에 'user:1' 키에 '{\"name\": \"John\", \"email\": \"john@example.com\"}' 값을 저장하고, 다시 그 값을 읽어서 보여줘"
        })
        return response

result = asyncio.run(run_redis_agent())
print(result)
```

## 주의사항 및 팁

1. **경로 설정**: MCP 서버 실행 파일의 절대 경로를 사용하는 것이 좋습니다.
2. **오류 처리**: MCP 서버 연결 오류를 적절히 처리하세요.
3. **비동기 처리**: LangGraph와 MCP 서버 통신은 비동기로 처리됩니다.
4. **도구 권한**: 필요한 도구만 노출하여 보안을 강화하세요.
5. **성능 최적화**: 장기 실행 작업은 별도의 프로세스로 분리하는 것이 좋습니다.

## 참고 자료

- [LangGraph MCP 통합 공식 문서](https://langchain-ai.github.io/langgraph/agents/mcp/)
- [Model Context Protocol 공식 레포지토리](https://github.com/modelcontextprotocol/mcp)
- [langchain-mcp-adapters 라이브러리](https://github.com/langchain-ai/langchain-mcp-adapters) 