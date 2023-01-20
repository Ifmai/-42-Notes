C dilinde, mutex (mutual exclusion, birbiriyle çelişen) mekanizması, birden fazla thread'in aynı anda aynı verilere erişmesini engelleyen bir yapıdır. Mutex, tek bir thread'in aynı anda verilere erişmesine izin verir ve diğer thread'lerin erişimine engel olur. Bu sayede, verilere aynı anda erişen thread'ler arasında çakışma olmaz ve verilerin hatalı kullanılması önlenir.

C dilinde, mutex kullanımı için pthread.h kütüphanesi kullanılır. Bu kütüphane, mutex oluşturmak, kilitlemek ve kilidini açmak gibi işlemleri yapmak için gerekli fonksiyonları sağlar.

```c
  // Mutex kilidi alınır
  // Oluşturulan mutex 'i kitler ve buraya gelen diğer thread burda bekler çünkü bu fonksiyona ondan önce giren thread yapısı bu mutex'i çoktan kitlemiştir ve o işini bitirip aşağıdan mutex'in kilidini açana kadar burada bekler.
  // Paylaşılan veri kullanılır
  pthread_mutex_lock(&mutex); 
  i++;
  printf("Thread: i = %d\n", i);
  // Mutex kilidi açılır
  // Hangi thread içeri girdiyse çıkarken mutex kilidini açar ve diğer thread arkadaşıda bu sayede içeri girebilir. Bu sayede ikisinin aynı anda aynı veriyi değiştirmesini engellemiş oluruz. Datarice işlemi dediğimiz olayı engelleriz. Bunu thread.md dosyasında anlatmıştım.
  pthread_mutex_unlock(&mutex);
```

Mutex'lerin ne işe yaradığını anladığınızı umuyorum. Şimdi bunları nasıl kullanıyoruz ?

Kullanmak için önce bir mutex oluşturmamız gerekiyor.

### pthread_mutex_init
```c
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr);
```

Bu fonksiyonun ilk parametresi, oluşturulacak mutex için bir pthread_mutex_t tipinde değişken gerektirir. Bu değişken, oluşturulan mutexin tanımlayıcısını tutar. İkinci parametre ise, mutexin özelliklerini tanımlayan bir pthread_mutexattr_t tipinde değişkendir ve genellikle NULL olarak ayarlanır.

pthread_mutex_init() fonksiyonu, mutex oluşturulurken bir hata oluşursa 0 döndürür. Mutex oluşturulurken bir hata olmazsa, fonksiyon 0 dışında bir değer döndürür.

### pthread_mutex_destroy

pthread_mutex_destroy() fonksiyonu, C dilinde kullanılmış olan bir mutex'i temizlemek için kullanılır. Bu fonksiyon, kullanılmış olan mutex değişkenini ve bu değişkene atanmış olan mutex özelliklerini bellekten siler.

```c
int pthread_mutex_destroy(pthread_mutex_t *mutex);

//Örnek kullanım :
pthread_mutex_destroy(&mutex);
```

### pthread_mutex_lock

pthread_mutex_lock() fonksiyonu, C dilinde bir mutex'in kilidini almak için kullanılır. Bu fonksiyon, bir thread'in mutex'e erişimine izin verir ve diğer thread'lerin erişimine engel olur. Bu sayede, mutex'e aynı anda erişen thread'ler arasında çakışma olmaz ve verilerin hatalı kullanılması önlenir.

```c
int pthread_mutex_lock(pthread_mutex_t *mutex);

//Örnek kullanım :
pthread_mutex_lock(&mutex);
```

### pthread_mutex_unlock

pthread_mutex_unlock() fonksiyonu, C dilinde bir mutex'in kilidini açmak için kullanılır. Bu fonksiyon, mutex'e aynı anda erişimine izin verilen thread'ler arasında çakışma olmamasını sağlar.

```c
int pthread_mutex_unlock(pthread_mutex_t *mutex);

//Örnek kullanım :
pthread_mutex_unlock(&mutex);
```