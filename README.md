# Power BI ile Çalışan Kaybı Analizi
Bu proje, IBM veri setini kullanarak bir işletmedeki çalışan kaybı (attrition) süreçlerini Power BI ile analiz etmek amacıyla hazırlanmıştır.
# Power BI ile Çalışan Kaybı Analizi
Bu proje, IBM veri setini kullanarak bir işletmedeki çalışan kaybı (attrition) süreçlerini Power BI ile analiz etmek amacıyla hazırlanmıştır.

# 1. Veri Kaynağı ve Hazırlık Süreci
Araştırmada kullanılan veri seti, IBM tarafından oluşturulan ve CC0 (Creative Commons Zero) lisansı ile kamuya sunulan HR Analytics Employee Attrition & Performance veri kümesidir. Bu veri seti; bir işletmedeki 1470 çalışana ait yaş, maaş, departman, iş tatmini ve fazla mesai gibi 35 farklı özniteliği detaylı bir şekilde içermektedir. Veri seti yapısal olarak eksiksiz ve analize hazır bir formatta temin edildiği için kapsamlı bir veri temizleme veya satır silme işlemi yapılmasına gerek duyulmamıştır.

# 2. Veri Modelleme
Bu çalışma kapsamında, verilerin analiz edilebilirliğini artırmak ve Power BI üzerinde performanslı bir raporlama yapısı kurabilmek amacıyla “Yıldız Şeması" mimarisi tercih edilmiştir. Modelin merkezinde EmployeeAttrition tablosu yer almaktadır. Bu tablo, çalışmaya konu olan çalışan kaybı (attrition) verilerini ve temel performans göstergelerini barındıran Fact tablosudur. Çevresinde ise Dim_Employee, Dim_Job, Dim_Survey, Dim_WorkConfig ve Dim_Education gibi dimension tabloları bulunmaktadır. Dim_Job, Dim_Survey, Dim_WorkConfig ve Dim_Education gibi boyut tabloları ile ana tablo olan EmployeeAttrition arasında bire-çok (1:*) ilişkiler kurulmuştur. Dim_Employee tablosu ile ana tablo arasında bire-bir (1:1) bir ilişki tercih edilmiştir. 

# 3. KONUYA AİT GRAFİKLER VE RAPORLAR
  # 3.1. Genel Bakış:

  ![alt text](image.png)

  Aşağıda kullanılan her bir görselin amacı, teknik altyapısı ve iş analizi yer almaktadır:
1.	Toplam Çalışan Sayısı (KPI Kartı): Bu gösterge, şirketin sahip olduğu toplam çalışan sayısını görmek ve diğer oranların hesaplanmasında temel değer olarak kullanmak amacıyla oluşturulmuştur. Şirkette aktif ve pasif olmak üzere toplam 1470 benzersiz çalışan bulunmaktadır. Bu sayı, yapılan analizlerin sağlıklı sonuçlar vermesi için yeterli bir veri setine sahip olduğumuzu göstermektedir.

Toplam Personel Sayısı = DISTINCTCOUNT(EmployeeAttrition[EmployeeNumber])

2.	Ayrılan Personel Sayısı (KPI Kartı): Belirli dönem içerisinde işten ayrılan çalışanların toplam sayısını göstermek amacıyla hazırlanmıştır. Attrition durumu “Yes” olan çalışanlar dikkate alınmış ve toplamda 237 kişinin işten ayrıldığı görülmüştür. Bu sayı, şirket için dikkate alınması gereken bir çalışan kaybını ifade etmektedir.

Ayrılan Sayısı = CALCULATE(COUNTROWS('EmployeeAttrition'), 'EmployeeAttrition'[Attrition] = "Yes")

3.	Gerçekleşen Ayrılma Oranı ve Hedef Karşılaştırması (Gösterge Grafiği): Bu görselde, gerçekleşen çalışan ayrılma oranı ile şirket tarafından belirlenen %10’luk hedef oran karşılaştırılmıştır. Mevcut ayrılma oranı %16,12 olarak hesaplanmıştır. Bu durum, hedeflenen oranın oldukça üzerinde olup çalışan bağlılığı konusunda iyileştirme yapılması gerektiğini göstermektedir.

