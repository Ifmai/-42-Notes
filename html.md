Öncelikle ne kadar frontend karşıtı olsamda. Fullstack olma açısından bilmek gerekir.
Bu yüzden üzgünüm...


Çoğu html kodlarının başında < !DOCTYPE html > görürsünüz bunun anlamı şudur.

Doctype bir tip belirleme aracıdır. Web siteleri kodu okurken bu tipe bakarak bu sayfanın ne ile alakalı olduğunu anlar
< !DOCTYPE html > üzerinden bir yorum yapıak olursak. Tarayıcımız bunun bir html web sitesini olduğunu anlayacaktır ve buna göre yorumlama işlemlerini yapıcaktır.

Html kodlarının ana bloğu şu şekilde oluşmaktadır. (Zorunlu bir kuraldır.)

    < !DOCTYPE html >
        < html >
            < head >
                sayfanın başlık ve diğer yapı tipleri burda bulunur.
            < /head >
              < body >
                 burası sayfanın içeriğidir
            < /body >
        < /html >


Head etiketnin alt etiketleri sırasıyla şöyledir.

    - < title > (Mutlaka tanımlanmalıdır.)
    -  < style >
    - < base >
    - < link >
    - < meta >
    - < script >
    - < noscript >


Title Etiketi:

    - Tarayıcı araç çubuğu üzerinde görüntülenir.
    - Sayfa sık kullanılanlara eklendiğinde başlık olarak görüntülenir.
    - Arama motoru sonuçlarında başlık olarak görüntülenir.

Style Etiketi:

    - style etiketi HTML belgeleri için stil bilgileri tanımlar."
    - style etiketi HTML etiketlerinin nasıl işleneceğini(biçimlendirme, görüntüleme) tanımlar.
    - HTML belgesi bir çok style etiketi içerebilir.
    - style etiketi "scoped" özelliği belirtilmemişse, head etiketi içerisinde tanımlanmalıdır."

Style içinde kullanabileceğiniz etiketler:

    - media : Ses dosyasının otomatik olarak oynatılacağını belirtir.
    - type : text/css için kullanılır. Tipini şekilini belirle vb.

Dip not: style etiketi html dosyası içinde yapılmış olan style'ları ilgilendirir. Başka bir .css dosyasından style alıcaksanız "link" etiketi kullanmanız gerekir.

Base Etiketi :

    - base etiketi belgedeki tüm göreceli URL'lar için URL veya hedef belirtir.
    - Bir belgede bir base etiketi bulunabilir ve bu etiket "head" etiketi içerisinde tanımlanmalıdır.

Base içinde kullanabileceğiniz etiketler:

    - href : URL alır ve belgedeki tüm göreceli URL'lar için temel URL belirtir.
    - target : Belgedeki tüm bağlantılar ve formlar için hedef belirtir.
    
Meta Etiketi :

    - <meta> etiketi veri hakkında bilgiler verir.
    - Bu etiket HTML belgesi hakkında meta verileri sağlar. Meta verileri tarayıcıda gözükmezler.
    - Meta etiketleri genellikle sayfanın description(açıklama), keywords(anahtar kelimeler), author(sayfa yazarı), last modified(son değiştirilme tarihi) ve diğer meta verilerini tanımlamak için kullanılır.
    - Meta verileri tarayıcılar (sayfa yüklenirken nasıl görüntüleneceği), arama motorları (indexleme ve anahtar kelimeler) veya diğer web servisleri tarafından kullanılırlar.

Metanın içinde kullanabileceğimiz etiketler:

    - charset : karakter kodu.
    - content : metin.
    - http-equiv : Bununda içinde kullanabileceğiniz diğer eklentiler : 
        - content-type
        - default-style
        - refresh
        - örnek <meta http-equiv="refresh" content="20"> sayfayı 20 saniyede bir yeniler.
    - name : buda http-equiv gibi çok işlevli.
        - application-name
        - author : <meta name="authoe" content="github.com/Ifmai"> -> Sayfa yazarının tanımlanması
        - description : <meta name="description" content="Ifmai ile Html"> -> Sayfa açıklamasanın tanımlanması.
        - generator
        - keywords : <meta name="keywords" content="HTML, CSS, Ifmai"> -> Arama motorları için anahtar kelimelerin tanımlanması.

Script Etiketi :

    - <script> etiketi istemci tarafında çalıştırılacak bir script tanımlar. JavaScript gibi.
    - <script> etiketi içerisinde script ifadeleri olabileceği gibi src özelliği ile harici bir script dosyası çağırılabilir.
    - Javascript ile HTML belgelerinizi statik bir yapıdan dinamik bir yapıya geçirebilirsiniz. Değişen içerikler, form kontrolleri vd.

Script içinde kullabileceğimiz etiketler :

    - asnyc : async.//Dip Not a bak.
    - charset : Karakter kodu.
    - defer : defer.
    - src : src.
    - type : tip.

Dip Not :
    
    - Src özelliği tanımlanmış <script> etiketinin içeriği boş olmalıdır.
    - <noscript> etiketi ile JavaScript desteklemeyen veya pasif edilmiş tarayıcılar için bilgi verilebilir.
    - Harici komut dosyası çalıştırmanın birkaç yolu vardır:
    - async="asnyc" özelliği belirtildiğinde, komut sayfanın öğeleri ile uyumsuz çalışır.(Sayfa çözümlenmeye devam ederken komut yürütülür.Uyumsuz)
    - async="asnyc" özelliği belirtilmez ve defer="defer" özelliği belirtilirse, sayfa çözümlemesi tamamlandıktan sonra komut yürütülür.(Erteleme)
    - Her iki özellikde belirtilmişse komut derhal getirilir ve yürütülür, daha sonra tarayıcı sayfayı çözümlemeye devam eder.

Noscript etiketi : 

    - <noscript> etiketi komutların devre dışı bırakıldığı veya komutları desteklemeyen tarayıcılar için alternatif bir içerik tanımlar.
    - Bu etiket ile <body> etiketinin sahip olabileceği tüm etiketler kullanılabilir.
    - <noscript> etiketi belgenin çerçeve desteklemeyen bir başka sayfaya bağlanması için veya gerektiğinde kullanıcıya mesaj vermek için kullanılabilir.