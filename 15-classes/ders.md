# 15. Gün — Sınıflar

Nesneyi tek tek süslü parantezle kurmak birkaç kayıt için yeter. Aynı kalıptan çok kayıt üretilecekse sınıf yazılır. Sınıf, kurucu ile alanları ve metodları bir arada tutan kalıptır.

Alt tarafta prototip durur. Sınıf, bu yapının düz yazılmış halidir. `new` olmadan çağrılırsa motor hata verir. Örnek her zaman `new` ile üretilir.

## Kalıp ve kurucu

```js
class Raf {
  constructor(ad, kapasite = 10) {
    this.ad = ad
    this.kapasite = kapasite
    this.urunler = []
  }

  ekle(urun) {
    if (this.urunler.length >= this.kapasite) {
      throw new Error(`${this.ad} dolu`)
    }
    this.urunler.push(urun)
  }

  ozet() {
    return `${this.ad}: ${this.urunler.length}/${this.kapasite}`
  }
}

const kuru = new Raf("kuru gıda", 2)
kuru.ekle("un")
console.log(kuru.ozet())
```

`constructor` bir kez, `new` sırasında çalışır. `this` o anki örneği gösterir. Ortak işi metoda koy, kopyayı her nesnenin içine gömme.

Alanları sınıf gövdesinde de açabilirsin. Kurucuya gerek yoksa bu daha sade:

```js
class Sayac {
  deger = 0

  artir() {
    this.deger += 1
    return this.deger
  }
}
```

## getter ve setter

Alan gibi okunur, arkada fonksiyon çalışır. Ağır hesap her okumada yeniden koşmasın diye dikkat et. Basit türetim için severim.

```js
class Fatura {
  constructor(tutar) {
    this.tutar = tutar
  }

  get kdvli() {
    return this.tutar * 1.2
  }

  set kdvli(yeni) {
    this.tutar = yeni / 1.2
  }
}

const fis = new Fatura(100)
console.log(fis.kdvli)
fis.kdvli = 240
console.log(fis.tutar)
```

## Statik

Örneğe değil, sınıfa ait iş. `Math.max` gibi. `new` olmadan `Sinif.metod()` diye çağrılır. `this` örneği göstermez, sınıfı gösterir.

```js
class Kod {
  static uret(n = 4) {
    return Math.random().toString(36).slice(2, 2 + n)
  }
}

console.log(Kod.uret())
```

## Kalıtım

Ortak kalıp üstte, fark altta durur. `extends` bu bağı kurar. Alt kurucuda `this` kullanılmadan önce `super(...)` çağrılır.

```js
class Kap {
  constructor(ml) {
    this.ml = ml
  }

  bilgi() {
    return `${this.ml} ml`
  }
}

class Termos extends Kap {
  constructor(ml, sicak = true) {
    super(ml)
    this.sicak = sicak
  }

  bilgi() {
    const hal = this.sicak ? "sıcak" : "soğuk"
    return `${super.bilgi()}, ${hal}`
  }
}

console.log(new Termos(500).bilgi())
```

Üstteki metodu altta yeniden yazınca buna ezmek denir. Üstteki haline hâlâ ihtiyaç varsa `super.bilgi()` ile çağır.

`instanceof` ile soyunu sorarsın. `new Termos(500) instanceof Kap` doğru çıkar.

## Nerede sınıf, nerede düz fonksiyon

Kayıt üretiliyor ve birkaç metod birlikte taşınıyorsa sınıf uygundur. Tek bir hesap ise fonksiyon yeter. Her işi sınıfa koymak kodu sadeleştirmez. Veri ile davranış bir arada duruyorsa sınıf açılır.

## Egzersizler

1. `Kitap` sınıfı yaz: ad, sayfa. `kalinMi` metodu 300 üstündeyse doğru dönsün.
2. Kurucuda sayfa gelmezse 0 kabul et.
3. `get kisaAd` ekle: ad üç kelimeden uzunsa ilk üçü ve `...` dönsün.
4. `Kod.uret` benzeri statik bir `Kimlik.numara()` yaz.
5. `Kitap`tan türeyen `EKitap` yaz, ekstra `link` alanı olsun. `bilgi` metodu üstteki metne linki eklesin.
6. `super` çağırmadan `this` kullanmayı dene, motorun ne dediğini oku.
7. Bir örneğin `instanceof` ile hem alt hem üst sınıfa ait olduğunu göster.
8. Kapasite dolunca hata fırlatan `ekle` metodunu `try/catch` ile dene.

---

[← Önceki gün](../14-error-handling/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../16-json/ders.md)
