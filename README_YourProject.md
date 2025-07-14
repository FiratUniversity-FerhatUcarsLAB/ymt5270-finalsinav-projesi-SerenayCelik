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
> *Öznitelikler arasındaki ilişkileri analiz ediniz. Korelasyon matrisi, scatter plot matrisi gibi görsellerle destekleyiniz.*

## Makine Öğrenmesi Uygulaması
### Kullanılan Yöntem
> *Veri setinize uyguladığınız makine öğrenmesi yöntemini (sınıflandırma, regresyon veya kümeleme) belirtiniz ve neden bu yöntemi seçtiğinizi açıklayınız.*

### Modeller ve Parametreler
> *Denediğiniz modelleri ve kullandığınız parametreleri açıklayınız. Orange'da yapılandırdığınız widget ayarlarını ekran görüntüleri ile destekleyebilirsiniz.*

### Model Değerlendirmesi
> *Uyguladığınız modelin performansını değerlendiriniz. Kullandığınız değerlendirme metriklerini açıklayınız.*

#### Metrikler
| Metrik | Değer |
|--------|-------|
| Örnek Metrik 1 | 0.85 |
| Örnek Metrik 2 | 0.78 |
| ... | ... |

### Sonuçların Yorumlanması
> *Elde ettiğiniz sonuçları detaylı bir şekilde yorumlayınız. Modelin güçlü ve zayıf yönleri nelerdir? Başka hangi modeller denenebilirdi?*

## Sonuç ve Öneriler
> *Projenizin genel bir değerlendirmesini yapınız. Elde ettiğiniz sonuçlar hakkında çıkarımlarınızı ve gelecek çalışmalar için önerilerinizi yazınız.*

## Kaynaklar
> *Proje boyunca yararlandığınız kaynakları (makaleler, web siteleri, videolar, vb.) buraya ekleyiniz.*

1. Kaynak 1
2. Kaynak 2
3. ...

## Ekler
### ipynb Proje Dosyası
> * proje dosyanızı (.ipynb) bu repoya yükleyiniz ve buradan referans veriniz.*

### Veri Seti Dosyası veya Bağlantısı
> *Kullandığınız veri setini bu repoya yükleyebilir veya bağlantısını burada paylaşabilirsiniz.*
>
> [Veri_Seti.csv](veri_seti.csv) veya [Veri Seti Bağlantısı](https://ornek-veri-seti-baglantisi.com)
