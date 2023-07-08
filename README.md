# CT_lung_detection

# Akciğer BT Görüntüleri ile Segmentasyon Yapımı 
Bu projenin amacı BT görüntülerinden akciğeri segmente ederek direkt olarak ilgi alnı haline getirerek yapay zeka nın odak alanın akciğerler olmasını sağlayarak modelin daha iyi eğitilmesini kolaylaştırır.

Bu projede her bir hastanın akciğer görüntüleri ile Segmentesyon yaparak 3D görüntüler elde edilmesi amaçlanmaktadır. Öncelikle DICOM formatındaki datanın nasıl ele alınacağını sonrasında Akciğer BT görüntülerine bu öğrenilen yöntemlerle segemnetasyonu gözlemlenecektir. Bu projenin devamında da 3 boyutlu dataları derin ağ mimarileri yardımıyla eğitilerek kanser teşhisinde yardımcı destek mekanizması oluşturulması planlanmaktadır.

### DICOM

DICOM, tıbbi görüntüleme sistemlerinin ekmek kapısıdır. Biyomedikal Mühendisi, sağlık hizmetleri alanında BT Uzmanı veya Sağlık Hizmetleri Veri Bilimcisi/Analistiyseniz, tıbbi görüntüleme sistemleriyle ilgili her yerde olduğu için muhtemelen DICOM'u kullanmış veya en azından duymuşsunuzdur.

DICOM, Tıpta Dijital Görüntüleme ve İletişim, örneğin; BT, MRI, Ultrason vb. birden fazla üretici arasında, böylece DICOM uyumlu olan tüm tıbbi makineler bir ağ üzerinden bilgi gönderirken aynı dili konuşabilir.

DICOM dosyaları genellikle yalnızca piksel verilerinden başka bilgilere sahiptir. DICOM Standartları, DICOM dosyalarında depolanan verileri standart hale getirmek için bir dizi öznitelik sağlar. Her öznitelik, sabit bir değer temsiliyle belirli bir veri türüne (ör. dize, tamsayı, kayan nokta vb.) sahiptir. Bu niteliklere meta veri denir. DICOM meta verisi örnekleri:

* Hastayla ilgili özellikler: isim, yaş, cinsiyet, vb.
* Modalite ile ilgili özellikler: modalite (CT, MRI, Ultrason, vb.), üretici, satın alma tarihi vb.
* Görüntüyle ilgili nitelikler: şekil, örnekleme, en boy oranı, piksel verileri vb.


> Not:  Bahsettiğimiz görüntüyle ilgili özniteliklerin, tıbbi görüntüler üzerinde gerçek dünya hesaplamalarını uygulamak için yararlı olduklarından anlaşılması çok önemlidir. Fakat bahsedeceğimiz büyük ölçüde güveneceğiz.

DICOM dosyalarını karakterize edebilecek düzinelerce özellik vardır. Yani hepsini okunamaktadır. Yalnızca DICOM ile ilgili bir şey üzerinde çalışırken karşılaşabileceğiniz niteliklere odaklanmak gerekir. Bu amaçla, Innolitics tarafından oluşturulmuş bu harika DICOM Standart Tarayıcısını şiddetle tavsiye edilir, sadece öğrenmek istediğiniz özelliği aranır.
