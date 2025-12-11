# oncology-provider-profiling-prediction
Machine learning analysis for Oncology provider profiling and prescription prediction

# Oncology Provider Profiling – Machine Learning Analysis

## 1. Overview
Kaggle “Prescription-based Prediction” dataset을 기반으로  
Oncology provider의 처방 패턴을 분석하고 항암 처방 여부를 예측하는 머신러닝 모델(Logistic Regression 중심)을 구축한 프로젝트입니다.

🔹 군집(Cluster) 기반 Provider 프로필 요약  
🔹 항암 처방 여부 예측(Classification)  
🔹 전통 ML vs. MLP 비교

---

## 2. Data Notice
본 저장소는 **전처리 완료된 Provider-level long_df**를 입력 데이터로 사용합니다.

원천 Kaggle 데이터(239,930명 → Onco provider 필터링 → wide-format → ATC 매핑 → long-format 변환 등 전체 전처리 과정)는  
용량 및 데이터 공유 제한으로 인해 저장소에는 포함하지 않았으며,  
**전처리 전체 과정은 분석 보고서에 상세히 기술되어 있습니다.**

---

## 3. Main Steps
- Data preprocessing (long_df 기준)
- Clustering (Hellinger + KMeans)
- Statistical testing (Chi-square, ANOVA)
- Feature engineering  
- Classification models (Logistic, RF, XGB, LGBM)
- Deep learning MLP baseline
- Final ROC comparison

---

## 4. Files
- `analysis.ipynb` — 전체 분석 코드  
- `README.md` — 프로젝트 설명  

---

## 5. Results Summary
- **Logistic Regression: AUC 0.897 (Best 모델)**
- Cluster가 Provider 행동을 가장 잘 요약하는 핵심 변수로 확인됨
- 딥러닝(MLP)은 소표본·단순 tabular 환경에서 성능이 낮음 (AUC 0.42)

---

## 6. Analysis Steps (Details)

### **Step 1. Load Data**
- long_df (Provider × Drug) 기반 데이터 로드
- Provider-level aggregation 구조 확인

### **Step 2. Exploratory Data Analysis**
- 수치형·범주형 변수 분포  
- TA별 처방량 및 히트맵 시각화

### **Step 3. Clustering (Hellinger + KMeans)**
- 상위 TA 비중 기반 비율화  
- Hellinger 변환 후 정규화  
- KMeans(k=6) 클러스터링  
- t-SNE 시각화

### **Step 4. Cluster Profiling**
- Provider 메타정보 결합  
- 군집별 TA 구성·처방 특성·온코 비중 분석

### **Step 5. Feature Engineering**
- onco_rx, onco_share  
- therapy 비율  
- brand/generic 처방량  
- ATC3 변수 생성  
- 최종 모델 입력 테이블 구성

### **Step 6. Statistical Testing**
- Chi-square: cluster, gender → y_onco 유의  
- ANOVA: tot_rx, onco_share, therapy_pct 유의

### **Step 7. Regression Attempt**
- y_L1_total_rx 회귀 적합  
- 선형성·잔차·다중공선성 문제 → 분류 모델로 전환

### **Step 8. Classification Models**
- Logistic Regression (Best: AUC 0.897)  
- Random Forest / XGBoost / LightGBM  
- ROC, FN/FP 비교

### **Step 9. Deep Learning Baseline (MLP)**
- 2-layer MLP  
- 소표본 제한으로 과적합 발생  
- ROC-AUC 0.42

### **Step 10. Final ROC Comparison**
- Logistic / RF / XGB / LGBM / MLP ROC 비교 시각화

---

## 7. Contact
A71039 이경은  
