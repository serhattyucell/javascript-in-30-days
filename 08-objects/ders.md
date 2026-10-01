# 8. Gün — Kapsam ve nesneler

Bu bölümde iki konu yan yanadır. İlki bir adın nerede göründüğüdür: kapsam. İkincisi bir kaydı tek yerde tutmaktır: nesne.

## Kapsam

Kapsam, bir adın hangi satırlardan görülebildiğidir.

**Küresel.** Dosyanın en dışında tanımlanan ad her yerden görülür. Tarayıcıda `var` ve fonksiyon bildirimi `window` üstüne de düşer. `let` ve `const` düşmez. Küresel alana çok ad koymak çarpışma yaratır.

**Fonksiyonun içi.** `let` veya `const` ile içeride tanımlanan isim dışarı sızmaz.

```js
function mutfak() {
  const bardak = 4
  console.log(bardak)
}
mutfak()
```

Dışarıda `bardak` yoktur. Konsol `ReferenceError` basar.

**Blok.** `if` ve `for` süslü parantezi de `let`/`const` için duvardır.

```js
if (true) {
  const gizli = 1
}
```

`var` bu duvarı tanımaz. `if` içinde yazılan `var`, fonksiyon boyu görünür. Yeni kodda `var` kullanılmaz.

İç kapsam dıştakini okur. Dış, içtekini okuyamaz. Aynı isim içeride yeniden tanımlanırsa içteki, dıştakini o blok boyunca gölgeler.

## Nesne

Nesne, isimlendirilmiş alanların çantasıdır. Anahtar ve değer. Süslü parantez.

```js
const kayit = {
  ad: "Serhat",
  sehir: "Van",
  aktif: true,
}
```

Boş başlayıp alan eklenebilir:

```js
const dolap = {}
dolap.raf = 2
dolap["cekmece"] = 1
```

Nokta, anahtar düzgün bir isimse yeter. Değişkenden gelen veya boşluklu anahtarda köşeli parantez şart.

```js
const alan = "sehir"
console.log(kayit[alan])
console.log(kayit.ad)
```

Olmayan alan okunursa `undefined` gelir, program durmaz.

## Alanı güncellemek ve silmek

```js
kayit.sehir = "Trabzon"
kayit.yil = 2026
delete kayit.aktif
```

`const kayit` yeniden atanamaz. `kayit.sehir = "Trabzon"` serbesttir; nesnenin kimliği durur, içi değişir.

## Metod

Fonksiyon da bir değerdir. Nesnenin içine konunca metoda dönüşür. Klasik fonksiyon yazılırsa `this`, o nesneyi gösterir.

```js
const lamba = {
  acik: false,
  ac() {
    this.acik = true
    return this.acik
  },
}

console.log(lamba.ac())
```

Ok fonksiyonunda `this` nesneyi otomatik göstermez. Nesne metodunda ok fonksiyonu kullanılmaz.

## Hazır araçlar

```js
const anahtarlar = Object.keys(kayit)
const degerler = Object.values(kayit)
const ciftler = Object.entries(kayit)
console.log(anahtarlar)
console.log("ad" in kayit)
console.log(kayit.hasOwnProperty("ad"))
```

Kopyalamak için 11. günde yayma ele alınır. Bu bölümde sığ kopya:

```js
const yedek = Object.assign({}, kayit)
```

Bu kopya üst seviyededir. İçinde başka nesne varsa ikisi aynı iç nesneyi paylaşır.

## Gezmek

```js
for (const anahtar of Object.keys(kayit)) {
  console.log(anahtar, kayit[anahtar])
}
```

`for...in` de anahtar verir ama prototipten gelenleri de dolaşabilir. `Object.keys` daha dar ve öngörülebilir olduğu için tercih edilir.

## Dizi ile nesne

Sıra önemliyse ve öğeler aynı türdense dizi kullanılır. Bir kaydın özellikleri varsa nesne kullanılır. “Üçüncü öğe” diziye, “bu kaydın şehri” nesneye gider. İkisi birlikte de durur: nesnelerin dizisi. 9. günün `map` metodu bunu işler.

```js
const menu = [
  { ad: "çorba", fiyat: 80 },
  { ad: "pilav", fiyat: 90 },
]
console.log(menu[1].fiyat)
```

## Egzersizler

1. Bir fonksiyonun içinde `const` tanımlayın, dışarıdan okumayı deneyin, hatayı okuyun.
2. Bir `if` bloğunda `let` tanımlayın, blok dışında okumayı deneyin. Aynı deneyi `var` ile yapın, farkı yazın.
3. Bir kişi nesnesi kurun: `ad` alanı `Serhat`, `sehir` alanı `İzmir` olsun. Bir alanı nokta ile, bir alanı köşeli parantezle okuyun.
4. Nesneye yeni alan ekleyin, bir alanı `delete` ile silin.
5. `tanit` adlı bir metod ekleyin. `this.ad` ve `this.sehir` ile bir cümle döndürsün.
6. `Object.keys` ve `Object.values` çıktısını yazdırın.
7. Üç kayıttan oluşan bir dizi kurun. Her kayıtta şehir ve nüfus olsun. Şehirler İzmir, Van ve Trabzon olsun. İkinci kaydın nüfusunu yazdırın.
8. `Object.assign` ile kopya alın, kopyanın adını değiştirin, aslının değişmediğini görün.

---

[← Önceki gün](../07-functions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../09-higher-order-functions/ders.md)
