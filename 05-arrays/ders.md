# 5. Gün — Diziler

Bir değişken bir değer tutar. Beş şehir bir değişkene sığmaz. Dizi, sırası olan listedir. Köşeli parantezle yazılır.

```js
const sehirler = ["İzmir", "Van", "İstanbul", "Trabzon"]
```

Öğeler çoğu zaman aynı türdendir. Karışık tür yasak değildir ama okumayı zorlaştırır. Bir listede hem şehir hem sayı duruyorsa neyin nerede olduğu ayrıca hatırlanır.

## Boş ve dolu kurmak

```js
const bos = []
const sayilar = [4, 8, 15]
const harfler = "Serhat".split("")
const sifirlar = Array(3).fill(0)
console.log(harfler)
console.log(sifirlar)
```

```text
["S", "e", "r", "h", "a", "t"]
[0, 0, 0]
```

`Array(3)` üç boş yuva açar. `fill(0)` yuvaları 0 yapar. `split("")` metni harf harf böler. Ayırıcı boş metinse her karakter ayrı öğe olur.

## Sıraya ulaşmak

İlk öğenin sırası `0`dır. Olmayan sıraya gidilirse hata çıkmaz, `undefined` gelir. Bu sessizlik yanıltır. Var olmayan bir şehri basmadan önce `length`e bakılır.

```js
const sehirler = ["İzmir", "Van", "İstanbul"]
console.log(sehirler.length)
console.log(sehirler[0])
console.log(sehirler[sehirler.length - 1])
console.log(sehirler[9])
```

```text
3
İzmir
İstanbul
undefined
```

Son öğe `length - 1` incidir. Üç öğede son sıra `2`dir. `sehirler[3]` yoktur.

## İçini değiştirmek

`const` listenin kendisine yeni bir liste atanmasını engeller. İçindeki öğenin değişmesini engellemez.

```js
const sehirler = ["İzmir", "Van"]
sehirler[1] = "Trabzon"
console.log(sehirler)
```

```text
["İzmir", "Trabzon"]
```

Şu satır ise hata verir, çünkü listenin kendisi yeniden kuruluyor:

```js
const sehirler = ["İzmir"]
sehirler = ["Van"]
```

## Sona, başa, ortaya

| Metod | Ne yapar | Listeyi değiştirir mi | Ne döndürür |
| --- | --- | --- | --- |
| `push` | sona ekler | evet | yeni uzunluk |
| `pop` | sondan çıkarır | evet | çıkarılan öğe |
| `unshift` | başa ekler | evet | yeni uzunluk |
| `shift` | baştan çıkarır | evet | çıkarılan öğe |
| `splice` | ortadan keser, ekler | evet | kesilenlerin listesi |
| `slice` | bir dilim kopyalar | hayır | yeni liste |

```js
const sira = ["İzmir", "Van"]
sira.push("İstanbul")
console.log(sira)
const son = sira.pop()
console.log(son)
console.log(sira)
sira.unshift("Trabzon")
console.log(sira)
```

```text
["İzmir", "Van", "İstanbul"]
İstanbul
["İzmir", "Van"]
["Trabzon", "İzmir", "Van"]
```

`push` sonrası liste üç şehir olur. `pop` sonuncuyu hem çıkarır hem sana verir. `son` değişkeninde `"İstanbul"` durur, listede kalmaz.

`splice(baslangic, kacTaneSil, eklenecek)` hem siler hem o boşluğa yeni öğe koyar. Döndürdüğü şey kalan liste değil, silinenlerdir.

```js
const gunler = ["pazartesi", "salı", "çarşamba", "perşembe"]
const silinen = gunler.splice(1, 2, "SALI", "ÇARŞAMBA")
console.log(gunler)
console.log(silinen)
```

```text
["pazartesi", "SALI", "ÇARŞAMBA", "perşembe"]
["salı", "çarşamba"]
```

1. sıradan başlayıp 2 öğe silindi, yerlerine iki yeni gün kondu.

`slice(bas, son)` son sırayı almaz. Argümansız `slice()` bütün listenin kopyasını verir. Asıl liste bozulmasın diye önce bu kopya alınır.

```js
const asil = ["İzmir", "Van", "Trabzon"]
const dilim = asil.slice(0, 2)
console.log(dilim)
console.log(asil)
```

