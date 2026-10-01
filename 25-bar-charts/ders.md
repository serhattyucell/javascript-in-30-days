# 25. Gün — Çubuk grafikler

İki liste çubuğa çevrilir. Veri aşağıdadır. Çubuğun uzunluğu en büyük değere göre oranlanır. Grafik kütüphanesi yoktur. Bir `div` kullanılır, genişliği yüzdedir.

Sayılar milyon cinsindedir, yuvarlanmıştır. Amaç tam sayım değil, çubukların birbirine oranıdır.

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
  { ad: "Arapça", milyon: 274 },
  { ad: "Portekizce", milyon: 264 },
  { ad: "Rusça", milyon: 255 },
  { ad: "Türkçe", milyon: 88 },
]
```

Türkçe satırı ölçeği görmek içindir. 88, 1500’ün yanında kısa bir çubuk olmalıdır. Kısa değilse oran yanlış hesaplanmıştır.

## Oran

En büyük değeri bul. `reduce` ile biriken en büyüğü tut veya `Math.max(...liste.map((x) => x.milyon))` kullan.

Her satırın genişliği `(deger / enBuyuk) * 100` yüzdedir. En büyük çubuk `100%` olur. Ötekiler ona göre kısalır. Sıfır veya negatif değerde genişlik `0%` olsun. Eksi yüzde yazma.

Küçük bir kontrol, sayfadan önce konsolda:

```js
const enBuyuk = 1500
console.log((88 / enBuyuk) * 100)
```

```text
5.8666...
```

Türkçe çubuğu yaklaşık yüzde 6 genişlik alır. İngilizce yüzde 100 alır.

## Satır

HTML’de boş bir `div id="grafik"` olsun. Satırı JavaScript üretsin.

```html
<div class="satir">
  <span class="ad"></span>
  <span class="cubuk"></span>
  <span class="sayi"></span>
</div>
```

```css
.satir {
  display: grid;
  grid-template-columns: 8rem 1fr 5rem;
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

Genişlik `cubuk.style.width = yuzde + "%"` ile verilir. Ad solda, sayı sağda görünsün. Sayıyı binlik ayraçla göstermek için:

```js
new Intl.NumberFormat("tr-TR").format(1430)
```

Bu, `1.430` metnini verir. Türkçe ayraç noktadır.

## İki görünüm

İki düğme: “nüfus” ve “diller”. Biri seçilince listeyi `replaceChildren` ile boşalt, öteki veriyi bas, başlığı değiştir. Seçili düğmeye bir sınıf ekle, ötekinden çıkar. İkisi birden seçili görünmesin.

İsteğe bağlı üçüncü düğme: ilk beş. `slice` aslı bozmasın. Önce kopya al, büyükten küçüğe sırala, sonra `slice(0, 5)`. Veri baştan sıralı gelse bile koda güvenme. Sıralamayı sen yap.

Başlık “10 ülke” diye elle yazılmasın. `liste.length`ten gelsin. Diziden bir satır silinince başlık da 9 desin.

## Bitti sayılması için

- En uzun çubuk satırı doldursun. 88 milyonluk satır gözle görülür kısa olsun.
- Düğme, seçili olduğunu renk ile söylesin.
- Sıfır veya negatif değerde çubuk `0%` olsun.
- Başlık, verinin boyundan gelsin.

---

[← Önceki gün](../24-planet-weight/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../26-country-cards/ders.md)