Ayrılma Oranı = DIVIDE([Ayrılan Sayısı], [Toplam Personel Sayısı], 0) 

4.	Cinsiyete Göre Ayrılma Oranları (Pasta Grafiği): Bu analizde, işten ayrılan çalışanların cinsiyete göre dağılımı incelenmiştir. Sonuçlara göre ayrılan çalışanların %63,29’u erkek, %36,71’i kadın çalışanlardan oluşmaktadır. Bu durum, erkek çalışanlarda işten ayrılma oranının daha yüksek olduğunu göstermektedir.

Cinsiyet Adı = IF('Dim_Employee'[Gender] = "Male", "Erkek", "Kadın")

Ayrılan Sayısı = CALCULATE(COUNTROWS('EmployeeAttrition'), 'EmployeeAttrition'[Attrition] = "Yes")

5.	Pozisyona Göre Ayrılan Personel Sayısı (Sütun Grafiği): Bu grafikte, hangi pozisyonlarda çalışan kaybının daha fazla olduğu gösterilmiştir. Özellikle Laboratuvar Teknisyeni ve Satış Yöneticisi pozisyonlarında ayrılma sayısının yüksek olduğu görülmektedir. Satış Yöneticisi gibi önemli pozisyonlarda yaşanan kayıplar, şirketin performansını ve ekip yapısını olumsuz etkileyebilir.

Ayrılan Sayısı = CALCULATE(COUNTROWS('EmployeeAttrition'), 'EmployeeAttrition'[Attrition] = "Yes")

6.	Departman Filtresi (Dilimleyici / Slicer): Bu dilimleyici, raporun daha interaktif kullanılmasını sağlamak amacıyla eklenmiştir. Kullanıcı, Ar-Ge, İnsan Kaynakları veya Satış gibi departmanları seçerek sayfadaki tüm metrikleri sadece seçilen departmana göre inceleyebilmektedir. 
7.	Sayfa Navigasyonu (Düğmeler): Rapor içerisinde yer alan düğmeler, kullanıcıların sayfalar arasında hızlı ve kolay bir şekilde geçiş yapmasını sağlamak amacıyla eklenmiştir. Bu sayede raporun kullanımı daha pratik ve anlaşılır hale getirilmiştir.

  # 3.2. Demografik Analiz:

  ![alt text](image-1.png)

  Aşağıda kullanılan her bir görselin amacı, teknik altyapısı ve iş analizi yer almaktadır:

1.	Yaş Ortalaması ve Ortalama Hizmet Süresi (KPI Kartları): Bu KPI kartları, şirket genelindeki çalışanların yaş ortalamasını ve şirkette ne kadar süredir çalıştıklarını göstermek amacıyla hazırlanmıştır. Yaş ortalamasının 36,92 olması, şirketin hem dinamik hem de belirli bir tecrübeye sahip bir çalışan profiline sahip olduğunu göstermektedir. Ortalama hizmet süresinin 7,01 yıl olması ise çalışanların şirkete orta ve uzun vadede bağlı kaldığını göstermektedir.

Ortalama Yas = AVERAGE('Dim_Employee'[Age])
Ortalama Kidem = AVERAGE('EmployeeAttrition'[YearsAtCompany])

2.	Departmanlara Göre Personel Dağılımı (Treemap / Ağaç Haritası): Bu görsel, çalışanların departmanlara göre nasıl dağıldığını alan büyüklükleri üzerinden göstermektedir. Böylece personel yoğunluğunun hangi alanlarda daha fazla olduğu kolayca anlaşılabilmektedir. Görselde Yaşam Bilimleri ile Tıp / Sağlık departmanlarının en büyük alanları kapladığı görülmektedir. Bu durum, şirketin ana faaliyet alanlarının bu iki departman etrafında şekillendiğini ve insan kaynağının büyük kısmının bu alanlarda toplandığını göstermektedir.

