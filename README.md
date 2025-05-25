# Churn Prediction with Random Forest

Bu proje, Akbank ML Bootcamp kapsamında gözetimli öğrenme teknikleri kullanılarak bir bankanın müşterilerinin bankayı terk edip e
(churn) tahmin etmek amacıyla yapılmıştır.

## Proje Amacı

Müşteri kaybı (churn), bankalar için önemli bir problemdir. Bu proje ile müşteri bilgileri kullanılarak, hangi müşterilerin ayrıl
taşıdığını önceden tahmin etmek ve böylece CRM ekiplerine proaktif aksiyon alma imkânı sunmak hedeflenmiştir.

## Veri Seti

- Kaynak: [Kaggle - Churn Modelling Dataset](https://www.kaggle.com/datasets/louishgy/churn-modelling)
- Gözlem Sayısı: 10.000 müşteri
- Özellikler: Yaş, ülke, cinsiyet, kredi skoru, bakiye, maaş, ürün sayısı, kredi kartı kullanımı, aktif müşteri durumu, vs.
- Hedef Değişken: `Exited` (1 = ayrıldı, 0 = kaldı)

## Kullanılan Yöntemler

- Keşifsel Veri Analizi (EDA): pandas, matplotlib, seaborn
- Ön İşleme: 
  - Gereksiz sütunlar çıkarıldı (CustomerId, Surname, RowNumber)
  - Kategorik değişkenler (Geography, Gender) one-hot encoding ile sayısala çevrildi
  - Sayısal veriler StandardScaler ile ölçeklendirildi
- Eğitim/Test Ayrımı: %80 eğitim - %20 test
- Modelleme: Logistic Regression, Random Forest, XGBoost
- Hiperparametre Optimizasyonu: GridSearchCV ile Random Forest için en iyi parametreler bulundu
- Model Değerlendirme: Accuracy, Precision, Recall, F1-score, ROC-AUC

## En İyi Model

- Algoritma: Random Forest Classifier
- En iyi parametreler:
  - n_estimators: 200
  - max_depth: 10
  - min_samples_split: 2
  - min_samples_leaf: 1
- Çapraz Doğrulama AUC Skoru: 0.84
- Test Seti AUC Skoru: 0.85

## Sonuçlar ve Yorumlar

### Model Performansı

| Metrik       | Skor | Açıklama |
|--------------|------|----------|
| Accuracy     | 0.86 | Tahminlerin %86’sı doğru |
| Precision    | 0.76 | Churn edecek denilenlerin %76’sı gerçekten ayrıldı |
| Recall       | 0.55 | Gerçekten ayrılanların %55’i yakalandı |
| F1-score     | 0.64 | Precision ve Recall’un dengeli ortalaması |
| ROC-AUC      | 0.85 | Genel ayrım gücü yüksek |

Model genel olarak başarılıdır. Özellikle kalan müşterileri doğru tahmin etmede güçlüdür. Ayrılan müşterileri daha fazla yakalaya
Recall geliştirilebilir. ROC-AUC değerinin yüksek olması modelin dengeli ve güvenilir çalıştığını gösterir.

### Özellik Önemleri

| Sıra | Özellik         | Açıklama |
|------|------------------|----------|
| 1    | Age              | Yaş arttıkça churn riski artıyor |
| 2    | IsActiveMember   | Aktif olmayan müşteriler daha fazla ayrılıyor |
| 3    | Balance          | Yüksek bakiye ama pasif kullanıcılar riskli |
| 4    | CreditScore      | Düşük kredi skoru churn ihtimalini artırabiliyor |
| 5    | EstimatedSalary  | Dolaylı etkili bir değişken |

Model anlamlı değişkenleri öncelikli kullanarak mantıklı sonuçlar vermiştir.

### Aksiyon Önerileri

- 40 yaş üstü, pasif ve yüksek bakiyeli müşterilere özel teklifler sunulabilir
- CRM sistemine entegre edilerek churn skoru takibi yapılabilir
- Sadakat programları ve kampanyalar churn riskine göre özelleştirilebilir

### Geliştirme Önerileri

- Yeni değişkenler eklenerek Recall oranı iyileştirilebilir
- Gözetimsiz öğrenme ile müşteri segmentasyonu yapılabilir

## Kaggle Bağlantı

- Kaggle Notebook: https://www.kaggle.com/code/caglaery/churn-prediction

