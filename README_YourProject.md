# YMT5270 Final Sınav Projesi: H2O ile Veri Analizi ve Makine Öğrenmesi

## Öğrenci Bilgileri
- **Ad Soyad**: Serenay ÇELİK
- **Öğrenci Numarası**: 242138201
- **E-posta**: serenaycelik23@gmail.com

## Proje Özeti
> *Bu projede, kalp hastalığı tahmini yapmak amacıyla Kaggle'de yer alan “Heart Failure Prediction” veri seti kullanılmıştır. Veri seti, 918 hasta örneği ve 12 öznitelikten oluşmaktadır. Bu veri seti, halihazırda bağımsız olarak mevcut olan ancak daha önce birleştirilmemiş farklı veri setlerinin bir araya getirilmesiyle oluşturulmuştur. Bu veri setinde, 11 ortak özellik üzerinden birleştirilen 5 kalp veri seti, araştırma amaçlı bugüne kadar mevcut en büyük kalp hastalığı veri setidir. Derlemesinde kullanılan beş veri seti; Cleveland: 303 gözlem, Macarca: 294 gözlem, İsviçre: 123 gözlem, Long Beach VA: 200 gözlem ve Stalog (Kalp) Veri Seti: 270 gözlem veri kümeleridir. Tekrarlanan 272 gözlemin çıkarılmasıyla toplam 918 örnek gözlem değerlendirilmiştir. Hedef değişken, kalp hastalığının varlığına işaret eden ikili bir sınıflandırma problemidir. Öncelikle veri setinin yapısı incelenmiş, eksik veriler kontrol edilmiş ve sayısal değişkenler arasındaki korelasyon analiz edilmiştir. Aykırı değerler ve hedef değişkenin dağılımı görselleştirilmiştir. Veri setinin uyguluğundan analiz yöntemi olarak sınıflandırma tercih edilmiştir. Veri H2O.ai platformuna aktarılmış ve AutoML yöntemi kullanılarak çeşitli modeller denenmiştir. En iyi model %88.95 doğruluk, %100 precision ve recall oranı ile başarılı sonuçlar elde etmiştir.*

## Veri Seti
### Veri Seti Bilgileri
- **Veri Seti Adı**: Heart Failure Prediction Dataset
- **Kaynak**: *https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction*
- **Lisans**: *Open Data Commons Open Database License (ODbL) v1.0*
- **Veri Seti Boyutu**: *918 satır, 12 sütun*

### Veri Seti Tanımı
> *Veri seti, kalp hastalığı teşhisi için klinik ve demografik bilgileri içermektedir. Hastaların yaşı, cinsiyeti, kan basıncı, kolesterol seviyesi gibi sayısal ve kategorik değişkenler bulunmaktadır. Veri setindeki bilgiler, gerçek hasta verilerinden elde edilmiş ve çeşitli tıbbi ölçümler içermektedir. Veri setinde eksik veri bulunmamaktadır. Veri, kalp hastalığı tanısı konmuş ve konmamış hastalardan oluştuğundan dengeli bir sınıflandırma problemi sunmaktadır.*

### Öznitelik Açıklamaları
| Öznitelik Adı | Veri Tipi | Açıklama | Örnek Değer |
|---------------|-----------|----------|-------------|
| Age | Sayısal | Hastanın yaşı (yıl) | 	63 |
| Sex | Kategorik | Cinsiyet (M: Erkek, F: Kadın) | "M" |
| ChestPainType | Kategorik | 	Göğüs ağrısı tipi | "ATA" |
| RestingBP | Sayısal | Dinlenme anındaki kan basıncı (mmHg) | 140 |
| Cholesterol | Sayısal | Kolesterol seviyesi (mg/dL) | 289 |
| FastingBS | Kategorik | Açlık kan şekeri (0 = normal, 1 = yüksek) | "1" |
| RestingECG | Kategorik | 	Dinlenme EKG sonucu | "Normal" |
| MaxHR | Sayısal | Maksimum kalp atış hızı | 172 |
| ExerciseAngina | Kategorik | Egzersiz anjinası (Y: evet, N: hayır) | "N" |
| Oldpeak | Sayısal | Egzersiz sonrası ST depresyonu | 0.0 |
| ST_Slope | Kategorik | 	ST segment eğimi | "Up" |
| HeartDisease | Kategorik | 	Hedef değişken: kalp hastalığı var mı? (1=Evet, 0=Hayır) | "1" |

<img width="924" height="286" alt="image" src="https://github.com/user-attachments/assets/962a5130-293c-49e1-b43c-c2ad6fda4ad3" />

## Keşifsel Veri Analizi (Explanatory Data Analysis - EDA)
### Temel İstatistikler
> *Veri setinde sayısal değişkenlerin ortalamaları, medyanları ve standart sapmaları incelendi. Örneğin, yaş ortalaması yaklaşık 54, kolesterol seviyeleri 198 civarında değişmektedir. Veride eksik değer bulunmamaktadır.*

