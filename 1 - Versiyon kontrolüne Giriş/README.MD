# Kullanıcı adınızı ve email bilgisi
Git ayarlarından en önemli olanları kullanıcı adınız ve email adresinizdir. Git, ayar olarak tanımladığınız değerleri commit vb işlemlerde otomatik olarak kullanır. Bu ayarların değerini belirlemek için komut satırında aşağıdaki komutları çalıştırıyoruz
```c++
git config --global user.name "ali özgür"
git config --global user.email "ali.ozgur@example.com"
```
Yukarıdaki komutlarda

--global seçeneği ile Git'e global ayarları düzenlediğinizi söylüyoruz
user.name (ve user.email) ile değerini değiştirmek istediğiniz ayarın anahtar'ını belirtiyoruz
Ardından da çift tırnak içinde ilgili ayarın değerini giriyoruz
Bu ayarları --global ibaresi ile tüm projelerinizde geçerli olacak şekilde yaptık, proje seviyesinde bu ayarları yapmak için komut satırında (terminal'de) projenizin klasörüne konumlanıp git config user.name "ali özgür" komutu ile --global seçeneğini kullanmadan yapabilirsiniz.

Kendi yaptığımız veya kurulum ile hazır gelen ayarların değerlerini görmek için aşağıdaki komutları kullanabiliriz.

Global seviyede tüm ayarları listelemek için
```c++
git config --global -l
```

Global seviyede tek bir ayar'ın değerini (örneğimizde user.name anahtarına sahip ayar) görmek için ise
```c++
git config --global user.name
```

# Editör Ayarı
Editör ayarı
Git'in bazı komutları sizden interaktif olarak yorum veya bilgi girmenizi ister. Bu tür durumlar için Git'in hangi metin düzenleme uygulamasını kullanacağını ayarlayabilirsiniz. Git varsayılan olarak Vi veya Vim) kullanır. Ancak bu editörlerin kullanımı başlangıç seviyesindeki kullanıcılar için zor olabilir. 
```c++
git config --global core.editor <editör>
```
Yukarıdaki komut ile editörünüzü değiştirebilirsiniz.

# Basit Anlamda Versiyon Kontrolü İş Akışı
Git'in derinliklerine dalmadan önce gelin basit bir versiyon kontrol iş akışına adım adım göz atalım.

Versiyon kontrolünün en temel bileşeni *repository* denilen yapıdır. Repository, dosyalarınızdaki tüm değişiklikleri ve bu değişiklikler ile ilgili ilave bilgileri (değişikliği kim, ne zaman yaptı ve değişiklik ile ilgili girilen açıklamalar) ayrı birer versiyon olarak kayıt altında tutan bir veri tabanıdır. Git tüm bu bilgileri genellikle dosya sisteminde gizli bir klasör olarak oluşturulan *.git* isimli klasör içinde bir dizi dosya olarak tutar.

Yukarıda bahsettiğimiz repository'yi kendi bilgisayarınızda oluşturmak için iki yöntem kullanabilirsiniz.

Henüz versiyon kontrolünde olmayan bir projeniz varsa *git init komutu ile projenizi tüm klasör ve dosyaları ile birlikte versiyon kontrolüne alabilirsiniz
Projeniz uzaktaki veya şirket ağınızdaki bir Git sunucusunda versiyon kontrolü altında tutuluyorsa projeyi kendi bilgisayarınıza git clone komutu ile indirebilirsiniz.
Projeniz için yukarıdaki yöntemlerden biri ile repository oluşturduktan sonra aşağıdaki basit akışı kullanarak değişikliklerinizi yapmaya başlayabilirsiniz

