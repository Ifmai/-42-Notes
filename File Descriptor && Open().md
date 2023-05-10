File descriptor (dosya tanımlayıcısı) UNIX ve Linux sistemlerinde, i/o işlemleri için dosya veya i/o aygıtlarını tanımlamak için kullanılan bir tür indekstir. Her dosya veya i/o aygıtı için, sistem tarafından benzersiz bir file descriptor atanır. Bu tanımlayıcı, i/o işlemleri için dosya veya aygıtın hangi kaynak olduğunu tanımlar. Örneğin, bir dosya açma işlemi sırasında, sistem tarafından atanan bir file descriptor, o dosyanın hangi kaynak olduğunu tanımlar ve i/o işlemleri sırasında kullanılır.

File descriptor, `open()` gibi dosya açma işlemleri sırasında veya `socket()` gibi network i/o işlemleri sırasında elde edilir. Bu tanımlayıcılar, i/o işlemleri için kullanılır ve `read()`, `write()`, `close()` gibi i/o işlevleri tarafından kullanılır. Örnek olarak bir dosya açmak için kullanılabilir:

```c
int fd;
fd = open("example.txt", O_RDONLY);// buraya devamına 0777 filan izin ataması yapmaya çalışmayın 0777 decimal olarak algılamaz octal 8 lik sistem olarak alır ve bu da 511'e denk gelir chmode 777 yapmaya çalışırken aslında yaptığınız chmod 511 olur.
```

Bu kod örneğinde, `example.txt` dosyası sadece okunur modunda açılır ve sistem tarafından atanan bir file descriptor `fd` değişkenine atanır. Bu file descriptor daha sonra okuma veya yazma işlemleri için kullanılabilir.

File descriptor ler sistem tarafından atanır ve sistem tarafından yönetilir. Bu nedenle, file descriptor ler program tarafından yönetilmez ve program tarafından atanmaz.

### Open Fonksiyonu

`open()` fonksiyonu için açma modları, dosyanın nasıl açılacağını ve i/o işlemleri için hangi izinlerin verileceğini tanımlar. Açma modları `open()` fonksiyonunun ikinci parametresi olarak kullanılır ve `O_RDONLY`, `O_WRONLY`, `O_RDWR` gibi sabit değerler kullanılır.

-   `O_RDONLY`: Dosya sadece okunur modunda açılır. Bu modda, dosya içeriği okunabilir ama yazılamaz veya değiştirilemez.
-   `O_WRONLY`: Dosya sadece yazma modunda açılır. Bu modda, dosya içeriği yazılabilir ama okunamaz veya değiştirilemez.
-   `O_RDWR`: Dosya okuma ve yazma modunda açılır. Bu modda, dosya içeriği hem okunabilir hem de yazılabilir ve değiştirilebilir.

Ayrıca `open()` fonksiyonu ile birlikte `O_CREAT` ve `O_EXCL` gibi izinlerde kullanılabilir. `O_CREAT` dosya yoksa oluşturulur. `O_EXCL` dosya zaten mevcutsa hata verir.

Açma modları, i/o işlemleri için hangi izinlerin verileceğini tanımlar ve bu nedenle programların dosya veya i/o aygıtlarına nasıl erişeceğini ve i/o işlemlerini nasıl gerçekleştireceğini belirler


### Dip Not

- Open ile ne kadar dosya açabileceğinizi öğrenmek için ulimit -n yazarsanız terminale görebilirsiniz.
- 0 1 2 hali hazırda olan ve özel olarak ayrılmiş fd'lerdir
	- 0 -> Standart input
	- 1 -> Standart output
	- 2 -> Erorr output
- 3 den 11' e kadar 8 adet open ile dosya açalım ve sonrasında close(fd) ile 5.ci fd'yi kapatırsak ve ardından yeni bir dosya açar isek open ile 12 ye değil 5 'e açacaktır. Sıradan ilk bulduğu yere açar.
