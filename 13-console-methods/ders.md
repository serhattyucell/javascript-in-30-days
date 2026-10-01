# 13. Gün — Konsol metodları

`console.log` bir değeri basar. Nesne listesi, süre, grup ve “bu iddia yanlışsa bağır” için başka kapılar vardır. Tarayıcının geliştirici aracında renklenir. Node’da da çoğu vardır, renkler daha sönüktür.

Hepsi sayfada görünmez. Öğrenirken ve hata ararken kullanılır. Biten uygulamada konsola bırakılmaz.

## log, warn, error

```js
console.log("akış")
console.warn("stok az")
console.error("kayıt yazılamadı")
```

`error` kırmızı, `warn` sarıdır. Beklenen durum `log`, dikkat isteyen durum `warn`, işi kıran durum `error` ile yazılır. Sayfa kaydırılırken kırmızı satır kaybolmaz.

Şablon metin yeni kodda tercih edilir. Eski yer tutucuyu tanımak için bir örnek yeter. `%s` metin, `%d` sayıdır.

```js
const ad = "Serhat"
const puan = 88
console.log("%s puanı %d", ad, puan)
console.log(`${ad} puanı ${puan}`)
```

İki satır da `Serhat puanı 88` basar.

## table

Nesne listesinde `log` tek bir yığın basar. `table` sütun açar.

```js
const kisiler = [
  { ad: "Serhat", sehir: "İzmir" },
  { ad: "Serhat", sehir: "Van" },
]
console.table(kisiler)
console.table(kisiler, ["sehir"])
```

Konsolda iki sütunlu bir tablo görünür. İkinci çağrı yalnız `sehir` sütununu bırakır. Liste boşsa tablo da boştur. Hata değildir.

## assert

İddia doğruysa susar. Yanlışsa hata basar.

```js
const stok = 0
console.assert(stok > 0, "stok bitti", { stok })
```

`stok` 0 olduğu için koşul yanlıştır. Konsolda “stok bitti” ve `{ stok: 0 }` görünür. `stok` 3 yapılırsa satır susar. Susmak, iddianın tuttuğu anlamına gelir.

## time

İki nokta arası süreyi ölçer. İsimler aynı olmalıdır. Farklı isim eşleşmez, süre yazılmaz.

```js
console.time("ciftler")
const cift = Array.from({ length: 100000 }, (_, i) => i).filter((n) => n % 2 === 0)
console.timeEnd("ciftler")
console.log(cift.length)
```

Konsolda milisaniye cinsinden bir süre ve `50000` görünür. Süre makineye göre değişir. `cift.length` okunur ki araç, kullanılmayan listeyi atlamasın.

## count, group, clear, trace

`count` aynı etiketin kaç kez geçtiğini sayar. `countReset` sayacı sıfırlar.

```js
;["İzmir", "Van", "İzmir"].forEach((sehir) => {
  console.count(sehir)
})
```

```text
İzmir: 1
Van: 1
İzmir: 2
```

`group` ilgili satırları katlar. Konsolda açılır kapanır bir başlık olur.

```js
console.group("sipariş 19")
console.log("Serhat")
console.log("Van")
console.groupEnd()
```

`console.clear()` ekranı süpürür. Deneme sırasında olur. Bitmiş kodda bırakılmaz.

`console.trace()` o satıra gelene kadar kim kimi çağırdı, zinciri basar. “Bu fonksiyon nereden geldi” sorusu içindir. `error` kadar gürültülü değildir.

## Egzersizler

1. Bir `warn` ve bir `error` bas. Konsolda renklerine bak. İkisini de `log` ile bastığında rengin kaybolduğunu gör.
2. Üç nesnelik bir listeyi `console.table` ile yazdır. Alanlar `sehir` ve `yil` olsun. Şehirler İzmir, Van, Trabzon. Sonra yalnız `sehir` sütununu göster.
3. `console.assert` ile bir listenin boş olmadığını iddia et. Boş liste ver, iletiyi gör. Dolu liste ver, sustuğunu gör.
4. 100 bin öğelik bir listede `map` süresini `time` / `timeEnd` ile ölç. Aynı ölçümü bir de `for` döngüsüyle yap. Hangisi daha uzun sürdü, not et. Fark küçük olabilir.
5. `["Van", "İzmir", "Van"]` üzerinde `count` kullan. Van 2, İzmir 1 olsun.
6. `group` içinde üç satır bas: `Serhat`, `İstanbul`, `2026`. Grubu `groupEnd` ile kapat. Kapatmayı unutursan sonraki loglar da grubun içinde kalır.
7. `dis()` adlı bir fonksiyon `ic()` çağırsın. `ic` içinde `console.trace` olsun. Zincirde `ic` ve `dis` görünsün.

---

[← Önceki gün](../12-regular-expressions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../14-error-handling/ders.md)
