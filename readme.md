# 📦 판매량 예측 프로젝트

이 프로젝트는 제품 리뷰의 **이미지**, **텍스트**, **메타데이터**를 통합적으로 활용하여 제품의 **판매량을 예측**하는 모델을 구현한 것입니다.  
멀티모달 데이터를 조합하여, 전통적인 회귀 모델을 기반으로 판매량 예측 성능을 높이는 것이 목표입니다.



## 🔍 사용한 데이터셋

모든 데이터는 구글 드라이브에서 로드되며, 총 3가지 주요 CSV 파일과 이미지 압축 파일로 구성됩니다.

- `product.csv`: 제품별 카테고리, 브랜드, 가격 등 **제품 메타데이터** 및 판매량 레이블 포함
- `reviews.csv`: **리뷰 텍스트 데이터** (리뷰 본문, 날짜 등 포함)
- `review_image_path.csv`: 리뷰와 연결된 **이미지 경로 정보**
- `review_images.zip`: 실제 **리뷰 이미지 파일들** (압축 해제 후 사용)

> 사용 전, 경로를 로컬 또는 Colab 환경에 맞게 수정해야 합니다.



## 🧠 사용한 모델

### 1. 이미지 임베딩
- **ResNet18** (사전학습된 모델 사용, `torchvision.models`)
- 마지막 Fully Connected Layer를 제거하고, 이미지 특징 벡터를 추출 (`resnet.fc = Identity()`)

### 2. 텍스트 처리
- 리뷰 텍스트는 BERT 등의 언어모델 없이 기본 전처리 후 수치화


### 3. 예측 모델
- 이미지 + 텍스트 + 메타데이터를 결합하여, **XGBoost** 회귀 모델로 판매량을 예측



## 📁 프로젝트 구조

```
├── README.md                         # 프로젝트 설명 파일
├── 리뷰이미지+리뷰텍스트+메타데이터=_판매량_예측.ipynb  # 전체 코드 노트북
├── data/
│   ├── product.csv
│   ├── reviews.csv
│   ├── review_image_path.csv
│   └── review_images/               # 압축 해제된 이미지 폴더
└── models/
    └── resnet18_fusion.pt           # 학습된 모델 저장 (선택)
```



## 🚀 실행 방법

### 1. 필수 패키지 설치

```bash
pip install numpy==1.26.4 pandas scikit-learn matplotlib tqdm gensim torch torchvision torchaudio transformers pillow
```

### 2. Jupyter Notebook 실행

```bash
jupyter notebook 리뷰이미지+리뷰텍스트+메타데이터=_판매량_예측.ipynb
```

### 3. 구글 드라이브 연동 및 경로 수정
- `drive.mount()`로 드라이브 연동
- 데이터 경로를 자신의 드라이브 구조에 맞게 변경

### 4. 셀을 순서대로 실행
- 데이터 로딩 → 전처리 → 임베딩 생성 → 회귀 모델 학습 → 예측 및 평가