<img width="670" height="332" alt="image" src="https://github.com/user-attachments/assets/feadcf3c-4bf5-4089-9572-273cdff1d3a5" />

<img width="650" height="328" alt="image" src="https://github.com/user-attachments/assets/0cbaa5ba-e021-4779-9f6f-bdb75f9e8aea" />

<img width="433" height="460" alt="image" src="https://github.com/user-attachments/assets/e8319bd8-6d39-4ec2-8a64-00e026292107" />

<img width="202" height="283" alt="image" src="https://github.com/user-attachments/assets/2266634d-64d9-4c29-94b2-b72a4741d3ed" />

### Veri Ön İşleme
> - *Eksik veri bulunmamaktadır.*
> - *Aykırı değerlerin tespiti ve işlenmesi*
> - *Aykırı değerler özellikle kolesterol ve kan basıncı değişkenlerinde gözlenmiştir ancak doğal sağlık durumu göstergesi olabileceğinden çıkarılmamıştır.*
> - *Kategorik değişkenler H2O platformunda model için uygun şekilde faktöriyel (kategori) tipe dönüştürülmüştür.*

### Görselleştirmeler
HeartDisease hedef değişkenin dağılımı dengeli ve model için uygundur.

<img width="583" height="577" alt="image" src="https://github.com/user-attachments/assets/0a759ef4-8c39-4fad-ac7e-d0000bed998e" />

Korelasyon matrisi ile değişkenler arası ilişkiler analiz edilmiş; yaş ve maksimum kalp atış hızı arasında negatif korelasyon gözlenmiştir.

<img width="822" height="747" alt="image" src="https://github.com/user-attachments/assets/f59ac47d-6753-4108-9236-be5e39fac545" />

Kutu grafiklerle aykırı değerler ve veri dağılımları gösterilmiştir.

<img width="994" height="595" alt="image" src="https://github.com/user-attachments/assets/c390ac3d-39c8-43d1-9a55-5d9d1a114d43" />

### Öznitelik İlişkileri
> *Sayısal değişkenler arasında yüksek korelasyon bulunmamakla birlikte, bazı düşük-orta seviyede ilişkiler tespit edilmiştir.*
<img width="822" height="747" alt="image" src="https://github.com/user-attachments/assets/f59ac47d-6753-4108-9236-be5e39fac545" />

## Makine Öğrenmesi Uygulaması
### Kullanılan Yöntem
> *Bu projede, H2O.ai kütüphanesinin AutoML (Automated Machine Learning) modülü kullanılarak sınıflandırma problemi çözülmüştür. AutoML, farklı makine öğrenmesi algoritmalarını belirli parametreler altında otomatik olarak deneyerek en iyi performans göstereni seçmeyi sağlamaktadır. AutoML süreci içerisinde H2O şu algoritmaları otomatik olarak değerlendirmiştir; Gradient Boosting Machine (GBM), XGBoost, Random Forest, Deep Learning (Çok katmanlı sinir ağı), GLM (Genelleştirilmiş Doğrusal Model), Stacked Ensemble (birden fazla modelin çıktısını birleştiren topluluk yöntemi).*

### Modeller ve Parametreler
Model eğitimi sırasında veri, %80 eğitim ve %20 test olacak şekilde ayrılmıştır. Hedef değişken (HeartDisease) H2OFrame ortamında kategorik (asfactor()) yapılmıştır. Eğitim sonrası AutoML, en iyi performansı gösteren modeli otomatik olarak belirlemiştir. Bu projede en iyi model, yüksek doğruluk (%88.95) ve mükemmel precision/recall (%100) değerlerine ulaşan bir Stacked Ensemble modeli olmuştur. Bu model, diğer modellerin çıktılarından öğrenerek nihai tahmin yapan bir topluluk modelidir.

<img width="437" height="78" alt="image" src="https://github.com/user-attachments/assets/d385ccb0-9a5d-42ca-a0c3-910a92e3bde7" />

En fazla 10 farklı modelin denenmesi istenmiştir. Tekrarlanabilirlik için rastgele sayı üretiminde kullanılan sabit değer (seed) 1 seçilmiştir.

<img width="771" height="366" alt="image" src="https://github.com/user-attachments/assets/d896a9cd-55e6-482d-959e-34080a040d4f" />

Bu tablo, H2O AutoML tarafından oluşturulan model sıralama (leaderboard) tablosudur. Otomatik olarak eğitilen modellerin performans metriklerine göre en iyi modelden en zayıfa doğru sıralandığını göstermektedir.