```text
["İzmir", "Van"]
["İzmir", "Van", "Trabzon"]
```

## Aramak

```js
const renkler = ["mavi", "sarı", "mavi"]
console.log(renkler.indexOf("mavi"))
console.log(renkler.lastIndexOf("mavi"))
console.log(renkler.includes("kırmızı"))
```

```text
0
2
false
```

`indexOf` ilk eşleşmenin sırasıdır. `lastIndexOf` son eşleşmenin sırasıdır. Yoksa ikisi de `-1` döner. Yalnız var mı diye bakılırken `includes` kullanılır, sonuç `true` veya `false` olur.

## Birleştirmek

`concat` iki listeyi yeni bir listede birleştirir. Eskiler durur. `join` listeyi tek metne yapıştırır. Ayırıcıyı sen seçersin. `flat` iç içe listeyi düzleştirir. Sayı, kaç kat inileceğidir.

```js
const a = ["İzmir", "Van"]
const b = ["İstanbul", "Trabzon"]
const c = a.concat(b)
console.log(c.join(" - "))
console.log([1, [2, 3], [4, [5]]].flat(2))
```

```text
İzmir - Van - İstanbul - Trabzon
[1, 2, 3, 4, 5]
```

## Sıralamak

`sort` ve `reverse` asıl listeyi değiştirir. Kopya gerekirse önce `slice()` alınır.

`sort` varsayılan olarak metin sırası yapar. Sayıda bu şaşırtır. `"10"`, `"2"`den önce gelir çünkü ilk karaktere bakılır. `"1"` , `"2"`den küçüktür.

```js
const puanlar = [10, 2, 40, 7]
const kopya = puanlar.slice()
kopya.sort((x, y) => x - y)
console.log(kopya)
console.log(puanlar)
```

```text
[2, 7, 10, 40]
[10, 2, 40, 7]
```

`x - y` küçükten büyüğe sırlar. Sonuç negatifse `x` öne gelir. `y - x` büyükten küçüğe sırlar. `puanlar` kopya üzerinde sıralandığı için eski halinde kalır.

## Liste içinde liste

İki sütunlu tablo, listenin içinde liste olabilir. İlk köşeli parantez satırı, ikinci köşeli parantez o satırdaki sütunu seçer.

```js
const tablo = [
  ["İzmir", 2020],
  ["Van", 2024],
]
console.log(tablo[0][0])
console.log(tablo[1][1])
```

```text
İzmir
2024
```

`tablo[1]` ikinci satırdır, yani `["Van", 2024]`. Onun `[1]` sırası 2024’tür.

6. gün bu listenin içinde yürüyecek. 9. gün `map` ve `filter` ile yeni liste üretecek. Bu gün metodun listeyi bozup bozmadığı ve ne döndürdüğü ayrılır.

## Egzersizler

1. `["İzmir", "Van", "İstanbul", "Trabzon"]` kur. Uzunluğu, ilk şehri ve son şehri yazdır. Son şehir için `length - 1` kullan.
2. `push` ile `"İzmir"`i bir kez daha ekle. `pop` ile sonuncuyu çıkar. Çıkan adı ve kalan listeyi ayrı yazdır.
3. Ortadaki şehri `splice` ile `"Van"` yap. Silinenler listesini de yazdır.
4. `slice()` ile kopya al. Kopyada `reverse` çağır. Asıl listenin sırasının durduğunu göster.
5. `[8, 100, 3, 25]` listesini küçükten büyüğe sırala. `sort`a fonksiyon vermeden bir de dene. Neden `100` başa geçmiyor, not et.
6. İki şehir listesini `concat` ile birleştir, `join(" / ")` ile tek metin yap.
7. `"İzmir;Van;Trabzon"` metnini `split(";")` ile böl. `includes("Van")` ile bak.
8. İki satırlık bir tablo kur. Her satır `["şehir", yıl]` olsun. İkinci satırın yılını `tablo[1][1]` ile yazdır.
9. `const liste = ["Serhat"]` iken `liste = ["Van"]` dene, hatayı oku. Sonra `liste.push("Van")` dene. Neden biri patlıyor öteki çalışıyor, bir cümle yaz.

---

[← Önceki gün](../04-conditionals/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../06-loops/ders.md)
