# Branching Çalışma Şeklinizi Değiştirebilir
Bazı araçların sağladığı imkanlar günlük iş yapma şeklimizi çok derinden etkileyip, yaptığımız işe daha farklı bakabilmemizi sağlar. Git'in branching yaklaşımı (Türkçeye dallanma olarak da çevirebiliriz) da bahsettiğim bu dönüştürücü etkiye sahip araçlardan birisidir. Branching konusundaki hakimiyetimizin artması ve sağlamlaşması ile birlikte daha farklı iş yapmaya başlayıp daha iyi birer yazılım geliştirici olabilirsiniz.

Branching denilen yöntem aslında Git dışındaki diğer versiyon kontrol sistemlerinde de öteden beri kullanılmakta ve yazılım geliştiricilerin hayatını önemli derecede kolaylaştırmaktadır. Ancak, Git'deki branching yaklaşımı kullanım kolaylığı ve yüksek performansı nedeniyle kendine has olduğunu da söylemeliyiz.

Öyleyse gelin şimdi yavaş yavaş branching'in (dallanma) ne olduğunu anlayalım.

# Birden Fazla Bağlamda Çalışmak
Daha önceki bölümün son alt başlığında (git commit) zaman zaman bireysel olarak kısa zaman dilimlerinde aynı projenin farklı özellikleri ile ilgili değişiklikler yapılması gerekebileceğinden bahsetmiştik. Büyük projelerde ise bu durum kişisel bir tercih olmaktan çıkıp iş bölümü/uzmanlık gibi kriterlere bağlı olarak proje/ürün yönetiminin önemli bir parçası halinde ele alınır. Örneğin 5 kişilik bir ekibin her bir üyesi aynı yazılımın farklı özellikleri ile ilgili çalışabilir veya iki farklı kişi aynı özelliğin farklı şekillerde nasıl geliştirilebileceği ile ilgili deneysel çalışma yapıyor olabilirler. Bahsettiğim tüm bu alternatif senaryolar aslında kendi yaşam döngüleri olabilen, çoğu zaman kısa veya uzun süreli eş zamanlı ilerleyen farklı birer bağlama denk gelir.

Pratikte üzerinde çalıştığınız projenin/yazılımın her zaman son stabil durumu yansıtan ana bir bağlamı ve X numaralı hata bildiriminin düzeltilmesi, yeni bir Y özelliği üzerinde yapılan çalışma veya deneysel bir özellik ile ilgili yapılan çalışma gibi birden fazla yan bağlamı olacaktır.

# Branching olmasa da olur mu?
Net olarak birbirinden ayrılmış farklı bağlamlar oluşturmak için branching benzeri araçlar olmasaydı aşağıdakilere benzer senaryolarda nasıl davranacağımız konusunda sıkıntılar yaşayacaktık

1. Örneğin müşteriniz veya yöneticiniz iki alternatif sayfa tasarımından birincisini değil de ikincisini beğendi ve bu arada siz de sayfa tasarımı dışında birkaç tane bug fix ve birkaç tane de dokümantasyon değişikliğini farklı zamanlarda tamamladınız. Bu durumda müşterinizin beğendiği ikinci tasarımı diğer tüm düzenlemeleri kaybetmeden nasıl devreye alacaktınız?
2. Üzerinde çalıştığınız alışveriş sitesi için özel olarak geliştirdiğiniz Sepet modülü yerine 3. parti bir modül kullanılması kararı alındı ve sizin de kendi modülünüzü ana yazılımdan sökmeniz istendi. Bu durumda sökmeniz gereken modül kodunu tespit edip diğer modülleri etkilemeden nasıl sökecektiniz?
3. Yeni geliştirdiğiniz Beni Haberdar Et işlevi yazılımınızın geri kalan özelliklerinin bir çoğunun değiştirilmesine sebep olmuşken birden Beni Haberdar Et işlevinin saçma ve gereksiz olduğuna karar verilseydi bu işlevi aradan geçen zamanda yazılımın farklı yerlerinde yapılan diğer değişikliklerden izole ederek nasıl çöpe atacaktınız?
Birden fazla konu ile ilgili değişikliklerin tamamını tek bir bağlam ile yönetmeye çalışırsanız işler hızla sarpa saracaktır. Bu karmaşanın önüne geçmek için her bir değişiklik için projenizin tamamının farklı klasörlere kopyalamayı deneyebilirsiniz. Ancak bu durumda

