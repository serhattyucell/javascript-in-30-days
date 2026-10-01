# 26. Gün — Ülke kartları

Önceki günde çubuk vardı. Bu bölümde kart ızgarası kurulur. Arama kutusu 23. gündeki süzgecin devamıdır. Veri önce sayfanın içinde durur. İstenirse [restcountries](https://restcountries.com) gibi bir adresten `fetch` ile de çekilebilir. Önce yerel dizi bitirilir. Ağ, sonraki adımdır.

## Veri

Her kayıtta en az ad, başkent, bölge ve nüfus olsun. On-on iki ülke yeter. Gerçek sayıları kabaca yazman sorun değil; ders kartın kendisi.

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

Listeyi sen büyüt. Aynı bölgeden en az iki ülke olsun ki süzgeç bir işe yarasın.

## Kart

Izgara `repeat(auto-fill, minmax(14rem, 1fr))` ile kurulsun. Kartta ülke adı başlık, altta başkent, bölge ve nüfus. Nüfus `Intl.NumberFormat` ile.

## Süzgeç

Üstte bir arama kutusu ve bölge için düğmeler: hepsi, Asya, Afrika, Avrupa, Amerika. İkisi birlikte çalışsın. Sonuç, adı aramaya uyan **ve** bölgesi seçili olan ülkeler.

Aramayı `input` olayına bağla. Her seferinde eski kartları kaldır, yenilerini bas. Eşleşme yoksa ızgaranın yerine tek cümle: “bu süzgeçte ülke yok”.

Bölge listesini elde yazma. `ulkeler` içinden `Set` ile tekil bölgeleri çıkar, düğmeleri ondan üret. Yeni bölge eklenince düğme kendiliğinden gelsin.

## İsteğe bağlı ağ

Yerel hali bittikten sonra `fetch("https://restcountries.com/v3.1/all?fields=name,capital,region,population")` denenebilir. Gelen biçim yerel diziden farklıdır. Bir `map` ile dersin kullandığı biçime çevrilir:

- `name.common` → `ad`
- `capital?.[0]` → `baskent`
- `region` → `bolge`
- `population` → `nufus`

İstek sürerken “yükleniyor” yaz. `try/catch` ile ağ hatasında o yazıyı “veri gelmedi” yap, sayfa beyaz kalmasın. `yanit.ok` kontrolünü unutma.

## Bitti saymam için

- Arama ve bölge aynı anda süzüyor
- Kart sayısı, süzgeç tutunca değişiyor
- Boş sonuçta ızgara dağılmıyor, bir mesaj duruyor
- Veri fonksiyonu var: `suz(ulkeler, { aranan, bolge })`. DOM’a dokunmuyor, dizi döndürüyor

---

[← Önceki gün](../25-bar-charts/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../27-portfolio/ders.md)
