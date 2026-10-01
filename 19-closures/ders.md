# 19. Gün — Closure

Closure, bir fonksiyonun doğduğu yerdeki değişkenleri, o yer bittikten sonra da hatırlamasıdır. Kulağa sihir gibi gelir. Aslında basit: fonksiyon, kendi kapsamının çantasıyla birlikte taşınır.

9. günde `carp(3)` bir fonksiyon döndürmüş ve `3` değerini unutmamıştı. Bu bölüm o yapının adıdır.

```js
function sayacKur(baslangic = 0) {
  let deger = baslangik
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
```

`deger` dışarıdan okunamaz. `a` ile `b` ayrı çanta taşır. Biri ötekini bozmaz. Bu, sınıf kullanmadan küçük bir kapsül kurmanın yoludur.

## Döngüde klasik tuzak

`var` ile kurulan döngüde `setTimeout` hepsi aynı `i`’yi görür, çünkü `var` tek bir değişken paylaşır.

```js
for (var i = 0; i < 3; i += 1) {
  setTimeout(() => console.log("var", i), 0)
}
```

Üç satır da `3` basar. `let` her turda yeni bağ kurar:

```js
for (let i = 0; i < 3; i += 1) {
  setTimeout(() => console.log("let", i), 0)
}
```

Yeni kodda `let` yeter. Eski kodda fonksiyonu her tur çağırmak da aynı işi görür: her çağrı kendi `i` kopyasını kapar.

## Nerede işime yarar

- Sayaç, sepet, “bir kez kurulup sonra içeriden değişen” durum.
- Olay dinleyicisine bağlam vermek: tıklanınca hangi karttı, closure tutar.
- `once` gibi sarmalayıcılar: fonksiyon ilk seferde çalışır, sonra boş döner.

```js
function birKez(is) {
  let yapildi = false
  return (...argumanlar) => {
    if (yapildi) return
    yapildi = true
    return is(...argumanlar)
  }
}

const bagir = birKez(() => console.log("yalnız bir kez"))
bagir()
bagir()
```

## Neyi şişirmemeli

Closure, büyük bir diziyi veya DOM düğümünü tutuyorsa o bellek durur. Fonksiyon yaşıyorsa çanta da yaşar. Bitmiş bir ekranın verisini sonsuza kadar bir dinleyicinin içinde unutma. Dinleyiciyi kaldırınca fonksiyon gider, çanta da gidebilir.

## Egzersizler

1. `sayacKur` ile iki bağımsız sayaç üret, birini üç kez, ötekini bir kez artır.
2. `carp` yerine `ekle(n)` yaz. `ekle(10)(4)` sonucu 14 olsun. Buna içi içe çağrı denir; dönen fonksiyon argümanı bekler.
3. `var` ve `let` ile döngü tuzakını kendi konsolunda gör.
4. `birKez` sarmalayıcısını yaz, üç kez çağır, yalnız ilkinin yazdığını gör.
5. Bir `kasa(bakiye)` fonksiyonu yaz. İçinden `yatir` ve `cek` döndürsün. Dışarıdan `bakiye` değişkenine doğrudan erişilemesin. Eksi bakiyede `cek` hata fırlatsın.

---

[← Önceki gün](../18-promises/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../20-clean-code/ders.md)
