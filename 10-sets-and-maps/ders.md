# 10. Gün — Set ve Map

Liste sıra tutar ve tekrara izin verir. `["Van", "Van"]` iki öğedir. Bazen tekrar istenmez. Bazen anahtar metin değildir. İki yapı bunun içindir: `Set` ve `Map`.

## Set

Tekil değerlerin çantasıdır. Aynı değer ikinci kez girmez. Ekleme sırası durur.

```js
const gelen = new Set()
gelen.add("İzmir")
gelen.add("Van")
gelen.add("İzmir")
console.log(gelen.size)
console.log(gelen.has("Van"))
gelen.delete("Van")
console.log(gelen.has("Van"))
```

```text
2
true
false
```

`İzmir` iki kez eklendi, sayıda 1 sayılır. `size` uzunluk değil, öğe sayısıdır. Listede `length` vardı. Burada `size` vardır.

Tekrarlı bir listeyi tekilleştirmek en sık iştir. Üç nokta, seti listeye geri açar.

```js
const ham = ["Van", "İzmir", "Van", "Trabzon"]
const tek = [...new Set(ham)]
console.log(tek)
```

```text
["Van", "İzmir", "Trabzon"]
```

`for...of` ile dolaşılır. Sıra numarası yoktur.

```js
for (const sehir of gelen) {
  console.log(sehir)
}
```

`clear()` hepsini siler.

Eşitlik `===` gibidir. İki ayrı nesne içeriği aynı olsa bile iki öğe sayılır. Set, alanları kıyaslamaz. Referansa bakar.

İki set arasında hazır birleşim metodu yoktur. Listeye açıp `filter` ile yazılır.

```js
const a = new Set([1, 2, 3])
const b = new Set([3, 4])
const birlesim = new Set([...a, ...b])
const kesisim = new Set([...a].filter((n) => b.has(n)))
const fark = new Set([...a].filter((n) => !b.has(n)))
console.log([...birlesim])
console.log([...kesisim])
console.log([...fark])
```

```text
[1, 2, 3, 4]
[3]
[1, 2]
```

Kesişim ikisinde de bulunanlardır. Fark, `a`da olup `b`de olmayandır.

## Map

Anahtar ve değer. Nesneden farkı şunlardır: anahtar metin olmak zorunda değildir, ekleme sırası durur, öğe sayısı `.size` ile okunur.

```js
const nufus = new Map()
nufus.set("İzmir", 4)
nufus.set("Van", 1)
console.log(nufus.get("İzmir"))
console.log(nufus.has("Trabzon"))
nufus.delete("Van")
console.log(nufus.size)
```

```text
4
false
1
```

`get` yoksa `undefined` döner, hata vermez. `set` aynı anahtara yeniden yazılırsa eski değer gider.

Kurarken çiftler verilebilir:

```js
const kisa = new Map([
  ["iz", "İzmir"],
  ["vn", "Van"],
])

for (const [kod, ad] of kisa) {
  console.log(kod + " -> " + ad)
}
```

```text
iz -> İzmir
vn -> Van
```

`keys`, `values` ve `entries` de vardır. Döngüdeki `[kod, ad]` çifti 11. gündeki parçalamadır.

Anahtar nesne de olabilir. `get` aynı nesneyi ister. Aynı görünen yeni bir süslü parantez başka referanstır, bulunamaz.

```js
const defter = { ad: "Serhat" }
const notlar = new Map()
notlar.set(defter, "İstanbul")
console.log(notlar.get(defter))
console.log(notlar.get({ ad: "Serhat" }))
```

```text
İstanbul
undefined
```

## Hangisi seçilir

| İhtiyaç | Yapı |
| --- | --- |
| Sıra önemli, tekrar olabilir | liste |
| Aynı değerden bir tane | set |
| Anahtar metin, biçim sabit | nesne |
| Anahtar sayı ya da nesne, sık ekle-sil | map |

Nesne çoğu kayıt için yeter. Map, anahtar metin olmadığında ya da dışarıdan gelen anahtarlarla karışılmasın istendiğinde seçilir.

## Egzersizler

1. `["Van", "Van", "İzmir", "Trabzon", "İzmir"]` listesini sete çevir. `size` 3 olmalıdır. Listeye geri aç, tekrarları gör.
2. `new Set(["İzmir", "Van"])` ve `new Set(["Van", "Trabzon"])` için kesişimi ve farkı yazdır. Kesişim yalnız `Van` olmalıdır.
3. Şehirden nüfusa giden bir `Map` kur. İzmir, Van, İstanbul, Trabzon. Birini sil, birini `get` ile sor, olmayan bir anahtar için `undefined` gör.
4. Map’i `for...of` ile dolaş. Her satır `Van: 1` biçiminde olsun.
5. Bir nesneyi anahtar yap, değeri `"Serhat"` olsun. Aynı nesneyle `get` çalışsın. Yeni `{ }` ile `get` `undefined` versin. Nedenini bir cümle yaz.
6. `"van izmir van trabzon izmir"` metnini boşluktan böl. Her şehrin kaç kez geçtiğini `Map` ile say. `van` iki, `izmir` iki, `trabzon` bir çıkmalı. Görmeyince değere 0 say, sonra 1 ekle.

---

[← Önceki gün](../09-higher-order-functions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../11-destructuring-and-spread/ders.md)
