# 29. Gün — Renk animasyonu

Kısa bir yazı kurulur. Her harf ayrı bir renktedir ve renkler yavaşça yer değiştirir. Görünüm bir CSS kuralı ve bir zamanlayıcıyla biter. Yeni bir kütüphane gerekmez.

## Yazıyı böl

Metni `split("")` ile harflere ayır. Her harf bir `span`. Boşluk da span olsun, yoksa kelimeler yapışır. Boşluk span’ine bir sınıf ver, genişliği çökmesin: `inline-block` ve en az `0.3em`.

```js
const yazi = "Serhat"
const sahne = document.querySelector("#sahne")

function kur(metin) {
  sahne.replaceChildren()
  ;[...metin].forEach((harf) => {
    const span = document.createElement("span")
    span.textContent = harf
    if (harf === " ") span.classList.add("bosluk")
    sahne.append(span)
  })
}
```

`split("")` bazı emojilerde bozulur. Burada düz metin var, yeter. `[...metin]` kod noktalarına daha yakındır, onu kullan.

## Renk

Sabit bir palet tut.

```js
const palet = ["#1d4e89", "#c4552a", "#2f6f4e", "#e3b23c", "#5c4d7a"]
```

Her span’e `kaydir` diye bir sayı koy, başta indeksi. Her turda o sayıyı bir artır, `palet.length` ile moda al, rengi `style.color` ile bas.

```js
let tur = 0
function boya() {
  const harfler = sahne.querySelectorAll("span")
  harfler.forEach((span, indeks) => {
    const renk = palet[(indeks + tur) % palet.length]
    span.style.color = renk
  })
  tur += 1
}
```

`setInterval(boya, 400)`. Sayfa açılınca bir kez hemen boya, ilk 400 ms siyah kalmasın.

## Durdurmak

Bir düğme aralığı `clearInterval` ile kessin, tekrar basınca yeni aralık kursun. İki kez basılınca iki zamanlayıcı üst üste binmesin. Kimliği bir değişken tut, kurmadan önce eskisini temizle.

İkinci bir düğme paletin yönünü çevirsin: `tur += 1` yerine bir `adim` değişkeni `1` ya da `-1` olsun. Negatif mod JavaScript’te negatiftir. İndeksi şöyle düzelt:

```js
const i = (indeks + tur) % palet.length
const guvenli = (i + palet.length) % palet.length
```

## Görünüm

Yazı büyük, sayfa ortasında, arka plan açık. `prefers-reduced-motion: reduce` varsa zamanlayıcıyı hiç kurma, harfleri bir kez boyayıp bırak. Hareketi istemeyen kişiye animasyon dayatma.

```css
#sahne {
  font-size: clamp(2.5rem, 8vw, 6rem);
  font-weight: 700;
  letter-spacing: 0.04em;
}
.bosluk {
  display: inline-block;
  min-width: 0.35em;
}
```

## Bitti saymam için

- Metni değişkenden değiştirince harf sayısı uyuyor
- Durunca renk donuyor, başlatınca kaldığı yerden akıyor
- İki kez başlatma, hızı ikiye katlamıyor
- Azaltılmış hareket tercihi açıksa zamanlayıcı yok
- Palet ve metin, boyama fonksiyonunun içinde gömülü değil

---

[← Önceki gün](../28-scoreboard/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../30-final-projects/ders.md)
