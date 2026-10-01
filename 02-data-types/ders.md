# 2. Gün — Veri tipleri

Bu bölümde sayı, metin ve tür dönüşümü ele alınır. Metinden parça alma ve `Math` nesnesi de buradadır.

## İlkel ve ilkel olmayan

İlkel tipler tek bir değer taşır: sayı, metin, `true`/`false`, `undefined`, `null`, ayrıca `symbol` ve `bigint`. Başka bir değişkene kopyalandığında kopya bağımsız kalır.

```js
let a = 5
let b = a
a = 9
console.log(b) // 5
```

Nesne ve dizi ilkel değildir. Başka bir değişkene aktarıldıklarında aynı veriyi paylaşırlar. Biri değişince diğeri de değişir. Dizi 5. günde, nesne 8. günde ayrı işlenir.

## Sayı

Tamsayı da ondalık da aynı tiptir. `typeof 3` ve `typeof 3.14` ikisi de `"number"`.

```js
const fiyat = 42.5
const adet = 3
console.log(fiyat * adet)
```

Sıfıra bölme `Infinity` üretir. Anlamsız bir işlem `NaN` bırakır. `NaN`, “sayı değil” anlamına gelir; tipi yine `"number"` çıkar.

```js
console.log(4 / 0)
console.log("elma" * 2)
console.log(typeof NaN)
```

### Math

`Math` hazır bir nesnedir. `new` ile oluşturulmaz, doğrudan kullanılır.

```js
console.log(Math.round(4.6))
console.log(Math.floor(4.9))
console.log(Math.ceil(4.1))
console.log(Math.min(3, 9, 1))
console.log(Math.max(3, 9, 1))
console.log(Math.random())
console.log(Math.abs(-12))
console.log(Math.sqrt(81))
console.log(Math.pow(2, 8))
console.log(Math.PI)
```

`Math.random()` 0 ile 1 arasında bir kesir verir, 1 bu aralığa dahil değildir. 1 ile 6 arasında tam sayı şöyle üretilir:

```js
const zar = Math.floor(Math.random() * 6) + 1
console.log(zar)
```

`floor` aşağı yuvarlar, `* 6` aralığı 0–5 yapar, `+ 1` zarın 1–6 olması içindir.

## Metin

Metin tek tırnak, çift tırnak veya ters tırnak ile yazılır. Ters tırnak şablon kurulmasını sağlar; `${}` içine değer yerleştirilir.

```js
const kisi = "Serhat"
const sehir = "İstanbul"
console.log(`${kisi}, ${sehir}.`)
```

İki metin `+` ile de birleşir. Sayı ile metin `+` ile toplanırsa sayı metne döner. `"4" + 2` sonucu `"42"` olur, `6` olmaz. Çıkarmada değer sayıya zorlanır: `"4" - 2` sonucu `2` olur. Tür kendiliğinden değişebildiği için şüpheli yerde dönüşüm açık yazılır.

Uzunluk `length` ile okunur. İlk karakterin indeksi `0`dır.

```js
const kelime = "Trabzon"
console.log(kelime.length)
console.log(kelime[0])
console.log(kelime[kelime.length - 1])
```

### Metin metodları

Hepsi yeni bir metin döndürür. Aslını bozmaz.

```js
const not = "  Van iskelesi  "
console.log(not.toUpperCase())
console.log(not.toLowerCase())
console.log(not.trim())
console.log(not.includes("iskele"))
console.log(not.indexOf("iskele"))
console.log(not.replace("iskele", "kalesi"))
console.log(not.split(" "))
console.log("Serhat".repeat(2))
console.log("İzmir".startsWith("İz"))
console.log("İzmir".endsWith("mir"))
console.log("İzmir".charAt(1))
console.log("İzmir".slice(1, 4))
console.log("İzmir".substring(0, 2))
```

`indexOf` bulamazsa `-1` döner. `slice` başlangıcı alır, bitişi almaz. Eksi indeks sondan sayar: `"İzmir".slice(-3)` sonucu `"mir"` olur.

`split` metni diziye böler. `"İzmir,Van,Trabzon".split(",")` üç elemanlı bir dizi olur. Tersi `join` dur; diziler bölümünde ele alınır.

## Türü sormak ve dönüştürmek

`typeof` operatörü bir metin döndürür: `"number"`, `"string"`, `"boolean"`, `"undefined"`, `"object"`, `"function"`.

Dönüşüm için açık fonksiyonlar kullanılır:

```js
console.log(Number("12"))
console.log(Number("12.5"))
console.log(Number("elma")) // NaN
console.log(String(12))
console.log(parseInt("18px"))
console.log(parseFloat("18.2kg"))
console.log((18.456).toFixed(1))
```

`Number("")` sonucu `0` olur. `parseInt("12abc")` baştaki sayıyı okur ve `12` kalır. `Number("12abc")` ise `NaN` olur. Dışarıdan gelen metinde `Number` tercih edilir; fazladan karakter varsa belirsizlik görünür kalsın diye.

`toFixed` metin döndürür, sayı değil. Üstüne matematik binecekse tekrar `Number` ile sar.

## Egzersizler

1. Bir ürün fiyatı ve adet tutun. Toplamı konsola yazın. Sonra fiyata yüzde 18 ekleyin.
2. `Math` ile 1 ile 20 arasında rastgele bir tam sayı üretin.
3. `"  İstanbul  "` metnini kırpın, küçük harfe çevirin ve `"stan"` geçip geçmediğine bakın.
4. `Serhat` değerini bir değişkene koyun. İlk harfi, son harfi ve uzunluğu yazdırın.
5. `"İzmir,Van,Trabzon"` metnini diziye bölün.
6. `"200"` metnini sayıya çevirip 15 ekleyin.
7. `"üç"` kelimesini `Number` ile çevirin. `NaN` için `Number.isNaN` kullanın.
8. Şablon metinle `Serhat` ve `Van` değerlerinden “Serhat, Van” cümlesini kurun. Sayı yerine iki değişken kullanın.

---

[← Önceki gün](../01-introduction/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../03-booleans-operators-date/ders.md)
