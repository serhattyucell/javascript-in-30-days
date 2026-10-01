# 6. Gün — Döngüler

Aynı `console.log`u elle on kez yazmak hem uzun hem hatalıdır. Döngü, bir blok bitene kadar tekrarlar. Bu gün `for`, `while`, `do while`, `for...of` vardır. `break` döngüyü keser. `continue` yalnız o turu atlar.

Sayacı artırmayı unutmak sonsuz döngü yapar. Sekme kilitlenirse sekmeyi kapat. Konsoldaki sayaç her turda değişmiyorsa dur.

## for

Üç parçası vardır. Parantezin içinde noktalı virgülle ayrılır.

1. Başlangıç. Döngüden önce bir kez çalışır. `let i = 0`
2. Koşul. Her turdan önce bakılır. Yanlışsa döngü biter. `i < 5`
3. Tur sonu. Gövde bitince çalışır. `i += 1`

```js
for (let i = 0; i < 5; i += 1) {
  console.log(i)
}
```

```text
0
1
2
3
4
```

5 yazılmaz. Koşul `i < 5` olduğu için `i` 5 olunca gövdeye girilmez. `i += 1` olmazsa `i` hep 0 kalır ve koşul hiç bozulmaz.

Listenin sırasına da bu döngü gider. Hem sıra numarası hem şehir basılacaksa `for` uygundur.

```js
const sehirler = ["İzmir", "Van", "İstanbul", "Trabzon"]
for (let i = 0; i < sehirler.length; i += 1) {
  console.log(i + 1 + ". " + sehirler[i])
}
```

```text
1. İzmir
2. Van
3. İstanbul
4. Trabzon
```

`i` 0’dan başladığı için ekrandaki numara `i + 1` olur. İnsan 1’den sayar, liste 0’dan sayar.

## while

“Şu doğru olduğu sürece” demektir. Sayaç senin artırdığın bir değişkendir. Artmazsa yine sonsuz döngü olur. Koşul baştan yanlışsa gövde hiç çalışmaz.

```js
let kalan = 3
while (kalan > 0) {
  console.log("deneme " + kalan)
  kalan -= 1
}
```

```text
deneme 3
deneme 2
deneme 1
```

## do while

Gövde en az bir kez çalışır. Kontrol sondadır. “Önce bir kez dene, sonra bak” işine gider. Parola veya menü sorusu bu biçime yakındır.

```js
let giris = ""
do {
  giris = "Serhat"
  console.log(giris)
} while (giris === "")
```

```text
Serhat
```

Gövde bir kez çalıştı, `giris` artık boş değildir, döngü durdu. Gerçek sayfada `giris` `prompt` ile alınır. Burada biçim yeter.

## for...of

Listenin öğesini doğrudan verir. Sıra numarası gerekmiyorsa en okunaklı döngü budur.

```js
const sehirler = ["İzmir", "Van", "Trabzon"]
for (const sehir of sehirler) {
  console.log(sehir)
}
```

```text
İzmir
Van
Trabzon
```

Metin de harf harf yürür. `"Van"` üç tur döner: `V`, `a`, `n`.

Sıra da gerekirse `entries()` çift üretir. Köşeli parantez o çifti iki ada böler. Bu bölme 11. günde ayrıca anlatılır.

```js
for (const [sira, sehir] of sehirler.entries()) {
  console.log(sira, sehir)
}
```

```text
0 İzmir
1 Van
2 Trabzon
```

Nesnenin alan adlarında `for...of` yetmez. O iş 8. günde `Object.keys` iledir.

## break ve continue

`break` döngüyü tamamen keser. `continue` o turu atlar, sonraki tura geçer.

```js
for (let n = 1; n <= 8; n += 1) {
  if (n === 5) {
    break
  }
  console.log(n)
}
```

```text
1
2
3
4
```

5’e gelince döngü biter. 6, 7, 8 hiç yazılmaz.

```js
for (let n = 1; n <= 6; n += 1) {
  if (n % 2 === 0) {
    continue
  }
  console.log(n)
}
```

```text
1
3
5
```

Çift sayıda 2’ye bölümden kalan 0’dır. O tur atlanır. Tek sayılar yazılır.

İç içe döngüde `break` yalnız içtekini keser. İkisini birden kesmek için etiket vardır. Etiket okumayı zorlaştırır. İş büyüdüğünde döngü bir fonksiyonun içine alınır ve `return` ile çıkılır. Fonksiyon 7. gündedir.

## İç içe döngü

Dış tur bir kez dönerken iç tur kendi boyunu baştan sona bitirir. Saat ve dakika gibi düşün. Saat bir kez ilerler, dakika 60 kez döner.

```js
for (let satir = 1; satir <= 3; satir += 1) {
  let cizgi = ""
  for (let sutun = 1; sutun <= 3; sutun += 1) {
    cizgi += satir * sutun + " "
  }
  console.log(cizgi)
}
```

```text
1 2 3
2 4 6
3 6 9
```

Birinci satırda `satir` 1’dir. İç döngü 1, 2, 3 ile çarpar. İkinci satırda `satir` 2 olur, çarpımlar 2, 4, 6 olur.

## Egzersizler

1. `for` ile 0’dan 10’a kadar sayıları yazdır. 10 dahil olsun. Koşul `i <= 10` olmalıdır. `i < 10` yazılırsa 10 basılmaz. İkisini de dene.
2. 10’dan 0’a geri say. Başlangıç `10`, koşul `i >= 0`, tur sonu `i -= 1` olsun.
3. 0 ile 50 arasındaki çift sayıları yazdır. Tek sayıda `continue` kullan.
4. `["İzmir", "Van", "İstanbul", "Trabzon"]` listesini `for...of` ile `1. İzmir` biçiminde yazdır. Numara için ya ayrı bir sayaç tut ya da `entries()` kullan.
5. `while` ile `2`den başla, sayı 100’ü geçene kadar ikiye katla. Her değeri yazdır. Kaç adım sürdüğünü ayrı bir sayaçla say.
6. 1’den 7’ye kadar say. 4’te `break` ile çık. Konsolda 5, 6, 7 olmamalı.
7. İç içe döngüyle 5 satır, her satırda 5 tane `#` yazdır.
8. `[4, 8, 15, 16]` listesinin toplamını döngüyle hesapla. Toplam bir `let` içinde biriksin, her turda öğe eklensin. `reduce` bu gün kullanılmaz. O 9. gündedir.
9. Bir sayının asal olup olmadığını bul. 2’den başlayıp sayının kareköküne kadar böl. Bölen çıkarsa asal değildir. 1 ve 0 asal değildir. 2, 9 ve 13 ile dene. 9 asal olmamalı, 13 olmalıdır.

---

[← Önceki gün](../05-arrays/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../07-functions/ders.md)
