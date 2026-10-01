# 9. Gün — Yüksek seviye fonksiyonlar

Yüksek seviye fonksiyon, fonksiyonu değer gibi taşır. Başka bir fonksiyonu argüman alır ya da fonksiyon döndürür. Listeyi sayaçla dolaşıp yeni liste kurmak yerine bu metodlar kullanılır. Sayaç kaybolur. Geriye “ne istendiği” kalır.

Hepsi aynı liste üzerinde gösterilecek:

```js
const sehirler = ["İzmir", "Van", "İstanbul", "Trabzon"]
```

## Geri çağırma

```js
function tekrarla(kere, is) {
  for (let i = 0; i < kere; i += 1) {
    is(i)
  }
}

tekrarla(3, (i) => console.log("tur " + i))
```

```text
tur 0
tur 1
tur 2
```

`tekrarla` ne basılacağını bilmez. Kendisine verilen fonksiyonu her tur çağırır. Verilen fonksiyona geri çağırma denir.

## Fonksiyon döndürmek

İç fonksiyon, dışının argümanını hatırlar. Buna closure denir. Ayrıntısı 19. gündedir.

```js
function kat(katsayi) {
  return (n) => n * katsayi
}

const ucKat = kat(3)
console.log(ucKat(5))
```

```text
15
```

`kat(3)` bir fonksiyon döndürür. O fonksiyon 3’ü unutmaz. `ucKat(5)` bu yüzden 15 olur.

## Zamanlayıcı

`setTimeout` bir işi geciktirir. `setInterval` tekrarlar. Süre milisaniyedir. 1000, bir saniyedir. İkisi de bir kimlik döndürür. `clearTimeout` ve `clearInterval` o kimlikle durdurur.

```js
const kimlik = setTimeout(() => {
  console.log("bir saniye geçti")
}, 1000)
```

Sayfa açık kalsın. Bir saniye sonra ileti gelir. `clearTimeout(kimlik)` o bekleme bitmeden çağrılırsa ileti hiç gelmez.

## forEach

Her öğe için bir iş yapar. Yeni liste üretmez. Dönüş değeri kullanılmaz.

```js
sehirler.forEach((sehir, indeks) => {
  console.log(indeks + " " + sehir)
})
```

```text
0 İzmir
1 Van
2 İstanbul
3 Trabzon
```

Yeni liste gerekiyorsa `forEach` değil `map` kullanılır.

## map

Aynı uzunlukta yeni bir liste döndürür. Her öğeyi dönüştürür. Asıl liste durur.

```js
const fiyatlar = [10, 20, 30]
const kdvli = fiyatlar.map((f) => f * 1.2)
console.log(kdvli)
console.log(fiyatlar)
```

```text
[12, 24, 36]
[10, 20, 30]
```

`map`in içindeki fonksiyon ne döndürürse yeni listenin o sırasına o konur. `return` unutulursa yeni liste `undefined` ile dolar.

## filter

Koşulu geçenleri yeni listede tutar. Geçmeyenler düşer. Uzunluk kısalabilir.

```js
const stok = [0, 4, 0, 2]
const varOlan = stok.filter((adet) => adet > 0)
console.log(varOlan)
```

```text
[4, 2]
```

## reduce

Listeyi tek değere indirir. Toplam, sayım, gruplama buradadır. İlk değer ikinci argümandır. Verilmezse ilk öğe başlangıç olur. Boş listede ilk değer yoksa hata çıkar. Bu yüzden `0` verilir.

```js
const toplam = [4, 5, 6].reduce((birikim, n) => birikim + n, 0)
console.log(toplam)
```

```text
15
```

Tur tur: birikim 0 ile başlar. 4 eklenir, 4 olur. 5 eklenir, 9 olur. 6 eklenir, 15 olur. Fonksiyon birikimi geri vermelidir. `return` yoksa sonraki tur `undefined` ile devam eder.

## every, some, find, findIndex

```js
const notlar = [70, 80, 90]
console.log(notlar.every((n) => n >= 50))
console.log(notlar.some((n) => n >= 90))
console.log(notlar.find((n) => n > 75))
console.log(notlar.findIndex((n) => n > 75))
```

```text
true
true
80
1
```

`every` hepsi koşulu sağlıyorsa `true`dur. `some` en az biri sağlıyorsa `true`dur. `find` koşulu sağlayan ilk öğeyi verir. Yoksa `undefined`. `findIndex` o öğenin sırasını verir. Yoksa `-1`.

Boş listede `every` `true` döner. Karşı örnek olmadığı için. Boş listede “hepsi geçti” demek şaşırtır. Önce uzunluğa bakılır.

## sort yine

5. günde sayı sırası için `x - y` geçti. Yüksek seviye sayılmasının nedeni, karşılaştıran fonksiyonu argüman almasıdır. Asıl listeyi değiştirir. Önce `slice` ile kopya alınır.

```js
const kayitlar = [
  { ad: "Serhat", sehir: "Van", yas: 30 },
  { ad: "Serhat", sehir: "İzmir", yas: 22 },
]
const sirali = kayitlar.slice().sort((a, b) => a.yas - b.yas)
console.log(sirali[0].sehir)
console.log(kayitlar[0].sehir)
```

```text
İzmir
Van
```

22 yaş İzmir’e aittir, kopyada başa gelir. Asıl listenin başı hâlâ Van’dır.

Zincir kurulur. Önce `filter`, sonra `map`. Her halka yeni liste verdiği için asıl bozulmaz.

```js
const sonuc = [1, 2, 3, 4]
  .filter((n) => n % 2 === 0)
  .map((n) => n * 10)
console.log(sonuc)
```

```text
[20, 40]
```

Çift sayılar 2 ve 4’tür. Onar katı 20 ve 40 eder.

## Egzersizler

1. `[3, 5, 8]` listesini `map` ile iki katına çıkar. Sonuç `[6, 10, 16]` olsun. Asıl listenin değişmediğini yazdır.
2. `[40, 70, 55, 90]` içinden 60’tan büyük notları `filter` ile ayır.
3. `reduce` ile `[4, 5, 6]` toplamını bul. Sonra ortalamayı bul. Ortalama, toplamın uzunluğa bölümüdür.
4. `every` ile bütün notların 50 üstü olup olmadığına bak. `some` ile 100 olup olmadığına bak. 100 yoksa `false` görmelisin.
5. `[{ ad: "Serhat", sehir: "İzmir", yas: 17 }, { ad: "Serhat", sehir: "Van", yas: 21 }]` listesinde yaşı 18’den büyük ilk kaydı `find` ile bul. Şehir `Van` çıkmalı.
6. `setTimeout` ile 2 saniye sonra `Serhat, Trabzon` yazdır. Sayfayı kapatma.
7. `katla(n)` yaz. İçinden `(x) => x * n` döndürsün. `katla(10)(4)` sonucu `14` değil `40` olsun. Çarpma, toplama değildir.
8. Üç fiyatlı nesne listesini ucuzdan pahalıya sırala. Asıl liste bozulmasın. `slice` sonra `sort` kullan.
9. `forEach` ile her şehrin uzunluğunu yazdır. Aynı işi `map` ile yap. `map`in yeni bir sayı listesi döndürdüğünü, `forEach`in `undefined` döndürdüğünü gör.

---

[← Önceki gün](../08-objects/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../10-sets-and-maps/ders.md)
