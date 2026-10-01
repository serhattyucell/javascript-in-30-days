# 30. Gün — Kapanış

İki iş vardır. İkisi de yeni konu değildir. Biri veriyi kart ve süzgeç yapar. Öteki girilen metni kalıpla denetler. İkisi birlikte, önceki günlerdeki araçları aynı sayfada tutar.

## Birinci iş: durak rafı

26. günkü ülke kartına benzeyen bir raf kurulur. Kayıtlar bu günlerin işleridir.

```js
const isler = [
  { ad: "Gezegen tartısı", gun: 24, etiket: "form" },
  { ad: "Çubuk grafik", gun: 25, etiket: "veri" },
  { ad: "Ülke kartları", gun: 26, etiket: "süzgeç" },
  { ad: "Portfolyo", gun: 27, etiket: "durum" },
  { ad: "Skor tablosu", gun: 28, etiket: "kayit" },
  { ad: "Renk akışı", gun: 29, etiket: "zaman" },
]
```

Her kartta ad, gün ve etiket. Üstte arama, adın veya günün içinde baksın. `24` yazınca yalnız 24. günün kartı kalsın. Etiketler `Set` ile toplanıp düğme olsun. `veri` seçilince yalnız o etiket kalsın. Arama ile etiket birlikte çalışsın. 26. gündeki `suz` ile aynı kalıptır.

Süzgeç DOM görmez. Liste girer, liste çıkar. Çizmek başka fonksiyondadır. Önce konsolda dene:

```js
function suzIsler(liste, { aranan, etiket }) {
  const igne = aranan.toLocaleLowerCase("tr-TR")
  return liste.filter((is) => {
    const metin = (is.ad + " " + is.gun).toLocaleLowerCase("tr-TR")
    const etiketTutar = etiket === "hepsi" || is.etiket === etiket
    return metin.includes(igne) && etiketTutar
  })
}
```

`suzIsler(isler, { aranan: "grafik", etiket: "hepsi" })` tek kart döndürmelidir. Çubuk grafik.

Kartta küçük bir not kutusu olsun. Not, `localStorage`a `{ ad: not }` diye yazılır. Sayfa yenilince not durur. Boş not o anahtarı siler, çekmece şişmesin. Anahtar `not.` ile başlasın. `not.Gezegen tartısı` gibi. `clear` çağırma.

## İkinci iş: kısa form

Alanlar: ad, e-posta, parola, parola tekrarı. Gönderilince sayfa yenilenmesin. `preventDefault` unutulursa uyarı bir an görünüp gider.

Her alanın altında tek satırlık hata yeri olsun. İlk açılışta hepsi boş dursun. Kullanıcı yazınca veya gönderince dolsun. Hata varken kutu kırmızı olsun. Düzelince kırmızılık kalksın. Renk sınıf ile gelsin, `style.border` ile gömülmesin.

Kurallar:

- Ad `trim` edildikten sonra en az 2 karakter. Yalnız harf ve boşluk. Deneme adı `Serhat` olsun, geçsin. `S1` kalmasın.
- E-posta kabaca `bir@iki.uc` biçiminde olsun. Boşluk olmasın, bir tane `@` olsun, sonrasında bir nokta olsun. Her gerçek adresi yakalamak zorunda değildir.
- Parola en az 8 karakter. En az bir rakam ve bir harf. Kısa olanla “en az 8 karakter”, harfsiz olanla “harf yok” ayrı cümle olsun. İkisi aynı ileti olmasın.
- İki parola aynı olsun. Değilse “parolalar aynı değil”.

`denetle` DOM görmesin. Hata nesnesi döndürsün. Boş nesne, form temiz demektir.

```js
function denetle(kayit) {
  const hatalar = {}
  if (kayit.ad.trim().length < 2) {
    hatalar.ad = "ad kısa"
  }
  return hatalar
}

console.log(Object.keys(denetle({ ad: "S", eposta: "", parola: "", tekrar: "" })))
console.log(Object.keys(denetle({ ad: "Serhat", eposta: "a@b.c", parola: "abc12345", tekrar: "abc12345" })))
```

İlk çağrıda `ad` anahtarı durur. İkinci çağrıda, diğer kurallar da eklenince, anahtar listesi boş olmalıdır. Boşsa form geçerlidir:

```js
const temiz = Object.keys(hatalar).length === 0
```

Geçerliyse formu temizle. Kartların üstünde “kayıt alındı” yaz. Girilen adı bir süre göster. `setTimeout` ile üç saniye sonra o yazı kalkabilir. Parolayı ekrana basma. Çekmeceye de yazma.

## Bu gün bitince

Konsol, tip, karar, döngü, fonksiyon, nesne, liste dönüşümü, hata, sınıf, JSON, tarayıcı çekmecesi, promise, kapsam, ağaç ve olay aynı araç kutusundadır. Son sayfa bunları yan yana koyar.

Sonraki iş yeni bir komut ezberlemek değildir. Eldeki iş küçük fonksiyonlara bölünür. Veri ekrandan ayrı tutulur. Hata olunca boş `catch` ile yok edilmez.

Üç gün sonra okunmayan bir ad kötüdür. `d` yerine `sehirler` yazmak, yeni bir kütüphane eklemekten daha çok iş bitirir.

---

[← Önceki gün](../29-color-animation/ders.md) · [İçindekiler](../README.md)
