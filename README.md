# 🥘 bibimbap : Grammar Error Correction Promptathon 

본 레포지토리는 Grammar Error Correction Promptathon  실험을 재현하고 확장하기 위한 코드 및 가이드를 제공합니다.


## 프로젝트 개요

* **목표**: Solar Pro API를 활용하여 프롬프트 만으로 한국어 맞춤법 교정 성능을 개선한다.
  
### 접근 전략:
### ✅ 템플릿 설계 및 실험
- 기본 템플릿 외에도 성능 향상을 위해 다양한 프롬프트 템플릿을 설계하고 실험했습니다.
- 실험한 대표 템플릿:
  - `basic`: 단순 교정 요청
  - `detailed`: 오류 유형 명시 (띄어쓰기, 문장 부호 등)
  - `formal`: 공식 문서 스타일 강조
  - `enhanced_korean_pro_v3`: 구체적 규칙 기반 템플릿
  - `meta_auto`: 메타데이터(age, gender, source) 기반 교정 조건 포함

### 🔄 실험 자동화
- `main.py`를 개선하여:
  - 모든 템플릿을 자동 평가
  - validation recall이 가장 높은 템플릿을 선택
  - 해당 템플릿을 이용해 test set을 교정하고 제출 파일(`submission_baseline.csv`) 생성

### 🧪 성능 비교
- `metrics.py`를 활용하여 Recall과 Precision을 계산
- LCS 기반 토큰 비교로 TP/FP/FN/FR 구분
- 템플릿별 성능 로그를 통해 최종 선택
---

## ⚙️ 환경 세팅 & 실행 방법

### 1. 사전 준비 

```bash
git clone https://github.com/your-org/your-repo.git
cd your-repo/experiment
```

### 라이브러리 설치

```bash
pip install -r requirements.txt
```

### 실험 실행

```bash
python run_experiment.py --input sample_input.txt --output result.json
```

> 실행 옵션 (예시):
> `--input`: 실험 대상 파일
> `--output`: 결과 저장 파일 경로

---


## 실험의 한계 및 향후 개선

* **한계**:

  * 긴 문장/복문에서 누락되는 오류 존재
  * 도메인 특화 문서(법률/의료 등)에서는 성능 저하
* **향후 개선 방향**:

  * 오류 유형 자동 분류 → 맞춤형 프롬프트 분기
  * User Feedback loop를 통한 교정 정확도 향상

---

## 폴더 구조

```
📁 bibimbap/
├── code/
│   ├── config.py              # 실험 환경 설정 (API, 모델, 경로 등)
│   ├── prompts/
│   │   └── templates.py       # 템플릿 정의 (basic, detailed, formal 등)
│   └── utils/
│       ├── experiment.py      # 템플릿별 실험 실행 클래스
│       └── metrics.py         # LCS 기반 정답 평가 함수
├── data/
├── main.py                    # 전체 실험 자동화 파이프라인
├── requirements.txt           # 라이브러리 목록
└── .env                       # API Key 설정용 (비공개)

