# 16. Gün — JSON

JSON, veriyi metin olarak taşımanın ortak biçimidir. Sunucu bu metni gönderir, tarayıcı aynı biçimde geri yollar. JavaScript nesnesine benzer ama dil değildir. Nesne bellekte durur. JSON bir metin dosyası gibi durur. İkisi aynı şey değildir.

Kurallar şunlardır:

- Anahtar da değer de çift tırnak kullanır. Tek tırnak bozuktur.
- Yorum yazılmaz.
- Sondaki virgül yasaktır.
- Fonksiyon, `undefined` ve `symbol` taşınmaz.

Geçerli bir belge:

```json
{
  "ad": "Serhat",
  "sehir": "Van",
  "aktif": true,
  "duraklar": ["İzmir", "Trabzon"],
  "not": null
}
```

Bunu bir `.js` dosyasına yapıştırmak hata verir. JSON, `script` içinde çalışan kod değildir. Ya tırnak içinde metin olarak durur ya da `fetch` ile dosyadan gelir.

## Metinden nesneye

`JSON.parse` metni nesneye çevirir.

```js
const ham = '{"ad":"Serhat","sehir":"İzmir"}'
const kisi = JSON.parse(ham)
console.log(kisi.sehir)
console.log(typeof ham)
console.log(typeof kisi)
```

```text
İzmir
string
object
```

`ham` hâlâ metindir. `kisi` artık nesnedir, noktayla alan okunur.

Bozuk metin `SyntaxError` fırlatır. 14. gündeki `try/catch` ile sarılır.

```js
try {
  JSON.parse("{ad:}")
} catch (hata) {
  console.log(hata.name)
}
```

```text
SyntaxError
```

Anahtar tırnaksız, bu yüzden bozuktur.

`parse` ikinci argüman olarak bir dönüştürücü alır. Her alan oradan geçer. Fonksiyon ne döndürürse o yazılır. `undefined` dönerse alan düşer.

```js
const hamTarih = '{"gun":"2026-10-01","sehir":"Van"}'
const kayit = JSON.parse(hamTarih, (anahtar, deger) => {
  if (anahtar === "gun") {
    return new Date(deger)
  }
  return deger
})
console.log(kayit.gun.getFullYear())
```

```text
2026
```

`gun` metin olarak geldi, `Date`e çevrildi. `sehir` olduğu gibi döndü.

## Nesneden metne

`JSON.stringify` nesneyi metne çevirir.

```js
const dolap = { ad: "Serhat", sehir: "İstanbul", not: undefined }
const metin = JSON.stringify(dolap)
console.log(metin)
```

```text
{"ad":"Serhat","sehir":"İstanbul"}
```

`undefined` alan kaybolur. Fonksiyon da kaybolur. `NaN` ve `Infinity` `null` olur.

İkinci argüman filtredir. Liste verilirse yalnız o anahtarlar yazılır.

```js
console.log(JSON.stringify(dolap, ["sehir"]))
```

```text
{"sehir":"İstanbul"}
```

Üçüncü argüman girintidir. İnsan okusun diye `2` verilir. Ağda giderken boş bırakılır, dosya şişmesin.

```js
console.log(JSON.stringify({ ad: "Serhat", sehir: "Trabzon" }, null, 2))
```

Fonksiyon verilirse her alandan geçilir. Şifre dışarı sızmasın diye o alan `undefined` döndürülür.

```js
const hesap = { ad: "Serhat", sifre: "gizli" }
const guvenli = JSON.stringify(hesap, (anahtar, deger) => {
  if (anahtar === "sifre") {
    return undefined
  }
  return deger
})
console.log(guvenli)
```

```text
{"ad":"Serhat"}
```

`localStorage` yalnız metin saklar. 17. günde nesne önce `stringify`, okurken `parse` edilir. `fetch` cevabı çoğu zaman JSON gelir. 18. günde `response.json()` bu `parse` işini görür.

`JSON.parse(JSON.stringify(nesne))` sade verinin derin kopyasını üretir. İçinde `Date`, `undefined` veya fonksiyon varsa bozulur. Tarayıcıda daha temizi `structuredClone`dur.

## Egzersizler

1. `{ ad: "Serhat", sehir: "Van", yil: 2026 }` nesnesini `JSON.stringify` ile 2 boşluk girintili metne çevir. Konsolda satır satır gör.
2. O metni `parse` et. `sehir`i `"Trabzon"` yap. Yeniden `stringify` et. Eski metindeki Van’ın durduğunu, yeni metinde Trabzon olduğunu gör. `parse` kopya üretir, eski metin değişmez.
3. `"{ad:Serhat}"` metnini `parse` et. Hatayı yakala, `name`in `SyntaxError` olduğunu yazdır.
4. İçinde `not: undefined` ve `merhaba() {}` bulunan bir nesneyi çevir. Metinde ikisinin de kaybolduğunu gör.
5. `stringify` filtresiyle `sifre` alanını düşür. Metinde `sifre` kelimesi geçmesin.
6. `parse` dönüştürücüsüyle `"aktif"` anahtarının değeri `"evet"` ise `true`, `"hayir"` ise `false` yapsın. `{"aktif":"evet","sehir":"İzmir"}` dene. `kayit.aktif === true` olsun.
7. Üç şehirlik bir nesne listesini JSON yap. `metin.length` ile karakter sayısını ölç. Sonra `parse` edip listenin `length`i 3 mü, bak. İki uzunluk aynı şey değildir. Biri karakter, biri öğe sayısıdır.

---

[← Önceki gün](../15-classes/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../17-web-storages/ders.md)
