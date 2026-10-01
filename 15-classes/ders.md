# 15. Gün — Sınıflar

Aynı biçimde iki kayıt süslü parantezle yazılır. Yüz kayıt olunca kalıp bir kez yazılır. Sınıf, kurucu ile alanları ve metodları bir arada tutan kalıptır. Alt tarafta prototip durur. Sınıf o yapının düz yazılışıdır. `new` olmadan çağrılırsa hata verir.

## Kurucu

`constructor` , `new` sırasında bir kez çalışır. `this` o anki örneği gösterir.

```js
class Raf {
  constructor(ad, kapasite = 10) {
    this.ad = ad
    this.kapasite = kapasite
    this.urunler = []
  }

  ekle(urun) {
    if (this.urunler.length >= this.kapasite) {
      throw new Error(this.ad + " dolu")
    }
    this.urunler.push(urun)
  }

  ozet() {
    return this.ad + ": " + this.urunler.length + "/" + this.kapasite
  }
}

const kuru = new Raf("İzmir", 2)
kuru.ekle("un")
console.log(kuru.ozet())
```

```text
İzmir: 1/2
```

`new Raf("İzmir", 2)` kurucuyu çağırır. `this.ad` o örneğin adıdır. `ozet` hesabı yapar, basmaz. Basma işi `console.log`tadır.

Kapasite dolunca `ekle` hata fırlatır. 14. gündeki `try/catch` ile yakalanır.

```js
const kucuk = new Raf("Van", 1)
kucuk.ekle("cay")
try {
  kucuk.ekle("tuz")
} catch (hata) {
  console.error(hata.message)
}
```

```text
Van dolu
```

Alanlar sınıf gövdesinde de açılır. Hepsi aynı başlıyorsa kurucuya gerek kalmayabilir.

```js
class Sayac {
  deger = 0

  artir() {
    this.deger += 1
    return this.deger
  }
}

const s = new Sayac()
console.log(s.artir())
console.log(s.artir())
```

```text
1
2
```

İki `new Sayac()` iki ayrı sayaçtır. Birinin `deger`i ötekini değiştirmez.

## getter ve setter

Alan gibi okunur, arkada fonksiyon çalışır. Ağır hesabı her okumada yenilemek pahalıdır. Kısa türetim için uygundur.

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

```text
120
200
```

`fis.kdvli` parantezsiz okunur. Yine de fonksiyondur. `set` ile yazılınca 240, KDV dahil tutardır. KDV hariç tutar 200’dür.

## Statik metod

Örneğe değil, sınıfa aittir. `new` olmadan `Sinif.metod()` diye çağrılır. `Math.max` bu biçimdedir.

```js
class Kod {
  static uret(n = 4) {
    return Math.random().toString(36).slice(2, 2 + n)
  }
}

console.log(Kod.uret())
```

Çıktı her seferinde farklı dört karakter civarındadır. `new Kod()` gerekmez. `this` bir örneği göstermez.

## Kalıtım

Ortak kalıp üstte, fark altta durur. `extends` bağı kurar. Alt kurucuda `this` kullanılmadan önce `super(...)` çağrılır. Unutulursa hata çıkar.

```js
class Kap {
  constructor(ml) {
    this.ml = ml
  }

  bilgi() {
    return this.ml + " ml"
  }
}

class Termos extends Kap {
  constructor(ml, sehir) {
    super(ml)
    this.sehir = sehir
  }

  bilgi() {
    return super.bilgi() + ", " + this.sehir
  }
}

const t = new Termos(500, "Trabzon")
console.log(t.bilgi())
console.log(t instanceof Kap)
```

```text
500 ml, Trabzon
true
```

Üstteki metod altta yeniden yazılırsa alta ezme denir. Üsttekine hâlâ ihtiyaç varsa `super.bilgi()` ile çağrılır. `instanceof` soyu sorar. Termos bir kaptır, `true` çıkar.

Kalıtım iki katı geçmesin. “Bu bir termosdur” demek her işte gerekmez. Tek bir hesap varsa fonksiyon yeter. Veri ile birkaç metod birlikte taşınıyorsa sınıf açılır.

## Egzersizler

1. `Sehir` sınıfı yaz. Kurucu `ad` ve `nufus` alsın. `buyukMu()` nüfus 1 milyondan büyükse `true` dönsün. `new Sehir("İzmir", 4000000).buyukMu()` doğru olsun. `new Sehir("Trabzon", 800000).buyukMu()` yanlış olsun.
2. Nüfus gelmezse `0` kabul et. `new Sehir("Van").nufus` `0` olsun.
3. `get kisa()` ekle. Ad üç harften uzunsa ilk üç harf ve `...` dönsün. `İzmir` için `İzm...` olsun.
4. `Kimlik.numara()` statik metodu yaz. `new` olmadan çağrılsın. İçinde `Kod.uret` mantığıyla dört karakter üret.
5. `Sehir`den türeyen `Durak` yaz. Ekstra `hat` alanı olsun. `bilgi()` üstteki ada hattı eklesin: `İzmir / 42`. `super` kullan.
6. `super` çağırmadan `this.hat = hat` yazmayı dene. Motorun iletisini oku, sonra `super`ü başa al.
7. Örneğin hem `Durak` hem `Sehir` için `instanceof` sonucunun `true` olduğunu göster.
8. Kapasitesi 1 olan rafa iki ürün ekle. İkinci eklemede hatayı `try/catch` ile yakala, mesajı yazdır.

---

[← Önceki gün](../14-error-handling/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../16-json/ders.md)