Toplam Personel Sayısı = DISTINCTCOUNT(EmployeeAttrition[EmployeeNumber])

3.	Eğitim Düzeyine Göre Personel Dağılımı (Çubuk Grafik): Bu grafik, şirket çalışanlarının eğitim seviyelerine göre dağılımını analiz etmek amacıyla oluşturulmuştur. En kalabalık grubun 572 kişi ile Lisans mezunları olduğu görülmektedir. Lisans mezunlarını 398 kişi ile Yüksek Lisans mezunları takip etmektedir. Bu dağılım, şirketin genel olarak eğitim seviyesi yüksek bir çalışan profiline sahip olduğunu göstermektedir.
4.	Kıdem Gruplarına Göre Personel Dağılımı (Halka Grafik): Bu görselde çalışanlar, sadece yıl bazında değil belirli kıdem grupları altında sınıflandırılmıştır. Çalışanların %51,84’ü (762 kişi) “Deneyimli (3–9 Yıl)” grubunda yer almaktadır. Bu durum, şirketin ana iş gücünü orta seviye deneyime sahip çalışanların oluşturduğunu göstermektedir. Yeni başlayanların oranı (%23,27) ile kıdemli çalışanların oranının (%24,9) birbirine yakın olması, şirket içinde dengeli bir tecrübe dağılımı ve bilgi aktarımı potansiyeli olduğunu göstermektedir.

Kıdem Grubu =  IF(EmployeeAttrition[YearsAtCompany] < 3, "Yeni Başlayan (0-2 Yıl)", IF(EmployeeAttrition[YearsAtCompany] < 10, "Deneyimli (3-9 Yıl)",  "Kıdemli (+10 Yıl)") )

Toplam Personel Sayısı = DISTINCTCOUNT(EmployeeAttrition[EmployeeNumber])


5.	Sayfa Navigasyonu (Düğmeler): Rapor içerisinde yer alan düğmeler, kullanıcıların sayfalar arasında hızlı ve kolay bir şekilde geçiş yapmasını sağlamak amacıyla eklenmiştir. Bu sayede raporun kullanımı daha pratik ve anlaşılır hale getirilmiştir.

  # 3.3. Finansal Etki ve Performans:

  ![alt text](image-2.png)

  Aşağıda kullanılan her bir görselin amacı, teknik altyapısı ve iş analizi yer almaktadır:
1.	En Yüksek Maaşlı 10 Çalışanın Toplam Maliyeti (KPI Kartı): Şirketin en yüksek maliyetli (ve muhtemelen en kıdemli) çalışan grubunun toplam finansal hacmini saptamak. İlk 10 çalışanın aylık toplam maliyetinin 198,68 bin (B) birim olduğu görülmektedir. Bu grup, şirketin en büyük yetenek yatırımıdır ve bu kişilerin kaybı finansal açıdan en yüksek riski temsil eder.

Top 10 Personel Maas Maliyeti = CALCULATE( SUM('EmployeeAttrition'[MonthlyIncome]), TOPN(10, 'EmployeeAttrition', 'EmployeeAttrition'[MonthlyIncome], DESC ))

2.	Yüksek Performanslı Personel Maliyeti (KPI Kartı): Hem yüksek performans gösteren (Rating >= 3) hem de yüksek maaş alan (MonthlyIncome > 10.000) "yıldız çalışan" grubunun toplam maliyetini izlemek. Şirketin toplam 4,17 Milyon (M) birimlik maaş yükü, performans notu yüksek olan nitelikli çalışanlara gitmektedir. Bu, şirketin performans odaklı bir ücretlendirme politikası izlediğinin bir göstergesidir.

Yüksek Performans Yüksek Maaş Maliyeti = SUMX( FILTER( EmployeeAttrition, EmployeeAttrition[MonthlyIncome] > 10000 && RELATED(Dim_Survey[PerformanceRating]) >= 3 ), EmployeeAttrition[MonthlyIncome] )

