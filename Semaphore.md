### Semaphore Nedir ? 

Bilgisayar biliminde, semaphore paylaşılan kaynakların erişimini kontrol etmek için kullanılan bir programlama yapısıdır. Özellikle çoklu iş parçacıklı veya çoklu işlem uygulamalarında kullanılır. Bu sayede sadece bir iş parçacığı veya işlem kaynağa aynı anda erişebilir. Böylece yarış durumları ve diğer senkronizasyon sorunları önlenebilir.

Semaphore, genellikle bir tamsayıdır ve kullanılabilir kaynakların sayısını takip etmek için kullanılır. Bir iş parçacığı veya işlem kaynağa erişmek istediğinde, önce semaphore'un değerini kontrol eder. Değer sıfırdan büyükse, iş parçacığı veya işlem semaphore'un değerini azaltır ve kaynağa erişir. Eğer değer sıfırsa, iş parçacığı veya işlem kaynak mevcut olana kadar bloke olur. Bir iş parçacığı veya işlem kaynağı kullandıktan sonra, semaphore'un değerini arttırır ve kaynak başka iş parçacıkları veya işlemler tarafından kullanılabilir hale getirilir.

Semaphore iki türlüdür: binary semaphore ve counting semaphore. Binary semaphore sadece 0 veya 1 değerini alır ve kaynak kullanılıp kullanılmadığını gösterir. Counting semaphore 0 veya daha büyük değer alır ve kullanılabilir kaynakların sayısını gösterir.

Semaphore çoklu iş parçacıklı programlama ve bilgisayar sistemlerinde paylaşılan kaynakların erişimini kontrol etmek için yararlı bir araçtır.


##### Buna bir örnek vericek olursak 

bir örnek olarak, bir web sunucusu uygulamasında birden fazla iş parçacığının aynı anda bir dosyaya erişmesini engellemek için semaphore kullanabilirsiniz. Örneğin, uygulama aşağıdaki gibi bir semaphore değişkeni kullanabilir:

```c
semaphore = 1;
```

Bu semaphore, dosya kaynağının sadece bir iş parçacığı tarafından aynı anda erişilebileceğini gösterir. Eğer bir iş parçacığı dosya kaynağına erişmek isterse, önce semaphore değişkenini kontrol eder. Eğer semaphore değeri 1 ise, iş parçacığı semaphore değerini 0 yapar ve dosya kaynağına erişir. Eğer semaphore değeri 0 ise, iş parçacığı dosya kaynağına erişmek için bekler. Dosya kaynağını kullandıktan sonra, iş parçacığı semaphore değerini 1 yapar ve başka iş parçacıklarının dosya kaynağına erişebilmelerini sağlar.

Bu şekilde, semaphore, birden fazla iş parçacığının aynı anda dosya kaynağına erişememesini ve senkronizasyon sorunlarını önleyerek uygulamanın çalışmasını düzenler.


### Semaphore'ları nerede tanımlamamız gerekir ?

Semaphore'lar genellikle main parent process tarafından tanımlanır ve fork ile açılan child process'ler tarafından kullanılır. Bu sayede child process'ler, semaphore'ları kullanarak main parent process ile haberleşebilir ve bu sayede işlemlerin senkronize edilmesi sağlanabilir. Ancak semaphore'ların fork ile açılan process'ler tarafından tanımlanması da mümkündür. Bu durumda, fork ile açılan her process semaphore'ları kullanabilir.

### Nasıl Tanımlayabiliriz ? 

Şimdiiii burası karışık. Şöyle karışık philo projesinde sem_init() fonksiyonunu kullanmak yasak. Bu yüzden projeye uygun biçimde size tanımlamayı göstericem.

###### Bilmeniz gereken Semaphore fonksiyonları

- Sem_unlink
	- Bir C programlama dili içindeki bir fonksiyondur. Bu fonksiyon, sistemden bir semaforu kaldırmak için kullanılır. Semafor, eşzamanlı bir sistemde paylaşılan kaynakların erişimini kontrol etmek için kullanılan bir veri yapısıdır. sem_unlink() fonksiyonu tek bir argüman alır, bu argüman kaldırılacak semaforun adıdır ve başarılıysa 0, başarısızsa -1 döndürür. Bir semafor unlinked olduktan sonra, hiçbir işlem tarafından erişilemez ve onunla ilişkili tüm kaynaklar serbest bırakılır.

