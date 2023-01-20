
Thread, bir programda birden fazla iş parçacığının aynı anda çalıştırılabildiği anlamına gelir. Threadler, bir programın birkaç işlemi aynı anda yapabilmesine olanak verir, böylece program daha hızlı çalışır. Örneğin, bir programda bir thread bir dosyayı okurken, diğer thread bir veritabanına bağlanabilir. Bu sayede, bir işlem tamamlanırken diğer işlemler de aynı anda çalıştırılabilir.

Threadler, genellikle bir işletim sisteminde bir programın çalışması sırasında oluşturulur. Bir programda birden fazla thread oluşturulabilir ve her bir thread farklı bir işlemi yapabilir. Bu sayede, bir program daha hızlı çalışabilir ve daha verimli bir şekilde kullanılabilir.

Bu kod, pthread_create() fonksiyonu kullanılarak iki farklı thread oluşturur ve her bir threadin içinde farklı bir işlev yer alır. Bu threadler, pthread_join() fonksiyonu ile bekletilir ve sonra "Function 1 çalışıyor" ve "Function 2 çalışıyor" mesajları ekrana yazdırılır. Son olarak, "İki thread tamamlandı" mesajı ekrana yazdırılır.

Thread dediğimiz yapı aslında bize bir paralel progralama yapmamızı sağlıyor. Şimdi bir yeni tabir daha paralel programlama nedir ?
Paralel programlama bir programın main kısmı çalışırken yanda paralel bir biçimde farklı fonksiyonları koşturmamızdır kısaca ve basite indirerek böyle bir açıklama yapabilirim.

### Vikipedi açıklaması :
Paralel hesaplama, ya da Koşut hesaplama, aynı görevin, sonuçları daha hızlı elde etmek için çoklu işlemcilerde eş zamanlı olarak işletilmesidir. Bu fikir, problemlerin çözümünün ufak görev parçalarına bölünmesi ve bunların eş zamanlı olarak koordine edilmesine dayanır.

Threadler bize bunu yaparken yardımcı olan yapıdır. Üç farklı thread aynı değişkeni kullanıyorsa hepsi aynı adresi tutuyorlar. Örneğin iki adet thread açtık ve bir fonksiyona gönderdik bu fonksiyonda bir i değişkenimiz ve bir a değişkenimiz olsun a 1000 olana kadar i değişkenini 1'er 1'er artırsınlar. 2 thread de işini bitirdiğinde i değeri 1000 değil 2000 olucakıtr mainde.
Bu örnekle ne demek istediğimi anladığınızı umuyorum.

Ancak threadler aynı adresi kullandıkları datarice dediğimi data yarışı olayı gerçekleşiyor nasıl ? 
- Bir değişkenin değerini arttırmak üç adımdan oluşuyor. 
	- 1-> Değişken değerinin okunması
	- 2-> Değişken değerinin arttırılması
	- 3-> Değişken değerinin yazılması/işlenmesi
Bu işlemler olurken biri okuyup arttırırken diğeri işlediği durumda ortalık karışıyor çünkü biri 5 yaparken diğeri 6 yapıyor aynı değişkenle bu durumda diğer thread 6 olarak okucakken ikinci thread sonradan 5 yaptığı için değeri 5 olarak okuyor. Bu durumun yaşanmaması içinde mutex yapıları ile threadleri bekletip işlem yaptırıyoruz. Onuda mutex'i anlattığım notta bulabilirsiniz.

### pthread_create
pthread_create() fonksiyonu, C dilinde bir thread oluşturmak için kullanılır. Bu fonksiyon, bir thread oluşturulmasını ve bu threadin bir işlevi çalıştırmasını sağlar.
- Bir int değeri geri döndürür. Eğer 0 dışında bir değer dönerse thread yapısı oluşturulurken hata olmuştur. 0 dönerse düzgün oluşturuldu demektir.
	- 1-> parametre olarak pthread_t adındaki bir değişkenin adresini alır.
	- 2-> bu parametre thread'in pthread_attr_t tipinde özelliklerini tanımladığımız bir değişkendir ve genellikle NULL bırakılır.
	- 3-> bu parametre ise thread'in hangi fonksiyonu çalıştırıcaksa o fonksiyonu buraya yazıyoruz.(void* döndüren bir fonksiyon olmak zorundadır.)
	- 4-> fonksiyonunuz bir parametre alabiliyor bunun içinde kendi data struct yapımızı buraya yazıyoruz. Çünkü bir parametre alıyor tüm parametrelerimizi tek seferde göndermenin tek yolu struct kullanmak.
### pthread_join
Şimdi thread yapılarımızı 2 şekilde aktif edebiliyoruz bunlardan biri join işlemi eğer biz threadlerimizi join ile başlatırsak şöyle bir durum söz konusu oluyor. Threadlerin görevi bitene kadar main akışı durur ve devam etmek için threadlerin görevini yerine getirip kapanmasını beklerler.
    Bir int in değeri döndürür. pthread_join() fonksiyonu, threadin çalışması tamamlandıktan sonra 0 döndürür. Eğer threadin çalışması sırasında bir hata oluşursa, fonksiyon 0 dışında bir değer döndürür.
        1-> oluşturduğumuz thread.
        2-> thread'in döndürdüğü değerleri tutan değişkendir ancak bu genellikle NULL'dur.

### pthread_detach
Şimdi join ile başlattığımızda main akışı duruyordu ancak detach ile bu durum böyle işlemiyor. detach ile başlattığımız threadler çalışırken main akmaya devam edicektir.
    Threadin çalışmasının "detached" (ayrılmış) hale getirilmesini sağlar. Bu fonksiyon, bir threadin çalışması tamamlandıktan sonra otomatik olarak temizlenmesini sağlar.
    Bir int değeri döndürür. pthread_detach() fonksiyonu, threadin "detached" hale getirilmesi sırasında bir hata oluşursa 0 döndürür. Threadin "detached" hale getirilmesi sırasında bir hata olmazsa, fonksiyon 0 döndürür.
        1-> sadece bir değişken alır o da sadece thread'in ismini.