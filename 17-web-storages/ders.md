# 17. Gün — Web depoları

Çerezden ayrı, tarayıcının verdiği iki çekmece vardır. İkisi de metin tutar, ikisi de siteye özeldir. Fark, ömürlerindedir.

- `sessionStorage` sekme kapanınca silinir. Aynı sekmede yenilemeye dayanır.
- `localStorage` sen silene kadar durur. Başka sekme, yarın, haftaya.

Node’da bu ikisi yoktur. Denemeyi tarayıcıda yap. Kota dolunca yazma `QuotaExceededError` fırlatabilir. Onu 14. gündeki gibi yakala.

## Yazmak ve okumak

Arayüz ikisinde de aynı: `setItem`, `getItem`, `removeItem`, `clear`, `key`, `length`.

```js
localStorage.setItem("mutfak", "açık")
console.log(localStorage.getItem("mutfak"))
localStorage.removeItem("mutfak")
```

Olmayan anahtar `null` döner, `undefined` değil. Koşulda ikisi de boş sayılır ama `===` ile bakacaksan `null` bekle.

Değer her zaman metindir. Sayı yazsan bile okuyunca metin gelir.

```js
localStorage.setItem("adet", 3)
console.log(typeof localStorage.getItem("adet"))
```

Nesne ve dizi için dünkü JSON:

```js
const sepet = [
  { ad: "un", adet: 1 },
  { ad: "tuz", adet: 2 },
]
localStorage.setItem("sepet", JSON.stringify(sepet))

const gelen = JSON.parse(localStorage.getItem("sepet") || "[]")
console.log(gelen[0].ad)
```

`|| "[]"` koydum çünkü ilk açılışta anahtar yoktur, `parse(null)` patlamaz aslında, `null` metni bozuk sayılmaz ve `null` döner. Sonra `[0]` okursan patlar. Bu yüzden varsayılanı kendim koyarım.

## Temizlemek

```js
localStorage.removeItem("sepet")
sessionStorage.clear()
```

`clear`, o kaynaktaki her şeyi siler. Başka bir kaydı da götürebilir. Anahtarlar `not.` gibi bir ön ekle yazılır; silerken hepsi körlemesine `clear` edilmez.

## Hangisini seçerim

Sekme içi sihirbaz, adım adım form, “bu sayfa yenilensin ama tarayıcı kapanınca unutulsun”: oturum deposu.

Tema, dil, sepet, “beni hatırla”, taslak not: yerel depo.

İkisi de gizli kasa değil. Sayfadaki her kod okur. Şifre, jeton, kart numarası koyma. Onlar için çerez ve sunucu tarafı var; o bu otuz günün dışı.

Sekmeler arası haber için `window` üstünde `storage` olayı var. Başka sekme `localStorage` değiştirince bu sekme duyar. Aynı sekmede duymaz.

```js
window.addEventListener("storage", (olay) => {
  console.log(olay.key, olay.newValue)
})
```

## Egzersizler

1. Adını `localStorage`’a yaz, sayfayı yenile, hâlâ durduğunu gör. Sonra sil.
2. Aynı anahtarı `sessionStorage`’a yaz. Sekmeyi kapatıp yeni sekmede aç, gittiğini gör.
3. Bir görev listesini dizi olarak sakla. Sayfa açılınca oku, yoksa boş dizi kabul et.
4. Sayı sakla, okuyunca `Number` ile çevir, toplama yap. Çevirmeden `+` yaparsan bitiştiğini gör.
5. Bozuk bir JSON’u depoya elle yaz, `parse` ederken hatayı yakala, depoyu o anahtardan temizle.
6. İki anahtar koy, `clear` yerine yalnız birini `removeItem` ile sil, ötekinin durduğunu kontrol et.

---

[← Önceki gün](../16-json/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../18-promises/ders.md)