1. Projenizin repository’sini oluşturduktan sonra dosyalarınız üzerinde istediğiniz değişiklikleri istediğiniz uygulamayı kullanarak yapabilirsiniz. Bu aşamada yaptığınız değişiklikleri versiyon kontrolü için birebir ve doğrudan takip etmenize gerek yoktur.
2. Yaptığınız değişiklikler istediğiniz bir noktaya ulaştığında veya bir özellik veya sorun giderme düzenlemesi ile ilgili çalışmanız tamamlandığında versiyon kontrolü bakış açısı ile değişikliklerinizi değerlendirmeniz gerekir. Bu aşamada değişikliklerinizi commit adı verilen bir bütünü olarak tarif etmelisiniz. Böylece projenizin yeni bir versiyonunu oluşturma işleminin ilk adımını tamamlamış olacaksınız.
3. Fakat, commit işlemi öncesinde dosyalarınızda yaptığınız değişikliklerin bir özetini görmek isteyebilirsiniz. git status komutu ile hangi dosyaları değiştirdiğinizi, sildiğinizi veya hangi dosyaları eklediğinizi kolayca görebilirsiniz.
4. Bir sonraki aşamada değişen dosyalarınızdan hangilerinin commit'e dahil olduğunu belirlemeniz gerekiyor. Bu adımda commit'e dahil etmek istediğiniz dosyaları *staging area* denilen ara bir alana alırız.
5. Dosyaların içeriğinin değiştirilmiş olması, silinmesi veya yeni dosya eklenmesi bu dosyaların otomatik olarak staging area'ya eklenmesini sağlamaz. Bu işlemi ilgili dosyaları seçerek sizin yapmanız gerekir.

Dosyalarınızı staging area'ya ekledikten sonra şimdi commit işlemine hazırsınız. Commit işlemi ile dosyalarınızdaki değişiklikler yeni bir versiyon olarak Git'de kayıt altına alınır.
Zaman zaman, özellikle de bir takım çalışması söz konusu ise, projenizdeki değişikliklere göz atmak isteyebilirsiniz. Projeniz için oluşturduğunuz commit'lerin tarihçesini incelemek için git log komutunu kullanabilirsiniz.
Yaptığınız değişikliklerin takımın geri kalanı tarafından da görülmesini ve kullanılmaya başlanmasını sağlamak için değişikliklerinizi zaman zaman uzaktaki repository’de yayınlamanız gerekir. Bunun için git push komutunu kullanırız.

## Local (Yerel) & Remote (Uzak) Repository'ler
Local repository, kendi bilgisayarınızda proje klasörünüzün altında bulunan .git klasörüdür. Bu repository üzerinde sadece siz çalışabilirsiniz ve değişiklikler yerel diskinize kaydedilir.
Remote repository'ler ise genellikle uzaktaki bir sunucuda yer alırlar ve bu sunucudaki .git klasöründen ibarettirler. Takım çalışması söz konusu ise takımdaki kişiler değişikliklerini bu uzaktaki repository üzerinden paylaşırlar.

# Versiyon kontrolü altına almak istemediğimiz dosyalar
Tüm geliştirme ortamları ve işletim sistemlerinde kullandığımız araçlar tarafından ara bir ürün olarak üretilen ve aslında doğrudan versiyon kontrolü altına almak istemediğimiz dosya veya klasörler olacaktır. Örneğin Mac OS X'in otomatik olarak ürettiği gizli DS_Store isimli klasör veya C++ derleyicileri tarafından üretilen .o uzantılı obj dosyaları gibi. Hangi dosyaların versiyon kontrolü altında tutulacağına ve hangilerinin göz ardı edileceğine Git otomatik olarak karar vermez, bu kararı sizin vermeniz gerekir.

Versiyon kontrolü altına almak istemediğiniz dosya ve klasörleri tanımlamak için proje klasörüne eklenen .gitignore dosyası kullanılır. Bu dosyaya göz ardı etmek istediğiniz dosya ve klasörlerin tespit edilebilmesi için doğrudan isimler veya basit kurallar ekleriz. Projelerinizi versiyon kontrolü altına aldıktan sonra ilk iş olarak GitHub'ın yayınladığı derlemeyi veya kendi deneyiminiz ve bilginiz ile karar vereceğiniz dosya ve klasörleri *.gitignore* dosyasına ekleyiniz. Projenizin ilerleyen aşamalarında bu işlemi yapmanız biraz daha zahmetli olacaktır.

