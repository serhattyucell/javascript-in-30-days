# 8. Gün — Kapsam ve nesneler

İki konu vardır. Birincisi bir adın hangi satırlardan görüldüğüdür. Buna kapsam denir. İkincisi bir kaydı tek yerde tutmaktır. Buna nesne denir.

## Kapsam

Kapsam, bir adın hangi satırlardan okunabildiğidir.

**Küresel.** Dosyanın en dışında tanımlanan ad her yerden görülür. Çok ad oraya saçılırsa isimler çarpışır. `var` ve klasik `function` tarayıcıda `window`un üzerine de düşer. `let` ve `const` düşmez. Yeni kodda küresel alana az şey konur.

**Fonksiyonun içi.** İçerideki `let` ve `const` dışarı sızmaz.

```js
function gizliKutu() {
  const sehir = "Van"
  console.log(sehir)
}

gizliKutu()
console.log(sehir)
```

İlk satır `Van` basar. İkinci satır hata verir: `sehir` dışarıda yoktur. Konsol `ReferenceError` der.

**Blok.** `if` ve `for` süslü parantezi de `let` ve `const` için duvardır.

```js
if (true) {
  const gizli = 1
}
console.log(gizli)
```

Bu da `ReferenceError` verir. Aynı yerde `var` yazılsaydı blok duvarı delinirdi ve dışarıdan okunurdu. Yeni kodda `var` kullanılmaz.

İç taraf dıştakini okur. Dış taraf içtekini okuyamaz. Aynı ad içeride yeniden tanımlanırsa, o blokta içteki ad dıştakini gölgeler.

## Nesne

Nesne, adı olan alanların paketidir. Anahtar ve değer. Süslü parantez. Liste sıra tutar. Nesne “bu kaydın şehri Van” demek içindir.

```js
const kayit = {
  ad: "Serhat",
  sehir: "Van",
  aktif: true,
}

console.log(kayit.ad)
console.log(kayit["sehir"])
```

```text
Serhat
Van
```

Nokta, anahtar düzgün bir adsa yeter. Anahtar bir değişkenden geliyorsa veya boşluk taşıyorsa köşeli parantez şarttır.

```js
const alan = "sehir"
console.log(kayit[alan])
```

```text
Van
```

`kayit.alan` bambaşka bir kapı arar. Adı gerçekten `alan` olan bir alan yoktur, sonuç `undefined` olur. Hata çıkmaz. Olmayan alan da `undefined` verir. Bu yüzden yazım hatası sessiz kalabilir.

Boş başlayıp alan eklenebilir:

```js
const not = {}
not.kisi = "Serhat"
not["sehir"] = "İstanbul"
console.log(not)
```

```text
{ kisi: "Serhat", sehir: "İstanbul" }
```

## Güncellemek ve silmek

`const kayit` yeniden atanamaz. `kayit.sehir = "Trabzon"` serbesttir. Paketin kimliği durur, içi değişir.

```js
kayit.sehir = "Trabzon"
kayit.yil = 2026
delete kayit.aktif
console.log(kayit)
```

```text
{ ad: "Serhat", sehir: "Trabzon", yil: 2026 }
```

`delete` alanı kaldırır. `aktif` artık yoktur.

## Metod

Fonksiyon da bir değerdir. Nesnenin içine konunca metod olur. Klasik fonksiyon yazılırsa `this`, o nesneyi gösterir.

```js
const lamba = {
  acik: false,
  sehir: "İzmir",
  ac() {
    this.acik = true
    return this.sehir + " lambası açık"
  },
}

console.log(lamba.ac())
console.log(lamba.acik)
```

```text
İzmir lambası açık
true
```

`this.acik`, lambanın kendi `acik` alanıdır. Ok fonksiyonunda `this` nesneyi otomatik göstermez. Nesne metodunda ok kullanılmaz.

## Hazır araçlar

```js
console.log(Object.keys(kayit))
console.log(Object.values(kayit))
console.log("ad" in kayit)
```

`Object.keys` alan adlarının listesini verir. `Object.values` değerlerin listesini verir. `Object.entries` ikisini çift çift verir. `"ad" in kayit` o kapı var mı diye bakar, `true` veya `false` döner.

`for...in` de alan adı verir ama nesnenin kalıtımdan gelen adlarına da uğrayabilir. `Object.keys` yalnız kendininkilere bakar. Gezmek için o tercih edilir.

```js
for (const anahtar of Object.keys(kayit)) {
  console.log(anahtar + ": " + kayit[anahtar])
}
```

Kopya bu gün sığdır. `Object.assign({}, kayit)` üst alanları yeni bir nesneye taşır. İçerde başka nesne varsa iki kopya aynı iç nesneyi paylaşır. Yayma ile kopya 11. gündedir.

## Liste mi, nesne mi

“Üçüncü şehir” deniyorsa liste. “Serhat’ın şehri” deniyorsa nesne. İkisi birlikte durur: nesnelerin listesi. 9. günün `map`i tam bu listedir.

```js
const kisi = [
  { ad: "Serhat", sehir: "İzmir" },
  { ad: "Serhat", sehir: "Trabzon" },
]
console.log(kisi[1].sehir)
```

```text
Trabzon
```

İkinci kayıt `kisi[1]`dir. Onun `sehir` alanı nokta ile okunur.

## Egzersizler

1. Bir fonksiyonun içinde `const sehir = "Van"` tanımla. Fonksiyonun dışında `console.log(sehir)` dene. `ReferenceError` iletisini oku.
2. Bir `if` bloğunda `let n = 1` tanımla, blok dışında okumayı dene. Aynı deneyi `var` ile yap. `var`ın blok dışından okunduğunu, `let`in okunmadığını gör.
3. `ad: "Serhat"`, `sehir: "İzmir"` olan bir nesne kur. `ad`ı nokta ile, `sehir`i bir değişken ve köşeli parantez ile oku.
4. Nesneye `yil: 2026` ekle. `sehir`i `delete` ile sil. Kalan nesneyi yazdır.
5. `tanit` metodu ekle. `this.ad` ve `this.sehir` ile `Serhat, İzmir` cümlesi döndürsün. Konsola fonksiyon basmasın, `return` etsin.
6. `Object.keys` ve `Object.values` çıktısını yazdır. Anahtar listesinde `ad` geçiyor mu, `"ad" in nesne` ile bak.
7. Üç kayıtlık bir liste kur. Şehirler İzmir, Van ve Trabzon olsun. Her kayıtta `sehir` ve `nufus` olsun. İkinci kaydın nüfusunu yazdır.
8. `Object.assign` ile kopya al. Kopyanın adını değiştir. Asıl nesnenin adının değişmediğini yazdırarak göster.

---

[← Önceki gün](../07-functions/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../09-higher-order-functions/ders.md)
