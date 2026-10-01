# 3. Gün — Boolean, operatörler, tarih

Koşul, “şu doğruysa şunu yap” demektir. Doğru ya da yanlış değer üretmeyi bilmeden koşul yazılmaz. Bu gün o değeri üreten karşılaştırmalar, bir de takvim vardır. Yarınki `if` bu günün üzerine oturur.

Örnekleri konsola yapıştır. Altındaki sonuç sende de aynı olmalıdır.

## true ve false

Mantık değerinin yalnız iki hali vardır: `true` ve `false`. Karşılaştırma da bu ikisinden birini bırakır.

```js
console.log(7 > 3)
console.log(7 === 7)
console.log(7 === "7")
```

```text
true
true
false
```

Üçüncü satır yanlıştır çünkü soldaki sayı, sağdaki metindir. Türler aynı değildir.

## Hangi değer dolu sayılır

`if`in içine metin veya sayı yazılırsa JavaScript onu mantığa çevirir. Çeviriyi kendin görmek için `Boolean(...)` kullanılır.

Dolu sayılanlar: dolu metin, 0 dışı sayı, dolu liste, dolu nesne, `true`.

Boş sayılanlar: `0`, `""`, `null`, `undefined`, `NaN`, `false`.

```js
console.log(Boolean("İzmir"))
console.log(Boolean(""))
console.log(Boolean(0))
console.log(Boolean(12))
```

```text
true
false
false
true
```

`null` bilerek boş bırakılmış değerdir. `undefined` henüz değer verilmediğini söyler. Bir kutu boşaltılacaksa `null` yazılır. Kutuya hiç dokunulmadıysa zaten `undefined` kalır.

## Atama ile karşılaştırma

`=` değer koyar. `==` kıyaslar. İkisi sık karışır.

```js
let puan = 10
puan = 12
console.log(puan)
```

`puan = 12` kıyas değildir. Kutunun içini 12 yapar. Kıyas `==` veya `===` iledir.

Aynı işlemi kısa yazmak:

```js
let puan = 10
puan += 5
puan -= 2
puan *= 3
puan /= 2
console.log(puan)
```

Adım adım: 10’a 5 eklenir, 15 olur. 2 çıkar, 13 kalır. 3’le çarpılır, 39 olur. 2’ye bölünür, 19.5 kalır.

## Karşılaştırma

`>` `<` `>=` `<=` bilinen sıradır. Eşitlikte iki kapı vardır.

- `==` türü zorlar. `"4" == 4` doğrudur, çünkü metin sayıya çevrilir.
- `===` hem değeri hem türü ister. `"4" === 4` yanlıştır.

Bu derslerde eşitlik `===`, eşitsizlik `!==` ile yazılır. Türü zorlayan eşitlik gece yarısı hata çıkarır.

```js
console.log(4 == "4")
console.log(4 === "4")
console.log(null == undefined)
console.log(null === undefined)
```

```text
true
false
true
false
```

`null` ile `undefined` yalnız gevşek eşitlikte birbiriyle eşleşir. `===` onları ayırır. Bu yüzden “hiç değer yok” diye bakılırken `===` seçilir.

## Mantık

`&&` ikisi de doğruysa doğrudur. Biri aksarsa bütün ifade aksar. `||` birinin doğru olması yeter. `!` ters çevirir.

Serhat 20 yaşında ve bileti var. İçeri girmek için yaş 18 veya üstü olmalı ve bilet bulunmalı.

```js
const yas = 20
const bilet = true
console.log(yas >= 18 && bilet)
console.log(yas < 18 || bilet)
console.log(!bilet)
```

```text
true
true
false
```

Bu işaretler son baktıkları değeri de döndürebilir. Boş metin dolu değildir, bu yüzden sağdaki yedek adı seçer:

```js
console.log("" || "Serhat")
console.log("Van" || "Serhat")
```

```text
Serhat
Van
```

İkinci satırda soldaki doludur, sağa bakılmaz.

## Bir artır, bir azalt

`puan++` önce eski değeri kullanır, sonra bir ekler. `++puan` önce ekler, sonra kullanır. Tek başına bir satırda fark görünmez. İfadenin içinde görünür.

```js
let puan = 10
console.log(puan++)
console.log(puan)
```

