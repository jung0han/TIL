텍스트 임베딩은 문자열의 관련성을 측정 할 수 있으며 일반적으로 아래의 용도로 사용됩니다.

- **검색** (쿼리 문자열과의 관련성을 기준으로 결과 순위 지정)
- **클러스터링** (텍스트 문자열을 관련성을 기준으로 그룹화)
- **추천** (문자열이 관련된 항목을 추천)
- **이상 탐지** (관련성이 거의 없는 이상 값을 탐지)
- **다양성 측정** (유사성 분포를 분석)
- **분류** (텍스트 문자열을 가장 유사한 라벨로 분류)

> 새로 발표된 [Assistants API](https://platform.openai.com/docs/assistants)에 검색 기능과 메시지 기록 관리 기능이 내장되어 있습니다.
> 직접 임베딩을 만들고 관리하는 것에 대해 어려움을 느낀다면 [Assistants API](https://platform.openai.com/docs/assistants)을 알아보세요.

임베딩은 부동 소수점 숫자의 벡터입니다. 두 벡터 사이의 거리가 작을수록 관련성이 높음을 의미하고 거리가 멀면 관련성이 낮다는 의미입니다.

## 임베딩을 얻는 방법

임베딩을 얻으려면 임베딩 모델 ID를 선택하고 [임베딩 API 엔드포인트](https://platform.openai.com/docs/api-reference/embeddings)에 요청을 보냅니다.

요청 샘플

```python
from openai import OpenAI
client = OpenAI()

response = client.embeddings.create(
    input="Your text string goes here",
    model="text-embedding-ada-002"
)

print(response.data[0].embedding)
```

응답 샘플

```json
{
  "data": [
    {
      "embedding": [
        -0.006929283495992422,
        -0.005336422007530928,
        ...
        -4.547132266452536e-05,
        -0.024047505110502243
      ],
      "index": 0,
      "object": "embedding"
    }
  ],
  "model": "text-embedding-ada-002",
  "object": "list",
  "usage": {
    "prompt_tokens": 5,
    "total_tokens": 5
  }
}
```

## 문자열에 대한 토큰 수 확인 방법

OpenAI의 토크나이저 [titoken](https://github.com/openai/tiktoken)으로 문자열을 토큰으로 분할 할 수 있습니다.

```python
import tiktoken

def num_tokens_from_string(string: str, encoding_name: str) -> int:
    """Returns the number of tokens in a text string."""
    encoding = tiktoken.get_encoding(encoding_name)
    num_tokens = len(encoding.encode(string))
    return num_tokens

num_tokens_from_string("tiktoken is great!", "cl100k_base")
```

`text-embedding-ada-002`와 같은 2세대 모델은 `cl100k_base` 모델을 사용하세요.

## K nearest 임베딩 벡터 검색 방법

많은 벡터를 빠르게 검색하려면 벡터 데이터베이스를 사용하는 것이 좋습니다.

- [Chroma](https://cookbook.openai.com/examples/vector_databases/chroma/using_chroma_for_embeddings_search), an open-source embeddings store
- [Elasticsearch](https://cookbook.openai.com/examples/vector_databases/elasticsearch/readme), a popular search/analytics engine and vector database
- [Milvus](https://cookbook.openai.com/examples/vector_databases/milvus/getting_started_with_milvus_and_openai), a vector database built for scalable similarity search
- [Pinecone](https://cookbook.openai.com/examples/vector_databases/pinecone/readme), a fully managed vector database
- [Qdrant](https://cookbook.openai.com/examples/vector_databases/qdrant/getting_started_with_qdrant_and_openai), a vector search engine
- [Redis](https://cookbook.openai.com/examples/vector_databases/redis/readme) as a vector database
- [Typesense](https://cookbook.openai.com/examples/vector_databases/typesense/readme), fast open source vector search
- [Weaviate](https://cookbook.openai.com/examples/vector_databases/weaviate/readme), an open-source vector search engine
- [Zilliz](https://cookbook.openai.com/examples/vector_databases/zilliz/getting_started_with_zilliz_and_openai), data infrastructure, powered by Milvus

## 거리 함수의 선택

[코사인 유사성](https://en.wikipedia.org/wiki/Cosine_similarity)을 권장하지만 거리 함수는 종류는 그리 중요하지 않습니다.

- 코사인 유사성은 내적을 이용해 약간 더 빠르게 계산 할 수 있습니다.
- 코사인 유사성과 유클리드 거리의 결과는 동일한 순위를 가져옵니다.

출처 : https://platform.openai.com/docs/guides/embeddings/use-cases?lang=python