# Değişikliklerinizi Geri Almak
Git'in en güzel yanlarından biri de yaptığınız herhangi bir değişikliği kolayca geri alabilmemizi sağlamasıdır.
# Son Commit Bilgilerini Düzeltmek
Commit işlemlerinizi ne kadar dikkatli yaparsanız yapın bazen commit'e dahil etmeyi unuttuğunuz veya yanlışlıkla dahil ettiğiniz dosyalar olabilir veya commit mesajında eksik bilgi vermiş olabilirsiniz. Bu durumda son commit işleminizi yeniden yapmak için `git commit` komutunu --amend seçeneği ile kullanabilirsiniz. Sadece commit mesajınızı değiştirmek istiyorsanız `-- amend -m` seçenekleri ile git commit komutunu çalıştırabilirsiniz, eğer son commit'e dosya eklemek veya dosya çıkarmak isterseniz commit komutundan önce önceki bölümlerde de bahsettiğimiz `git add` ve `git rm` komutları ile önce Staging işlemini yapabilirsiniz.

# Local Değişiklikleri Geri Almak
Henüz commit etmediğimiz değişikliklere Local değişiklik denir. Bazen önceki halinden daha kötü olan kod yazabilirsiniz ve bu değişikliği geri almak isteyebilirsiniz. Bu gibi durumlarda değiştirdiğiniz halinden memnun olmadığınız dosyadaki değişiklikleri geri alıp dosyanın son commit edilmiş haline geri dönmek istediğinizde, önceki bölümlerde de sıkca kullandığımız, git checkout komutunu -- seçeneği ile çalıştırmanız yeterli olacaktır.
```sh
$ git checkout -- dosya1.md veya
$ git checkout -- klasor/dosya2.md şeklinde kullanabilirsiniz.
```
Tüm dosyalarda yaptığınız değişiklikleri geri almak istiyorsanız git reset komutunu --hard seçeneği ile kullanabilirsiniz

```sh
$ git reset --hard HEAD
```
Bu komut ile Git tüm dosyaların son commit edilen değişiklikleri içeren HEAD versiyonundaki hallerinin Working Copy'nize geri yükler.
git checkout -- ve git reset --hard komutları sonrasında kayıt altına alınmamış olan tüm değişiklikler geri dönüşü olmayacak şekilde yok olur. Bu nedenle bu komutları çalıştırırken dikkatli olmalısınız ve iki defa düşünmelisiniz.

# Commit Edilen Bir Değişikliği Geri Almak
Hatalı bir düzenleme yaptığınızda (ki bu genelde test edilmeden yapılan commit'ler sonrasında oluşan bir durumdur) veya geliştirdiğiniz bir özelliğin artık gerekli olmadığına karar verildiğinde yaptığınız değişikliği geri almanız gerekecektir.

`git revert` komutu commit ettiğiniz herhangi bir değişikliği geri almak için kullanılır. Bu komut ile commit işleminizin kendisi veya bilgileri silinmez sadece commit işleminizdeki değişiklik geri alınır. Örneğin eklediğiniz bir satırı kaldırmak isterseniz git revert komutu ile bunu yapabilirsiniz. Aslında git revert komutu değişikliğinizi geri almak için otomatik olarak yeni bir commit oluşturur ve geri alma işlemi bu commit sayesinde değişiklik tarihçesinde görünür hale gelir.

<img src="https://aliozgur.gitbooks.io/git101/content/ileri_seviye_komutlar_ve_islemler/01_git_revert.jpg" style="width:100%;">

Yukarıdaki ekran görüntüsünde ilk önce git revert komutunu çalıştırdık. Bu komutun en önemli parametresi geri almak istediğimiz commit'in hash değeri (hash'in ilk yedi karakterini kullanabiliriz). Komutu çalıştırdıktan sonra değişiklik tarihçesini incelediğimizde git'in otomatik olarak bir commit oluşturduğunu ve bu commit'in bilgilerinde hangi değişikliğin geri alındığına dair ayrıntıların yer aldığını görüyoruz.

