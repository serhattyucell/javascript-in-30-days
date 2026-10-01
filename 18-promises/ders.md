# 18. Gün — Promise, fetch, async

Bazı işler hemen bitmez. Beklerken sayfa donmasın diye JavaScript sonucu bir söze sarar. Sözün adı promise’tir. Üç hali vardır: bekliyor, yerine geldi, reddedildi. Bir kez sonuçlanır, sonra dönmez.

## Söz vermek

`new Promise` bir fonksiyon ister. İlk parametre başarı, ikincisi rettir. Burada adları `olur` ve `olmaz`.

```js
function bekle(ms) {
  return new Promise((olur) => {
    setTimeout(() => olur(ms + " ms geçti"), ms)
  })
}
```

`bekle(500)` hemen bir promise döndürür. 500 ms sonra o söz “500 ms geçti” metniyle yerine gelir. Çağırmak yetmez. Sonucu `then` veya `await` ile alınır.

```js
bekle(500).then((mesaj) => console.log(mesaj))
```

Yarım saniye sonra konsolda `500 ms geçti` görünür. Ondan önceki satırlar beklemeden devam eder. Bu, sayfanın kilitlenmemesidir.

Ret şöyle yazılır:

```js
function stokGetir(adet) {
  return new Promise((olur, olmaz) => {
    if (adet < 0) {
      olmaz(new Error("eksi stok yok"))
    } else {
      olur({ adet })
    }
  })
}

stokGetir(4)
  .then((kayit) => console.log(kayit.adet))
  .catch((hata) => console.error(hata.message))
  .finally(() => console.log("bitti"))
```

```text
4
bitti
```

`stokGetir(-1)` çağrılırsa `then` atlanır, `catch` `eksi stok yok` basar, `finally` yine çalışır. `then` içinden yeni bir promise döndürülürse zincir onu bekler.

## fetch

Tarayıcıdan adres çağırmanın güncel yoludur. `fetch` hemen bir promise verir. Dikkat: 404 ve 500 de sözü yerine gelmiş sayar. Ağ kopunca ret olur. Durum koduna `yanit.ok` ile bakılır. `ok`, kod 200–299 arasındaysa doğrudur.

```js
async function yorumlariAl() {
  const yanit = await fetch(
    "https://jsonplaceholder.typicode.com/comments?postId=1"
  )
  if (!yanit.ok) {
    throw new Error("sunucu " + yanit.status)
  }
  return yanit.json()
}
```

`yanit.json()` da promise’tir. Metin gerekirse `yanit.text()` kullanılır. Bu adres deneme içindir. Cevap, yorum nesnelerinin listesidir. `email` alanı vardır.

Başkasının adresi tarayıcıdan izin vermiyorsa konsol CORS diye kızarır. İzin sunucunun işidir. Kalıbı değiştirerek aşılmaz.

## async ve await

`async` fonksiyon her zaman promise döndürür. İçindeki `await`, promise sonuçlanana kadar o fonksiyonu bekletir. Sayfanın geri kalanı donmaz. Yazım, sıradan koda benzer. Yeni kodda uzun `then` zinciri yerine bu kullanılır.

```js
async function goster() {
  try {
    const liste = await yorumlariAl()
    console.log(liste.length)
    console.log(liste[0].email)
  } catch (hata) {
    console.error(hata.message)
  }
}

goster()
```

Konsolda bir sayı ve bir e-posta görünür. Ağ yoksa `catch` mesajı basar.

`await` , `async` fonksiyonun içinde durur. Düz `script` etiketinin en üstüne yazılırsa sözdizimi hatası olur. Bir `async function main()` sar, onu çağır.

İki iş birbirini beklemek zorunda değilse sıraya koymak zaman kaybettirir. `Promise.all` ikisini birden bekler. Biri reddederse hepsi düşer. Biri düşse de ötekilerin sonucu isteniyorsa `Promise.allSettled` kullanılır.

```js
async function ikisi() {
  console.time("yan yana")
  const [a, b] = await Promise.all([bekle(200), bekle(300)])
  console.timeEnd("yan yana")
  console.log(a, b)
}

ikisi()
```

Süre 500 değil, yaklaşık 300 ms olur. İkisi aynı anda başlar. Biten, yavaş olanın süresidir. `await bekle(200)` sonra `await bekle(300)` yazılsaydı süre yaklaşık 500 ms olurdu. Birbirine bağlı değillerse `Promise.all` seçilir.

Eskiden “bitince şu fonksiyonu çağır” denirdi. Üç ağ isteği iç içe okunmaz hale gelirdi. Ağ işinde `async` kullanılır. `setTimeout` ve tıklama hâlâ geri çağırmadır. Onlar promise değildir.

## Egzersizler

1. `bekle(500)` yaz. `then` ile mesajı bastır. İleti hemen değil, yarım saniye sonra gelsin.
2. Aynı fonksiyonu `async` bir `main` içinden `await` ile çağır. Sonuç aynı metin olsun.
3. Negatif adette ret dönen `stokGetir`i `try/catch` ile çağır. `eksi stok yok` gör.
4. Yukarıdaki yorum adresini `fetch` ile çağır. İlk yorumun `email` alanını yazdır. Liste boşsa “yok” yaz. `liste[0]`a bakmadan önce uzunluğu kontrol et.
5. Adresi bilerek `https://jsonplaceholder.typicode.com/yok-boyle-bir-yol` yap. `yanit.ok` false olmalıdır. `throw` çalışsın, `catch` sunucu kodunu bassın.
6. İki `bekle` çağrısını `Promise.all` ile yan yana tut. Ayrı ayrı `await` satırının daha uzun sürdüğünü `console.time` ile gör.
7. `fetch` sonucunun ilk yorumunu `localStorage`a JSON diye yaz. Sayfayı yenile. Anahtar varsa ağ yerine oradan oku. Yoksa `fetch` et, sonra yaz. Ağ bir kez yetsin.

---

[← Önceki gün](../17-web-storages/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../19-closures/ders.md)
