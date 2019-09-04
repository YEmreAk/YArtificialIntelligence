# Model Eğitim Süreci

## Verileri Hazırlama

### Veriler Aynı Dağıtımdan Geliyorsa

* `train`, `dev` ve `test` şeklinde 3 parçaya ayır
* Çok fazla veri varsa `dev` ve `test`'e belli bir sınırdan fazla resim konulmaz
  * Örn: 1M resim için `%98 %2 %2` \(max 20K resim\)
* Veri miktarı az ise `%60 %20 %20` şeklinde olur

### Veriler Farklı Dağıtımdan Geliyorsa

* Asıl odaklanan resimlerin %80'i train aşamasına aktarılmalı
* Geri kalanı dev ve test alanına paylaştırılmalıdır
* Ardından veriler karıştırılmalıdır

> ⚠ Tüm verileri karıştırırsak odaklı olan verileri kaybederiz, hazır resimlerin gelme oranı artarü bu sebeple karıştırmayı en sonda yapıyoruz.

## Eğitim

* Basit bir model oluştur ve hemen eğit
  * ML yapısı çokça tekrarlı eğitimlerle ilerleyen bir yapıdır
* Eğer **veri sayısı az** ise `transfer learning` yöntemi kullanılır

### Transfer Learning

* Daha önceden benzer bir model eğitimi var ise \(`pre-trained-model`\) eğitilmiş modelin `weight` ve `bias` değerleri kullanılır
  * Model `feature map`i etkili bir şekilde ortaya çıkarmıştır, baştan ortaya çıkarmaya gerek yoktur
* `pre-trained-model` ile yeni modelin ortak özellikleri tanıma amacı olması lazım
  * Örn: 2'si de resim algılayacak. 1'i resim 1'i ses ise bilgi aktarımı yapılamaz.
* `low-level feature`'lar olduğu gibi kullanılır
* Sadece; son katman ve x, y değerleri güncellenir

## Hata Analizleri

* _Error analysis_ uygulanır
  * Çok fazla veriye bakmak yerine makul miktarda bakılır
  * Hatalı olan kümeye uygulanır

## Yanlış Etiketlenmiş Veriler

* Az ise üzerlerinde uğraşmaya deymez
  * Sinir ağları, rastgele hatalara karşı dayanıklıdır
* Çok fazla var ise düzeltme işlemi yapılmalıdır

### Yanlış Etiketleri Düzeltme

* `dev` ve `test` kümelerinin her ikisi de güncellenir
  * Şans eseri, yanlış olanlar doğru etiketlenmiş olabilir. Yeni eğitimde yanlış etiketlenirler
  * `dev` ve `test` verisi aynı veri dağıtımdan gelmelidir
* `train` içerisindeki verilerin tamamını kontrol etmemize gerek yoktur
  * Geçen vakte yazık 😢