Değişiklikleri geri almak için kullanabileceğimiz diğer bir komut ise git reset komutu. Bu komut da herhangi bir bilginizi silmeden işlemi gerçekleştirir, ancak git revert komutundan farklı olarak otomatik yeni bir commit üretmeden değişikliğinizi geri almanızı sağlar.


<img src="https://aliozgur.gitbooks.io/git101/content/ileri_seviye_komutlar_ve_islemler/02_git_reset.jpg" style="width:100%;">

Bu komut için de git revert komutunda olduğu gibi geri almak istediğimiz commit'in hash değerini veriyoruz. Kullandığımız diğer bir seçenek olan --hard seçeneği ise local tüm commitlerinizi silerek geri alma işleminin yapılmasına neden olur, bu nedenle --hard seçeneğini kulllanırken dikkatli olmalısınız. Local commit'lerinizin korunmasını istiyorsanız `--keep` komutunu kullanabilirsiniz.

# İki versiyon arasındaki farkları yorumlamak
Versiyon kontrol sistemlerinde iki versiyon arasındaki değişikliklere İngilizce difference (fark) kelimesinin kısaltması olan diff denir. Git'de iki versiyon arasındaki farkları görmek için git diff komutunu kullanabilirsiniz. Örneğin git diff 374c6f..5d903e dosya1.md komutu ile dosya1.md dosyasının 374c6f ve 5d903e hash'li commitlerdeki iki versiyonunun diff'ini alıyoruz.

<img src="https://aliozgur.gitbooks.io/git101/content/ileri_seviye_komutlar_ve_islemler/03_git_diff.jpg" style="width:100%;">

# Çakışmaları Nasıl Çözeriz
Çakışma oluştuğunda ilk yapmanız gereken şey çakışmanın neden olduğunu anlamak olmalıdır. Örneğin takım arkadaşınız aynı dosyada sizin de değiştirdiğiniz bir satırı mı değiştirdi veya aynı dosyada bir satır mı sildi veya sizinle aynı isimli yeni bir dosya mı oluşturdu?

`git status` komutunu çalıştırdığınızda Git size branch'inizde entegre edilmemiş dosyalar olduğunu söyleyecektir.

<img src="https://aliozgur.gitbooks.io/git101/content/ileri_seviye_komutlar_ve_islemler/04_conflict.jpg" style="width:100%;">

Yukarıdaki ekran görüntüsünde dosya1.md isimli dosyamızda çakışma olduğunu görebiliriz. Bu çakışmayı düzeltmek için dosyamızı açıp çakışan satırları düzeltmemiz gerekiyor.


<img src="https://aliozgur.gitbooks.io/git101/content/ileri_seviye_komutlar_ve_islemler/05_dosya1.jpg" style="width:100%;">

dosya1.md dosyasını açtığımızda yukarıdakine benzer bir görüntü ile karşılaşıyoruz.

1. <<<<<<<<< HEAD ile başlayan ve ============ kadar devam eden kısım dosyanın bizim branch'imizde olan versiyonuna ait
2. ================ belirtecinden sonraki kısım da değişiklikleri entegre etmek istediğiniz branch'de yer alan dosyanın içeriğini gösterir.

Dosyamızın içeriğinin ne olacağına karar verip kaydettikten sonra normal bir commit işlemi ile çakışmayı çözme işlemini tamamlıyoruz.
```sh
$ git add dosya1.md ile dosyamızı Staging Area'ya ekliyoruz
$ git commit -m "değişiklikler entegre edildi" komutu ile de commit işlemini tamamlarız.
```

# Merge İşlemini Nasıl Geri Alabiliriz?
Dosyanızın merge işlemine başlamadan önceki haline istediğiniz zaman geri dönebilirsiniz. Bunun için yapmanız gereken tek şey `git merge --abort` komutunu çalıştırmak.