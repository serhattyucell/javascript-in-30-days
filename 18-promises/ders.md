# 18. Gün — Promise, fetch, async

Bazı işler hemen bitmez. Dosya, ağ, zamanlayıcı. JavaScript onları beklerken sayfayı dondurmaz. Sonuç “henüz yok, sonra gelir” diye bir söze sarılır. O sözün adı promise.

Promise üç haldedir: bekliyor, yerine geldi, reddedildi. Bir kez yerine gelir ya da reddedilir, sonra dönmez.

## Söz vermek

```js
function bekle(ms) {
  return new Promise((yerineGetir) => {
    setTimeout(() => yerineGetir(`${ms} ms geçti`), ms)
  })
}
```

Kurucu bir fonksiyon alır. Onun ilk parametresi başarı, ikincisi ret.

```js
function stokGetir(adet) {
  return new Promise((yerineGetir, reddet) => {
    if (adet < 0) reddet(new Error("eksi stok yok"))
    else yerineGetir({ adet })
  })
}
```

Tüketmek:

```js
stokGetir(4)
  .then((kayit) => console.log(kayit.adet))
  .catch((hata) => console.error(hata.message))
  .finally(() => console.log("bitti"))
```

`then` başarıyı, `catch` reti alır. `then` içinden yeni bir promise döndürürsen zincir onu bekler. Bu, iç içe callback piramidinin düz hâlidir.

## fetch

Tarayıcıdan adres çağırmanın güncel yolu. `fetch` hemen bir promise verir. Dikkat: 404 ve 500 de “söz yerine geldi” sayılır. Ağ koparsa ret olur. Durum kodunu sen bak.

```js
async function yorumlariAl() {
  const yanit = await fetch("https://jsonplaceholder.typicode.com/comments?postId=1")
  if (!yanit.ok) {
    throw new Error(`sunucu ${yanit.status}`)
  }
  return yanit.json()
}
```

`yanit.json()` da promise’tir. Metin gerekirse `yanit.text()` kullanılır.

Başkasının API’sine tarayıcıdan giderken adres, CORS izni vermiyorsa konsolda kızarır. Ders için açık bir deneme adresi yeter. Kendi sayfan değilse anahtar gömme.

## async ve await

`async` fonksiyon her zaman promise döndürür. İçindeki `await`, bir promise sonuçlanana kadar o fonksiyonu bekletir. Dışarıdaki kod akmaya devam eder. Yazım, sıradan koda benzer ve okunması kolaydır. Yeni kodda zincir yerine bu biçim kullanılır.

```js
async function goster() {
  try {
    const liste = await yorumlariAl()
    console.log(liste.length)
  } catch (hata) {
    console.error(hata.message)
  }
}

goster()
```

`await` yalnız `async` fonksiyonun içinde durur. Dosyanın en üstünde, modülde, yeni tarayıcılarda da durabilir. Düz script etiketinde durmaz. Şüphede bir `async function main()` sar, onu çağır.

İki iş birbirini beklemek zorunda değilse sıraya koyup zaman kaybetme:

```js
const [a, b] = await Promise.all([bekle(200), bekle(300)])
```

`Promise.all` biri reddederse hepsi düşer. Biri düşse de ötekilerin sonucunu istiyorsan `Promise.allSettled`.

## Callback ile kıyas

Eskiden “bitince şu fonksiyonu çağır” derdim. İç içe üç ağ isteği okunmaz hale gelirdi. Promise, o işi düz bir zincire ve `try/catch`’e bağlar. Callback hâlâ `setTimeout` ve olaylarda duruyor. Ağ işinde `async` kullan.

## Egzersizler

1. `bekle(500)` yaz, `then` ile mesajı bastır.
2. Aynı fonksiyonu `async/await` ile çağır.
3. Ret dönen bir promise yaz, `try/catch` ile mesajını yakala.
4. `fetch` ile yukarıdaki yorum adresini çağır, ilk yorumun `email` alanını yazdır.
5. Adresi bilerek boz, `yanit.ok` kontrolün çalışsın.
6. İki `bekle` çağrısını `Promise.all` ile yan yana tut. Ayrı `await` satırından daha kısa sürdüğünü konsol zamanıyla gör.
7. `fetch` sonucunu `localStorage`’a JSON diye yaz, sayfayı yenileyince depodan oku. Ağ bir kez yetsin.

---

[← Önceki gün](../17-web-storages/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../19-closures/ders.md)
