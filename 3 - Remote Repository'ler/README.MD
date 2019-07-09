# Remote Bir Repository'ye Bağlantı Sağlamak
Remote bir repository'yi yerel diskinize `git clone` komutu ile indirdiğinizde Git otomatik olarak bu işlemi yapmak için kullandığınız bağlantı bilgilerini hatırlar. Git bu bilgi'yi varsayılan olarak `origin` adı verilen remote bir repository olarak kayıt altına alır. Local olan bir respository için ise böyle bir bilgi tutulmaz. Ancak bölüm girişinde de ele aldığımız gibi Local bir repository'yi baz alarak yeni bir remote repository oluşturabiliriz. Bunun için git clone komutunu kullanabiliriz. Örneğin:
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/01_git_remote_add.jpg" style="width:100%;">
Yukarıdaki ekran görüntüsünde ilk komutumuz olan `git remote add` ile local repository'miz ile remote repository'miz arasındak bağlantıyı kuruyoruz. İkinci komutumuz olan `git remote -v` ile de remote repositorymiz ile ilgili bilgileri görebiliriz.

Dikkat ettiyseniz her bir remote repository için biri `fetch` diğeri de `push` işlemleri için kullanılan iki adres bulunur. fetch adresini remote repository'den yapılacak olan okuma işlemleri, push adresini de remote repository'ye yapılan yazma işlemleri için kullanılır. Genel olarak bu iki adres aynı olmakla birlikte performans ve güvenlik gibi gerekçeler ile iki farklı adres de kullanılabilir.
# Remote Repository'deki Verilerin İncelenmesi
git clone komutu remote bir repository'yi yerel diskimize indirdikten sonra `git branch -va` komutunu çalıştırdığımızda aşağıdaki görüntüde yer alan bilgiler listelenecektir.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/02_git_branch_va.jpg" style="width:100%;">
Dikkat edecek olursanız local repository'lerimiz hala yerinde duruyor ancak listemizde ilave olarak origin/HEAD ve origin/master isimli iki remote kaydı var. Peki daha önceki bölümde `git add git101_ornek` komutu ile oluşturduğumuz remote repository kayıtlarımız neden listlenmiyor? Bunun nedeni önceki bölümde kullandığımız git add komutu ile local ve remote repository arasında sadece bir ilişki/bağlantı tanımladık, aslında bu komut sonrasında local ve remote arasında herhangi bir veri trasferi gerçekleşmez.
Git'in remote repository ile ilgili yerel diskinizde tuttuğu bilgileri güncellemesini sağlamak için `git fetch` komutunu kullanmanız gerekir.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/03_git_fetch.jpg" style="width:100%;">
Fetch komutu yerel diskinizdeki branchlerinizi ve Working Copy'deki dosyalarınızı güncellemez veya değiştirmez. Bu komut ile sadece takım arkadaşlarınızın remote repository'de yayınladıkları değişikliklere ilişkin bilgiler yerel diskinize indirilir. Daha sonra bu değişikliklerden hangilerini hangi local branch'e entegre edeceğinize kendiniz karar verebilirsiniz.

Bu işlemden sonra tekrar `git branch -va` komutunu çalıştırdığımızda `git ornek_101/master` isimli remote repositorymizdeki branchlere ilişkin bilgileri de görebiliriz.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/04_git_fetch.jpg" style="width:100%;">

Bilgilerini güncellediğimiz git101_ornek/master isimli branch'de değişiklikler yapmak için öncelikle bu branch'i baz alarak yeni bir local branch oluşturup dosyaların Working Copy alanımıza kopyalanmasını sağlamamız gerekiyor. Bunun için git checkout komutunu `--track` parametresi ile kullnıyoruz.

<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/05_git_checkout_track.jpg" style="width:100%;">

git checkout --track komutu ile aşağıdaki işlemler gerçekleşir

1. Remote branch ile aynı isimde local bir branch oluşturulur
2. Yeni oluşturulan branch aktif hale getirilir
3. --tracking parametresini kullandığımız için yeni oluşan local branch ile remote branch arasında "tracking relationship" adı verilen ve local branch'in hangi remote branch'deki değişiklikleri takip ettiğini gösteren ilişki kurulur