1. Bu klasörler versiyon kontrolünde olmadığı için ekibin geri kalanı ile iş birliği yapmanız çok zorlaşacak
Farklı değişiklikleri entegre etmek çok zor ve hataya açık bir işlem olacak
2. Uzun lafın kısası projenizdeki değişiklikleri profesyonel bir yaklaşımla ele almak istiyorsanız farklı bağlamlarda çalışmak ve bu bağlamları düzgün yönetmek için bir yol bulmanız gerekiyor.

# Neyse ki branching var
Branching bir önceki bölümde değindiğimiz tüm sorunların önüne geçmek için kullanabileceğimiz bir araç ve yaklaşımdır. Branching ile farklı bağlamları birbirinde kolayca izole ederek her birini kolayca ve ayrı ayrı yönetebilirsiniz.

Herhangi bir anda yaptığınız değişiklikler sadece aktif olarak üzerinde çalıştığınız branch'e (dal) yansıyacak diğer branch’ler bu değişikliklerden etkilenmeyecektir. Böylece aynı anda birden fazla branch üzerinde özgürce çalışabilirsiniz ve en önemlisi de bu çalışmalarınızdan bir kısmının çöpe dönmesinden çekinmeden denemelerinizi yapabilirsiniz.

# Branch'ler İle Çalışmak
Git'de branch kullanımı tercihe bağlı değildir, aslında farkında olmasanız bile projeniz üzerinde çalışırken her zaman aktif tek bir branch üzerinde çalışırsınız. Git'de projenizi ilk oluşturduğunuzda Git varsayılan olarak sizin için `master` adı verilen bir branch oluşturur ve siz bu branch üzerinde çalışmaya başlarsınız.

Gelin şimdi `git branch` komutunun basit kullanımı ile ilgili birkaç örnek görelim.

`git branch deneme` komutunu çalıştırdığınızda git sizin için projenizdeki dosyaların o anki halini barındıran `deneme` isimli bir branch oluşturur. Git git branch komutu ile oluşturduğunuz yeni branch'i otomatik olarak aktif hale getirmez.

Branch'inizi oluşturduktan sonra `git branch` komutunu çalıştırdığınızda git size projeniz için oluşturduğunuz tüm branch'leri listeler ve aktif olan branch'i başına da * simgesi olacak şekilde gösterir.

`git status` komutunu çalıştırdığınızda da aktif olan branch `"On branch ...."` ifadesi ile gösterilir.

Branch'leriniz ile ilgili daha fazla ayrıntı görmek için ise `git branch` komutunu `-v` parametresi ile çalıştırabilirsiniz.

## NOT:Yarım Yamalak Değişiklikleri Asla Commit etmeyin

Tam anlamıyla bitirmediğiniz ve test etmediğiniz bir değişikliği asla commit etmeyin. Üzerinde çalışacağınız değişiklikleri planlarken bu değişiklikleri mümkün olduğunca küçük parçalar halinde ele almaya özen gösterirseniz yaptığınız değişiklikleri kayıt altına almak için henüz tamamlanmamış değişiklikleri commit etmek zorunda kalmazsınız. Buna rağmen ara safhada kayıt altına almak istediğiniz değişiklikler olursa Git'in **Stash** özelliğini kullanabilirsiniz.

# Değişikliklerinizi Geçici Olarak Kaydetmek -> Git Stash
Commit işlemi ile dosyalarınızda yaptığınız değişiklikler kalıcı olarak repository'de kayıt altına alınır. Ancak günlük çalışmamızda bazen tam olarak bitmeyen değişiklikleri de kayıt altına almak isteyebiliriz. Örneğin bir değişiklik üzerinde çalışırken başka bir konu ile ilgili kritik bir sorun bildirildiğinde yapmakta olduğumuz işi yarım bırakıp yeni soruna odaklanmak zorunda kalabilirsiniz.

Bu gibi durumlarda yeni sorun ile ilgilenmeye başlamak için önceki değişikliklerinizi kaybetmeden yeni ve temiz bir branch oluşturmalısınız. Yarım kalan değişiklikleri kayıt altına almak için git stash komutunu kullanmalısınız.

<img src="https://aliozgur.gitbooks.io/git101/branching_dallanma_ve_merging_birlestirme/07_git_stash.jpg" style="width:100%;">

