# 10. Gün — Set ve Map

Dizi sıra tutar, tekrara izin verir. Bazen tekrar istemem. Bazen de anahtar her türden olsun isterim. İki yapı bunun için var: `Set` ve `Map`.

## Set

Tekil değerlerin çantası. Sıra, ekleme sırasıdır. Aynı değeri ikinci kez koymaz.

```js
const gelenler = new Set()
gelenler.add("İzmir")
gelenler.add("Van")
gelenler.add("İzmir")
console.log(gelenler.size)
console.log(gelenler.has("Van"))
gelenler.delete("Van")
```

Diziden tekilleştirmek en sık kullandığım hâl:

```js
const ham = ["a", "b", "a", "c"]
const tek = [...new Set(ham)]
console.log(tek)
```

Üç nokta, seti diziye açar. Yayma 11. günde yeniden ele alınır.

Döngü `for...of` ile olur. İndeks yoktur.

```js
for (const kisi of gelenler) {
  console.log(kisi)
}
```

`clear` hepsini siler.

Eşitlik `===` gibidir. Nesneler içeriği aynı olsa bile ayrı referanssa sete ikisi de girer. İçerik karşılaştırması yapmaz.

## İki set arasında

Dilin hazır bir birleşim metodu yoktur; işlem ayrıca yazılır.

```js
const a = new Set([1, 2, 3])
const b = new Set([3, 4])

const birlesim = new Set([...a, ...b])
const kesisim = new Set([...a].filter((n) => b.has(n)))
const fark = new Set([...a].filter((n) => !b.has(n)))
```

## Map

Anahtar ve değer. Nesneden farkı: anahtar yalnızca metin veya sembol olmak zorunda değil. Sayı, nesne, hatta başka bir map olabilir. Ayrıca ekleme sırasını tutar. Boyutu `.size` ile net gelir.

```js
const fiyat = new Map()
fiyat.set("un", 40)
fiyat.set("yağ", 90)
console.log(fiyat.get("un"))
console.log(fiyat.has("tuz"))
fiyat.delete("yağ")
console.log(fiyat.size)
```

Kurarken çiftler verebilirsin:

```js
const gunKisaltma = new Map([
  ["pt", "pazartesi"],
  ["sa", "salı"],
])
```

Gezmek:

```js
for (const [kisa, uzun] of gunKisaltma) {
  console.log(kisa, uzun)
}
```

`keys`, `values`, `entries` de var.

## Hangisini seçerim

- Sıralı liste, tekrar olabilir: dizi.
- Aynı kayıttan bir tane: set.
- Anahtar metinse ve biçim sabitse: nesne.
- Anahtar sayı ya da nesneyse, ya da sık ekleme ve silme varsa: map.

Nesne, çoğu iş için map yerine yeter. Map, anahtar metin olmadığında veya dışarıdan gelen anahtarlar prototiple karışmasın istendiğinde seçilir.

## Egzersizler

1. Tekrarlı bir isim dizisini sete çevir, boyutunu yazdır.
2. İki sayı kümesinin kesişimini ve farkını üret.
3. Bir `Map` kur: ürün adı → stok adedi. Bir ürün ekle, birini sil, birini sorgula.
4. Map’i `for...of` ile dolaş, anahtar ve değeri yazdır.
5. Anahtarı nesne olan bir map dene: bir kitap nesnesini anahtar, ödünç alan kişiyi değer yap. `get` ile aynı nesne referansını kullanırsan değeri bulursun; yeni bir `{...}` ile bulamazsın. Bunu gözünle gör.
6. Bir metindeki kelimeleri say. `split` ve `Map` kullan. Her kelimeyi görünce değerini bir artır.

---

[← Önceki gün](../09-higher-order-functions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../11-destructuring-and-spread/ders.md)