4.	Kıdem Yılı ve Aylık Gelir Dağılımı (Çizgi Grafiği): Kıdem süresi (Years at Company) arttıkça gelirin nasıl değiştiğini ve bu değişimde ayrılan (Yes) ve kalan (No) personelin farkını görmek. Grafikteki keskin zirveler (özellikle 10. ve 20. yıllar), şirketteki belirli terfi/zam dönemlerini işaret etmektedir. Dikkat çekici olan bulgu; kalan personelin (Kırmızı koyu çizgi) gelir seviyesinin, ayrılan personele göre çok daha yüksek zirvelere ulaşmasıdır. Düşük maaş artışı, kıdemli çalışanların ayrılma kararında tetikleyici bir unsur olabilir.

5.	Rol Bazlı Maaş Ortalaması ve Ayrılma Sayıları (Sütun ve Çizgi Grafiği): Unvan bazlı ayrılma sayıları ile o unvandaki ortalama gelir arasındaki ilişkiyi kıyaslamak. "Yönetici" (Manager) ve "Ar-Ge Direktörü" pozisyonlarında maaş ortalaması en yüksek seviyedeyken ayrılma sayıları minimumdadır. Buna karşın, maaş ortalaması düşük olan "Laboratuvar Teknisyeni" ve "Satış Temsilcisi" rollerinde ayrılma sayıları zirve yapmaktadır. Bulgu: Düşük gelir düzeyi ile yüksek ayrılma oranı arasında ters yönlü güçlü bir ilişki vardır.

Ortalama Gelir = AVERAGE('EmployeeAttrition'[MonthlyIncome])

Ayrılan Sayısı = CALCULATE(COUNTROWS('EmployeeAttrition'), 'EmployeeAttrition'[Attrition] = "Yes")