```text
10
11
```

İlkinde konsol henüz artmamış 10’u basar, sonra kutu 11 olur. Karışıklık olmasın diye ayrı satırda `puan += 1` yazılır.

## Üçlü operatör

Tek satırlık seçim. Uzun karar yarın `if` ile yazılır.

```js
const sicaklik = 28
const hal = sicaklik > 24 ? "ince giy" : "ceket al"
console.log(hal)
```

```text
ince giy
```

Kalıp şudur: `koşul ? doğruysa bu : yanlışsa bu`. Soru işareti “ise”, iki nokta “değilse” diye okunur.

## Öncelik

Çarpma toplamadan önce yapılır. `2 + 3 * 4` önce `3 * 4` der, 12 bulur, 2 ekler, 14 olur. Parantez sırayı zorlar. `(2 + 3) * 4` sonucu 20’dir. Sıra kafa karıştırıyorsa parantez konur.

## Tarayıcının üç penceresi

Bunlar yalnız tarayıcıda vardır.

- `alert("kapı kilitli")` tek bir Tamam düğmesi gösterir.
- `prompt("Ad", "Serhat")` metin ister. İptalde `null` gelir.
- `confirm("çıkılsın mı?")` Tamam derse `true`, İptal derse `false` gelir.

```js
const ad = prompt("Ad", "Serhat")
if (ad) {
  alert(`${ad}, İzmir`)
}
```

Bu üçü sayfayı kilitler. Kullanıcı pencereyi kapatmadan sayfa donar. Günlük arayüzde form kullanılır. Form 23. gündedir. Bu gün yalnız ne yaptıklarını görmek için bir kez dene.

## Tarih

`Date` şimdiki anı ya da verilen anı tutar. Ay **0’dan** başlar. Ocak `0`, Aralık `11` olur. Aralık’ı `12` sanmak takvimi bir ay kaydırır.

```js
const simdi = new Date()
console.log(simdi.getFullYear())
console.log(simdi.getMonth())
console.log(simdi.getDate())
console.log(simdi.getDay())
console.log(simdi.getHours())
```

`getFullYear` dört haneli yıldır. `getMonth` 0–11 arasındadır. Ekranda 1–12 göstermek için sonuca `1` eklenir. `getDate` ayın günüdür, 1’den başlar. `getDay` haftanın günüdür, pazar `0`, cumartesi `6` olur. İki ad yakındır, işleri ayrıdır.

`getTime()` 1 Ocak 1970’ten bu yana geçen milisaniyeyi verir. İki tarih çıkarılınca aradaki süre milisaniye olur. Güne çevirmek için `1000 * 60 * 60 * 24`e bölünür. Payda, bir gündeki milisaniyedir.

```js
const gidis = new Date("2026-10-01")
const donus = new Date("2026-10-11")
const gun = (donus.getTime() - gidis.getTime()) / (1000 * 60 * 60 * 24)
console.log(gun)
```

```text
10
```

İnsan gözü için `simdi.toLocaleDateString("tr-TR")` gün.ay.yıl biçimini verir.

## Egzersizler

1. `"Van"`, `""` ve `0` için `Boolean` sonucunu yazdır. Hangileri dolu, bir satır not et.
2. `"9"` ile `9` üzerinde `==` ve `===` dene. Biri neden doğru, öteki neden yanlış, yaz.
3. `yas` ve `uye` değişkeni tut. Yaş en az 18 ve üye ise `"içeri"` yazsın. Üçlü operatör kullan. İki farklı değerle dene, iki sonucu da gör.
4. `puan = 0` ile başla. `+=` ile 10 yap, `/=` ile yarısını al, `+=` ile 3 ekle. Her adımdan sonra yazdır.
5. Bu anın yılını, ayını (1–12) ve gününü tek satırda yazdır. Ay için `getMonth() + 1` kullan.
6. `2026-01-01` ile bugün arasındaki gün sayısını hesapla. Yukarıdaki milisaniye bölmesini kullan.
7. `confirm` ile bir soru sor. `true` ise konsola `Serhat, Trabzon`, `false` ise `iptal` yaz.

---

[← Önceki gün](../02-data-types/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../04-conditionals/ders.md)