### Model Değerlendirmesi
> *AutoML tarafından eğitilen modeller arasından en yüksek performansı gösteren model, StackedEnsemble_BestOfFamily modeli olmuştur. Bu model, birden fazla temel modelin çıktısını birleştirerek daha yüksek doğruluk ve daha düşük hata oranı sağlayan bir topluluk (ensemble) modelidir. Sınıflandırma modelinin başarımını değerlendirmek için çeşitli performans metrikleri kullanılmıştır.*

> Accuracy (Doğruluk): Modelin yaptığı doğru tahminlerin, toplam tahmin sayısına oranıdır. Tüm sınıflar için genel başarıyı ifade eder. Veri dengeli olduğu sürece güvenilir bir metriktir.
> 
> Precision (Kesinlik): Modelin pozitif olarak tahmin ettiklerinin ne kadarının gerçekten pozitif olduğunu ölçer. Yanlış pozitif sayısı düşükse precision değeri yüksektir.
>
> Recall (Duyarlılık): Gerçek pozitif vakaların ne kadarının doğru tahmin edildiğini gösterir.
>
> F1 Skoru: Precision ve recall’un harmonik ortalamasıdır. Birinin yüksek diğerinin düşük olduğu durumlarda ortalamadan daha dengeli bir sonuç verir.
>
> AUC (Area Under the ROC Curve): Modelin pozitif ve negatif sınıfları ne kadar iyi ayırabildiğini gösterir. 1.0 değeri mükemmel ayırma gücü, 0.5 değeri ise tamamen rastgele tahmin anlamına gelir.
>
> Log Loss (Logaritmik Kayıp): Modelin tahmin olasılıklarının ne kadar “emin” olduğunu ölçer. Düşük logloss, modelin hem doğru hem de emin tahminler yaptığını gösterir.
>
> RMSE ve MSE: Bu iki metrik, modelin hata büyüklüğünü ifade eder. RMSE (kök ortalama kare hata) ve MSE (ortalama kare hata) ne kadar düşükse, modelin tahminleri gerçek değerlere o kadar yakındır.

#### Metrikler
| Metrik | Değer |
|--------|-------|
| Accuracy | 0.8895 |
| Precision | 1.0 |
| Recall | 1.0 |
| F1 Skoru | 0.9009 |
| AUC | 0.9312 |
| LogLoss | 0.3236 |
| RMSE (Hata) | 0.3123 |

### Sonuçların Yorumlanması
> *Precision ve Recall’un 1.0 olması, özellikle kalp hastalığı gibi kritik bir problemde, modelin tüm hasta bireyleri doğru şekilde tespit ettiğini ve hiç yanlış pozitif üretmediğini göstermektedir. Accuracy (%88.95) çok yüksektir. Veri dengeli olduğu için bu değer yanıltıcı değildir. F1 Skoru, precision ve recall arasında mükemmel bir denge sağlandığını göstermektedir. AUC değeri 0.93, modelin pozitif ve negatif sınıfları ayırt etme konusunda oldukça başarılı olduğunu ortaya koyar. Logloss ve RMSE gibi hata metrikleri düşüktür; bu da modelin kararsız sınıflarda bile doğruya yakın tahminler yaptığı anlamına gelir. Model yüksek doğruluk ve mükemmel precision & recall değerleri ile başarılı bir sınıflandırma gerçekleştirmiştir. Hastaları kaçırmaması ve yanlış pozitif sayısının sıfır olması, modelin güvenilirliğini artırmaktadır. Model, kalp hastalığı tahmini için kullanılabilir düzeydedir. Ancak, modelin daha fazla veri ve farklı özelliklerle desteklenmesi ileride daha iyi performans sağlayabilir.*

## Sonuç ve Öneriler
> *H2O AutoML kullanarak kalp hastalığı tahmininde etkili bir model geliştirmiştir. Elde edilen sonuçlar tıbbi karar destek sistemlerinde kullanılabilir. Gelecekte; Veri seti büyütülüp çeşitlendirilerek, model hiperparametre ayarları optimize edilerek veya farklı makine öğrenmesi teknikleri denenerek sonuçlar değerlendirelebilir. Bu sayede modelin genellenebilirliği ve doğruluğu artırılabilir.*

## Kaynaklar

1. Kaggle Heart Failure Prediction Dataset: https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction
2. H2O.ai Documentation: https://docs.h2o.ai/h2o/latest-stable/h2o-docs/index.html
3. ChatGPT

## Ekler
### ipynb Proje Dosyası
> * proje dosyanızı (.ipynb) bu repoya yükleyiniz ve buradan referans veriniz.*

### Veri Seti Dosyası veya Bağlantısı
> *Kullandığınız veri setini bu repoya yükleyebilir veya bağlantısını burada paylaşabilirsiniz.*
>
> [Veri_Seti.csv](veri_seti.csv) veya [Veri Seti Bağlantısı](https://ornek-veri-seti-baglantisi.com)
