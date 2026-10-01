# 17. Gün — Web depoları

Sayfa yenilenince JavaScript’teki değişkenler silinir. Tarayıcı, siteye özel iki çekmece verir. İkisi de yalnızca metin tutar. Çerez değildir. Sunucuya her istekte gitmez.

| Çekmece | Ömrü |
| --- | --- |
| `sessionStorage` | Sekme kapanınca silinir. Yenilemeye dayanır. |
| `localStorage` | Sen silene kadar durur. Yarın da, başka sekmede de durur. |

Node’da bu ikisi yoktur. Deneme tarayıcıda, bir `index.html` açarak yapılır. Kota dolunca yazma hata fırlatabilir. 14. gündeki gibi yakalanır.

## Yazmak ve okumak

Arayüz ikisinde de aynıdır: `setItem`, `getItem`, `removeItem`, `clear`.

```js
localStorage.setItem("sehir", "İzmir")
console.log(localStorage.getItem("sehir"))
```

```text
İzmir
```

Sayfayı yenile, aynı satırı yalnız `getItem` ile tekrar çalıştır. `İzmir` hâlâ oradadır. Değişken olsaydı kaybolurdu.

Olmayan anahtar `null` döner, `undefined` değil.

```js
console.log(localStorage.getItem("yok"))
```

```text
null
```

Değer her zaman metindir. Sayı yazılsa bile okuyunca metin gelir.

```js
localStorage.setItem("adet", 3)
console.log(typeof localStorage.getItem("adet"))
```

```text
string
```

Toplamadan önce `Number(...)` gerekir. `"3" + 1` sonucu `"31"` olur. `Number("3") + 1` sonucu `4` olur.

Nesne ve liste için 16. günün `JSON.stringify` ve `JSON.parse` çifti kullanılır.

```js
const rota = [
  { sehir: "İzmir", gun: 1 },
  { sehir: "Van", gun: 2 },
]
localStorage.setItem("rota", JSON.stringify(rota))

const gelen = JSON.parse(localStorage.getItem("rota") || "[]")
console.log(gelen[0].sehir)
```

```text
İzmir
```

`|| "[]"` ilk açılış içindir. Anahtar yoksa `getItem` `null` döner. `parse` onu nesne yapmaz, sonra `[0]` okumak patlar. Varsayılan boş liste olarak verilir.

Bozuk metin `parse`i kırar. `try/catch` ile yakala, o anahtarı `removeItem` ile sil.

## Silmek

```js
localStorage.removeItem("rota")
```

`clear()` o sitedeki **her** anahtarı siler. Başka bir sayfanın anahtarını da götürür. Anahtarlar `rota.` gibi bir ön ekle yazılır. Silinecekse tek tek `removeItem` çağrılır.

Sekme kapanınca gitmesi gereken taslak `sessionStorage`a konur. Tema, dil, sepet, “adı hatırla” `localStorage`da kalır. Şifre, jeton ve kart numarası ikisine de konmaz. Sayfadaki her kod okuyabilir. Bunlar gizli kasa değildir.

Başka sekme `localStorage` değiştirince bu sekme `storage` olayını duyar. Aynı sekmede duymaz.

```js
window.addEventListener("storage", (olay) => {
  console.log(olay.key, olay.newValue)
})
```

Bunu görmek için aynı adresi iki sekmede aç. Birinde `setItem` çağır. Öteki sekmenin konsoluna bak.

## Egzersizler

1. `localStorage.setItem("ad", "Serhat")` yaz. Sayfayı yenile. Yalnız `getItem` ile oku. `Serhat` duruyorsa çekmece çalışıyordur. Sonra `removeItem` ile sil, `null` gör.
2. Aynı anahtarı `sessionStorage`a yaz. Sekmeyi kapat, yeni sekmede aç, `getItem` `null` olsun.
3. `["İzmir", "Van", "Trabzon"]` listesini `rota` anahtarıyla sakla. Sayfa açılınca oku. Anahtar yoksa boş liste kabul et.
4. `setItem("adet", 4)` yaz. Okuyunca `Number` ile çevir, 10 ekle. Sonuç `14` olsun. Çevirmeden topla, `410` veya `"410"` gör. Farkı not et.
5. `localStorage.setItem("bozuk", "{ad:")` yaz. `parse` ederken hatayı yakala, anahtarı sil.
6. `ad` ve `sehir` diye iki anahtar koy. Yalnız `sehir`i sil. `ad`ın durduğunu kontrol et. `clear` çağırma.

---

[← Önceki gün](../16-json/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../18-promises/ders.md)
