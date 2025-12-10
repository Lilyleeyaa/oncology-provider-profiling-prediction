# oncology-provider-profiling-prediction
Machine learning analysis for Oncology provider profiling and prescription prediction

# Oncology Provider Profiling – Machine Learning Analysis

## 1. Overview
Kaggle “Prescription-based Prediction” dataset을 활용하여  
Oncology provider 처방 패턴을 군집화하고 항암 처방 여부 예측 모델(Logistic 중심)을 구축한 프로젝트입니다.

## 2. Main Steps
- Data preprocessing (wide → provider-level aggregation)
- Clustering (Hellinger + KMeans)
- Statistical testing (Chi-square, ANOVA)
- Classification models (Logistic, RF, XGB, LGBM)
- Deep learning MLP baseline
- Final ROC comparison

## 3. Files
- `analysis.ipynb`: 전체 분석 코드  
- `README.md`: 프로젝트 설명  

## 4. Results Summary
- Logistic Regression: **AUC 0.897** (Best model)
- Cluster가 Provider 행동을 가장 잘 요약하는 핵심 변수
- 딥러닝은 소표본·simple tabular 구조에서 성능 저조

## 5. Contact
A71039 이경은

## ref. Analysis detail

본 프로젝트의 전체 분석 과정은 다음 단계로 구성되어 있습니다.

### **Step 1. Load Data**
- Kaggle Prescription-based Prediction 데이터 로드  
- long-format (provider × drug) 구조 확인

### **Step 2. Exploratory Data Analysis**
- 수치형/범주형 변수 분포 확인  
- TA별 처방량 분포 및 Provider × TA 히트맵 시각화

### **Step 3. Clustering (Hellinger + KMeans)**
- 상위 15개 TA + OTHER로 구성  
- 비율화 → Hellinger 변환 → normalize  
- KMeans(k=6) 클러스터 도출  
- t-SNE로 군집 시각화

### **Step 4. Cluster Profiling**
- provider 특성과 cluster를 결합  
- 군집별 연속형/범주형 요약  
- 군집별 TA 비중, ONCO 구성 비율, 주요 molecule 분석

### **Step 5. Feature Engineering**
- npi 단위로 total_rx, onco_rx, onco_share 등 파생변수 생성  
- ONCO Subcategory 비율, ATC3 기반 변수 생성  
- 최종 모델 입력 테이블 생성

### **Step 6. Statistical Testing**
- Chi-square: cluster, gender → y_onco와 유의  
- ANOVA: tot_rx, onco_share, therapy 비율 등 유의  
- 모델링 전략 결정(회귀 제외 → 분류 중심)

### **Step 7. Regression Attempt**
- y_L1_total_rx 회귀 적합  
- 회귀 가정 미충족(선형성/잔차 분포/다중공선성)으로 분류 모델로 전환

### **Step 8. Classification Models**
- Logistic Regression  
- Random Forest  
- XGBoost / LightGBM  
- ROC-AUC, Precision, Recall, FN/FP 등 성능 비교  
- Logistic Regression이 최종 모델로 선정(AUC 0.897)

### **Step 9. Deep Learning Baseline (MLP)**
- 2-layer MLP (Dropout, L2, EarlyStopping)  
- 소표본 + 단순 tabular 구조로 인해 과적합 발생  
- ROC-AUC 0.42로 전통 ML 대비 성능 낮음

### **Step 10. Final ROC Comparison**
- Logistic / RF / XGB / LGBM / MLP ROC 한 장 비교 시각화

