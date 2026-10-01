# 27. Gün — Portfolyo

Tek sayfalık bir vitrin kurulur. Fotoğraf zorunlu değildir. Ad, bir cümle, üç proje kartı ve kartlar arasında gezen bir şerit yeter. Amaç gösterişli bir özgeçmiş değildir; veri dizisinden arayüz kurmak ve durumu bir değişkende tutmaktır.

## İçerik

Metinler JavaScript’te dursun.

```js
const profil = {
  ad: "Serhat",
  satir: "Arayüz kurmayı ve veriyi ekranda göstermeyi çalışıyor.",
}

const projeler = [
  { ad: "Gezegen tartısı", ozet: "Kütleyi başka çekimde göstermek.", yil: 2026 },
  { ad: "Ülke çubukları", ozet: "İki listeyi orantılı çubuk yapmak.", yil: 2026 },
  { ad: "Ülke kartları", ozet: "Arama ve bölgeyle süzmek.", yil: 2026 },
]
```

Örnek ad Serhat’tır. Cümle değiştirilebilir. Projeler önceki günlerin işi olsun.

## Sayfa

Üstte ad ve cümle. Altta bir şerit: aynı anda bir proje görünsün. Sağda ve solda düğme, altta kaçıncı kartta olduğunu söyleyen noktalar.

Durum tek sayı: `sira`. Düğme onu artırır veya azaltır. Sona gelince başa, baştayken geri gidince sona sar. Noktaya basınca `sira` o indekse zıplasın.

Kart her seferinde baştan basılabilir. Üç kart yan yana dizilip kap `translateX` ile de kaydırılabilir. İkinci yol daha çok CSS ister. İkisi de geçerlidir. Durum tek sayıda duracağı için ilk yol daha sadedir.

Noktalar `projeler.length` kadar üretilsin. Seçili olana sınıf ekle.

## Klavye

Sol ve sağ ok, düğmeyle aynı işi yapsın. Odak bir `input` içindeyse karışma. `aria-label` ver ki düğmeler “önceki” ve “sonraki” desin, yalnız ikon olmasın.

## Görünüm

Geniş bir kart, bol boşluk, tek vurgu rengi. Yazı kutusu 65 karakteri geçmesin, satır uzamasın. Telefon genişliğinde düğmeler alta insin, yan yana sıkışmasın.

İstersen şerit beş saniyede bir `setInterval` ile ilerlesin. Sayfa görünmüyorken dönmesin: `document.hidden` ise tur atla. Fare kartın üstündeyken de durdur, okuma bölünmesin.

## Bitti saymam için

- Veriyi değiştirince kart sayısı ve noktalar kendiliğinden uyuyor
- Başta geri, sonda ileri sarma çalışıyor
- Seçili nokta görsel olarak ayrılıyor
- `sira` hiçbir zaman dizinin dışına taşmıyor; hesap bir fonksiyonda, `goster(sira)` yalnız çiziyor

---

[← Önceki gün](../26-country-cards/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../28-scoreboard/ders.md)
