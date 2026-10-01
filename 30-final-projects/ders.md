# 30. Gün — Kapanış

Son günde iki iş vardır. İkisi de yeni konu değildir. Biri veriyi kart ve süzgeç yapar, öteki girilen metni kalıpla denetler. Bu iki iş, otuz günü bir araya getirir: tipten döngüye, nesneden DOM’a, depodan ağa.

## Birinci iş: atölye raftı

26. günkü ülke kartına benzeyen bir raf kurulur. Kayıtlar bu otuz günün işleridir.

```js
const isler = [
  { ad: "Gezegen tartısı", gun: 24, etiket: "form" },
  { ad: "Çubuk grafik", gun: 25, etiket: "veri" },
  { ad: "Ülke kartları", gun: 26, etiket: "süzgeç" },
  { ad: "Portfolyo", gun: 27, etiket: "durum" },
  { ad: "Skor tablosu", gun: 28, etiket: "depo" },
  { ad: "Renk akışı", gun: 29, etiket: "zaman" },
]
```

Her kartta ad, gün ve etiket. Üstte arama, gün alanına ya da ada baksın. Etiketler `Set` ile toplanıp düğme olsun. Süzgeç yine ayrı bir fonksiyon, çizmeyi başka fonksiyon yapsın.

Kartta küçük bir “not” alanı aç. Notu `localStorage`’a `{ ad: not }` sözlüğü diye yaz. Sayfa yenilince not yerinde kalsın. Boş not anahtarı silsin, depo şişmesin.

## İkinci iş: kısa bir form

Bir kişi kaydı: ad, e-posta, parola, parola tekrarı. Gönderilince sayfa yenilenmesin. Her alanın altında tek satırlık hata yeri olsun. İlk boyamada hepsi boş dursun, kullanıcı yazınca veya gönderince dolsun. Kırmızı çerçeveyi hata varken ekle, düzelince kaldır.

Kurallar:

- Ad en az 2 karakter, yalnız harf ve boşluk. Türkçe harfi 12. gündeki gibi ele al. Önce `trim`.
- E-posta kabaca `bir@iki.uc` biçiminde olsun. Her gerçek adresi yakalamak zorunda değilsin. `\s` içermesin, bir tane `@` olsun, sonrasında bir nokta olsun.
- Parola en az 8 karakter, en az bir rakam ve bir harf.
- İki parola aynı olsun.

Kalıpları ölç, mesajları Türkçe yaz. `test` yetmiyorsa neden yetersiz olduğunu ayrı ayrı söyle: “rakam yok” ile “çok kısa” aynı cümle olmasın.

Geçerliyse formu temizle, kart listesinin üstünde “kayıt alındı” de, girilen adı kartların yanında bir süre göster. Parolayı ekrana basma, depoya yazma.

```js
function denetle(kayit) {
  const hatalar = {}
  if (kayit.ad.trim().length < 2) hatalar.ad = "ad kısa"
  // diğer alanlar
  return hatalar
}
```

`denetle` DOM görmesin. Boş nesne dönerse form temizdir: `Object.keys(hatalar).length === 0`.

## Kapanış

Otuz günde dilin çevresi dolaşılmıştır. Konsol, tip, dal, döngü, fonksiyon, nesne, liste dönüşümü, hata, sınıf, metin olarak veri, tarayıcı deposu, promise, kapsam, ağaç ve olay görülmüştür. Son günlerde bunlar yan yana konup sayfa çıkarılmıştır.

Sonraki iş, yeni bir API ezberlemek değildir. Eldeki iş küçük fonksiyonlara bölünür, veri ekrandan ayrı tutulur, hata olunca yok sayılmaz.

Üç gün sonra okunmayan bir ad kötüdür. O adı düzeltmek, yeni bir kütüphane eklemekten daha çok iş bitirir.

---

[← Önceki gün](../29-color-animation/ders.md) · [İçindekiler](../README.md)