Şimdi gelin .gitignore dosyasında kuralları nasıl tanımlayabileceğimize bir göz atalım
```cpp
*.[oa]
.~
```

İlk satırda o veya a uzantısı ile biten dosyaların versiyon kontrolü dışında tutulması için bir kural tanımlıyoruz. İkinci satırda ise ~ karakteri ile biten (çoğu metin düzenleme uygulaması geçici dosyaları ~ ile biten dosyalar olarak otomatik oluşturur) dosyaların versiyon kontrolü haricinde tutması için kural tanımlıyoruz.

.gitignore dosyasında tanımlama yaparken aşağıdaki kurallar geçerlidir

1. Boş satırlar veya # ile başlayan satırlarda yaptığınız tanımlamalar Git tarafından dikkate alınmaz.
*, ?, [ ], { }, [!] ve \ gibi karakterler kullanılarak oluşturulan ve globbing patterns adı verilen tanımlayıcılar kullanabilirsiniz
2. Klasörleri belirtmek için / karakteri kullanılır. Örneğin /projemde/versiyon/kontrolü/istemedigim/bir/klasor/ şeklinde bir tanım yaptığımızda ilgili klasör ve altındaki tüm dosyalar Git tarafından göz ardı edilir.
3. Tanımladığınız bir kuralın tersini ! simgesi ile tanımlarız. Örneğin !/projemin/kaynak/kodu/ şeklinde bir tanım yaptığımızda bu klasör dışındaki tüm klasör ve dosyalar Git tarafından göz ardı edilecektir.

# İlk commit’imiz
Projemizi versiyon kontrolüne alıp göz ardı edilmesini istediğimiz klasör ve dosyaları da belirledikten sonra aşağıdaki komutlar ile ilk commit işlemimizi yapabiliriz
```sh
$ git add -A
$ git commit -m "İlk commit işlemimizi yaptık"
```
İlk komutun tüm proje dosyalarının Staging Area'ya eklenmesi için,
İkinci komutun ise dosyalarımızın bir açıklama ile commit edilmesi için kullanıldığını söylemek ile yetinelim.

# Staging Area
Çoğu versiyon kontrol sisteminde değişiklikleriniz iki yerde kaydedilir

1. Yerel diskinizdeki çalışma klasörünüz (working folder) veya
2. Versiyon kontrol sisteminin veri tabanı
Ancak git'de değişikliklerinizin kayıt altına alındığı üçüncü bir alan daha vardır ki buna Staging Area denir ve git'in en temel kavramlarından birisidir. Staging Area'yı, proje dosyalarımızdaki bir dizi değişikliği remote repository'ye göndermeden önce kayıt altında tuttuğunuz veri tabanı/alan olarak tanımlayabiliriz.

## Sadece Birbiri İle Alakalı Değişiklikleri Commit Edin

Değişikliklerinizi commit etmeye karar verdiğinizde birbiri ile alakalı değişiklikleri tek bir commit olarak ele almaya özen gösterin. Birbiri ile alakalı olmayan değişiklikleri aynı commit ile versiyon kontrol sisteminde kayıt altına aldığınızda aşağıdakilere benzer sorunlar yaşama ihtimaliniz artacaktır

1. Commit’inizdeki değişiklikleri inceleyen ekip arkadaşlarınız yaptığınız değişikliklerden hangisinin hangi konu ile ilgili olduğunu anlamakta güçlük çekeceklerdir.
2. Alakalı alakasız değişiklikler tek bir commit içinde yer aldığı için herhangi bir nedenle belirli ve tek bir değişikliği geri almakta güçlük çekeceksiniz.
Alakalı alakasız değişiklikleri tek bir commit ile ele almak yerine örneğin iki ayrı sorunu gidermek için yaptığınız değişiklikler iki ayrı commit ile kayıt altına alınmalı veya daha büyük bir özellik üzerinde çalışırken bu özelliği oluşturan ve anlamsal bir bütün olarak ifade edilen daha küçük özellikleri de ayrı commit’ler ile kayıt altına almalısınız.

