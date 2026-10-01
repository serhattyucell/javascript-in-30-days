# 24. Gün — Gezegende ağırlık

Bu günde yeni sözdizimi yoktur. 21, 22 ve 23. günlerdeki DOM ve olay bilgisi tek sayfada toplanır. İş şudur: bir kütle girilir, bir gök cismi seçilir, o cismin çekiminde kütlenin ağırlığı yazılır.

Ağırlık, kütle çarpı çekimdir. Kütle kilogramdır. Sonuç Newton olabilir; “dünya tartısında kaç okunur” sorusu da ayrı yazılır. Birimler karışmasın diye ikisi ayrı gösterilir.

```js
const cisimler = [
  { ad: "Dünya", cekim: 9.81 },
  { ad: "Ay", cekim: 1.62 },
  { ad: "Mars", cekim: 3.71 },
  { ad: "Jüpiter", cekim: 24.79 },
  { ad: "Merkür", cekim: 3.7 },
  { ad: "Venüs", cekim: 8.87 },
]
```

Dünya’da 70 kg kütle kabaca 70 × 9.81 Newton eder. “Orada tartıda ne okurdum” sorusu ise `kütle * (çekim / 9.81)`. İkisini de göster. İlki fizik, ikincisi his.

## Sayfa

- Sayı girişi, birim yazısı kilogram
- Cisimler için bir `select`. Seçenekleri HTML’e elle yazma, diziden üret
- Bir “hesapla” düğmesi
- Sonuç alanı: cismin adı, Newton, dünya tartısı hissi
- Geçersiz girişte sonuç yerine kısa bir uyarı

Form kullan. `submit` olayında `preventDefault`. Boş, `NaN` veya sıfırdan küçük kütlede hesaplama. Üst sınır koy, mesela 500. Sihirli sayıyı isimlendir.

Seçenek değişince de sonucu güncelle. Kullanıcı düğmeyi aramasın. Düğme yine dursun, klavye ile form göndermek için.

## Görünüm

Ortada dar bir kart. Arkası düz, açık bir zemin. Cisim adını büyük, sayıyı daha büyük yaz. Newton’u bir ondalıkla göster, `toFixed(1)` metin döndürür, ekran için uygun. Başlıkta seçilen cismin adı geçsin.

İstersen her cisme bir renk bağla, kartın kenarı o renge dönsün. Renk verisi dizide dursun, CSS’te hepsi ayrı kural olmasın; bir tane özel özellik yeter:

```js
kart.style.setProperty("--kenar", cisim.renk)
```

```css
.kart {
  border: 4px solid var(--kenar, #ccc);
}
```

## Bitti saymam için

- Listeye yeni bir cisim eklediğimde açılır menü kendiliğinden uzasın
- Negatif sayıda uyarı çıksın, eski sonuç ekranda kalmasın
- Sayfa yenilenince form sıfırlansın, depolamana gerek yok
- Hesap bir fonksiyon olsun, DOM’a dokunmasın. Başka bir fonksiyon sonucu yazsın. 20. günün kuralı

---

[← Önceki gün](../23-events/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../25-bar-charts/ders.md)
