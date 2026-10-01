# 29. Gün — Renk animasyonu

Kısa bir yazı kurulur. Her harf ayrı bir renktedir. Renkler yavaşça yer değiştirir. Yeni bir kütüphane gerekmez. Metin harflere bölünür, bir `span` boyanır, `setInterval` rengi kaydırır.

## Yazıyı bölmek

`split("")` bazı birleşik karakterlerde bozulur. Düz metinde `[...metin]` her karakteri ayırır. Boşluk da bir `span` olsun. Olmazsa kelimeler yapışır. Boşluk `span`ine bir sınıf ver, genişliği çökmesin.

```js
const yazi = "Serhat"
const sahne = document.querySelector("#sahne")

function kur(metin) {
  sahne.replaceChildren()
  ;[...metin].forEach((harf) => {
    const span = document.createElement("span")
    span.textContent = harf
    if (harf === " ") {
      span.classList.add("bosluk")
    }
    sahne.append(span)
  })
}
```

`Serhat` altı `span` üretir. Konsolda `sahne.children.length` `6` olmalıdır. Değilse bölme yanlıştır.

```css
#sahne {
  font-size: clamp(2.5rem, 8vw, 6rem);
  font-weight: 700;
}
.bosluk {
  display: inline-block;
  min-width: 0.35em;
}
```

`clamp` küçük ekranda yazıyı küçültür, büyük ekranda `6rem`de durur.

## Renk

Palet sabit durur. Her turda renk bir kayar. Kayan sayının adı `tur`.

```js
const palet = ["#1d4e89", "#c4552a", "#2f6f4e", "#e3b23c", "#5c4d7a"]
let tur = 0

function boya() {
  const harfler = sahne.querySelectorAll("span")
  harfler.forEach((span, indeks) => {
    const ham = (indeks + tur) % palet.length
    const sira = (ham + palet.length) % palet.length
    span.style.color = palet[sira]
  })
  tur += 1
}
```

İlk harf tur 0’da paletin 0. rengi olur. İkinci harf 1. renk olur. Tur 1 olunca ilk harf 1. renge kayar. `%` sayıyı paletin boyuna sarar. Beş renk varsa 5, 0’a döner.

JavaScript’te negatif sayıda `%` negatif sonuç verir. `-1 % 5` sonucu `-1`dir. Palet indeksi negatif olamaz. `(ham + palet.length) % palet.length` onu düzeltir. Yön tersine dönünce bu satır gerekir.

Sayfa açılınca `boya()` bir kez hemen çağrılır. İlk 400 ms siyah kalmasın.

```js
let kimlik = 0

function baslat() {
  dur()
  kimlik = setInterval(boya, 400)
}

function dur() {
  clearInterval(kimlik)
}
```

`baslat` önce `dur` der. İki kez basılınca iki zamanlayıcı üst üste binmez. Binirse renk iki kat hızlanır. Kimlik tutulmazsa eski aralık kesilemez.

Yön için bir `adim` değişkeni `1` veya `-1` olsun. `tur += adim` yazılır. Düğme `adim`i ters çevirir.

## Hareketi azaltmak

İşletim sisteminde “hareketi azalt” açıksa zamanlayıcı kurulmaz. Harfler bir kez boyanır ve kalır.

```js
const azHareket = window.matchMedia("(prefers-reduced-motion: reduce)").matches
if (!azHareket) {
  baslat()
} else {
  boya()
}
```

## Bitti sayılması için

- Metin `"Serhat Van"` olunca harf ve boşluk sayısı `sahne.children.length` ile aynıdır. Boşluk da `span`dir.
- Durunca renk donar. Başlatınca kaldığı yerden akar. `tur` sıfırlanmak zorunda değildir.
- İki kez başlatmak hızı ikiye katlamaz. `baslat` önce eski aralığı keser.
- Azaltılmış hareket tercihi açıksa `setInterval` yoktur.
- Palet ve metin, `boya`nın içine gömülü değildir. Dışarıda durur. Metin değişince yalnız `kur` yeniden çağrılır.

---

[← Önceki gün](../28-scoreboard/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../30-final-projects/ders.md)