git stash ile üzerinde çalıştığınız ancak henüz commit etmediğiniz değişikliklerin geçici olarak Git tarafından kayıt altına alınmasını ve aktif branch'inizin herhangi bir değişikliğin olmadığı temiz bir duruma getirilmesini sağlarsınız. git stash komutunu çalıştırdıktan sonra tekrar git status komutunu çalıştırırsanız önceki bölümde commit edilmemiş bir değişiklik olarak görünen dosya2.md dosyasındaki değişiklik artık listelenmez çünkü master branch’imiz git stash sonrası temiz bir duruma geldi.

git stash list komutunu kullanarak aktif branch'inizde geçici olarak kayıt altına aldığınız değişikliklerin listelenmesini sağlayabilirsiniz.

<img src="https://aliozgur.gitbooks.io/git101/branching_dallanma_ve_merging_birlestirme/08_git_stash_list.jpg" style="width:100%;">

# Basit Bir Branching Akışı
Gelin şimdi hep birlikte günlük çalışmanız sırasında kullanabileceğiniz basit bir branching akışını ele alalım. Çalışma senaryomuzun şöyle geliştiğini düşünelim

1. Bir web sitesi üzerinde çalışmaya başladınız
2. Bu siteye yeni bir özellik eklemek için bir branch oluşturdunuz
3. Bu yeni branch üzerinden değişikliklerinizi yapmaya başladınız
Bu sırada web sitesinde bir güvenlik açığı tespit edildiğini bildiren bir email aldınız. Acil olarak bu güvenlik açığını gidermeniz için yapmakta olduğunuz çalışmayı bırakmanız ve bu durumu düzeltmeniz gerekiyor. Böyle bir durumda aşağıdaki adımları takip edebilirsiniz

1. Aktif branch'inizi web sitenizin son stabil versiyonunun bulunduğu master branch olarak değiştirdiniz. `git checkout master` komutunu kullandık.
2. Güvenlik açığını giderme çalışmanız için yeni bir branch oluşturdunuz. `git branch loginsorunu` komutunu kullanarak branch oluşturduk ve `git checkout loginsorunu` komutu ile bu branch'i aktif hale getirdik.
3. Güvenlik açığını giderecek değişikliği tamamladınız, testlerinizi yaptınız ve bu değişikliği Staging Area'ya ekleyip sonrasında da commit ettiniz. `git add login.xyz login.html login.css` ile değişiklikleri Staging Area'ya gönderdik. `git commit -m "Özel karakter içeren kullanıcı adlarında ortaya çıkan güvenlik sorunu giderildi"` ile değişikliklerimizi commit ettik.
4. master branch’imizi aktif hale getirdik. `git checkout master` komutu ile.
5. Commit ettiğiniz değişikliği web sitenizin stabil versiyonunu içeren master branch’imize merge ettik. `git merge loginsorunu`
6. Daha önce üstünde çalışmakta olduğunuz yeni özellik ile ilgili değişiklikleri içeren branch'inizi aktif hale getirerek çalışmanıza kaldığınız yerden devam edebilirsiniz. `git checkout yeniozellik_xyz` komutu ile.

# Checkout, HEAD ve Working Copy kavramları
Git'de bir branch otomatik olarak o branch için yaptığınız son commit işlemine bir işaretçi tutar ve hangi dosyaların o branch'e ait olduğunu bilir. Herhangi bir anda bir proje için tek bir branch aktif olabilir. Bu branch'e HEAD denir ve Working Copy içindeki (Working Copy'yi projenizin yerel diskinizdeki dosyalarının tamamı olarak düşünebilirsiniz) dosyalar aktif olan branch'e yani HEAD'e aittir. Diğer branch’lerinizdeki dosyalar diskiniz üzerinde değil Git'in veri tabanında (.git klasörü içinde özel bir formatta) bulunur.

Farklı bir branch'i aktif hale getirmek için git checkout komutu kullanılır. Bu durumda Git otomatik olarak sizin için iki şey yapar

1. Aktif hale getirdiğiniz branch'i HEAD yapar ve
2. Aktif hale getirdiğiniz branch'e ait dosyaları Git veri tabanınızdan yerel diskinize kopyalar ve önceki branch'e ait dosyaları diskinizden kaldırır. Yani Working Copy'nize yeni branch'e ait olan dosyaları koyar.

