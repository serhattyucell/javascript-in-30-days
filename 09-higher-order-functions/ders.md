# 9. Gün — Yüksek seviye fonksiyonlar

Yüksek seviye fonksiyon, fonksiyonu değer gibi taşır. Bir fonksiyon başka bir fonksiyonu argüman alır ya da fonksiyon döndürür. Diziyi sayaçla dolaşıp yeni dizi üretmek yerine bu metodlar kullanılır. Yazım, sayacın nasıl arttığını değil, işlemin ne olduğunu gösterir.

## Geri çağırma

```js
function tekrar(kere, is) {
  for (let i = 0; i < kere; i += 1) {
    is(i)
  }
}

tekrar(3, (i) => console.log(`tur ${i}`))
```

## Fonksiyon döndürmek

İç fonksiyon, dıştaki argümanı hatırlar. Bu yapı 19. gündeki closure konusudur. Bu bölümde yalnızca kısa bir örnek vardır.

```js
function carp(katsayi) {
  return (n) => n * katsayi
}

const ucKat = carp(3)
console.log(ucKat(5))
```

## Zaman

`setTimeout` geciktirir, `setInterval` tekrarlar. Süre milisaniyedir. İkisini de `clearTimeout` / `clearInterval` ile durdurursun.

```js
const kapı = setTimeout(() => {
  console.log("bir saniye geçti")
}, 1000)

const nabiz = setInterval(() => {
  console.log("tik")
}, 2000)

clearInterval(nabiz)
```

`clearInterval`’i hemen çağırırsan hiç tik görmezsin. Denemek için birkaç tur sayıp öyle kes.

## forEach

Her eleman için bir iş. Yeni dizi üretmez. Dönüş değerini kullanmam.

```js
const sehirler = ["İzmir", "Van", "İstanbul"]
sehirler.forEach((sehir, indeks) => {
  console.log(indeks, sehir)
})
```

## map

Aynı uzunlukta yeni dizi. Her elemanı dönüştürürsün.

```js
const fiyatlar = [10, 20, 30]
const kdvli = fiyatlar.map((f) => f * 1.2)
console.log(kdvli)
console.log(fiyatlar)
```

## filter

Koşulu geçenleri yeni dizide tutar.

```js
const stok = [0, 4, 0, 2]
const varOlan = stok.filter((adet) => adet > 0)
```

## reduce

Listeyi tek değere indirir. Toplam, sayım, gruplama. İlk değer ver, vermezsen ilk eleman başlangıç olur.

```js
const toplam = [4, 5, 6].reduce((birikim, n) => birikim + n, 0)
console.log(toplam)
```

Nesneleri etiketlerine göre kümelemek de buna gider:

```js
const raflar = [
  { tur: "kuru", ad: "un" },
  { tur: "yas", ad: "süt" },
  { tur: "kuru", ad: "pirinç" },
]
const grup = raflar.reduce((kutu, urun) => {
  if (!kutu[urun.tur]) kutu[urun.tur] = []
  kutu[urun.tur].push(urun.ad)
  return kutu
}, {})
```

## every, some, find, findIndex

```js
const notlar = [70, 80, 90]
console.log(notlar.every((n) => n >= 50))
console.log(notlar.some((n) => n >= 90))
console.log(notlar.find((n) => n > 75))
console.log(notlar.findIndex((n) => n > 75))
```

`find` bulamazsa `undefined`. `findIndex` bulamazsa `-1`. `every` boş dizide `true` döner. Mantıkta “karşı örnek yok” diye düşünülür. Şaşırma.

## sort, bir daha

5. günde görülen `sort`, karşılaştırma fonksiyonu aldığı için burada da durur. Orijinali bozar.

```js
const kayitlar = [
  { ad: "Serhat", sehir: "Van", yas: 30 },
  { ad: "Serhat", sehir: "İzmir", yas: 22 },
]
kayitlar.slice().sort((a, b) => a.yas - b.yas)
```

Zincir kurulur. `filter` ardından `map` ardından `reduce`. Her halka yeni dizi veriyorsa sorun yok. `sort` halkada orijinali bozmamak için önce `slice`.

```js
const sonuc = [1, 2, 3, 4]
  .filter((n) => n % 2 === 0)
  .map((n) => n * 10)
console.log(sonuc)
```

## Egzersizler

1. Sayı dizisini `map` ile iki katına çıkar.
2. 50’den büyük notları `filter` ile ayır.
3. `reduce` ile dizinin toplamını ve ortalamasını bul.
4. Tüm notlar 60 üstü mü, `every` ile bak. En az bir tane 100 var mı, `some`.
5. İnsan nesneleri dizisinde yaşı 18’den büyük ilk kişiyi `find` ile bul.
6. `setTimeout` ile 2 saniye sonra bir cümle bastır.
7. Bir `katla(n)` yazın. Dönüş değeri `x => x * n` olsun.
8. Ürün listesini fiyata göre ucuzdan pahalıya sırala. Asıl dizinin bozulmadığını göster.
9. `forEach` ile her ismin uzunluğunu yazdır. Aynı işi `map` ile yapınca ne döndüğüne bak.

---

[← Önceki gün](../08-objects/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../10-sets-and-maps/ders.md)
