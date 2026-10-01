# 7. Gün — Fonksiyonlar

Fonksiyon, adı olan bir iş paketidir. Aynı hesap üç yerde kopyalanmaz; bir kez yazılır ve adıyla çağrılır. Girdiye parametre, çıktıya dönüş değeri denir.

## Bildirim

```js
function selam(kisi, sehir) {
  return `${kisi}, ${sehir}`
}

console.log(selam("Serhat", "Trabzon"))
```

`return` yoksa fonksiyon `undefined` bırakır. `return` sonrasındaki satırlar çalışmaz. Fonksiyon orada biter.

## İfadeye bağlamak

Fonksiyon bir değişkene atanabilir. Bu biçimde satır, tanımın üstünden önce çalışmaz. Klasik `function` bildirimi dosyada yukarı taşınır, tanımdan önce de çağrılabilir. Yeni kodda değişken ve ok fonksiyonu tercih edilir; sıra, dosyada görülen sıradır.

```js
const kare = function (n) {
  return n * n
}
```

## Parametre

Parantezdeki ad, çağrıda verilecek değerin yer tutucusudur. Sıra önemlidir.

```js
function indir(fiyat, oran) {
  return fiyat - fiyat * oran
}

console.log(indir(200, 0.1))
```

Eksik argüman `undefined` gelir. Fazla argüman yok sayılır.

Varsayılan değer verilebilir. Argüman gelmezse o kullanılır.

```js
function fincan(adet = 1, tur = "çay") {
  return `${adet} ${tur}`
}

console.log(fincan())
console.log(fincan(2, "kahve"))
```

## Sınırsız argüman

Kaç değer geleceği bilinmiyorsa rest parametresi kullanılır. Üç noktadan sonraki ad bir dizidir. Rest, son parametre olmak zorundadır.

```js
function toplam(...sayilar) {
  let sonuc = 0
  for (const n of sayilar) {
    sonuc += n
  }
  return sonuc
}

console.log(toplam(4, 5, 6, 7))
```

Eskiden `arguments` adlı gizli bir liste vardı. Ok fonksiyonunda o yoktur. Yeni kodda `...` kullanılır.

## Ok fonksiyonu

Kısa yazımıdır. Tek ifadede `return` ve süslü parantez düşer.

```js
const ikiKat = (n) => n * 2
const bol = (a, b) => {
  if (b === 0) return "bölünmez"
  return a / b
}
```

Tek parametrede parantez de düşebilir: `n => n * 2`. Okunaklılık için parantez durabilir.

Ok fonksiyonu ile klasik fonksiyon `this` bağında ayrılır. Ayrım, sınıflar bölümünde görünür. Kısa işlerde ok, nesnenin kendi metodunda klasik fonksiyon yazılır.

## Kendi kendine çalışan

Tanımlandığı anda bir kez çalışır. Ad vermek gerekmez. Eski kodda kapsam kirletmemek için kullanılırdı. Modül aynı işi görür; ara sıra tek seferlik kurulumda rastlanır.

```js
;(function () {
  const gizli = 7
  console.log(gizli)
})()
```

## Anonim ve geri çağırma

Adı olmayan fonksiyon, çoğu zaman başka bir fonksiyona argüman olur. Adı geri çağırma (callback) dur. 9. gün bu konudadır.

```js
function calistir(is) {
  is()
}

calistir(() => console.log("geldim"))
```

## İpucu

Fonksiyon tek bir iş yapar. Adı fiildir: `hesaplaIndirim`, `okuStok`. Birden fazla iş yapan fonksiyon bölünür. Ara sonuca da ad verilir; anlamsız sayı bırakılmaz.

## Egzersizler

1. Verilen sayının karesini döndüren `kare` yazın.
2. İki metni arada boşlukla birleştiren `birlestir` yazın. İkinci metin gelmezse yalnızca ilkini döndürsün. Deneme değerleri `Serhat` ve `İstanbul` olsun.
3. Sınırsız sayı alıp ortalamasını döndüren bir fonksiyon yazın. Eleman yoksa `0` döndürün.
4. Aynı işi ok fonksiyonuyla yazın.
5. Bir dizideki en büyük sayıyı döndüren fonksiyon yazın. Döngü kullanın. İkinci çözümde `Math.max(...dizi)` deneyin.
6. `selamla` adlı bir fonksiyon yazın. İçine verilen fonksiyonu kişi adıyla çağırsın.
7. Fiyata KDV ekleyen bir fonksiyon yazın. Oran varsayılan `0.2` olsun.
8. `return` koymadan bir fonksiyon çağırın. Gelen değerin `undefined` olduğunu görün.

---

[← Önceki gün](../06-loops/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../08-objects/ders.md)
