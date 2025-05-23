# Student Performance Prediction (Multi-Dataset Regression Project)

## Problem Tanımı

Bu projede öğrencilerin akademik performanslarını tahmin etmek amacıyla **iki farklı veri seti** kullanılarak **regresyon modelleri** geliştirilmiştir.  
İlk modelde doğrudan hedef değişkenle yüksek korelasyon içeren bir öznitelik modeli yapay olarak şişirdiği için ikinci, daha doğal bir veri setiyle yeni bir model oluşturulmuştur.

## Amaç

- Öğrencilerin notlarını çeşitli kişisel ve akademik faktörlere göre tahmin etmek
- Farklı regresyon modellerini karşılaştırarak en başarılı yaklaşımı belirlemek
- Gerçek veriyle daha açıklayıcı ve yorumlanabilir model üretmek

## Kullanılan Veri Setleri

1. [Predict Students Drop Out of the Course](https://www.kaggle.com/datasets/kapturovalexander/predict-students-drop-out-of-the-course)
2. [Student Performance - Multiple Linear Regression](https://www.kaggle.com/datasets/nikhil7280/student-performance-multiple-linear-regression)

## Veri Analizi

İlk veri setinde `Exam_Score (%)` ile `Final_Grade` arasında yüksek korelasyon olması nedeniyle model doğruluğu yapay biçimde yükselmiştir.  
> Bu özellik çıkarıldığında modelin R² skoru %50’lere kadar düşmüştür.

Bu nedenle ikinci veri seti ile daha sağlam bir model geliştirilmiştir.

## Kullanılan Yöntemler

- Label Encoding
- Train/Test Split
- Keşifsel Veri Analizi (EDA)
- Regresyon Modelleri:
  - Linear Regression
  - Ridge / Lasso
  - Decision Tree / Random Forest
- Performans Metrikleri:
  - MAE
  - RMSE
  - R²
- Feature Importance (özellik önem sıralaması)

## Model Sonuçları (İkinci Veri Seti)

| Model                 | MAE  | RMSE | R²    |
|----------------------|------|------|-------|
| Linear Regression     | 1.61 | 2.02 | 0.989 |
| Ridge Regression      | 1.61 | 2.02 | 0.989 |
| Lasso Regression      | 1.75 | 2.21 | 0.987 |
| Random Forest         | 1.81 | 2.27 | 0.986 |
| Decision Tree         | 2.34 | 2.97 | 0.976 |

## Özellik Önem Sıralaması (Random Forest)

- `Previous Scores`: %84.7
- `Hours Studied`: %14.1
- Diğer değişkenler: < %1

## Sonuç

- İlk modelde yapay başarıya neden olan öznitelik fark edilerek veri kalitesi sorgulanmıştır.
- İkinci modelde `Previous Scores` ve `Hours Studied` en önemli faktörler olarak öne çıkmıştır.
- Basit modeller (Linear/Ridge) dahi yüksek başarı göstermiştir.
