# Simple Linear Regression Projesi

> **Özet:** Bu README, proje dizininde bulunan `1-SimpleLinearRegression.ipynb` projesini açıklar. 
---

## İçindekiler

1. [Proje Hedefi](#proje-hedefi)
2. [Proje Aşamaları](#proje-aşamaları)

   * Veri yükleme
   * Keşifsel Veri Analizi (EDA)
   * Ön işleme (Preprocessing)
   * Model Eğitimi
   * Değerlendirme
   * Çıkarım (Inference)

---

## Proje Hedefi

Bu proje, öğrenci çalışma saatleri (`Study Hours`) ile sınav puanı (`Exam Score`) arasındaki ilişkiyi **basit doğrusal regresyon** (Simple Linear Regression) yöntemiyle modellemeyi amaçlamaktadır. Amaç; veri ön işleme, model eğitimi, değerlendirme ve örnek çıkarımlar gösterilerek bir eğitim/öğrenme projesi oluşturmak ve sonuçların yorumlanmasını sağlamaktır.

---

## Çalıştırma Ortamı & Kurulum

**Önerilen ortam:** Python 3.8+ (3.10 önerilir), virtualenv veya conda.

**Temel kütüphaneler:**

* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn
* jupyter (notebook çalıştırmak için)

---

## Proje Aşamaları

Aşağıda notebook'ta yapılan işlemlere göre düzenlenmiş açıklama yer almaktadır.

### 1) Veri yükleme

* Dosya: `1-studyhours.csv` (kod içinde `pd.read_csv("1-studyhours.csv")`).
* Beklenen sütunlar: `Study Hours` (bağımsız değişken / feature), `Exam Score` (bağımlı değişken / hedef).

**Amaç:** Modelin öğrenebilmesi için `X` ve `y` setlerini oluşturmak.

```python
X = df_data[["Study Hours"]]  # dataframe formatında X
y = df_data['Exam Score']      # seri (series) olarak y
```

### 2) Keşifsel Veri Analizi (EDA)

* `df.head()`, `df.info()`, `df.describe()` ile temel istatistikler alınır.
* `plt.scatter(df_data['Study Hours'], df_data['Exam Score'])` ile dağılım incelenir.

**Neye bakılır?**

* Veride boş (NaN) değer var mı?
* `Study Hours` ile `Exam Score` arasında doğrusal bir ilişki gözlemleniyor mu?
* Outlier (aykırı değer) olup olmadığı kontrol edilir.

### 3) Ön İşleme (Preprocessing)

* Özellik ölçeklendirme: `StandardScaler()` kullanılmış.
* Veri bölünmesi: `train_test_split(X, y, test_size=0.2, random_state=15)`.

**Dikkat:** Notebook'ta `scaler.fit_transform(X_train)` ve `scaler.transform(X_test)` şeklinde ölçeklendirme yapılıyor — bu doğrudur. Ancak görselleştirme veya doğrudan `regression.predict([[20]])` gibi ham değerler kullanıldığında ölçeklendirme unutulursa hatalı sonuçlar çıkar.

### 4) Model Eğitimi

* Model: `LinearRegression()` (scikit-learn)
* Eğitim: `regression.fit(X_train, y_train)` (burada `X_train` ölçeklendirilmiş olmalı).

### 5) Değerlendirme

* Tahmin: `y_pred_test = regression.predict(X_test)` (X\_test ölçeklendirilmiş olmalı)
* Metrikler:

  * MSE, MAE, RMSE
  * R² (r2\_score)
  * Notebook'ta bir `Adj_r2` hesaplama girişimi görülüyor fakat formül hatalı; doğru formül README `Kodda Bulunan Önemli Noktalar` bölümünde yer alır.
* Görselleştirme: Gerçek vs tahmin dağılımı ve eğitim veri kümesine ilişkin regresyon doğrusu çizimleri yapılmış.

### 6) Çıkarım (Inference)

* Notebook üzerinde örnek çıkarımlar mevcut (`regression.predict(scaler.transform([[20]]))`) — yani saat sayısı 20 için modelin tahmini hesaplanmak istenmiş.
* **Önemli:** Model eğitiminde ölçeklendirme kullanıldıysa çıkarımda da aynı scaler ile `transform` yapılmalıdır.

---


**Not:** İncelediğim notebook'ta `1-studyhours.csv` adlı veri dosyası çalışma dizininde bulunamadığından README'deki veri örnekleri ve şekillendirmeler koddan çıkarılmıştır. Proje dosyalarını tam olarak sağlarsanız README'yi doğrudan veriye dayalı örnek tablolar, görseller ve sonuçlarla güncelleyebilirim.