# Değişiklikleri Merge Etmek
Projemizde yaptığımız farklı konular ve bağlamlardaki değişiklikleri takip etmek bir önceki bölümde anlattığımız basit iş akışı ile günlük çalışmamızda bize ciddi kolaylıklar ve esneklikler sunmaktadır. Ancak branch'lerimiz üzerinde değişikliklerimizi tamamlayıp Staging ve Commit işlemlerimizi yaptıktan sonra tüm bu değişiklikleri projemizin stabil versiyonu olan master branch ile merge etmemiz gerekiyor (branch -> [merge] -> master). Merging en basit anlamda herhangi bir brach'de yaptığımız değişiklikleri master branch'imiz ile birleştirme veya master branch'e entegre etme işlemidir.
Bir branch'deki değişikliklerinizi sadece master branch’iniz ile merge etmek zorunda değilsiniz. Kullandığınız Git çalışma pratiğine bağlı olarak herhangi bir branch'i başka bir branch'e merge edebilirsiniz.

Değişikliklerinizi master branch’inize merge etmek durumlardan sadece bir tanesidir, günlük çalışmanız sırasında karşılaşacağınız diğer bir durum ise üzerinde çalıştığınız branch'e master branch'deki değişikliklerin merge edilmesidir (master -> [merge] -> branch). Bu durumu doğurabilecek aşağıdakilere benzer durumlar ile karşılaşabilirsiniz

1. Büyük bir ekipte çalışıyorsunuz ve ekip arkadaşlarınız yaptıkları değişiklikleri sık sık master branch'e merge ediyorlar. Bu durumda siz de uzun zamandır üzerinde çalıştığınız branch'in master'dan geri kalmaması için merge işlemi yapmak isteyebilirsiniz.
2. Tek başınıza çalışıyorsunuz ancak farklı zamanlarda farklı sebepler ile master branch'e merge ettğiniz bir çok düzeltme yaptınız. Diğer yandan da daha uzun soluklu bir çalışmanızı ayrı bir branch üzerinde yapıyorsunuz. Üzerinde çalıştığınız branch'in master'daki değişikliklerden geri kalmaması için merge işlemi yapmak isteyebilirsiniz.
Commit'leri değil branch'leri entegre etmek! Git'de değişikliklerinizi merge etme işlemi sırasında kaynak branch'inizde tekil olarak hangi değişiklikleri (commit'ler) merge etmek istediğinizi teker teker söylemezsiniz. Bunun yerine Git'de doğrudan kaynak branch'inizin tamamını hedef branch'e merge edersiniz, çünkü git hangi değişikliklerin hedef branch'de bulunmadığını otomatik olarak tespit edip sadece bunların entegre edilmesini sağlar. Kaynak branch'deki değişiklikler her zaman HEAD'e yani aktif branch'iniz hangisi ise ona entegre edilir.

Git'de merge işlemi çok basit iki adımda yapılır.

1. `git checkout` komutu ile değişikliklerin aktarılacağı hedef branch'inizi aktif (HEAD) hale getirirsiniz.
2. `git merge` komutu ile kaynak branch'deki commit edilmiş değişiklikler HEAD'e entegre edilir.

# Uzun Soluklu Branch'ler
İkinci türdeki branch'ler ise daha üst seviyede anlam taşırlar ve yeni özellikler, bug fix ve deneysel çalışmalar gibi odaklanmış konular yerine projenizi stabil, test ve development gibi aşamalarını temsil ederler. Bu tür branch’ler projeniz üzerinde geliştirme yaptığınız sürece varlıklarını sürdüreceklerdir. Tipik olarak bu tür branch'ler ile ilgili aşağıdaki kurallar geçerlidir

Genelde bu tür uzun soluklu branch’ler üzerinde doğrudan değişiklik yapmazsınız. Çalışmalarınızı kısa vadeli branch’ler üzerinde yaparak değişiklikleri bu branch'lere entegre edersiniz.
Uzun soluklu branch'ler arasında bir hiyerarşi vardır. Genellikle master branch projenizin stabil versiyonudur ve hiyerarşik olarak bir altında geliştirmelerinizi entegre ettiğiniz ve daha az stabil olabilen development branch'i yer alır.
Uzun soluklu branch'lerin hangi kriterlere göre oluşturulacağı, nasıl yönetileceği ve isimlerinin ne olacağı genellikle çalışan ekibe ve projeye göre değişebilir. Ancak her hâlükârda nasıl bir branching stratejisinin izleneceğine ekip olarak fikir birliği içinde karar verilmelidir.