6.	Hisse Senedi Opsiyon Seviyesine Göre Ayrılma (Huni Grafiği): Yan hakların (hisse opsiyonu) çalışan kaybını engellemedeki başarısını ölçmek. En yüksek ayrılma (154 kişi), 0 - Yok (Hisse Verilmemiş) kategorisinde gerçekleşmiştir. Hisse opsiyon seviyesi arttıkça ayrılma sayılarının dramatik şekilde düştüğü görülmektedir (Seviye 2 ve 3'te sadece 12-15 kişi). Öneri: Çalışanları tutundurmak için hisse opsiyonu gibi uzun vadeli teşvikler oldukça etkilidir.

Ayrılan Sayısı = CALCULATE(COUNTROWS('EmployeeAttrition'), 'EmployeeAttrition'[Attrition] = "Yes")

7.	Sayfa Navigasyonu (Düğmeler): Rapor içerisinde yer alan düğmeler, kullanıcıların sayfalar arasında hızlı ve kolay bir şekilde geçiş yapmasını sağlamak amacıyla eklenmiştir. Bu sayede raporun kullanımı daha pratik ve anlaşılır hale getirilmiştir.

  # 3.4. Çalışma Ortamı ve Memnuniyet:

  ![alt text](image-3.png)

  Aşağıda kullanılan her bir görselin amacı, teknik altyapısı ve iş analizi yer almaktadır:
1.	Pozisyon Bazlı Performans Dağılımı (Matris Tablo): İşten ayrılan 237 personelin performans düzeylerini unvan bazında detaylandırmak. Ayrılanlar arasında 200 kişinin "İyi" (3), 37 kişinin ise "Üstün" (4) performans notuna sahip olduğu görülmektedir. Özellikle Laboratuvar Teknisyeni ve Satış Yöneticisi rollerindeki yüksek performanslı kayıplar, şirketin nitelikli iş gücünü tutundurmada zorlandığını kanıtlamaktadır. Şirket sadece çalışan kaybetmemekte, aynı zamanda "yıldız" olarak nitelendirilebilecek personellerini de kaybetmektedir.

Ayrilan Sayisi = 
CALCULATE(
    COUNTROWS('EmployeeAttrition'),
    'EmployeeAttrition'[Attrition] = "Yes"
)

2.	Fazla Mesainin Ayrılma Üzerindeki Etkisi (Halka Grafik): Yoğun çalışma temposunun (Overtime) istifalar üzerindeki etkisini ölçmek. İşten ayrılanların %53,59’u (127 kişi) düzenli olarak fazla mesai yapan personellerdir. Bu veri, fazla mesainin çalışan tükenmişliği (burnout) üzerinde doğrudan etkili olduğunu ve ayrılma kararını tetikleyen majör bir faktör olduğunu göstermektedir.

Ayrilan Sayisi = 
CALCULATE(
    COUNTROWS('EmployeeAttrition'),
    'EmployeeAttrition'[Attrition] = "Yes" )

3.	İş-Yaşam Dengesi ve Çalışan Kaybı İlişkisi (Yığılmış Çubuk Grafik): Çalışanların iş ve özel hayat arasındaki dengeyi nasıl algıladıklarını ve bunun bağlılığa etkisini görmek. En yüksek çalışan hacmi "3 - Çok İyi" seviyesinde toplansa da, iş-yaşam dengesi "Kötü (1)" ve "İyi (2)" olan gruplarda ayrılma oranlarının (pembe alanlar) belirgin olduğu görülmektedir. Çalışanların büyük bir kısmının bu dengeyi orta-üst seviyede görmesi olumludur, ancak "Mükemmel (4)" seviyesindeki kişi sayısının azlığı iyileştirme alanı olduğunu gösterir.

Toplam Personel Sayısı = DISTINCTCOUNT(EmployeeAttrition[EmployeeNumber])

4.	Ev-İş Arası Mesafe ve Ayrılma Oranları (Gruplandırılmış Sütun Grafik): Ulaşım süresinin ve mesafenin çalışan sadakati üzerindeki etkisini analiz etmek. Beklenenin aksine, en çok ayrılma 1 - Yakın (0-10 Km) mesafe grubunda yaşanmıştır. Bu durum, yakın mesafede yaşayan çalışanların bölgedeki rakip firmalara geçiş yapmasının daha kolay olabileceğini veya mesafeden ziyade iş içeriğinin daha etkili olduğunu düşündürmektedir. Uzak mesafede (21+ Km) çalışanların sayısı az olsa da, bu gruptaki "Ayrılan/Kalan" oranı dikkatle izlenmelidir.

5.	Sayfa Navigasyonu (Düğmeler): Rapor içerisinde yer alan düğmeler, kullanıcıların sayfalar arasında hızlı ve kolay bir şekilde geçiş yapmasını sağlamak amacıyla eklenmiştir. Bu sayede raporun kullanımı daha pratik ve anlaşılır hale getirilmiştir.

  # 3.5. Risk Analizi ve Gelecek Öngörüsü:

  ![alt text](image-4.png)

  Aşağıda kullanılan her bir görselin amacı, teknik altyapısı ve iş analizi yer almaktadır:
1.	Yüksek Riskli Personel Sayısı ve Tahmini Kayıp Maliyeti (KPI Kartları): Henüz ayrılmamış ancak ayrılma potansiyeli çok yüksek olan çalışan sayısını ve bu kişilerin kaybının yıllık toplam maliyetini saptamak. Şirkette aktif olarak çalışan 123 personelin "Yüksek Risk" grubunda olduğu saptanmıştır. Eğer bu risk gerçekleşirse, şirketin yıllık tahmini kaybı 9,60 Milyon (M) birim olacaktır. Bu rakam, tutundurma politikalarına ayrılacak bütçenin ne kadar kritik olduğunu rakamsal olarak kanıtlar.

Yüksek Riskli Personel Sayısı = CALCULATE( COUNT('EmployeeAttrition'[EmployeeNumber]),  'EmployeeAttrition'[Attrition] = "No", 
FILTER( 'EmployeeAttrition', 'EmployeeAttrition'[MonthlyIncome] < 3500 && RELATED('Dim_Survey'[JobSatisfaction]) <= 2) )

Tahmini Kayip Maliyeti = [Yüksek Riskli Personel Sayısı] * [Ortalama Gelir] * 12 

2.	Departman Bazlı Maaş ve Yoğunluk Analizi (Üst Tablo): Departmanlar arasındaki maaş hiyerarşisini ve personel dağılımını kıyaslayarak bütçe yükünü analiz etmek. Ar-Ge departmanı 961 çalışanla en yüksek yoğunluğa ve 1. sırada maaş sıralamasına sahiptir. Satış departmanının 446 çalışanı olmasına rağmen 2. sırada yer alması, birim başına düşen maliyetin yüksekliğini göstermektedir.

Departman Maaş Sıralaması = RANKX( ALL(Dim_Job[Departman Adı]), CALCULATE(SUM(EmployeeAttrition[MonthlyIncome])), 
, 
DESC )

Ortalama Gelir = AVERAGE('EmployeeAttrition'[MonthlyIncome])

Toplam Personel Sayısı = DISTINCTCOUNT(EmployeeAttrition[EmployeeNumber])

3.	Bireysel Risk Takip Listesi (Alt Tablo): Hangi çalışanın (Personel No bazlı) hangi unvanda olduğu, maaşı ve memnuniyet düzeyini bir arada görerek "nokta atışı" aksiyon alabilmek. Tabloda özellikle kırmızı (1) ve turuncu (2) simgeyle gösterilen çalışanlar, acil odaklanılması gereken kişilerdir. Örneğin; 10 numaralı personelin "Laboratuvar Teknisyeni" olduğu, 2670 birim maaş aldığı ve memnuniyetinin en düşük seviyede (1) olduğu görülmektedir. Bu liste, HR yöneticisi için bir "müdahale listesi" niteliğindedir.

4.	Pozisyon Seçici (Dilimleyici Kutuları): Analizi belirli bir unvan (örneğin sadece "Satış Temsilcisi") özelinde daraltarak o pozisyondaki finansal riski incelemek. Sayfanın sol altındaki pozisyon düğmeleri sayesinde, tüm risk tablosu ve maliyet kartları dinamik olarak değişmektedir.
5.	Sayfa Navigasyonu (Düğmeler): Rapor içerisinde yer alan düğmeler, kullanıcıların sayfalar arasında hızlı ve kolay bir şekilde geçiş yapmasını sağlamak amacıyla eklenmiştir. Bu sayede raporun kullanımı daha pratik ve anlaşılır hale getirilmiştir.

# 4. Kritik Bulgular ve Analiz Sonuçları
* Hedef Sapması: İşletmedeki %16,12’lik çalışan ayrılma oranı, şirketin maksimum %10 olarak belirlediği kritik eşiği aşmış durumdadır.

* Kurumsal Hafıza Kaybı: Toplamda 237 nitelikli personelin kaybedilmesi, hem ekonomik maliyet hem de ciddi bir kurumsal tecrübe kaybı yaratmıştır.

* Yetenek Yönetimi Paradoksu: Ayrılan personelin tamamının yüksek performanslı (200'ü "İyi", 37'si "Üstün") olması, şirketin en üretken iş gücünü rakiplerine kaptırdığını kanıtlamaktadır.

* Ücret ve Yan Hak Etkisi: Laboratuvar Teknisyenleri gibi düşük maaşlı rollerde ayrılma oranı zirve yaparken; hisse senedi opsiyonu alan çalışanlarda sadakatin çok daha yüksek olduğu saptanmıştır.

* İş-Yaşam Dengesi (Tükenmişlik): İşten ayrılanların %53,59'unun düzenli fazla mesai yapan grupta olması, fazla mesainin çalışan tutundurma üzerindeki negatif etkisini netleştirmiştir.

* Finansal Risk Projeksiyonu: Mevcut verilerle saptanan 123 yüksek riskli personelin ayrılması durumunda, işletmenin 9,60 Milyonluk bir mali yükle karşılaşacağı öngörülmektedir.

