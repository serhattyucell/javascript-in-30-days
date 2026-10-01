# 16. Gün — JSON

JSON, veriyi metin olarak taşımanın ortak biçimidir. Sunucu bu metni gönderir ve aynı biçimde alır. JavaScript nesnesine benzer ama dil değildir. Tırnak çifttir. Yorum yoktur. Sondaki virgül yasaktır. Anahtar da tırnaklıdır. Fonksiyon, `undefined` ve `symbol` taşınmaz.

Örnek bir belge:

```json
{
  "sehir": "Van",
  "acik": true,
  "raflar": ["un", "tuz"],
  "puan": null
}
```

## Metinden nesneye

```js
const ham = '{"ad":"Serhat","sehir":"İzmir"}'
const kisi = JSON.parse(ham)
console.log(kisi.ad)
```

Bozuk metin `SyntaxError` fırlatır. Kullanıcıdan veya dosyadan geliyorsa `try/catch` koy.

`parse` ikinci argüman olarak bir dönüştürücü alır. Anahtar ve değeri görür; fonksiyon ne döndürürse o yazılır. `undefined` dönerse o alan düşer. Tarihi metin olarak alıp `Date` nesnesine çevirmek için kullanılır.

```js
const hamTarih = '{"gun":"2026-10-01"}'
const kayit = JSON.parse(hamTarih, (anahtar, deger) => {
  if (anahtar === "gun") return new Date(deger)
  return deger
})
console.log(kayit.gun.getFullYear())
```

## Nesneden metne

```js
const dolap = { ad: "kiler", adet: 3, not: undefined }
const metin = JSON.stringify(dolap)
console.log(metin)
```

`undefined` alan kaybolur. Fonksiyon kaybolur. `NaN` ve `Infinity` `null` olur.

İkinci argüman filtre. Dizi verirsen yalnız o anahtarlar yazılır.

```js
console.log(JSON.stringify(dolap, ["ad"]))
```

Üçüncü argüman girinti. İnsan okusun diye 2 veririm. Tellere giderken boş bırakırım, dosya şişmesin.

```js
console.log(JSON.stringify(dolap, null, 2))
```

Fonksiyon verirsen her alandan geçersin, `parse`’taki gibi. Şifre alanını dışarı sızdırmamak için birebir işe yarar:

```js
const hesap = { ad: "Serhat", sifre: "gizli" }
const guvenli = JSON.stringify(hesap, (anahtar, deger) => {
  if (anahtar === "sifre") return undefined
  return deger
})
```

## Nesne ile JSON aynı şey değil

Nesne bellekte durur. JSON bir metindir. `localStorage` yalnız metin saklar; bu yüzden 17. günde `stringify` ve `parse` birlikte kullanılır. `fetch` cevabı çoğu zaman JSON olarak gelir; 18. günde `response.json()` bu `parse` işini görür.

Kopya almak için `JSON.parse(JSON.stringify(nesne))` derin kopya üretir. İçinde `Date`, `undefined`, fonksiyon veya dairesel bağ varsa bozulur. Küçük sade veride iş görür. Daha temizi `structuredClone`, tarayıcıda ve yeni Node’da var.

## Egzersizler

1. Üç alanlı bir nesneyi güzel girintili JSON metnine çevir, konsola bas.
2. O metni tekrar `parse` et, bir alanı değiştir, yeniden `stringify` et.
3. Bozuk bir metni `parse` etmeyi dene, hatayı yakala.
4. İçinde `undefined` ve bir fonksiyon olan nesneyi çevir. Metinde hangileri kayboldu, bak.
5. `stringify` filtresiyle şifre alanını düşür.
6. `parse` dönüştürücüsüyle `"aktif"` diye bir metin alanı görürsen onu booleana çevir.
7. Bir dizi nesneyi JSON yap, uzunluğunu `metin.length` ile ölç. Sonra parse edip dizi uzunluğuyla karşılaştır.

---

[← Önceki gün](../15-classes/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../17-web-storages/ders.md)
