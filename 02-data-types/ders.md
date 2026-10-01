# 2. Gün — Veri tipleri

1. günde bir değerin sayısı, metni ya da `true`/`false` olabileceği geçti. Bu gün o türlerle gerçekten işlem yapılır. Her örneği konsola yapıştır. Altındaki sonuç satırı sende de aynı çıkmalıdır.

## Kopya neden bazen bağımsızdır

İlkel tip tek bir değer taşır: sayı, metin, `true`/`false`, `undefined`, `null`. Bir de `symbol` ve `bigint` vardır. Onlar bu rehberde gerekmeyecek.

İlkel bir değer başka değişkene verilince kopya bağımsızdır. İkisi iki ayrı kâğıttır.

```js
let a = 5
let b = a
a = 9
console.log(a)
console.log(b)
```

```text
9
5
```

`b`, kopyalandığı andaki `5`’i tutar. `a` sonra `9` olsa da `b` kıpırdamaz.

Dizi ve nesne ilkel değildir. Onlar kâğıt değil, aynı çekmecenin iki kulpudur. Biri değişince öteki de değişir. Bu fark 5. ve 8. günde yeniden görülecek. Şimdilik “sayı ve metin kopyalanınca ayrılır” yeter.

## Sayı

`3` de `3.14` de aynı tiptedir. İkisinin `typeof` sonucu `"number"` olur. Ayrı bir “ondalık tip” yoktur.

```js
const fiyat = 42.5
const adet = 3
console.log(fiyat * adet)
```

```text
127.5
```

Sıfıra bölünce `Infinity` çıkar. Anlamı olmayan işlem `NaN` bırakır. `NaN`, “bu bir sayı değil” demektir. Buna rağmen `typeof NaN` sonucu yine `"number"` olur. Türün adı yanıltır, değerin kendisine bakılır.

```js
console.log(4 / 0)
console.log("elma" * 2)
console.log(typeof NaN)
```

```text
Infinity
NaN
number
```

`Number.isNaN("elma" * 2)` sonucu `true` olur. `===` ile `NaN` aramak işe yaramaz. `NaN === NaN` yanlıştır.

## Math

`Math` hazır duran bir araç kutusudur. `new` ile kurulmaz. Doğrudan `Math.karekok` gibi çağrılır. Türkçe adı yoktur, kutunun adı `Math` olarak kalır.

| Çağrı | Ne yapar | `Math.?( )` örneği | Sonuç |
| --- | --- | --- | --- |
| `round` | en yakın tam sayı | `Math.round(4.6)` | `5` |
| `floor` | aşağı yuvarlar | `Math.floor(4.9)` | `4` |
| `ceil` | yukarı yuvarlar | `Math.ceil(4.1)` | `5` |
| `min` | en küçük | `Math.min(3, 9, 1)` | `1` |
| `max` | en büyük | `Math.max(3, 9, 1)` | `9` |
| `abs` | eksi işaretini atar | `Math.abs(-12)` | `12` |
| `sqrt` | karekök | `Math.sqrt(81)` | `9` |
| `pow` | üs | `Math.pow(2, 8)` | `256` |
| `PI` | pi sayısı | `Math.PI` | `3.14159...` |

`Math.random()` 0 ile 1 arasında bir kesir verir. 1 hiç çıkmaz. Zar için aralık 1–6 olmalıdır. Üç adım vardır:

1. `Math.random()` bir kesir üretir, örneğin `0.42`.
2. `* 6` bunu 0 ile 6 arasına çeker, 6 hariç. `0.42 * 6 = 2.52`.
3. `Math.floor` aşağı yuvarlar, `2` kalır. `+ 1` bunu 1–6 yapar. Sonuç `3`.

```js
const zar = Math.floor(Math.random() * 6) + 1
console.log(zar)
```

Her çalıştırmada 1, 2, 3, 4, 5 veya 6 çıkar. Hepsi aynı değildir. Bu yüzden altta tek bir “doğru çıktı” yazılamaz.

## Metin

Metin üç türlü yazılır. Tek tırnak ve çift tırnak aynı işi görür. Bu derslerde çift tırnak kullanılır. Ters tırnak (klavye sol üst, `Esc` altı) şablon kurar. İçine `${}` ile değişken gömülür.

```js
const kisi = "Serhat"
const sehir = "İstanbul"
console.log(kisi + ", " + sehir + ".")
console.log(`${kisi}, ${sehir}.`)
```

İki satırın ikisi de `Serhat, İstanbul.` basar. İkincisi okunur, çünkü cümle tek parça durur.

Dikkat: sayı ile metin `+` ile yan yana gelirse sayı metne döner, toplanmaz.

```js
console.log("4" + 2)
console.log("4" - 2)
```

```text
42
2
```

`"4" + 2` birleştirmedir. Sonuç `"42"` metnidir. `"4" - 2` çıkarmadır. Çıkarma birleştirmeyi bilmez, `"4"`ü sayıya zorlar, sonuç `2` olur. Bu sessiz dönüşüm hataların sık kaynağıdır. Şüpheli yerde tür aşağıda gösterildiği gibi açık çevrilir.

Uzunluk `length` ile okunur. İlk harfin sırası `0`dır, `1` değil. `"Trabzon"` yedi harftir. Sıra numaraları `0, 1, 2, 3, 4, 5, 6` şeklindedir. Son harf `uzunluk - 1` incidir.

```js
const kelime = "Trabzon"
console.log(kelime.length)
console.log(kelime[0])
console.log(kelime[kelime.length - 1])
```

