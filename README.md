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


## Bu çalışmanın bu kısmında şunları tartışacağız:

* DICOM dosyalarını ImageIO kullanarak okuyun.
* DICOM öznitelikleri, Meta veriler.
* Belirli bir DICOM özniteliğine erişin.
* Matplotlib paketi kullanılarak görüntü gösterimi.
* Birden fazla dilimi istifleyin ve okuyun.
* Piksel Aralığını, Şekli, Dilim Kalınlığını, En Boy Oranını ve görüş alanını anlayın.
* Ipywidgets kullanarak eksenel, koronal ve sagital düzlemler boyunca etkileşimli bir görüntü temsili oluşturun.


## Hadi Başlayalım

Öncelikle gerekli paketleri import edelim. 
* ImageIO = DICOM dosyalarıyla başa çıkmak için
* NumPy = Piksel verileri bir NumPy dizisi olarak okunurken
* matplotlib = görüntüleri görselleştirmek için 
* Ipywidgets = çoklu görüntü dilimleri arasında gezinmek için kullanabileceğimiz etkileşimli bir kaydırıcı oluşturmak için de kullanılıcaktır.


### DICOM Dosyalarını Okuma
ImageIO paketinden (.imread) kullanarak bir DICOM dosyasını kolayca okuyabilir ve bir değişkende saklayabiliriz.


### DICOM Nitelikleri
(.meta) kullanıldığında, bu DICOM dosyasının özniteliklerini, meta verilerini içeren bir sözlük çıkarır.


### The Attributes of the DICOM File
Meta veriler bir sözlük olarak saklandığından, DICOM dosyasının anahtarlarını, niteliklerin adlarını gösterir:
im.meta.keys()

Results: 
odict_keys(['TransferSyntaxUID', 'SOPClassUID', 'SOPInstanceUID', 'StudyDate', 'SeriesDate', 'AcquisitionDate', 'ContentDate', 'StudyTime', 'SeriesTime', 'AcquisitionTime', 'ContentTime', 'Modality', 'Manufacturer', 'StudyDescription', 'SeriesDescription', 'PatientName', 'PatientID', 'PatientBirthDate', 'PatientSex', 'PatientAge', 'StudyInstanceUID', 'SeriesInstanceUID', 'SeriesNumber', 'AcquisitionNumber', 'InstanceNumber', 'ImagePositionPatient', 'ImageOrientationPatient', 'SamplesPerPixel', 'Rows', 'Columns', 'PixelSpacing', 'BitsAllocated', 'BitsStored', 'HighBit', 'PixelRepresentation', 'RescaleIntercept', 'RescaleSlope', 'PixelData', 'shape', 'sampling'])

> Not: Burada gördüğümüz öznitelikler, bu DICOM dosyasında yer alan özniteliklerin tamamı olmayabilir. Bunun nedeni, ImageIO'nun DICOM görüntülerini olabildiğince basit bir şekilde ele almasıdır. İsteğe bağlı bir okuma, ImageIO'nun desteklediği özniteliklerin sözlüğünü görmek için bu bağlantıyı kontrol etmektir.


### Belirli bir DICOM Özniteliğine Erişin
Belirli bir özniteliğe erişim için "Modality" kullanımı:


### Matplotlib Kütüphanesini Kullanarak Görüntü Temsili
Genellikle, "Pixel Data" özniteliği piksel değerlerine sahiptir:

Piksel değerleri bir NumPy dizisi olarak saklanır. NumPy, dizilerle ve bunların hızlı bir şekilde hesaplanmasıyla uğraşmak için uygundur. Şimdi piksel değerlerini gösterimi:

Pixel Data'nın neyi temsil ettiğini anladıktan sonra bu piksellerin görüntüsünü gösterimi için matplotlib kütüphanesinden yararlanılır.
