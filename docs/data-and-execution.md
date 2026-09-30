# 데이터 형식 및 실행 안내

## 데이터

원본 실험은 중학교 1학년 수학 JSON을 병합한 파일을 사용했습니다. 원본 데이터와 Chroma 인덱스는 이 저장소에 포함하지 않습니다. 필요한 입력 구조는 다음과 같습니다. 아래 예시는 형식 설명용으로 새로 작성한 예시이며 원본 실험 데이터가 아닙니다.

```json
[
  {
    "learning_data_info": {
      "learning_data_name": "example_001",
      "class_name": "텍스트",
      "text_qa": "2와 3의 합은 얼마인가요?",
      "text_an": "5입니다.",
      "text_description": "2에 3을 더하면 5가 됩니다."
    }
  }
]
```

## 실행 순서

1. Jupyter 또는 Colab에서 `notebooks/rag_math_tutor.ipynb`를 엽니다.
2. 입력 JSON을 준비하고 `MATH_DATA_PATH` 환경변수 또는 데이터 로딩 셀의 경로를 지정합니다.
3. Google API 키를 `GOOGLE_API_KEY` 환경변수 또는 노트북의 숨김 입력으로 제공합니다.
4. 설치 셀부터 순서대로 실행합니다. 데이터 임베딩 및 답변 생성 과정에서 Google API를 호출합니다.

원본 모델 설정은 `gemini-1.5-flash`, `models/text-embedding-004`입니다. 현재 이용 가능 여부는 재검증하지 않았습니다. 재실행 시 사용 가능한 모델을 `CHAT_MODEL`, `EMBEDDING_MODEL` 환경변수로 지정하고 패키지 호환성을 확인해야 합니다. 모델을 바꾸면 원본 실험과 조건이 달라지며, 임베딩 모델 변경 시 인덱스를 새로 생성해야 합니다.

설치 셀의 버전 범위는 기존 LangChain 호출을 보존하기 위한 설정이며 원본 환경의 정확한 잠금 파일은 아닙니다. 이번 공개 정리에서는 노트북 JSON과 Python 구문을 점검했으며 외부 API를 사용한 전체 실행은 수행하지 않았습니다.

## 공개용 정리 사항

- 원본의 핵심 실험 셀을 선별하고 미사용 라이브러리·주석 실습·대량 출력 제거
- API 키를 숨김 입력 또는 환경변수로 받도록 변경
- 개인 Drive 경로를 설정 가능한 파일 경로로 변경
- 설치 명령의 `U` 오기를 정리하고 실행 의존성 통합
- 일부 호출을 `invoke`로 정리하고 문서 변수 재사용을 구분
- 원본 모델명, 청크 설정, 검색 설정, 설명 프롬프트 보존

원본 Colab: [수학 튜터 PoC](https://colab.research.google.com/drive/1_MCMNDe8QT8Vcq0lVHKh0ujvt4Vo_sLZ)
