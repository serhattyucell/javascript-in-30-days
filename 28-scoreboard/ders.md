# 28. Gün — Skor tablosu

Küçük bir skor listesi kurulur. Ad ve puan girilir, tabloya düşer. Yüksek puan üstte durur. Sayfa yenilense de liste kaybolmaz. 17. günün `localStorage`ı bu iş içindir.

## Veri

```js
const ANAHTAR = "skorlar"
let skorlar = []
```

Her kayıt `{ ad, puan, zaman }` biçimindedir. `zaman` için `Date.now()` yeter. Aynı puanda daha erken eklenen üstte kalsın diye `zaman` küçük olan öne alınır.

Sayfa açılınca çekmeceden oku. Anahtar yoksa boş liste. Metin bozuksa 14. gündeki gibi yakala, anahtarı sil, boş listeyle devam et. Bozuk veri sayfayı düşürmesin.

```js
function oku() {
  try {
    const ham = localStorage.getItem(ANAHTAR)
    const liste = ham ? JSON.parse(ham) : []
    if (!Array.isArray(liste)) {
      return []
    }
    return liste
  } catch (hata) {
    localStorage.removeItem(ANAHTAR)
    return []
  }
}
```

`Array.isArray` gelen şey gerçekten liste mi diye bakar. Biri çekmeceye `"Serhat"` metni yazmışsa liste değildir, boş dönülür.

Yazmak:

```js
function yaz(liste) {
  localStorage.setItem(ANAHTAR, JSON.stringify(liste))
}
```

## Eklemek

Form: ad, puan, gönder. `submit` içinde `preventDefault`. Yoksa sayfa yenilenir ve az önce çizilen satır gider.

Ad `trim` edildikten sonra boşsa ekleme. Puan `Number` olsun. `NaN` ise ekleme. Negatif puana izin verilmez. Uyarı, tablonun yerini bozmasın. Eski satırlar ekranda kalsın, üstte tek cümle görünsün.

Eklemeden sonra sırala, çekmeceye yaz, tabloyu baştan çiz.

```js
skorlar.sort((a, b) => b.puan - a.puan || a.zaman - b.zaman)
```

`b.puan - a.puan` büyük puanı öne alır. Fark 0 ise `||` sağ tarafa bakar. Daha küçük `zaman` daha erkendir, o öne gelir. `sort` bu listeyi bilerek değiştirir. Kaynak bu listedir, ayrıca kopya şart değildir.

Deneme, sayfadan önce:

```js
const ornek = [
  { ad: "Serhat", puan: 10, zaman: 2 },
  { ad: "Serhat", puan: 30, zaman: 1 },
  { ad: "Serhat", puan: 10, zaman: 1 },
]
ornek.sort((a, b) => b.puan - a.puan || a.zaman - b.zaman)
console.log(ornek.map((k) => k.puan + "/" + k.zaman))
```

```text
["30/1", "10/1", "10/2"]
```

30 baştadır. İki tane 10 vardır. `zaman` 1 olan, `zaman` 2 olandan önce gelir.

## Tablo

`table` kullan. Başlık satırı: sıra, ad, puan. Gövde her çizimde `replaceChildren` ile kurulur. Sıra numarası indeksten gelir, kayıtta tutulmaz. Sıralama değişince numara yalan söylemesin. İlk üç sıraya ayrı bir sınıf ver.

Satırda bir “sil” düğmesi olsun. Tabloya tek dinleyici tak. Düğmede `data-zaman` tut. Tıklanınca o `zaman` ile kaydı listeden çıkar, `yaz` ve yeniden çiz. 23. gündeki `closest` burada da işe yarar.

“Hepsini sil” `confirm` ile sorsun. Evetse dizi boşalsın, `removeItem` çağrılsın. Hayırsa liste durur.

Boş listede tablo yerine “henüz skor yok” yaz. Boş bir başlık satırıyla bırakma.

Çizen fonksiyon ile yazan fonksiyon ayrı dursun. `yaz` DOM görmesin. `ciz` çekmeceye dokunmasın.

## Bitti sayılması için

- Yenileyince liste durur. 30 puanlık satır hâlâ üsttedir.
- Eşit puanda daha erken eklenen üsttedir. Yukarıdaki konsol denemesi bunu gösterir.
- Silmek tek satırı götürür. Öteki satırlar durur.
- Boş ad veya `abc` puanında eski tablo bozulmaz, kısa bir uyarı çıkar.
- `yaz` ve `ciz` ayrı fonksiyondur.

---

[← Önceki gün](../27-portfolio/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../29-color-animation/ders.md)
