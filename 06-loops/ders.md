# 6. Gün — Döngüler

Aynı işi elle on kez yazmak yerine döngü kullanılır. Döngü, bir koşul bozulana kadar bir bloğu tekrarlar. Bu bölümde `for`, `while`, `do while`, `for...of`, ayrıca erken çıkış için `break` ve tur atlamak için `continue` ele alınır.

## for

Sayacı döngünün kendisi yönetir. Üç parça vardır: başlangıç, koşul, her tur sonu.

```js
for (let i = 0; i < 5; i += 1) {
  console.log(i)
}
```

`i` 0, 1, 2, 3, 4 olur. Koşul `i < 5` bozulunca durur. `i += 1` yazılmazsa döngü sonsuza gider ve sekme kilitlenir. Sonsuz döngüde sekme kapatılır.

Diziyi böyle gezerim:

```js
const rafta = ["un", "tuz", "yağ"]
for (let i = 0; i < rafta.length; i += 1) {
  console.log(i, rafta[i])
}
```

İndeks gerekiyorsa `for` uygundur. Hem öğe hem sıra numarası yazdırılacaksa bu biçim seçilir.

## while

“Şu doğru olduğu sürece” anlamına gelir. Sayaç içeride ayrıca artırılır.

```js
let kalan = 3
while (kalan > 0) {
  console.log(`deneme ${kalan}`)
  kalan -= 1
}
```

Koşul baştan yanlışsa gövde hiç çalışmaz.

## do while

Gövde **en az bir kez** çalışır, kontrol sonda yapılır. Menü, parola sorma gibi “önce sor, sonra bak” işlerinde işe yarar.

```js
let giris = ""
do {
  giris = "hazır"
} while (giris === "")
```

Gerçek programda `giris`, `prompt` ile alınır. Burada yalnızca biçim gösterilir.

## for...of

Dizinin, metnin ve setin öğesini doğrudan verir. İndeks gerekmiyorsa en okunaklı biçim budur.

```js
const sehirler = ["İzmir", "Van", "Trabzon"]
for (const sehir of sehirler) {
  console.log(sehir)
}
```

Metinde harf harf yürür. İndeks de istenirse `entries()` kullanılır:

```js
for (const [sira, sehir] of sehirler.entries()) {
  console.log(sira, sehir)
}
```

Nesnenin anahtarlarında `for...of` yetmez. O konu 8. günde `Object.keys` ile ele alınır.

## break ve continue

`break` döngüyü tamamen keser. `continue` sadece o turu atlar.

```js
for (let n = 1; n <= 8; n += 1) {
  if (n === 5) break
  console.log(n)
}
```

```js
for (let n = 1; n <= 6; n += 1) {
  if (n % 2 === 0) continue
  console.log(n)
}
```

İç içe döngüde `break` yalnız içtekini keser. Dıştakini de kesmek için etiket kullanılabilir; bu yol önerilmez. İş büyüdüğünde döngü fonksiyona alınır ve `return` ile çıkılır.

## İç içe

Satır ve sütun, çarpım tablosu, ızgara. Dış tur bir kez dönerken iç tur kendi boyunu bitirir.

```js
for (let satir = 1; satir <= 3; satir += 1) {
  let cizgi = ""
  for (let sutun = 1; sutun <= 3; sutun += 1) {
    cizgi += `${satir * sutun} `
  }
  console.log(cizgi)
}
```

## Egzersizler

1. 0’dan 10’a kadar sayıları `for` ile yazdırın.
2. 10’dan 0’a geri sayın.
3. 0 ile 50 arasındaki çift sayıları yazdırın. `continue` kullanın.
4. `["İzmir", "Van", "İstanbul", "Trabzon"]` dizisini `for...of` ile numaralı yazdırın: `1. İzmir`.
5. `while` ile bir sayıyı 100’ü geçene kadar ikiye katlayın. Kaç adım sürdüğünü sayın.
6. 1’den 7’ye kadar sayın. 4’te `break` ile çıkın.
7. İç içe döngüyle 5x5 lik bir `#` ızgarası yazdırın.
8. Bir sayı dizisinin toplamını döngüyle hesaplayın. `reduce` bu bölümde kullanılmaz; 9. günde ele alınır.
9. Bir sayının asal olup olmadığını döngüyle bulun. 2’den sayının kareköküne kadar bölen arayın. Bölen çıkarsa sayı asal değildir.

---

[← Önceki gün](../05-arrays/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../07-functions/ders.md)
