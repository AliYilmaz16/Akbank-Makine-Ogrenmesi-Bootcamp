# Trafik Kazası Şiddeti Tahmin Sistemi – Akbank & Global AI Hub Makine Öğrenmesi Bootcamp Projesi

Bu proje, **Akbank & Global AI Hub Makine Öğrenmesi Bootcamp** kapsamında gerçekleştirilmiştir.  
Amaç, Birleşik Krallık'ta meydana gelen trafik kazalarının şiddetinin, kazaya ait temel bilgiler kullanılarak makine öğrenmesi modelleri yardımıyla tahmin edilmesidir.

---

## Kullanılan Veri Seti

- **Kaynak:** [Kaggle – UK Road Accident Dataset](https://www.kaggle.com/datasets/devansodariya/road-accident-united-kingdom-uk-dataset)
- **Toplam veri:** 1.504.150 satır  
- **Sütun sayısı:** 33 (temel bilgiler, çevresel koşullar vb.)
- **Hedef değişken:** `Accident_Severity`  
    - `1`: Ölümcül Kaza  
    - `2`: Ciddi Yaralanmalı Kaza  
    - `3`: Hafif Yaralanmalı Kaza  

---

## Veri Analizi (EDA)

- Veri setinde ciddi sınıf dengesizliği bulunmaktadır (Hafif kazalar çoğunluktadır).
- `Light_Conditions`, `Road_Type`, `Weather_Conditions` gibi değişkenlerin kaza şiddetiyle ilişkili olduğu gözlemlenmiştir.
- Sayısal değişkenler (araç sayısı, yaralı sayısı, hız limiti vb.) ile hedef arasında zayıf korelasyonlar mevcuttur.

---

## Veri Ön İşleme

- Gereksiz/boş sütunlar silinmiştir.
- 14 kategorik sütun encode edilmiştir:
  - Sıralı kategoriler → **Label Encoding**
  - Nominal ve yüksek kardinaliteli değişkenler → **One-Hot Encoding**
- Düşük varyanslı (bilgi taşımayan) 202 sütun çıkarılmıştır.
- **SMOTE** planlanmış ancak kaynak sınırları nedeniyle uygulanmamıştır.

---

## Modelleme ve Karşılaştırma

Aşağıdaki üç model test edilmiştir:

| Model               | Ortalama F1 (macro) | Standart Sapma |
|---------------------|---------------------|----------------|
| Logistic Regression | 0.3295              | 0.0012         |
| Decision Tree       | **0.3796**          | **0.0008**     |
| Random Forest       | 0.3639              | 0.0009         |

---

## Seçilen Nihai Model: Decision Tree

- **GridSearchCV** ile hiperparametre optimizasyonu yapılmıştır.
- **En iyi parametreler:**
  - `criterion='gini'`
  - `max_depth=None`
  - `max_features='log2'`
  - `min_samples_split=2`
- Test setinde **F1-macro** skoru: **0.380**
- Hafif kazalarda başarılı, ancak ölümcül kazalarda düşük başarı göstermektedir.

---

## Değerlendirme Metrikleri
<img width="415" alt="Ekran Resmi 2025-05-25 23 37 00" src="https://github.com/user-attachments/assets/fb79e831-b97a-42d9-bc4e-50d55a60058b" />  


- **Accuracy:** 0.76  
- **Macro F1 Score:** 0.38
- **Confusion Matrix:** Ölümcül kazalar yalnızca %6 doğrulukla tahmin edilmiştir.

---

##  Veri Dengesizliği Sorunu

- `Accident_Severity = 3` (Hafif kaza) sınıfı veri setinde baskındır.
- `class_weight='balanced'` kullanılmış olsa da, sınıf dengesizliği devam etmektedir.
- **Azınlık sınıflar** için (1 = Ölümcül, 2 = Ciddi) **Recall** değeri düşüktür.
- **SMOTE, ADASYN, focal loss** gibi yaklaşımlar ilerleyen çalışmalarda önerilmektedir.

---

## Gerçek Hayatta Kullanım Alanları

- Trafik kazası verilerinin analiziyle **emniyet ve şehir planlaması**
- **Yüksek riskli alanların** belirlenmesi
- **Karar destek sistemleri** ile trafik güvenliğini artırma

---

## Geliştirme Önerileri

- **SMOTE, ADASYN, Focal Loss** gibi dengeleme tekniklerinin kullanılması
- **SHAP / Feature Importance** gibi araçlarla önemli özniteliklerin belirlenmesi
- Modelin bir **web arayüzüne** entegre edilerek sahada aktif kullanımının sağlanması

---

## Proje Bağlantıları

- [Kaggle Notebook](https://www.kaggle.com/code/aliyilmazbm/akbank-makine-ogrenmesi-bootcamp-trafik-kazasi)

---

## Geliştirici

**Ali Yılmaz**  
Akbank & Global AI Hub  
Makine Öğrenmesi Bootcamp – Mayıs 2025
