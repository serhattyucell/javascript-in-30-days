# 28. Gün — Skor tablosu

Küçük bir skor listesi kurulur. Ad ve puan girilir, tabloya düşer. Yüksek puan üstte durur. Sayfa yenilense de liste kaybolmaz. 17. günün deposu bu iş için kullanılır.

## Veri

```js
let skorlar = []
```

Her kayıt `{ ad, puan, zaman }`. `zaman` için `Date.now()` yeter, aynı puanda son eklenen alta kalsın diye.

Başlangıçta depodan oku:

```js
const ham = localStorage.getItem("skorlar")
skorlar = ham ? JSON.parse(ham) : []
```

`parse` bozuksa `catch` ile boş listeye dön ve o anahtarı sil. Bozuk veri sayfayı düşürmesin.

## Eklemek

Form: ad metni, puan sayısı, gönder düğmesi. `preventDefault`.

Ad boşsa veya yalnız boşluksa kayıt eklenmez. `trim` uygulanır. Puan `Number` olur; `NaN` ise kayıt eklenmez. Negatif puana izin, formun yanında yazılan bir kuraldır.

Eklemeden sonra listeyi puana göre sırala:

```js
skorlar.sort((a, b) => b.puan - a.puan || a.zaman - b.zaman)
```

`sort` bu diziyi bilerek bozar. Burada asıl kaynak o, kopya şart değil. Sonra `localStorage`’a yaz, tabloyu baştan çiz.

## Tablo

`table` kullan. Başlık satırı: sıra, ad, puan. Gövdeyi her çizimde `replaceChildren` ile kur. İlk üç sıraya ayrı bir sınıf, rengi biraz değişsin. Sıra numarası indeksten gelsin, kayıtta tutulmasın. Sıralama değişince numara yalan söylemesin.

Satırda bir “sil” düğmesi olsun. Olay taşsın: tabloya tek dinleyici, `dataset` ile zaman damgasını veya bir id’yi taşı. Silince depoyu ve ekranı güncelle.

Bir de “hepsini sil”. `confirm` ile sor. Evetse dizi boşalsın, anahtar kalksın.

## Görünüm

Dar bir sütun, ortada. Form üstte, tablo altta. Puan sağa yaslı, ad sola. Boş listede tablo yerine “henüz skor yok” yazsın, boş bir tablo başlığıyla bırakma.

## Bitti saymam için

- Yenileyince liste duruyor
- Eşit puanda daha erken eklenen üstte
- Silmek tek satırı götürüyor, ötekiler duruyor
- Hatalı girişte eski tablo bozulmuyor, kısa bir uyarı çıkıyor
- Depoya yazan fonksiyon ile ekrana basan fonksiyon ayrı

---

[← Önceki gün](../27-portfolio/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../29-color-animation/ders.md)
