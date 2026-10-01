# 19. Gün — Closure

Closure, bir fonksiyonun doğduğu yerdeki değişkenleri, o yer bittikten sonra da hatırlamasıdır. 9. günde `kat(3)` bir fonksiyon döndürmüş ve `3`ü unutmamıştı. Adı budur.

Fonksiyon, kendi kapsamının çantasıyla birlikte taşınır. Dış fonksiyon biter, çanta durur. Çünkü iç fonksiyon hâlâ o değişkeni kullanıyordur.

```js
function sayacKur(baslangic = 0) {
  let deger = baslangic
  return {
    artir() {
      deger += 1
      return deger
    },
    oku() {
      return deger
    },
  }
}

const a = sayacKur()
const b = sayacKur(10)
console.log(a.artir())
console.log(a.artir())
console.log(b.artir())
console.log(a.oku())
```

```text
1
2
11
2
```

`deger` dışarıdan okunamaz. `a.deger` `undefined`dir. Kapı `artir` ve `oku`dur. `a` ile `b` ayrı çanta taşır. `a` iki kez artınca 2 olur. `b` 10’dan başlar, bir kez artınca 11 olur. Biri ötekini bozmaz.

Bu, sınıf kullanmadan küçük bir kapsül kurmaktır. İç durum gizlidir.

## Döngüde tuzak

`var` ile kurulan döngüde `setTimeout` hepsi aynı `i`yi görür. `var` tek bir değişken paylaşır. Turlar bitince `i` 3’tür. Zamanlayıcılar sonra çalışır, üçü de 3 basar.

```js
for (var i = 0; i < 3; i += 1) {
  setTimeout(() => console.log("var", i), 0)
}
```

```text
var 3
var 3
var 3
```

`let` her turda yeni bağ kurar. Her zamanlayıcı kendi turunun sayısını hatırlar.

```js
for (let i = 0; i < 3; i += 1) {
  setTimeout(() => console.log("let", i), 0)
}
```

```text
let 0
let 1
let 2
```

Yeni kodda `let` yeter. `setTimeout(..., 0)` “hemen değil, eldeki iş bitince” demektir. Döngü biter, sonra iletiler gelir. Bu yüzden `var` örneğinde artış çoktan bitmiştir.

## Ne işe yarar

- Sayaç ve “dışarıdan dokunulmasın” durumu. Yukarıdaki `deger` böyledir.
- Olay dinleyicisine bağlam vermek. Tıklanınca hangi karttı, closure tutar.
- Bir iş yalnız ilk seferde çalışsın diye sarmalayıcı.

```js
function birKez(is) {
  let yapildi = false
  return (...argumanlar) => {
    if (yapildi) {
      return
    }
    yapildi = true
    return is(...argumanlar)
  }
}

const bagir = birKez(() => console.log("yalnız bir kez"))
bagir()
bagir()
bagir()
```

```text
yalnız bir kez
```

İkinci ve üçüncü çağrı fonksiyonun içine girer ama `yapildi` true olduğu için hemen döner. İleti bir kez basılır.

Closure büyük bir listeyi veya DOM düğümünü tutuyorsa o bellek durur. Fonksiyon yaşıyorsa çanta da yaşar. Bitmiş bir ekranın verisini bir dinleyicinin içinde unutma. Dinleyici kalkınca fonksiyon gider, çanta da gidebilir.

## Egzersizler

1. `sayacKur` ile iki bağımsız sayaç üret. Birini üç kez, ötekini bir kez artır. Birincinin `oku`su 3, ikincinin `oku`su 1 olsun. Aynı çantayı paylaşmadıklarını böyle gör.
2. `ekle(n)` yaz. İçinden `(x) => x + n` döndürsün. `ekle(10)(4)` sonucu `14` olsun. `10` , closure’da kalsın.
3. `var` ve `let` örneklerini kendi konsolunda çalıştır. Üç tane `3` ile `0 1 2` farkını gör.
4. `birKez` sarmalayıcısını yaz. Üç kez çağır. Konsolda tek satır olsun.
5. `kasa(bakiye)` yaz. İçinden `yatir(miktar)` ve `cek(miktar)` döndürsün. Dışarıdan `bakiye` değişkeni okunamasın. `cek` bakiyeyi eksiye düşürecekse `Error` fırlatsın. `kasa(100).cek(40)` sonra `oku` 60 olsun. Şehir adı gerekmez. Kişiyi denemek istersen yorum olarak `Serhat, İstanbul` yaz, kasaya koyma.

---

[← Önceki gün](../18-promises/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../20-clean-code/ders.md)