- Sem_open
	- C programlama dili içinde bir fonksiyondur ve yeni bir semafor oluşturmak veya mevcut bir semaforu açmak için kullanılır. Semafor, eşzamanlı bir sistemde paylaşılan kaynakların erişimini kontrol etmek için kullanılan bir veri yapısıdır.
	- sem_open() fonksiyonu başarılıysa semaforeye bir gösterici döndürür veya başarısızsa -1 döndürür.
	- sem_open() fonksiyonu üç argüman alır:
		- İlk argüman, semaforun adıdır.
		- İkinci argüman, semaforun davranışını belirleyen bayraklarıdır. Bazı olası bayraklar şunları içerebilir: O_CREAT, semafor yoksa oluşturur ve O_EXCL, semafor yalnızca yoksa oluşturulduğunda garanti eder.
		- Üçüncü argüman, semaforun izin modu, oktal olarak belirtilir.

"mysem" adlı bir semafor oluşturmak için sem_open() nasıl kullanılacağını gösteren bir örnek :
```c
sem_t *sem;
sem = sem_open("mysem", O_CREAT, 0644, 1);
```

Bu örnek "mysem" adlı bir semafor oluşturur eğer henüz oluşmamışsa izinler 0644 ve başlangıç değeri 1 ile.

Önemli olan not dikkat etmek gerekir ki, semafor artık gerekli değilse, sem_close() ile kapatılması ve sem_unlink() ile unlinked yapılması gerekir, böylece onunla ilişkili tüm kaynaklar serbest bırakılır.

- Sem_close
	- C programlama dili içinde bir fonksiyondur ve daha önce sem_open() ile açılmış bir semaforu kapatmak için kullanılır. Bir semafor kapatıldığında, onunla ilişkili kaynaklar serbest bırakılır ve semafor artık hiçbir işlem tarafından erişilemez.
	- sem_close() fonksiyonu tek bir argüman alır, bu argüman kapatılacak semaforeye bir göstericidir. Fonksiyon başarılıysa 0, başarısızsa -1 döndürür.
	- Önemli olan not dikkat etmek gerekir ki, sem_close() ile bir semaforu kapatmak sistemden semaforu kaldırmaz. Bir semaforu sistemden tamamen kaldırmak için, sem_close() ile kapatıldıktan sonra sem_unlink() fonksiyonu ile unlinked yapılması gerekir.

 sem_open() ile daha önce açılmış bir semaforu kapatmak için sem_close() nasıl kullanılacağını gösteren bir örnek:
```c
sem_t *sem;
sem = sem_open("mysem", O_CREAT, 0644, 1);
sem_close(sem);
```


- Sem_wait && sem_post (mutex'deki lock ve unlock gibi)
	- sem_wait() ve sem_post() C programlama dili içinde kullanılan fonksiyonlardır ve eşzamanlı bir sistemde paylaşılan kaynakların erişimini kontrol etmek için kullanılır. Semafor, paylaşılan kaynakların erişimini kontrol etmek için kullanılan bir veri yapısıdır ve sem_wait() ve sem_post() sırasıyla semaforu elde etmek ve bırakmak için kullanılır.
	- sem_wait() semafor elde etmek için kullanılır. Tek bir argüman alır, bu argüman elde edilecek semaforeye bir göstericidir. Semaforun değeri sıfırdan büyükse, değer azaltılır ve çağrı hemen döndürür. Değer sıfırsa, semafor başka bir işlem tarafından bırakılana kadar çağrı bloke edilir.
	- sem_post() semaforu bırakmak için kullanılır. Ayrıca tek bir argüman alır, bu argüman bırakılacak semaforeye bir göstericidir. Semaforun değeri arttırılır ve semafore üzerinde bloke edilmiş herhangi bir işlem varsa, bunlardan biri bloke edilir.

Paylaşılan bir kaynağın erişimini kontrol etmek için sem_wait() ve sem_post() nasıl kullanılacağını gösteren bir örnek:

```c
sem_t *sem;
sem = sem_open("mysem", O_CREAT, 0644, 1);
sem_wait(sem);
// Paylaşılan kaynak erişimi
sem_post(sem);
```

Bu örnek başlangıç değeri 1 olan "mysem" adlı bir semafor açar, semaforu bekler, paylaşılan kaynağa erişir ve erişim sonrası semaforu bırakır.

sem_wait() ve sem_post()'un yarış koşullarını veya ölü bloğu önlemek için eşleştirilmeli ve doğru sırayla kullanılması gerektiği unutulmamalıdır.



### Semaphore ile mutex arasında ki fark ?

Aralarındaki fark şu biri fork'ların child process'ları arasında haberleşerek çalışırken. Mutexler farklı process üzerinde çalışırken haberleşemezler. 

Dip Not : Semaphorelar ana process dışında sadece child process üzerinde çalışır. Parentlar üzerinden iletişim kuramazlar bu yüzden philo bonus da fork ile açtığımız child process'lar üzerinden işlemler yapıyoruz.