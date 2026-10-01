# 5. Gün — Diziler

Dizi, sırası olan bir listedir. Köşeli parantezle yazılır. Elemanlar aynı türden olmak zorunda değildir. Karışık tür okumayı zorlaştırır.

```js
const raflar = ["un", "şeker", "tuz"]
```

## Boş ve dolu

```js
const bos = []
const sayilar = [4, 8, 15]
const karisik = ["armut", 3, true]
const diziKur = Array(3).fill(0)
const harfler = "Serhat".split("")
```

`Array(3)` üç boş yuva açar. `fill` o yuvaları doldurur. `split`, metin bölümünde metni bölmüştü; sonuç burada dizi olarak kullanılır.

## Ulaşmak ve ölçmek

İndeks sıfırdan başlar. Olmayan indekse gidilirse `undefined` alınır, hata oluşmaz.

```js
const sepet = ["ekmek", "peynir", "zeytin"]
console.log(sepet.length)
console.log(sepet[0])
console.log(sepet[sepet.length - 1])
console.log(sepet[9])
```

## Değiştirmek

`const` dizinin kendisinin yeniden atanmasını engeller. İçinin değişmesini engellemez.

```js
const sepet = ["ekmek", "peynir"]
sepet[1] = "zeytin"
console.log(sepet)
```

## Sona, başa, ortaya

| Metod | Ne yapar | Diziyi bozar mı |
| --- | --- | --- |
| `push` | sona ekler | evet |
| `pop` | sondan alır | evet |
| `unshift` | başa ekler | evet |
| `shift` | baştan alır | evet |
| `splice` | ortadan keser, ekler | evet |
| `slice` | kopya parça verir | hayır |

```js
const sira = ["İzmir", "Van"]
sira.push("İstanbul")
const son = sira.pop()
sira.unshift("Trabzon")
const ilk = sira.shift()
```

`splice(baslangic, silinecekAdet, eklenecekler...)` hem siler hem ekler. Döndürdüğü şey silinenlerin dizisidir, kalan dizi değil.

```js
const gunler = ["pt", "sa", "ça", "pe"]
const silinen = gunler.splice(1, 2, "salı", "çar")
console.log(gunler)
console.log(silinen)
```

`slice(bas, son)` son indeksi dahil etmez. Argümansız `slice()` tüm dizinin sığ bir kopyasını verir. Orijinal bozulmadan çalışılacaksa önce bu kopya alınır.

## Aramak

```js
const renkler = ["mavi", "sarı", "mavi"]
console.log(renkler.indexOf("mavi"))
console.log(renkler.lastIndexOf("mavi"))
console.log(renkler.includes("kırmızı"))
```

`includes` yoksa `false`. `indexOf` yoksa `-1`.

## Birleştirmek ve düzleştirmek

```js
const a = [1, 2]
const b = [3, 4]
const c = a.concat(b)
console.log(c.join(" - "))

const ice = [1, [2, 3], [4, [5]]]
console.log(ice.flat(2))
```

`concat` ve `flat` yeni dizi verir.

## Sıralamak ve ters çevirmek

`reverse` ve `sort` orijinali bozar. Önce kopyala.

`sort` varsayılan olarak **metin** sırası yapar. Sayıda `10`, `2`’den önce gelir çünkü `"10"` ile `"2"` kıyaslanır. Sayı sıralarken karşılaştırma fonksiyonu ver:

```js
const puanlar = [10, 2, 40, 7]
const kopya = puanlar.slice()
kopya.sort((x, y) => x - y)
console.log(kopya)
console.log(puanlar)
```

`x - y` küçükten büyüğe. `y - x` büyükten küçüğe.

## Dizi içinde dizi

Satır ve sütun gibi düşünülür.

```js
const tablo = [
  ["un", 2],
  ["yağ", 1],
]
console.log(tablo[0][0])
console.log(tablo[1][1])
```

## Özet

Bu metodların ne döndürdüğü ve diziyi bozup bozmadığı ayırt edilir. Eleman eleman gezmek 6. günde, `map` ve `filter` 9. günde ele alınır.

## Egzersizler

1. Beş duraklı bir liste kurun: İzmir, Van, İstanbul, Trabzon ve tekrar İzmir. Uzunluğu, ilk ve son öğeyi yazdırın.
2. Listeye `push` ile bir şehir ekleyin, `pop` ile sonuncuyu çıkarın, çıkan adı yazdırın.
3. Ortadaki öğeyi `splice` ile değiştirin.
4. Listenin kopyasını `slice` ile alın, kopyayı `reverse` edin. Aslının durduğunu kontrol edin.
5. `[8, 100, 3, 25]` dizisini sayı sırasına koyun.
6. İki diziyi `concat` ile birleştirin, `join` ile tek metin yapın.
7. `"İzmir;Van;Trabzon"` metninden dizi üretin, `"Van"` var mı bakın.
8. İki sütunlu bir tablo kurun: şehir ve yıl. İkinci satırın yılını indekslerle yazdırın.
9. `const liste = ["Serhat"]` iken `liste = ["Van"]` yazmayı deneyin. Sonra `liste.push("Van")` deneyin. Farkı not edin.

---

[← Önceki gün](../04-conditionals/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../06-loops/ders.md)
