# 14. Gün — Hata yönetimi

Hata, programın o satırdan sonra devam edemediğini gösterir. Yakalanmazsa sonraki kod çalışmaz. Yakalanırsa kullanıcıya düzgün bir ileti, konsola da bir iz kalır.

## try, catch, finally

Şüpheli işi `try` içine koy. Patlarsa `catch` çalışır. `finally` her halükârda çalışır: kutu kapansın, yükleniyor yazısı gizlensin.

```js
function bol(a, b) {
  if (b === 0) {
    throw new Error("sıfıra bölme")
  }
  return a / b
}

try {
  console.log(bol(10, 0))
  console.log("bu satır atlanır")
} catch (hata) {
  console.error(hata.message)
} finally {
  console.log("deneme bitti")
}
```

`throw` yoksa ve motor da şikâyet etmiyorsa `catch` hiç girmez. `finally` yine girer.

## throw

`throw` ile bir değer fırlatılır. Çoğu zaman bu değer `Error` nesnesidir. Düz metin de fırlatılır ama yığın izi kaybolur. Bu nedenle `new Error("...")` kullanılır.

Kendi türünü de üretebilirsin:

```js
class StokHatasi extends Error {
  constructor(urun) {
    super(`${urun} kalmadı`)
    this.name = "StokHatasi"
  }
}
```

`catch` içinde `instanceof` ile ayırırsın. Her hatayı aynı cümleyle yutma. Bilmediğin hatayı tekrar fırlat:

```js
try {
  throw new StokHatasi("un")
} catch (hata) {
  if (hata instanceof StokHatasi) {
    console.warn(hata.message)
  } else {
    throw hata
  }
}
```

## Sık türler

Motorun kendi ürettikleri:

- `ReferenceError` — hiç tanımlanmamış isim
- `TypeError` — olmayan metodu çağırmak, `null` üstünde alan okumak
- `SyntaxError` — kod daha çalışmadan bozuk. `try` ile çoğu söz dizimi hatasını yakalayamazsın, çünkü dosya parse edilemez. `JSON.parse` bozuk metinde söz dizimi hatası fırlatır, onu yakalarsın
- `RangeError` — dizi uzunluğuna saçma bir sayı vermek gibi, aralık dışı

```js
try {
  JSON.parse("{ad:}")
} catch (hata) {
  console.log(hata.name)
}
```

Hata nesnesinde `name`, `message`, `stack` vardır. Kullanıcıya `stack` gösterme. Onu kendi konsolunda tut.

## Nerede yutmamalısın

Boş `catch` görürsem rahatsız olurum. Hata kaybolur, üç gün sonra “neden kayıt yok” diye ararsın. En azından `console.error` koy. Daha iyisi: beklediğin hatayı çevir, gerisini yukarı bırak.

`try` bloğu bütün dosyayı sarmamalıdır. Yalnızca gerçekten fırlatabilecek yer sarılır: JSON çözmek, `localStorage` kotası, bölme, dışarıdan gelen sayı.

## Egzersizler

1. Sıfıra bölen bir fonksiyon yaz, `throw` etsin. Çağıranı `try/catch` ile sar, mesajı yazdır.
2. `finally` içine bir sayaç koy. Hem hata olunca hem olmayınca arttığını gör.
3. Bozuk bir JSON metnini `JSON.parse` ile çöz, hatanın `name` ve `message` alanlarını yazdır.
4. Tanımsız bir fonksiyon çağır. `ReferenceError` mı geliyor, bak.
5. `null` bir değişkenin `.ad` alanını okumayı dene. Gelen tür `TypeError`.
6. `StokHatasi` diye bir sınıf üret. Bir ürün listesinden düşerken adet 0 ise onu fırlat, `catch` içinde yalnız o türü yakala.
7. Bilerek boş bir `catch` yaz, sonra içine log ekle. İkisinde de hatanın kaybolup kaybolmadığına bak.

---

[← Önceki gün](../13-console-methods/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../15-classes/ders.md)
