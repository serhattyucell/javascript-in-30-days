# 13. Gün — Konsol metodları

`console.log` düz değer basmak için yeter. Nesne dizisi, süre ölçümü, grup, uyarı ve doğrulama için konsolun başka metodları vardır. Tarayıcının geliştirici aracında bunlar renklidir. Node’da da çoğu çalışır; renkler daha sönüktür.

## log, info, warn, error

```js
console.log("akış")
console.info("bilgi, genelde log ile aynı yere düşer")
console.warn("stok az")
console.error("kayıt yazılamadı")
```

`error` kırmızı, `warn` sarıdır. Beklenen durum `log`, dikkat isteyen durum `warn`, işi kıran durum `error` ile yazılır.

## Birden fazla değer ve yer tutucu

```js
const ad = "Serhat"
const puan = 88
console.log("%s puanı %d", ad, puan)
```

`%s` metin, `%d` sayı, `%o` nesnedir. Şablon metin de aynı işi görür ve yeni kodda o tercih edilir. Yer tutucu, eski örneklerde karşılaşıldığı için burada da durur.

## table

Dizi ve nesne listesinde `log` bir duvar basar. `table` sütun açar.

```js
const kisiler = [
  { ad: "Serhat", sehir: "İzmir" },
  { ad: "Serhat", sehir: "Van" },
]
console.table(kisiler)
```

İkinci argüman, görmek istediğin sütunların listesi olabilir: `console.table(kisiler, ["ad"])`.

## assert

İddia doğruysa susar. Yanlışsa hata basar. Testin küçük kardeşi.

```js
const stok = 0
console.assert(stok > 0, "stok bitti", { stok })
```

Koşul `true` ise konsol temiz kalır.

## time

İki nokta arası süreyi ölçerim. İsimler eşleşmek zorunda.

```js
console.time("filtre")
const cift = Array.from({ length: 100000 }, (_, i) => i).filter((n) => n % 2 === 0)
console.timeEnd("filtre")
```

`cift`’i kullanmasan da olur; ölçtüğün şey filtrenin kendisi. Derleyici bazı boş işleri atlayabilir. Ölçümü ciddiye alacaksan sonucu bir değişkende tut, bir kez de `cift.length` oku.

## count

Aynı etiketin kaç kez geçtiğini sayar.

```js
;["ayva", "armut", "ayva"].forEach((meyve) => {
  console.count(meyve)
})
console.countReset("ayva")
```

## group

İlgili satırları iç içe katlar. Açılır kapanır. Karışık logda hayat kurtarır.

```js
console.group("sipariş 19")
console.log("çay")
console.log("simit")
console.groupEnd()
```

`groupCollapsed` kapalı başlar.

## clear ve trace

`console.clear` ekranı süpürür. Deneme sırasında kullanılabilir; bitmiş uygulamada bırakılmaz.

`console.trace` o satıra gelene kadar çağrı zincirini basar. Fonksiyonun nereden çağrıldığını `error` kadar gürültülü olmadan gösterir.

## Egzersizler

1. Bir uyarı ve bir hata bas. Konsolda renklerine bak.
2. Üç nesnelik bir diziyi `console.table` ile yazdır. Sonra yalnız bir sütunu göster.
3. `console.assert` ile bir dizinin boş olmadığını iddia et. Boş dizi ver, mesajı gör. Dolu dizi ver, sustuğunu gör.
4. 100 bin elemanlı bir dizide `map` süresini `time` / `timeEnd` ile ölç.
5. Bir döngüde iki farklı etiketi `count` ile say.
6. `group` içinde üç satır bas, grubu kapat.
7. Küçük bir fonksiyonu başka bir fonksiyondan çağır, içerde `console.trace` koy. Zinciri oku.

---

[← Önceki gün](../12-regular-expressions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../14-error-handling/ders.md)
