# Electron sürüm oluşturma

> Sürüm oluşturma politikamıza ve uygulamanıza ayrıntılı bir bakış.

2.0.0 sürümünden itibaren Electron [semver](#semver)'i izler. Aşağıdaki komut, Electron'un en son kararlı yapısını yükleyecektir:

```sh
npm install --save-dev electron
```

Mevcut bir projeyi en son kararlı sürümü kullanacak şekilde güncellemek için:

```sh
npm install --save-dev electron@latest
```

## Sürüm 1.x

Electron versiyonları *< 2.0*, [semver](http://semver.org) belirtimine uymadı. Ana sürümler, son kullanıcı API değişikliklerine karşılık gelmektedir. Küçük versiyonlar Chromium'un ana sürümlerine karşılık gelir. Yama sürümleri, yeni özelliklere ve hata düzeltmelerine karşılık gelmiştir. Özellikleri birleştiren geliştiriciler için elverişli olsa da, müşteri tarafından yönlendirilen uygulamaların geliştiricileri için sorunlar yaratmaktadır. Slack, Stride, Teams, Skype, VS Code, Atom ve Masaüstü gibi büyük uygulamaların QA test çevrimleri uzun olabilir ve istikrar son derece istenen bir sonuçtur. Hata düzeltmelerini kavramaya çalışırken yeni özelliklerin benimsenmesinde yüksek bir risk söz konusudur.

1.x stratejisine bir örnek:

![](../images/versioning-sketch-0.png)

` 1.8.1 </ 0> ile geliştirilen bir uygulama, <code> 1.8.2 </ 0> özelliğini emme veya düzeltmeyi geri gönderme olmadan <code> 1.8.3 </ 0> hata düzeltmesini alamaz ve yeni bir serbest bırakma hattının sürdürülmesini gerçekleştiremez.</p>

<h2>Sürüm 2.0 ve Ötesi</h2>

<p>Aşağıda özetlenen 1.x stratejimizden birkaç önemli değişiklik var. Her değişiklik, geliştiricilerin/sürdürücülerin ve uygulama geliştiricilerin gereksinimlerini ve önceliklerini karşılamak üzere tasarlanmıştır.</p>

<ol>
<li>Semver'in sıkı kullanımı</li>
<li>Semver-uyumlu <code>-beta` etiketlerinin tanıtımı</li> 

* [Konvansiyonel taahhüt mesajları](https://conventionalcommits.org/)'na giriş
* Açıkça tanımlanan stabilizasyon dalları
* ` master</ 0> dalı süresizdir; yalnızca istikrar dalları sürüm bilgisi içerir</li>
</ol>

<p>Git dallanmasının nasıl çalıştığını, npm etiketinin nasıl çalıştığını, geliştiricilerin neler bekleyebileceğini ve değişikliklerin nasıl geri alınabileceğini ayrıntılı olarak ele alacağız.</p>

<h1>semver</h1>

<p>Electron 2.0'dan itibaren semver'i izleyecek.</p>

<p>Aşağıda, değişiklik türlerini ilgili semver kategorilerine (örn. Majör, Minör, Yama) açıkça eşleyen bir tablo verilmiştir.</p>

<ul>
<li><strong>Büyük Sürüm Artışları</strong>

<ul>
<li>Chromium sürümü güncellemeleri</li>
<li>node.js ana sürüm güncellemeleri</li>
<li>Elektron API kırma değişiklikleri</li>
</ul></li>
<li><strong>Küçük Versiyon Artımları</strong>

<ul>
<li>node.js küçük sürüm güncellemeleri</li>
<li>Elektron kırılmaz API değişiklikleri</li>
</ul></li>
<li><strong>Yama Sürümü Artımları</strong>

<ul>
<li>node.js yama sürümü güncelleştirmeleri</li>
<li>fix-related chromium yamaları</li>
<li>Electron hata düzeltmeleri</li>
</ul></li>
</ul>

<p>Çoğu krom güncellemesinin kırılma olarak değerlendirileceğini unutmayın. Geri gönderilebilecek düzeltmeler muhtemelen kiraz yamalar olarak seçilecek.</p>

<h1>Dengeleme Dalları</h1>

<p>Dengeleme dalları, yalnızca emniyet veya istikrarla ilgili kiraz toplama taahhütlerini alarak, ustaya paralel çalışan dallardır. Bu dallar hiçbir zaman ustaya birleştirilmezler.</p>

<p><img src="../images/versioning-sketch-1.png" alt="" /></p>

<p>Stabilizasyon dalları daima <strong> major</ i> veya <strong> minor</ i> sürüm çizgileridir ve aşağıdaki şablona göre adlandırılmıştır: <code> $ MAJOR- $ MINOR-x </ 1> e.g. <code> 2-0-X </ 1>.</p>

<p>Eşzamanlı olarak birden fazla dengeleme dalının bulunmasına izin veriyoruz, her zaman paralel olarak en az ikisini desteklemeyi ve gerektiğinde güvenlik düzeltmelerini geri göndermeyi düşünüyoruz.
<img src="../images/versioning-sketch-2.png" alt="" /></p>

<p>Eski satırlar GitHub tarafından desteklenmeyecek, ancak diğer gruplar kendi kendilerine sahiplik ve backport kararlılığı ve güvenlik düzeltmeleri alabilir. Bunu birlikte cesaretlendiriyoruz çünkü birçok uygulamanın geliştiricileri için hayatı kolaylaştırdığının farkındayız.</p>

<h1>Beta Bültenleri ve Hata Düzeltmeleri</h1>

<p>Geliştiriciler hangi sürümlerin <em>güvenli</em> olacağını bilmek istiyor. Görünüşte masum özellikler bile karmaşık uygulamalarda gerileme yaratabilir. Aynı zamanda sabit bir sürüme kilitleme tehlikelidir, çünkü sürümünüzden bu yana çıkan güvenlik yamalarını ve hata düzeltmelerini görmezden geliyorsunuzdur. Amacımız <code>package.json`'da aşağıdaki standart semver aralıklarına izin vermektir:</p> 
    * ` 2.0.0 </ 0> sürümünüze yalnızca kararlılık veya güvenlikle ilgili düzeltmeler kabul etmek için <code> ~ 2.0.0 </ 0> kullanın.</li>
<li>Güvenlik ve hata düzeltmelerinin yanı sıra kırılmaz <em> makul derecede kararlı </ 1> özellik işi kabul etmek için <code> ^ 2.0.0 </ 0> kullanın.</li>
</ul>

<p>İkinci nokta ile ilgili önemli olan <code> ^ </ 0> kullanan uygulamaların makul düzeyde bir kararlılık beklemesi gerektiğidir. Bunu gerçekleştirmek için Semver, belirli bir sürümün henüz <em>güvenli</em> veya <em>kararlı</em> olmadığını belirtmek için <em>yayın öncesi tanımlayıcıya</em> izin verir.</p>

<p>Hangisini seçerseniz seçin, bozucu değişiklikler Chromium hayatının bir gerçeği olduğu için periyodik olarak <code> package.json </ 0> sürümününe geçmek zorunda kalacaksınız.</p>

<p>Süreç şöyledir:</p>

<ol>
<li>Tüm yeni büyük ve küçük yayın satırları, <code>N >= 1` için `-beta.N` etiketi ile başlar. Tam da burada, özellik seti **kilitli** olur. Bu sürüm satırı, başka hiçbir özelliği kabul etmiyor ve yalnızca güvenlik kararlılıkları ile ilgilidir. örneğin `2.0.0-beta.1`.
    * Hata düzeltmeleri, regresyon düzeltmeleri ve güvenlik yamaları kabul edilebilir. Bunu yaptıktan sonra `N` bir arttırılarak yeni bir beta yayınlandı. Örneğin. `2.0.0-beta.2`
    * Belirli bir beta sürümünün kararlılığı *genel olarak kabul edilirse*, yalnızca sürüm bilgisi değiştirilerek, kararlı yapı olarak yeniden yayınlanacaktır. Örneğin. `2.0.0`.
    * Gelecekteki hata düzeltmeleri veya güvenlik yamalarının yayın kararlı iken bir araya getirilmesi gerekiyorsa, bunlar uygulanır ve buna göre *yama* sürümü artırılır. Örneğin. `2.0.1`.</ol> 
    
    Her büyük ve küçük darbe için, aşağıdakiler gibi bir şey beklemelisiniz:
    
    ```text
2.0.0-beta.1
2.0.0-beta.2
2.0.0-beta.3
2.0.0
2.0.1
2.0.2
```

Resimlerdeki bir yaşam döngüsü:

* En yeni özellikleri içeren yeni bir sürüm oluşturuldu. ` 2.0.0-beta.1 </ 0> olarak yayınlandı.
<img src="../images/versioning-sketch-3.png" alt="" /></li>
<li>Paketin sürüm şemasına aktarılan bir hata düzelme uzmana gelir, Düzeltme eki uygulanır ve yeni bir beta sürümü şu şeklide yayınlanır <code>2.0.0-beta.2`. ![](../images/versioning-sketch-4.png)
* Beta *genellikle kararlı* olarak kabul edilir ve `2.0.0` altında tekrar beta olmayan olarak yayınlanır. ![](../images/versioning-sketch-5.png)
* Daha sonra, sıfır günlük bir açıklama ortaya çıkar ve ustaca bir düzeltme uygulanır. Düzeltmeyi ` 2-0-x </ 0> çizgisine paketliyoruz ve <code> 2.0.1 </ 0> 'i serbest bırakıyoruz.
<img src="../images/versioning-sketch-6.png" alt="" /></li>
</ul>

<p>Çeşitli semver aralıklarının yeni sürümleri nasıl alacağına ilişkin birkaç örnek:</p>

<p><img src="../images/versioning-sketch-7.png" alt="" /></p>

<h1>Eksik Özellikleri: Alfalar ve Gececiler</h1>

<p>Stratejimiz, şu an uygun olduğunu düşündüğümüz birkaç takas hattı içeriyor. En önemlisi, master'daki yeni özelliklerin kararlı bir sürüm hattına erişmeden önce biraz zaman alması. Hemen yeni bir özellik denemek isterseniz, Electron'u kendiniz kurmanız gerekecek.</p>

<p>Gelecekteki değerlendirmelerde, aşağıdakilerden birini veya her ikisini birlikte sunabiliriz:</p>

<ul>
<li>gece boyunca inşa eden ustalar; bunlar milletlerin yeni özellikleri hızlıca test etmesine ve geri bildirimde bulunmasına izin verecektir</li>
<li>beta sürümlerine göre daha serbest denge kısıtlamaları olan alfa sürümleri; 
örneğin, bir denge kanalı <em>alpha</em> da ise, yeni özellikleri kabul etmek için izin verir</li>
</ul>

<h1>Özellik bayrakları</h1>

<p>Özellik bayrakları Chromium'da yaygın bir uygulamadır ve web geliştirme ekosisteminde iyi kurulmuştur. Elektron bağlamında, özellik bayrağı veya <strong> soft branch </ 0> aşağıdaki özelliklere sahip olmalıdır:</p>

<ul>
<li>çalışma ya da derleme zamanı sırasında etkinleştirilir/devre dışı bırakılır. Biz istek kapsamlı özellik bayrağı anlayışını desteklemiyoruz</li>
<li>bu bölümler tamamen yeni ve eski kod yollarıdır: Bu yeni özellik yeni ve eski kodların yenıden yapılandırılması içindir <em>uygun değil</em> koşullu kontrat özellikleri</li>
<li>belirleyici işaretler hassas bölümler birleştirildikten sonra doğal olarak kaldırılır</li>
</ul>

<p>İşaretlenen kodu sürüm verme stratejimizle aşağıdaki şekilde eşleştiriyoruz:</p>

<ol>
<li>istikrar dalında özellik işaretli kod üzerinde yinelemeyi düşünmüyoruz; Hatta özellik bayrakları dikkatli kullanımı risklidir</li>
<li>aPI sözleşmelerini özellik işaretli kodda, ana sözcüğe darbe indirmeden geçirebilirsiniz. İşaretlenen kod semver'e uymuyor olabilir</li>
</ol>

<h1>Anlamsal örneklendirme</h1>

<p>Biz güncelleme ve serbest bırakma sürecinin her düzeyinde netliği arttırmaya çalışıyoruz. <code> 2.0.0 </ 0> ile başlayarak, aşağıdaki gibi özetlenebilecek olan <a href="https://conventionalcommits.org/"> Konvansiyonel Karar Verme </ 1> spesifikasyonuna uymak için çekme talepleri isteyeceğiz:</p>

<ul>
<li>Semver ile sonuçlanan <strong>major</strong> tümseği ile başlamalıdır <code>BREAKING CHANGE:`.
* Semver ile sonuçlanan **minor** tümseği ile başlamalıdır `feat:`.
* Semver ** yamasına yol açacak komitelerin </ 0> bump'ı ` fix: </ 1> ile başlamalıdır.</p></li>
<li><p>Sıkıştırılmış mesajın yukarıdaki ileti biçimine uyması koşuluyla, taahhütlerin ezilmesine izin veririz.</p></li>
<li>Çekme isteğinde bulunan bazı taahhütlerin semantik önek içermemesi, 
aynı çekme isteğinden daha sonra yapılan bir taahhüt anlamlı bir mesaj içerdiği sürece kabul edilebilir.</li>
</ul>

<h1>Versionless <code>master`</h1> 
    
    * `master` şubesi `package.json` içerisinde daima `0.0.0-dev` içerecektir
    * Serbest branşlar asla ustaya birleştirilmez
    * Serbest şubeler `package.json` içerisinde doğru sürümler bulundurmalıdır