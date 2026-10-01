# 20. Gün — Temiz kod

Yeni bir komut yoktur. Önceki günlerdeki araçlar, üç gün sonra da okunacak biçimde yazılır. Airbnb, Standard ve Google’ın kılavuzları uzundur. Burada o kılavuzların bu derslerde kullanılan özü vardır.

Aynı repoda herkes aynı ritmi tutunca tartışma fikre düşer. Noktalı virgül yüzünden dönen inceleme zaman çalar. Hangi ritim seçildiği, seçime sadık kalmaktan daha önemsizdir.

## Ad

Ne yaptığını söylesin.

| Kötü | İyi | Neden |
| --- | --- | --- |
| `d` | `sehirler` | liste olduğu belli |
| `hesapla` | `hesaplaToplam` | neyi hesapladığı belli |
| `aktif` | `acikMi` | evet/hayır sorusu gibi |

Kısaltma yalnız herkesin bildiği yerde durur: `id`, `url`. Döngü sayacı `i` olabilir. Başka bir işin değişkeni `i` olmasın. `x` bir şehir tutuyorsa adı `sehir` olsun.

## Değişken

`const` varsayılandır. Gerçekten yeniden atanacaksa `let`. `var` yoktur. Kullanılmayan değişken durmaz. Anlamı gizli sayıya ad verilir.

```js
const KDV = 0.2
const kdvli = 100 * (1 + KDV)
```

`100 * 1.2` de çalışır. 1.2’nin KDV olduğu ancak okuyan hatırlarsa bellidir. Sabit onu söyler.

Bir satırda bir iş yapılır. `let a = 1, b = 2` yazılmaz.

## Fonksiyon

Tek iş. Ekrana basmakla hesap yapmak ayrı fonksiyondur. Hesap saf kalır, konsolsuz denenebilir.

Parametre üçü geçtiyse tek nesne geçirilir. 11. gündeki parçalama ile alınır. Sıra karışmaz.

```js
function etiket({ ad = "Serhat", sehir = "İzmir" }) {
  return ad + ", " + sehir
}
```

İç içe `if` büyürse önce olumsuz hal `return` edilir. Buna erken çıkış denir.

```js
function etiketYaz(kisi) {
  if (!kisi || !kisi.ad) {
    return "Serhat"
  }
  return kisi.ad + ", " + (kisi.sehir || "Van")
}

console.log(etiketYaz(null))
console.log(etiketYaz({ ad: "Serhat", sehir: "Trabzon" }))
```

```text
Serhat
Serhat, Trabzon
```

İlk kapı tutmazsa fonksiyon biter. İçeri giren dal daha az girintilidir.

## Liste, nesne, koşul

Yeni liste üretilecekse `map` ve `filter` daha az hata yapar. Sayaç kaybolur. Asıl listeyi değiştiren `sort` ve `splice` öncesinde kopya alınır. 5. ve 9. günde nedeni görüldü.

Aynı kavrama tek ad verilir. Bir yerde `isim`, ötekinde `ad` olmasın. Bu derslerde kişi adı `ad`, yer adı `sehir`dir.

Eşitlik `===` iledir. `if (acikMi === true)` yerine `if (acikMi)` yazılır. Değer zaten `true` veya `false` ise ikinci kıyas gürültüdür.

`switch`te `break`siz düşme bilerek yapılır ve yanına bir yorum konur. Üçlü operatör tek bakışta okunmuyorsa `if`e çevrilir.

## Sınıf ve dosya

Kurucu alan atar ve doğrular. İş metodda durur. Kalıtım iki katı geçmez. Daha derinleşirse “bu ondan türer” yerine içine bir nesne konur. Her iş sınıfa girmek zorunda değildir.

Bir dosya bir konu tutar. `index.html` ince, kod `main.js` içindedir. Dosya adı küçük harf ve tire olur: `sehir-listesi.js`.

Yorum, kodun ne yaptığını tekrar etmez. Kod onu söyler. Yorum, *neden* öyle yapıldığını söyler. “ay 0’dan başlar, ekranda 1 göster” gibi.

## Biçim

Bu rehberde şu ritim kullanılır:

- girinti iki boşluk
- satır sonuna noktalı virgül konmaz
- metin çift tırnak
- süslü parantez aynı satırda açılır
- satır 100 karakteri geçerse bölünür

Seçilen araç Prettier ise tartışma ona bırakılır. El ile her dosyada başka ritim tutulmaz.

## Egzersizler

1. Eski bir alıştırmayı aç. `var`, `==` ve `d` gibi anlamsız ad varsa düzelt. Düzelmiş halini çalıştır, sonucun değişmediğini gör.
2. Hem konsola yazan hem indirim hesaplayan bir fonksiyonu ikiye böl. `hesaplaIndirim(200, 0.1)` konsolsuz `180` dönsün.
3. `kur(ad, sehir, yil, aktif)` fonksiyonunu tek nesne parametresine çevir. Çağrı `{ ad: "Serhat", sehir: "İstanbul", yil: 2026, aktif: true }` olsun.
4. İç içe üç `if`i erken `return` ile düzleştir. Davranış aynı kalsın. İki çağrıyla dene.
5. `fiyat * 1.18` içindeki `1.18`i `KDV` sabitine çıkar. Ad, oranın ne olduğunu söylesin.
6. Bundan sonraki projelerde gevşemeyecek üç kuralı bir yere yaz. Dosyanın başına uzun yorum koyma. Üç madde yeter. Örnek: `const` varsayılan, `===`, fonksiyon tek iş.

---

[← Önceki gün](../19-closures/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../21-dom/ders.md)
