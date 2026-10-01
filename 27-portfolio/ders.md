# 27. Gün — Portfolyo

Tek sayfalık bir vitrin kurulur. Fotoğraf zorunlu değildir. Ad, bir cümle, proje kartları ve kartlar arasında gezen bir şerit yeter. Amaç gösterişli bir özgeçmiş değildir. Veri dizisinden arayüz kurmak ve o anki kartı tek bir sayıda tutmaktır.

## İçerik

Metinler JavaScript’te durur. HTML’e üç kart elle yazılmaz.

```js
const profil = {
  ad: "Serhat",
  satir: "İzmir, Van, İstanbul ve Trabzon arasında arayüz çalışıyor.",
}

const projeler = [
  { ad: "Gezegen tartısı", ozet: "Kütleyi başka çekimde göstermek.", yil: 2026 },
  { ad: "Çubuklar", ozet: "İki listeyi orantılı çubuk yapmak.", yil: 2026 },
  { ad: "Ülke kartları", ozet: "Arama ve bölgeyle süzmek.", yil: 2026 },
]
```

Cümle değiştirilebilir. Kart sayısı dizinin boyu kadardır. Dördüncü nesne eklenince dördüncü nokta da kendiliğinden gelir.

## Durum

Ekranda aynı anda bir proje görünsün. Sağda ve solda düğme, altta kaçıncı kartta olunduğunu söyleyen noktalar olsun.

Durum tek sayıdır: `sira`. Düğme onu artırır veya azaltır. Sona gelince başa, baştayken geri gidince sona sar. Noktaya basınca `sira` o indekse zıplar.

Sarmanın küçük bir hali:

```js
function sonraki(sira, boy) {
  return (sira + 1) % boy
}

function onceki(sira, boy) {
  return (sira - 1 + boy) % boy
}

console.log(sonraki(2, 3))
console.log(onceki(0, 3))
```

```text
0
2
```

Üç kartta son sıra `2`dir. Sonraki, `0`a döner. Baştayken önceki, `2`ye döner. `%` bölümden kalandır. Negatif kalanda `+ boy` düzeltir. Bu iki fonksiyon DOM görmez. Önce konsolda doğrula, sonra düğmeye bağla.

Kart her seferinde baştan basılabilir. Üç kart yan yana dizilip kap `translateX` ile de kaydırılabilir. İkinci yol daha çok CSS ister. İkisi de geçerlidir. Durum tek sayıda duracağı için ilk yol daha sadedir.

Noktalar `projeler.length` kadar üretilir. `sira` ile aynı indeksteki noktaya seçili sınıfı konur, ötekinden çıkar.

## Klavye ve hareket

Sol ve sağ ok, düğmeyle aynı işi yapar. Odak bir `input` içindeyse karışmaz. 23. gündeki erken çıkış burada da durur. Düğmelere `aria-label` ver: “önceki” ve “sonraki”. Yalnız ok işareti ekran okuyucuya yetmez.

İstenirse şerit beş saniyede bir `setInterval` ile ilerler. `document.hidden` ise tur atlanır. Sayfa arkadaysa dönmesin. Fare kartın üstündeyken de durur. `mouseenter` aralığı keser, `mouseleave` yeniden kurar. İki kez başlatma iki zamanlayıcı bindirmez. Kimliği bir değişkende tut, kurmadan önce eskisini `clearInterval` ile temizle.

## Görünüm

Geniş bir kart, bol boşluk, tek vurgu rengi. Satır `65ch` civarını geçmesin. `ch`, yaklaşık bir karakter genişliğidir. Telefon genişliğinde düğmeler alta insin.

## Bitti sayılması için

- Dizideki kart sayısı ile nokta sayısı aynı. Bir proje silinince ikisi birden azalır.
- Sondayken ileri, baştayken geri sarar. `sonraki` ve `onceki` konsolda doğrulanmıştır.
- Seçili nokta renk ile ayrılır.
- `sira` listenin dışına çıkmaz. Hesap bir fonksiyonda, `goster(sira)` yalnız çizer.

---

[← Önceki gün](../26-country-cards/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../28-scoreboard/ders.md)
