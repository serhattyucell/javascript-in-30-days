# 3. Gün — Boolean, operatörler, tarih

Bu bölümde doğruluk değeri, karşılaştırma, mantık operatörleri ve `Date` ele alınır. Bir sonraki günün koşulları bu başlıkların üzerine oturur.

## Boolean

Yalnızca iki değer vardır: `true` ve `false`. Karşılaştırma da birçok ifade de bu ikisinden birini bırakır.

```js
console.log(7 > 3)
console.log(7 === "7")
```

### Hangisi dolu sayılır

Koşulun içine sayı veya metin yazılırsa değer mantığa çevrilir.

Dolu sayılanlar: dolu metin, sıfır dışı sayı, dolu dizi, dolu nesne, `true`.

Boş sayılanlar: `0`, `""`, `null`, `undefined`, `NaN`, `false`.

```js
console.log(Boolean("kayık"))
console.log(Boolean(""))
console.log(Boolean(0))
console.log(Boolean(12))
```

`null`, bilerek boş bırakılmış değerdir. `undefined`, henüz değer verilmediğini gösterir. Bir alan boşaltılacaksa `null` yazılır. Alana hiç dokunulmadıysa değer zaten `undefined` kalır.

## Atama

`=` değer koyar. `==` kıyaslar. Bu ikisi sık karışır.

Kısayollar:

```js
let puan = 10
puan += 5
puan -= 2
puan *= 3
puan /= 2
console.log(puan)
```

## Aritmetik, bir kez daha

`+ - * / % **` bir önceki gündeki gibidir. Metinle toplama birleştirir, diğer işlemler sayıyı zorlar. Emin olmak için `Number` kullanılır.

## Karşılaştırma

`>` `<` `>=` `<=` bilinen sıralama.

Eşitlikte iki kapı var:

- `==` türü zorlar. `"4" == 4` doğru çıkar.
- `===` türü de değeri de ister. `"4" === 4` yanlış çıkar.

Karşılaştırmada `===` ve `!==` kullanılır. Türü zorlayan eşitlik beklenmedik sonuç üretir.

```js
console.log(4 == "4")
console.log(4 === "4")
console.log(null == undefined)
console.log(null === undefined)
```

## Mantık

`&&` ikisi de doğruysa doğru. `||` biri doğruysa doğru. `!` tersine çevirir.

```js
const yas = 20
const bilet = true
console.log(yas >= 18 && bilet)
console.log(yas < 18 || bilet)
console.log(!bilet)
```

Bu operatörler son baktıkları değeri de döndürebilir. `"" || "Serhat"` sonucu `"Serhat"` olur. Boş değerde yedek ad koymak için kullanılır.

## Artırma ve azaltma

`puan++` önce değeri kullanır, sonra bir ekler. `++puan` önce ekler, sonra kullanır. Tek başına satırda fark görünmez. İfadenin içinde sonuç şaşırtır. Ayrı satırda `puan += 1` yazmak daha açıktır.

## Üçlü operatör

Kısa karar buradadır. Uzun karar bir sonraki günde `if` ile yazılır.

```js
const sicaklik = 28
const hal = sicaklik > 24 ? "ince giy" : "ceket al"
console.log(hal)
```

## Öncelik

Çarpma toplamadan önce gelir. Sıra net değilse parantez konur. Parantez hem motor hem okuyan için sırayı sabitler.

```js
console.log(2 + 3 * 4)
console.log((2 + 3) * 4)
```

## Tarayıcının üç penceresi

Bunlar tarayıcıda çalışır, saf Node’da yok.

- `alert("kapı kilitli")` — tek bir tamam.
- `prompt("Ad", "Serhat")` — metin ister, iptalde `null` gelir.
- `confirm("çıkayım mı?")` — tamam `true`, iptal `false`.

```js
const ad = prompt("Ad", "Serhat")
if (ad) {
  alert(`${ad}, İzmir`)
}
```

Bu üç metod sayfayı kilitlediği için seyrek kullanılır. Form ve olay 23. günde ele alınır.

## Tarih

`Date` şimdiki anı ya da verilen anı tutar. Ay **0’dan** başlar. Ocak `0`, Aralık `11`. Bu unutulursa takvim bir ay kayar.

```js
const simdi = new Date()
console.log(simdi.getFullYear())
console.log(simdi.getMonth())
console.log(simdi.getDate())
console.log(simdi.getDay())
console.log(simdi.getHours())
console.log(simdi.getMinutes())
console.log(simdi.getSeconds())
console.log(simdi.getTime())
```

`getDay` haftanın günü: pazar `0`. `getDate` ayın günü. İsimler yakın, işleri ayrı.

İki anın farkı milisaniye cinsinden alınır. `getTime()`, 1970’ten bu yana geçen milisaniyedir.

```js
const bas = new Date("2026-10-01")
const bit = new Date("2026-10-11")
const gun = (bit.getTime() - bas.getTime()) / (1000 * 60 * 60 * 24)
console.log(gun)
```

Ekranda göstermek için `toLocaleDateString("tr-TR")` kullanılır.

## Egzersizler

1. Üç değer yazın: dolu bir metin, boş metin, `0`. Üçünün de `Boolean` karşılığını yazdırın.
2. `"9"` ile `9` üzerinde `==` ve `===` deneyin. Farkı bir cümleyle not edin.
3. Bir yaş ve bir `uye` değişkeni tutun. İkisi de uygunsa `"içeri"` yazsın. Üçlü operatör kullanın.
4. `puan +=` ile 0’dan başlayıp 10, sonra yarısı, sonra 3 fazlasını hesaplayın.
5. İçinde bulunulan yıl, ay (1–12) ve günü tek satırda yazdırın. Ayı `+ 1` ile düzeltin.
6. `2026-01-01` ile bugün arasındaki gün sayısını kabaca hesaplayın.
7. Tarayıcıda `confirm` ile bir soru sorun. Cevaba göre konsola iki farklı cümle yazdırın.

---

[← Önceki gün](../02-data-types/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../04-conditionals/ders.md)
