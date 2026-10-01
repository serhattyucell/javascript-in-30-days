# 26. Gün — Ülke kartları

25. günde çubuk vardı. Bu gün kart ızgarası kurulur. Arama kutusu 23. gündeki süzgecin devamıdır. Veri önce sayfanın içindedir. Ağ, yerel hali bittikten sonra eklenir.

Her kayıtta ad, başkent, bölge ve nüfus olsun. Aynı bölgeden en az iki ülke olsun. Yoksa bölge süzgeci bir işe yaramaz.

```js
const ulkeler = [
  { ad: "Türkiye", baskent: "Ankara", bolge: "Asya", nufus: 85000000 },
  { ad: "Japonya", baskent: "Tokyo", bolge: "Asya", nufus: 124000000 },
  { ad: "Kenya", baskent: "Nairobi", bolge: "Afrika", nufus: 55000000 },
  { ad: "Norveç", baskent: "Oslo", bolge: "Avrupa", nufus: 5500000 },
  { ad: "Peru", baskent: "Lima", bolge: "Amerika", nufus: 34000000 },
  { ad: "Mısır", baskent: "Kahire", bolge: "Afrika", nufus: 112000000 },
]
```

Başkentler gerçek ülke verisidir. Örnek kişide kullanılan şehirler burada değiştirilmez. Ankara Türkiye’nin başkentidir.

## Kart

Izgara şöyle kurulur:

```css
.izgara {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(14rem, 1fr));
  gap: 1rem;
}
```

Kartta ülke adı başlık olsun. Altta başkent, bölge ve nüfus. Nüfus `Intl.NumberFormat("tr-TR")` ile görünsün. `85000000` yerine `85.000.000` okunur.

## Süzgeç

Üstte bir arama kutusu. Bölgeler için düğmeler: hepsi, bir de veriden çıkan bölgeler. İkisi birlikte çalışır. Sonuç, adı aramaya uyan **ve** bölgesi seçili olan ülkelerdir.

Aramayı `input` olayına bağla. Her seferinde eski kartları `replaceChildren` ile kaldır, yenilerini bas. Eşleşme yoksa ızgaranın yerine tek cümle: “bu süzgeçte ülke yok”.

Bölge düğmelerini elle yazma. `ulkeler` içinden `Set` ile tekil bölgeleri çıkar, düğmeleri ondan üret. Yeni bir bölge eklenince düğme kendiliğinden gelsin. 10. gündeki set tam bu iş içindir.

Süzgeç DOM görmesin. Dizi girer, dizi çıkar.

```js
function suz(liste, { aranan, bolge }) {
  const igne = aranan.toLocaleLowerCase("tr-TR")
  return liste.filter((ulke) => {
    const adTutar = ulke.ad.toLocaleLowerCase("tr-TR").includes(igne)
    const bolgeTutar = bolge === "hepsi" || ulke.bolge === bolge
    return adTutar && bolgeTutar
  })
}
```

`suz(ulkeler, { aranan: "a", bolge: "Afrika" })` konsolda Kenya ve Mısır benzeri, adında a geçen Afrika ülkelerini vermelidir. Sayfaya bağlamadan önce bunu çalıştır. Fonksiyon doğruysa kartı çizmek ayrı ve kısa kalır.

## Ağ, isteğe bağlı

Yerel hali bitince şu adres denenebilir:

```js
fetch("https://restcountries.com/v3.1/all?fields=name,capital,region,population")
```

Gelen biçim yerel diziden farklıdır. Bir `map` ile dersin biçimine çevrilir:

- `name.common` adı olur
- `capital?.[0]` başkent olur. Köşeli parantezdeki `?` başkent yoksa patlamasın diyedir
- `region` bölge olur
- `population` nüfus olur

İstek sürerken “yükleniyor” yaz. `try/catch` ve `yanit.ok` olsun. Ağ yoksa “veri gelmedi” yaz, sayfa beyaz kalmasın.

## Bitti sayılması için

- Arama ve bölge aynı anda süzüyor. `af` yazıp Afrika seçince her iki koşul da tutan kartlar kalır.
- Kart sayısı, süzgeç tutunca değişir.
- Boş sonuçta ızgara dağılmaz, bir mesaj durur.
- `suz` DOM’a dokunmaz. Çizmek başka fonksiyondadır.

---

[← Önceki gün](../25-bar-charts/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../27-portfolio/ders.md)