Local branch'imizi hazırladığımıza göre gelin şimdi birkaç değişiklik yapalım. Bu değişiklikleri yaptıktan sonra her zamanki gibi önce değişikliklerimizi Staging Area'ya alıyoruz ve sonrasında da commit işlemini gerçekleştirerek local repository'de versiyon kontrolüne ilişkin işlemlerimizi bitiriyoruz. Son adım olarak da git push komutu ile localdeki bu değişikliklerimizi remote branch'de yayınlıyoruz.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/06_git_push.jpg" style="width:100%;">

# Remote Değişiklikleri Entegre Etmek
Takım arkadaşlarınız kendi değişikliklerini tamamlayıp remote branch'de yayınladıktan sonra siz de bu değişiklikleri inceleyip kendi local branch'inize entegre ederek çalışmanıza devam edebilirsiniz. Ancak remote branch'deki değişiklikleri entegre etmeden önce bu değişikliklere ilişkin bilgileri (dosyaları değil sadece değişikliklere dair Git'de tutulan bilgiler) görmeniz ve incelemeniz gerekir.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/07_git_fetch.jpg" style="width:100%;">
Remote branch'deki değişiklikleri indirmek için `git fetch` komutunu kullanıyoruz. Git fetch komutuna geçilen origin değeri ise daha önceki bölümlerde gösterdiğimiz remotes/origin/master isimli remote branch bağlantısına referans vermek için kullanılır.

git fetch komutu ile remote branch'deki değişiklikleri indirdikten sonra ise git log komutunu kullanarak bu remote branch'deki değişiklikler ile ilgili bilgileri görebiliriz. (değişiklik tarihi, kimin yaptığı, değişen dosyalar ve commiti sırasında girilen mesaj gibi)

Değişiklikleri inceledikten sonra bunları local branch'inize entegre etmeye karar verdiğimizde ise git pull komutunu kullanmamız gerekecek.

Git pull komutu aslında arka arkaya iki şey yapmanızı sağlar

1. Remote branch'deki değişiklikler ile ilgili bilgileri indirmek, yani git fetch
2. Remote branch'deki değişiklikleri local branch'inize entegre etmek yani git merge

İlerleyen bölümlerde çakışmaların tespit edilmesi, çözülmesi ve değişikliklerin entegre edilmesi konularını ayrıntılı olarak ele alacağız şimdilik sadece iş akışımızı özetleyip bu konuyu burada sonlandıralım. Akışımız özetle şöyle olacak

1. git fetch : remote'dan güncelleme bilgilerini indir
2. git diff : remote ve local arasındaki farkları incele
3. git merge : değişiklikleri otomatik merge et çakışma varsa bir sonraki adıma geçin
4. Çakışma olan dosyalarınızı açın ve çakışmaları düzeltin
5. git add: çakışmanın giderildi ve değişiiklik Staging Area'ya alındı

# Local Bir Branch'i Yayınlamak (Publish)
Kendi bilgisayarınızda oluşturduğunuz Local bir branch siz yayınlamaya karar vermediğiniz sürece sadece sizin bilgisayarınızda yer alacaktır. Yani local bazı branchlerinizi sadece kendi bilgisayarınızda tutarken istediklerinizi de takım arkadaşlarınız ve hatta tüm dünya ile paylaşabilirsiniz.

Gelin şimdi superyeniozellik isimli local branch'i remote repositorymizde paylaşalım.
<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/08_git_push.jpg" style="width:100%;">
Önce git checkout komutu ile branch'imizi aktif hale getiriyoruz ve sonra git push komutu ve -u seçeneği ile local branch'imizi remote repository'mizde yayınlıyoruz. Push komutu için verdiğimiz origin ve superyeniozellik değerleri ile HEAD branch'imizi origin remote repository'de superyeniozellik isimli branch olarak yayınlanmasını istediğimizi tanımlıyoruz. -u seçeneği ise local branchimiz ile remote branchimiz arasında, önceki bölümlerde de bahsettiğimiz, Takip İlişkisi (Tracking Relationship) kurulmasını sağlar.

<img src="https://aliozgur.gitbooks.io/git101/content/remote_repositoryler/09_git_branch_vva.jpg" style="width:100%;">