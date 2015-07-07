#Herkes İçin Java SE7, Herbert Schildt Notlarım

##Javaya Genel Bakış
####Java ilk program

Kural olarak <i><b>main'in bulunduğu sınıfın adı, programın tutulduğu dosya adıyla aynı olmalıdır.</b></i> Yani aşağıdaki kodda sınıfımızın ismi Example olduğundan kaynak kodu içeren dosya <i>Example.java</i> olarak isimlendirilmek zorundadır.

```java
// Example.java
class Example {
    public static void main(String[] args) {
        System.out.println("Merhaba Java");
    }
}
```

Şu komutlarla komut satırından programımızı derleyebiliriz. <br/>
Example.java dosyamızın masaüstünde kayıtlı olduğunu varsayalım.

```java
C:\Users\Fatih\Desktop> javac Example.java
C:\Users\Fatih\Desktop> java Example
```

<i><b>javac</b></i> komutuyla java derleyicisi <i>bytecode</i> içeren <i>Example.class</i> oluşturur. <br/>
<i><b>java</b></i> komutuyla bytecode jvm tarafından çalıştırılır. <br/> <hr/>

<b> System.out.println() hakkında </b> <br/>
System <- java.lang paketinde tanımlanmış final sınıftır. <br/>
out &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <- System sınıfının static üyesi ve PrintStream sınıfının referansıdır. <br/>
println &nbsp; <- PrintStream sınıfında tanımlı metoddur. <br/> <hr/>

####Primitif ( Basit ) Tipler
| Tamsayı   |      Kayan noktalı      |  Karakter | Mantıksal
|:----------:|:-------------:|:------:|:-----:|
| byte  |  float | char | boolean |
| short |    double   |
| int |  
| long|

* C/C++ dan farklı olarak tüm veri tipleri kesin olarak tanımlanmış belli bir aralığa sahip olmalıdır.  <br/> </br>
* Java işaretsiz(sadece pozitif) tamsayıları desteklemez. <br/>

<hr/>
<b>byte</b>,  8 bit(1 byte) &nbsp;&nbsp; [-128, 127] <br/>
<b>short</b>, 16 bit(2 byte) <br/>
<b>int</b>, 32 bit(4 byte) &nbsp;&nbsp;&nbsp; [-2, 147,483,648, 2, 147,483,647 ] <br/>
<b>long</b>, 64 bit(8 byte) <br/>
<br/>
<b>char </b>, 16 bit(2 byte) <br/>

<b>float</b>, 32 bit(4 byte) <br/>
<b>double</b>, 64 bit(8 byte) <br/>
<hr/>

* Bir tamsayıya gerek duyulduğunda çoğunlukla en iyisi <i>int</i> dır. (byte ve short deyimler otomatik integera yükseltildiğinden)  <br/> </br>
* Yüksek duyarlılık geremiyorsa kayan noktalı sayılar için float kullanılır.
```java
float num = 0.5f; // compile success
float num = 0.5;  // error: cannot convert from double to float
```


* Java'nın resmi tanımlamasında <i>char</i> bir tamsayı tipi olarak geçer.
```java
char ch1 = 88;  // X
char ch2 = 'Y'; // İki atama da geçerlidir
```


* İki karakteri toplayabilir, değerini artırabilirsiniz.
```java
ch3 = (char)(ch1 + ch2); // compile success
ch3++;                   // compile success
ch3 = ch1 + ch2;         // error: possibly loss conversion from int to char
ch3 = ch3 + 1;           // error: possibly loss conversion from int to char
```
<br/> <br/>

```java
// boolean değişkene atama
boolean flag = false;
```
<br/>

| java      |     matematik           |
|:---------:|:-----------------------:|
| 9         |  (9)<sub>10</sub>       |
| 05        |  (5)<sub>8</sub>        |
| 0xf       |  (f)<sub>16</sub>       |
| 0Xf       |  (f)<sub>16</sub>       |

* long literal tanımlamak için L harfi eklemeliyiz
```java
long num = 9223372036854775807L;
```
* Java SE7'den sonra ikili sayılar şu şekilde tanımlanabilir. <br/>
0b1010 denktir (1010)<sub>2</sub> </br>
0B1010 denktir (1010)<sub>2</sub>

* Ayrıca
```java
int x = 123_456_789; // SE7 den itibaren bu şekilde tanımlama yapılabilir.
```
<br/>
<b> Bilimsel Notasyon </b> <br/>
6.022E23 denktir 6.022 x 10<sup>23</sup> <br/>
2e+100 &nbsp;&nbsp; denktir 2 x 10<sup>100</sup> <br/>
0x12.2P2 denktir (12.2)<sub>16</sub> x 2<sup>2</sup>

* Javada true 1, false 0'a eşit değildir!!
```java
ch =      '@';   // @
ch =     '\'';   // '
ch =       97;   // a
ch =   '\141';   // (141)_8 = 97 = a
ch = '\u0061';   //(61)_16 = 97 = a
```

* Java'da stringler aynı satırda başlayıp bitmek zorundadır. <br/>
* double Math.sqrt(double a) denktir karekök(a) import gerekmiyor. <br/>
* Değişkenler kapsamlarına girildiğinde oluşturulur, çıkıldığında yok edilirler.
```java
class A {
    public static void main(String[] args) {
      int bar = 1;
      {
        int bar = 2; // derleme zamanı hatası -bar daha önce tanımlanmıştır
      }
    }
}
```
<br/>

* char ve boolean birbiriyle uyumlu değildir. Ayrıca nümerik tiplerin char ya da boolean'a otomatik dönüşümü yoktur.Literalde ise sorun olmaz.
```java
// Örneğin :
char ch = 88;  // is legal but
int   i = 88;
char  ch = i;  // is illegal
```

* boolean değişken 1 bitlik bilgiyi simgeler. Ancak bouyutu kesin olarak belirlenmemiştir. JVM bağımlıdır.
