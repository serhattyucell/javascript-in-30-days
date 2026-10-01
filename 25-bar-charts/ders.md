# 25. Gün — Çubuk grafikler

Bu bölümde iki liste çubuğa çevrilir. Veri aşağıdadır. Çubuğun uzunluğu en büyük değere göre oranlanır. Grafik kütüphanesi yoktur. Bir `div` kullanılır, genişliği yüzdedir.

## Veri

Nüfus milyon cinsinden, yuvarlanmış. Dil, o dili konuşan ülke sayısı gibi düşünme; burada “konuşan nüfus, milyon” kaba bir ölçek. Amaç barların birbirine oranı.

```js
const nufus = [
  { ad: "Hindistan", milyon: 1430 },
  { ad: "Çin", milyon: 1410 },
  { ad: "ABD", milyon: 340 },
  { ad: "Endonezya", milyon: 280 },
  { ad: "Pakistan", milyon: 247 },
  { ad: "Nijerya", milyon: 229 },
  { ad: "Brezilya", milyon: 216 },
  { ad: "Bangladeş", milyon: 173 },
  { ad: "Rusya", milyon: 144 },
  { ad: "Meksika", milyon: 130 },
]

const diller = [
  { ad: "İngilizce", milyon: 1500 },
  { ad: "Çince", milyon: 1100 },
  { ad: "Hintçe", milyon: 600 },
  { ad: "İspanyolca", milyon: 560 },
  { ad: "Fransızca", milyon: 310 },
  { ad: "Arapça", milyon: 274 },
  { ad: "Bengalce", milyon: 273 },
  { ad: "Portekizce", milyon: 264 },
  { ad: "Rusça", milyon: 255 },
  { ad: "Urduca", milyon: 232 },
]
```

## Çubuk

En büyük değeri bul, `Math.max` veya `reduce`. Her satırın genişliği `(deger / enBuyuk) * 100` yüzde olsun. En büyük çubuk dolu görünür, ötekiler ona göre kısalır.

```html
<div class="satir">
  <span class="ad"></span>
  <span class="cubuk"></span>
  <span class="sayi"></span>
</div>
```

Satırı JavaScript üretsin. `.cubuk` için CSS:

```css
.satir {
  display: grid;
  grid-template-columns: 8rem 1fr 4rem;
  gap: 0.5rem;
  align-items: center;
}
.cubuk {
  display: block;
  height: 1.1rem;
  background: #c4552a;
  width: 0;
}
```

Genişliği `style.width = yuzde + "%"` ile ver.

## İki görünüm

İki düğme: “nüfus” ve “diller”. Biri seçilince listeyi boşalt, öteki veriyi bas, başlığı değiştir. Seçili düğmenin sınıfı dursun, öteki çıksın.

İsteğe bağlı üçüncü görünüm: her iki listede de ilk beşi al. `slice` aslı bozmasın, önce kopya. Diziyi büyükten küçüğe sen sırala, veri baştan sıralı gelse bile koda güvenme.

Sayıyı ekranda binlik ayıracıyla göstermek için:

```js
new Intl.NumberFormat("tr-TR").format(1430)
```

## Bitti saymam için

- En uzun çubuk satırı doldursun, küçüğü belirgin kısa dursun
- Düğme, seçili olduğunu renk ile söylesin
- Sıfır veya negatif değer gelirse çubuk `0%` olsun, eksi genişlik yazma
- Başlık, “10 ülke” veya “10 dil” diye verinin boyundan gelsin, elle “10” yazma

---

[← Önceki gün](../24-planet-weight/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../26-country-cards/ders.md)
