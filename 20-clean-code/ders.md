# 20. Gün — Temiz kod

Dilin temel araçları önceki günlerde toplandı. Bu bölümde yeni bir API yoktur. Bundan sonra yazılan kodun haftalar sonra da okunması için birkaç kural konur. Airbnb, Standard ve Google kılavuzları uzundur. Burada o kılavuzların bu derslerde kullanılan özü durur.

Stil kavgası kişisel değil. Aynı repoda herkes aynı ritmi tutunca fark, fikre düşer. Noktalı virgül ve tırnak yüzünden dönen kod incelemesi zaman çalar.

## İsim

Ne yaptığını söylesin. `d` değil, `siparisler`. Fonksiyon fiil: `hesaplaToplam`. Boolean soru gibi: `acikMi`, `stokVar`. Kısaltma yalnız herkesin bildiği yerde: `id`, `url`.

Döngü sayacı `i` olabilir. Başka bir işin değişkeni `i` olmasın.

## Değişken

`const` varsayılan. Gerçekten yeniden atacaksan `let`. `var` yok. Kullanılmayan değişken durmasın. Sihirli sayıya isim ver:

```js
const KDV = 0.2
const kdvli = tutar * (1 + KDV)
```

Bir satırda bir iş. `let a = 1, b = 2` yazmam.

## Fonksiyon

Tek iş. Ekrana basmakla hesap yapmak ayrı fonksiyon olsun. Hesap saf kalsın, test edeyim. Uzunluk göz kararı: kaydırmaya başladıysam bölerim.

Parametre üçü geçtiyse nesne geçir, 11. gündeki parçalamayla al. Sıra karışmasın.

Erken çık. İç içe `if` büyürse önce olumsuz hali `return` et.

```js
function etiket(kisi) {
  if (!kisi || !kisi.ad) return "Serhat"
  return kisi.ad
}
```

## Dizi ve nesne

Diziyi `push` ile doldurmayı biliyorsun. Yeni liste üretiyorsan `map` ve `filter` daha az hata yapar. Orijinali bozan `sort` ve `splice` öncesi kopya aldığını düşün.

Nesne alanında tutarlı isim. Bir yerde `isim`, ötekinde `ad` olmasın. Aynı kavram tek kelime.

## Koşul

`===` kullan. `==` ile tür zorlama bu derste yok.

Boolean zaten boolean. `if (acikMi === true)` yerine `if (acikMi)`.

`switch` kullanıyorsan `break`’siz düşmeyi bilerek yap ve yorum yaz. Bilmeden bırakma.

Üçlü operatörü tek bakışta okunmuyorsa `if`’e çevir.

## Sınıf

Kurucu alan atasın ve doğrulasın. İş metodda olsun. Kalıtım iki katı geçmesin. Daha derinleşiyorsa bileşime bak: “bu bir termosdur” demek yerine termosa bir kap nesnesi vermek. Her yerde miras açma.

## Dosya

Bir dosya bir konu. `index.html` ince, kod `main.js` içinde. İsimler küçük harf ve tire: `sepet-listesi.js`. Senin klasörlerin de bu yüzden küçük.

Yorum, *ne* yaptığını tekrar etmesin. Kod onu söylüyor. Yorum, *neden* öyle yaptığını söylesin. “ay 0’dan başlar, ekranda 1 göster” gibi.

## Biçim

Bu rehberde şu ritim kullanılır:

- girinti iki boşluk
- satır sonuna noktalı virgül koymuyorum, dilin otomatik ekine güvenmiyorum diye değil; bu ders boyunca koymadım, karıştırmayalım
- metinde tek tırnak ya da çift seçilir ve dosya boyunca değiştirilmez; bu derslerdeki örnekler çift tırnak kullanır
- süslü parantez aynı satırda açılır
- satır 100 karakteri geçmesin, geçerse böl

Hangi ritmi seçtiğin, seçimine sadık kalmandan daha önemsiz. Depoda bir biçim aracı (Prettier) varsa tartışmayı ona bırak.

## Egzersizler

1. Eski bir pratiğini aç. `var`, `==` ve anlamsız isim varsa düzelt.
2. Hem konsola yazan hem indirim hesaplayan bir fonksiyonu ikiye böl.
3. Üçten fazla parametreli bir fonksiyonu tek nesne parametresine çevir.
4. İç içe üç `if`’i erken `return` ile düzleştir.
5. Bir sihirli sayıyı isimli sabite çıkar.
6. Kendine bir paragraf yaz: bundan sonraki projelerde hangi üç kuralı gevşetmeyeceksin. Dosyanın başına yorum diye koyma, README’ye üç madde olarak yaz.

---

[← Önceki gün](../19-closures/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../21-dom/ders.md)
