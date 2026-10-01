# 11. Gün — Parçalama ve yayma

Bu bölümde dizi ve nesne tek hamlede açılır. Parçalama, içinden seçip ad vermektir. Yayma, içini başka bir yere sermektir. Parçalamada süslü veya köşeli parantez vardır. Yaymada üç nokta vardır. Rest de üç nokta kullanır. Aynı işaret, durduğu yere göre anlam değiştirir.

## Diziyi parçalamak

Soldan sağa eşleşir.

```js
const renk = ["mavi", "sarı", "yeşil", "mor"]
const [ilk, ikinci] = renk
console.log(ilk, ikinci)
```

Atlamak için boş virgül:

```js
const [, , ucuncu] = renk
```

Varsayılan:

```js
const [a = "yok", b = "yok"] = ["sadece-bu"]
console.log(a, b)
```

Kalanı rest ile topla. Rest sonuncu olmak zorunda.

```js
const [bas, ...geri] = renk
console.log(geri)
```

Takas, geçici değişken olmadan:

```js
let sol = "bardak"
let sag = "tabak"
;[sol, sag] = [sag, sol]
```

Fonksiyon birden fazla değer döndürmek istediğinde dizi döndürür, çağıran parçalar.

```js
function enKucukVeBuyuk(liste) {
  const sirali = liste.slice().sort((x, y) => x - y)
  return [sirali[0], sirali[sirali.length - 1]]
}

const [min, max] = enKucukVeBuyuk([4, 9, 1])
```

Döngüde de işe yarar. `entries` çift üretir:

```js
for (const [sira, ad] of ["İzmir", "Van"].entries()) {
  console.log(sira, ad)
}
```

## Nesneyi parçalamak

İsim, anahtarla aynı olmalı. Sıra önemsiz.

```js
const kayit = { ad: "Serhat", sehir: "İstanbul", aktif: true }
const { ad, sehir } = kayit
```

Yeniden adlandırmak:

```js
const { ad: kisi, sehir: yer } = kayit
```

Varsayılan, anahtar yoksa devreye girer. `undefined` sayılır, `null` sayılmaz.

```js
const { not = "yok" } = kayit
```

İç içe:

```js
const siparis = { masa: 4, hesap: { tutar: 180, bahsis: 20 } }
const {
  hesap: { tutar },
} = siparis
```

## Parametrede parçalama

Fonksiyon nesne bekliyorsa, gövdede `siparis.ad` yazmak yerine parametreyi açarım. Hangi alanı kullandığım kapıda görünür.

```js
function fis({ ad, tutar }) {
  return `${ad}: ${tutar}`
}

console.log(fis({ ad: "çay", tutar: 30, ekstra: true }))
```

Kullanmadığım `ekstra` sessizce durur.

## Yayma

Üç nokta, değeri yerinde açar. Kopya üretirken ve birleştirirken kullanılır. Kopya sığdır: içteki nesneler paylaşılır.

Dizi:

```js
const a = [1, 2]
const b = [3, 4]
const birlikte = [...a, ...b]
const kopya = [...a]
kopya.push(9)
console.log(a)
```

Fonksiyon argümanına sermek:

```js
const notlar = [8, 3, 11]
console.log(Math.max(...notlar))
```

Nesne:

```js
const temel = { renk: "gri", boy: 10 }
const ozel = { ...temel, renk: "mavi" }
console.log(ozel)
console.log(temel)
```

Aynı anahtar iki kez gelirse **sonraki kazanır**. `{ ...yeni, ...eski }` yazarsan eski, yeninin üstünü ezer. Sırayı bilerek seç.

Rest, toplar. Yayma, serer. Sağda `...geri` duruyorsa rest. Çağrıda veya yeni dizi/nesne kurarken duruyorsa yayma.

## Egzersizler

1. Üç elemanlı bir diziden ilk ikisini ayrı değişkenlere al. Üçüncüyü rest ile tut.
2. İki değişkenin değerini parçalama ile takas et.
3. Bir kişi nesnesinden `ad` ve `sehir` çıkar. `sehir` yoksa `"bilinmiyor"` olsun.
4. `ad` alanını `tamAd` diye yeniden adlandırarak parçala.
5. İki nesneyi yayma ile birleştir. Ortak alanda sonrakinin kazandığını göster.
6. Bir dizi kopyasına eleman ekle, aslının değişmediğini yazdır.
7. `Math.min` içine bir sayı dizisini yay.
8. Parametresi parçalanmış bir `etiket({ ad, fiyat })` fonksiyonu yaz.

---

[← Önceki gün](../10-sets-and-maps/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../12-regular-expressions/ders.md)
