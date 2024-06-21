# Churn Tahmin MLOps Projesi

Bu proje, müşteri terk (churn) tahminine yönelik bir makine öğrenimi modeli geliştirme, eğitim süreci ve dağıtımını içeren MLOps ve MLflow tabanlı bir projedir. Proje kapsamında veri ön işleme, model eğitimi, hiperparametre optimizasyonu ve model dağıtımı adımları gerçekleştirilmiştir.
Bu depo, XGBoost kullanarak müşteri kaybını tahmin etmek için kapsamlı bir MLOps projesi içermektedir. Proje, veri ön işleme, model eğitimi, hiperparametre optimizasyonu, model değerlendirme ve Flask kullanarak modelin dağıtımını ve MLflow ile deney izlemeyi kapsar. Aşağıda, projede yer alan her adımın detaylı bir açıklaması bulunmaktadır.

## İçindekiler
- [Proje Genel Bakış]
- [Gereksinimler]
- [Kurulum]
- [Veri Ön İşleme]
- [Model Eğitimi ve Hiperparametre Optimizasyonu]
- [Model Dağıtımı]
- [API Kullanımı]
- [İzleme ve Takip]

## Proje Genel Bakış
Bu projenin amacı, müşteri kaybını tahmin eden bir makine öğrenme modeli geliştirmek ve dağıtmaktır. Müşteri kaybı tahmini, işletmelerin müşterilerini kaybetmelerini önlemek için hangi müşterilerin muhtemelen ayrılacağını belirlemelerine yardımcı olur. Projede kullanılan teknolojiler şunlardır:
- **Python**: Programlama dili
- **Pandas**: Veri manipülasyonu ve analizi
- **Scikit-learn**: Makine öğrenme kütüphanesi
- **XGBoost**: Gradient boosting framework
- **MLflow**: Deney izleme ve model kayıt sistemi
- **Flask**: Modeli API olarak dağıtmak için web framework
- **Imbalanced-learn**: Dengesiz veri kümeleri ile çalışma
- **SMOTE**: Dengesiz veri kümesini dengelemek için kullanılan yöntem

## Gereksinimler
Projeyi çalıştırmadan önce aşağıdaki bileşenlerin yüklü olduğundan emin olun:
- Python 3.8 veya daha yeni bir sürüm
- Pip paket yöneticisi

## Kurulum
1. Depoyu klonlayın:
   ```bash
   git clone https://github.com/SemihGul5/mlops-churn-prediction.git
   cd churn-prediction-mlops
2. Gerekli paketleri yükleyin:
   pip install -r requirements.txt

## Veri Ön İşleme
Veri ön işleme, veri setinin yüklenmesini, kategorik özelliklerin kodlanmasını, sayısal özelliklerin ölçeklendirilmesini ve SMOTE kullanılarak sınıf dengesizliğinin ele alınmasını içerir.

Adımlar:
  1. Veriyi bir CSV dosyasından yükleyin.
  2. Gereksiz sütunları çıkarın.
  3. Gender sütununu LabelEncoder kullanarak kodlayın.
  4. Özellikleri StandardScaler kullanarak ölçeklendirin.
  5. SMOTE uygulayarak sınıf dengesizliğini ele alın.
  6. Veriyi eğitim ve test setlerine ayırın.

## Model Eğitimi ve Hiperparametre Optimizasyonu
Model, GridSearchCV kullanılarak hiperparametre optimizasyonu ile eğitilir. En iyi parametreler MLflow kullanılarak kaydedilir ve model test verileri üzerinde değerlendirilir.

Adımlar:
  1. Ön işlenmiş eğitim ve test verilerini yükleyin.
  2. MLflow izleme URI'si ve deney adını ayarlayın.
  3. GridSearchCV kullanarak hiperparametre optimizasyonu gerçekleştirin.
  4. En iyi parametrelerle XGBoost modelini eğitin.
  5. Modeli değerlendirin ve metrikleri MLflow kullanarak kaydedin.

## Model Dağıtımı
Model, Flask kullanılarak bir API olarak dağıtılır. API, giriş verilerini alır, ön işler ve churn tahminini döner.

Adımlar:
  1. Eğitilmiş XGBoost modelini ve ölçekleyiciyi yükleyin.
  2. Ana sayfa ve tahmin için Flask rotalarını tanımlayın.
  3. Gelen verileri ön işleyin ve tahmin yapın.
  4. Tahminleri ve gerçek değerleri takip ederek performans metriklerini MLflow kullanarak kaydedin.

## API Kullanımı
### Tahmin Endpoint'i
  - URL: /predict
  - Yöntem: POST
  - İstek Gövdesi: Aşağıdaki anahtarlara sahip JSON nesnesi:
    - CreditScore
    - Gender
    - Age
    - Tenure
    - Balance
    - NumOfProducts
    - HasCrCard
    - IsActiveMember
    - EstimatedSalary
    - true_value (isteğe bağlı, performans metriklerini kaydetmek için)
### Örnek İstek
{
    "CreditScore": 600,
    "Gender": "Male",
    "Age": 40,
    "Tenure": 3,
    "Balance": 60000,
    "NumOfProducts": 2,
    "HasCrCard": 1,
    "IsActiveMember": 1,
    "EstimatedSalary": 50000,
    "true_value": 1
}
## İzleme ve Takip
Performans metrikleri MLflow kullanılarak izlenir ve takip edilir. Model, yeni tahminler yapıldıkça doğruluk, kesinlik, geri çağırma ve F1 skoru gibi metrikleri gerçek zamanlı olarak takip eder.
