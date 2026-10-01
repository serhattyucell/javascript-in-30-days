# 24. Gün — Gezegende ağırlık

Yeni sözdizimi yoktur. 21, 22 ve 23. günlerdeki DOM ve olay bilgisi tek sayfada toplanır. Bir kütle girilir, bir gök cismi seçilir, o cismin çekiminde kütlenin ağırlığı yazılır.

Ağırlık, kütle çarpı çekimdir. Kütle kilogramdır. Newton ile “dünya tartısında kaç okunur” ayrı yazılır. Birimler karışmasın.

```js
const cisimler = [
  { ad: "Dünya", cekim: 9.81 },
  { ad: "Ay", cekim: 1.62 },
  { ad: "Mars", cekim: 3.71 },
  { ad: "Jüpiter", cekim: 24.79 },
]
```

70 kg kütle Dünya’da `70 * 9.81` Newton eder. Yaklaşık `686.7`. “Orada tartıda ne okurdum” sorusu `kütle * (çekim / 9.81)`dir. Ay’da çekim 1.62’dir. `70 * (1.62 / 9.81)` yaklaşık `11.5` çıkar. Aynı kütle, daha küçük tartı.

Hesabı yapan fonksiyon DOM’a dokunmaz. Verir, sayı döndürür.

```js
function agirlik(kg, cekim) {
  return {
    newton: kg * cekim,
    tarti: kg * (cekim / 9.81),
  }
}

console.log(agirlik(70, 1.62))
```

Konsolda `newton` ve `tarti` alanlarını gör. Sonra aynı fonksiyonu sayfaya bağla.

## Sayfa

- Sayı girişi. Yanında “kilogram” yazsın.
- Cisimler için bir `select`. Seçenekleri HTML’e elle yazma. `cisimler` dizisinden `option` üret.
- Bir “hesapla” düğmesi.
- Sonuç alanı: cismin adı, Newton, tartı hissi.
- Geçersiz girişte sonuç silinsin, kısa bir uyarı yazsın.

Form kullan. `submit` içinde `preventDefault` olsun. Yoksa sayfa yenilenir, sonuç bir an görünüp gider.

Boş, `NaN` veya sıfırdan küçük kütlede hesaplama. Üst sınır `500` olsun. Sayıya ad ver:

```js
const EN_FAZLA_KG = 500
```

Seçenek değişince de sonucu güncelle. Düğme klavye ile göndermek için dursun.

## Görünüm

Ortada dar bir kart. Cisim adı büyük, sayı daha büyük olsun. Newton `toFixed(1)` ile bir basamak görünsün. `toFixed` metin döndürür. Ekran için uygundur. Üstüne matematik bindirme.

İstersen her cisme bir `renk` alanı ekle. Kartın kenarı o renge dönsün.

```js
kart.style.setProperty("--kenar", cisim.renk)
```

```css
.kart {
  border: 4px solid var(--kenar, #ccc);
}
```

`var`in ikinci değeri, renk yoksa gri kalsın diyedir.

## Bitti sayılması için

- Listeye `{ ad: "Merkür", cekim: 3.7 }` eklenince menü kendiliğinden uzasın. HTML’e elle `option` yazılmamış olsun.
- `-5` girilince uyarı çıksın, eski Newton ekranda kalmasın.
- Sayfa yenilenince form sıfır olsun. `localStorage` gerekmez.
- `agirlik` DOM görmesin. Başka bir fonksiyon sonucu yazsın. İkisini karıştırırsan hesabı test etmek için sayfa açmak gerekir.

---

[← Önceki gün](../23-events/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../25-bar-charts/ders.md)