```text
7
T
n
```

## Metin metodları

Metod, bir değerin üzerinde çağrılan iştir. Metin metodları yeni bir metin döndürür. Tırnak içindeki asıl değer durur.

Aşağıdaki her satırı ayrı çalıştır. Beklenen sonuç yanında yazıyor.

```js
const not = "  Van iskelesi  "
console.log(not.toUpperCase())
console.log(not.toLowerCase())
console.log(not.trim())
console.log(not.includes("iskele"))
console.log(not.indexOf("iskele"))
console.log(not.replace("iskele", "kalesi"))
console.log(not.split(" "))
```

| Çağrı | Sonuç | Ne işe yarar |
| --- | --- | --- |
| `toUpperCase()` | `  VAN İSKELESİ  ` | harfleri büyütür |
| `toLowerCase()` | `  van iskelesi  ` | harfleri küçültür |
| `trim()` | `Van iskelesi` | baştaki ve sondaki boşluğu keser |
| `includes("iskele")` | `true` | parça var mı, evet/hayır |
| `indexOf("iskele")` | `6` | parçanın başladığı sıra; yoksa `-1` |
| `replace(...)` | `  Van kalesi  ` | ilk eşleşeni değiştirir |
| `split(" ")` | üç parçalık liste | metni ayıraca böler |

`indexOf` iki boşluktan sonra sayar. `"  Van "` altı karakterdir (`boşluk boşluk V a n boşluk`), `iskele` 6. sırada başlar. Bulunamazsa `-1` döner. `includes` o durumda `false` döner. Var mı yok mu diye bakarken `includes` daha açıktır.

Başlangıç, bitiş ve dilim:

```js
console.log("İzmir".startsWith("İz"))
console.log("İzmir".endsWith("mir"))
console.log("İzmir".charAt(1))
console.log("İzmir".slice(1, 4))
console.log("İzmir".substring(0, 2))
console.log("İzmir".slice(-3))
console.log("Serhat".repeat(2))
```

```text
true
true
z
zmi
İz
mir
SerhatSerhat
```

`slice(1, 4)` 1. sırayı alır, 4. sırayı almaz. `z m i` kalır. Eksi sayı sondan sayar. `"İzmir".slice(-3)` son üç harf, yani `mir`.

`split` tersine `join` vardır. `"İzmir,Van,Trabzon".split(",")` üç şehirlik bir liste üretir. Listeyi yeniden metne yapıştırmak 5. gündedir.

## Türü sormak ve çevirmek

`typeof` bir metin döndürür: `"number"`, `"string"`, `"boolean"`, `"undefined"`, `"object"`, `"function"`.

Kullanıcı bir kutuya `18` yazdığında gelen şey çoğu zaman metindir. Toplamadan önce sayıya çevrilir.

```js
console.log(Number("12"))
console.log(Number("12.5"))
console.log(Number("elma"))
console.log(String(12))
console.log(parseInt("18px"))
console.log(parseFloat("18.2kg"))
console.log((18.456).toFixed(1))
```

```text
12
12.5
NaN
12
18
18.2
18.5
```

`String(12)` ekranda `12` görünür ama tırnaksız bir sayı değildir. `typeof String(12)` sonucu `"string"` olur.

Üç tuzak:

- `Number("")` sonucu `0` olur. Boş kutu sıfır sanılabilir.
- `parseInt("12abc")` baştaki sayıyı okur, `12` kalır. Geri kalanı atar.
- `Number("12abc")` ise `NaN` olur. Fazladan harf varsa `Number` daha dürüsttür, çünkü bozuk girişi gizlemez.

`toFixed(1)` bir basamak bırakır ve **metin** döndürür. Üstüne `+ 1` yapmak birleştirme yapar. Önce `Number(...)` ile sarmak gerekir.

```js
const yuvarlak = (18.456).toFixed(1)
console.log(yuvarlak + 1)
console.log(Number(yuvarlak) + 1)
```

```text
18.51
19.5
```

## Egzersizler

1. `fiyat = 80`, `adet = 4` olsun. Çarpımı yazdır. Sonra fiyata yüzde 18 ekle. Yüzde 18, fiyatı `1.18` ile çarpmaktır. Sonucu da yazdır.
2. `Math` ile 1 ile 20 arasında rastgele bir tam sayı üret. `* 6 + 1` kalıbını 20’ye uyarla. Üç kez çalıştır, üçünün de 1–20 arasında kaldığını gör.
3. `"  İstanbul  "` metnini `trim` ile kırp, `toLowerCase` ile küçült, `includes("stan")` ile bak. Üç sonucu ayrı satırda yazdır.
4. `const ad = "Serhat"` koy. Uzunluğu, ilk harfi ve son harfi yazdır. Son harf için `length - 1` kullan.
5. `"İzmir,Van,Trabzon"` metnini `split(",")` ile böl. Konsolda bir liste görmelisin.
6. `"200"` metnini `Number` ile çevir, 15 ekle. Sonuç `215` sayı olmalıdır. Çevirmeden `"200" + 15` dene. Neden `20015` çıktığını bir cümleyle yaz.
7. `Number("üç")` sonucunu yazdır. `Number.isNaN` ile kontrol et.
8. `kisi = "Serhat"`, `sehir = "Van"` olsun. Ters tırnakla `Serhat, Van` cümlesini kur.

---

[← Önceki gün](../01-introduction/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../03-booleans-operators-date/ders.md)