# Yaptığınız Değişiklikleri Listelemek
Son commit işleminizden sonra proje dosyalarınızda yaptığınız değişiklikleri listelemek için *git status* komutunu kullanabilirsiniz.

git status komutu ile git aşağıdaki 3 ana grupta yer alan dosyaları size listeler

Changes to be committed (Commit edilmeye hazır dosyalar): Bu gruptaki dosyalar git add veya git rm komutu ile Staging Area'ya eklediğimiz dosyalardır. Bu dosyalar bir sonraki commit'imizin içinde yer alacaktır
Changes not staged for commit (Commit için henüz hazır olmayan dosyalar): Bu gruptaki dosyalar değişiklik yaptığımız fakat henüz Staging Area'ya eklemediğimiz dosyalardır. Bu dosyalar bir önceki grubun içine eklemediğimiz sürece bir sonraki commit'e dahil olmayacaklarıdır
Untracked files (Versiyon takibinde olmayan dosyalar): Bu gruptaki dosyalar ise henüz versiyon kontrolü altına almadığımız dosyalardır.

# "git add" ve "git rm" komutları

Bir önceki başlıkta değindiğimiz ve git status komutu sonrasında git'in bize özetlediği 3 gruptan son ikisinde yer alan dosyaların ilk gruba dahil edilmesi için git add ve git rm komutlarını kullanabiliriz.

Aşağıda oluşturduğumuz git add komutu ile baslik_2.md ve baslik_2_1.md dosyaları ile resimler klasörü altındaki tüm dosyaların Staging Area'ya eklenmesini sağlayabiliriz.
```cpp
git add baslik_2.md baslik_2_1.md resimler/*
```

# Değişikliklerimizi Commit Edelim

Değişikliklerinizi git add ve git rm ile Staging Area'ya aldıktan sonra git commit komutu ile yeni bir versiyon olarak kayıt altına alabilirsiniz.
```cpp
git commit -m "1.7 numaralı alt başlık içeriği tamamlandı"
```
Yukarıdaki komutta yer alan -m parametresi ile yaptığınız değişiklikleri özetleyen bir mesajı da commit'inize ekleyebilirsiniz. Eğer birden fazla satırı olan bir commit mesajı gireceksiniz -m parametresini kaldırmanız yeterli olacaktır. Bu durumda 1.3 numaralı bölümde ayarladığınız editör açılır ve bu editöre mesajınızı istediğimiz uzunlukta girebilirsiniz.

## Commit Tarihçesi
Git projeniz üzerinde çalıştığınız her anda yaptığınız commit işlemlerini kayıt altına almaktadır. Özellikle ekip çalışması söz konusu ise commit işlemleri ile ilgili git tarafından kayıt altına alınan bu bilgiler daha da önem kazanmaktadır.

Git'in commit’leriniz ile ilgili kayıt altına aldığı tarihsel bilgileri görmek için git log komutunu kullanıyoruz. Bu komut tüm commit’ler ile ilgili bilgileri, en son commit en üstte olacak şekilde, tarihsel olarak sıralar. Eğer Terminal pencerenize sığmayacak kadar çok tarihsel kayıt var ise son satırda : simgesi yer alacaktır, klavyenizden SPACE/BOŞLUK tuşuna basarak bir sonraki sayfanın listelenmesini q tuşuna basarak da listelemenin sonlandırılmasını sağlayabilirsiniz.
Terminal'de listelenen her commit tarihçesi kaydı, diğer bilgilerin yanı sıra, aşağıdaki temel bilgileri içerir

1. Commit'in Hash değeri
2. Commit'i gerçekleştiren kişinin adı ve email'i
3. Commit tarihi
4. Commit mesajı

git log komutu ile birlikte commit işlemi ile ilgili bilgilendirici çoğu bilgiyi görmekle birlikte parametre olarak -p değerini kullanırsanız dosyalarda yapılan değişiklikler de ayrıntılı olarak listelenecektir.