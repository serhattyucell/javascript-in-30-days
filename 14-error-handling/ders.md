# 14. Gün — Hata yönetimi

Hata, programın o satırdan sonra devam edemediğini gösterir. Yakalanmazsa sonraki kod çalışmaz, konsol kırmızı kalır. Yakalanırsa kullanıcıya düzgün bir cümle yazılır, ayrıntı konsolda tutulur.

## try, catch, finally

Şüpheli iş `try` içine konur. Fırlarsa `catch` çalışır. `finally` her durumda çalışır. Kutu kapanacaksa, “yükleniyor” yazısı gizlenecekse yeri orasıdır.

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

```text
sıfıra bölme
deneme bitti
```

`throw` olunca `try`nin geri kalanı atlanır. `catch` mesajı basar. `finally` yine çalışır. `bol(10, 2)` çağrılsaydı konsol önce `5` basar, “bu satır atlanır” da çalışır, `catch`e girilmez, `finally` yine girer.

## throw

`throw` bir değeri dışarı fırlatır. Düz metin de fırlatılır ama yığın izi kaybolur. `new Error("...")` hem mesaj hem iz taşır. İz, hatanın hangi satırdan geldiğini gösterir. Kullanıcıya iz gösterilmez. Konsolda kalır.

Kendi türü de kurulur. `instanceof` ile ayırt edilir. Bilinmeyen hata yutulmaz, yeniden fırlatılır.

```js
class StokHatasi extends Error {
  constructor(urun) {
    super(urun + " kalmadı")
    this.name = "StokHatasi"
  }
}

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

```text
un kalmadı
```

`extends` 15. gündeki kalıtımdır. Burada yalnız “bu hata `Error`ın özel bir halidir” demek için durur. Boş `catch { }` hatayı yok eder. Üç gün sonra kayıt neden yok diye aranır. En azından `console.error(hata)` konur.

## Sık türler

Motorun kendi ürettikleri:

| Tür | Ne zaman |
| --- | --- |
| `ReferenceError` | hiç tanımlanmamış isim |
| `TypeError` | olmayan metodu çağırmak, `null` üstünde alan okumak |
| `SyntaxError` | dosya daha çalışmadan bozuksa. `JSON.parse` bozuk metinde bunu fırlatır, o yakalanır |
| `RangeError` | aralık dışı bir sayı, örneğin liste uzunluğuna saçma bir değer |

```js
try {
  JSON.parse("{ad:}")
} catch (hata) {
  console.log(hata.name)
  console.log(hata.message)
}
```

`name` `SyntaxError` olur. `message` nerede bozulduğunu söyler. Hata nesnesinde bir de `stack` vardır. Onu kullanıcıya basma.

`try` bütün dosyayı sarmaz. Yalnız fırlatabilecek yer sarılır: JSON çözmek, tarayıcı deposunun kotası, bölme, kutudan gelen sayı.

## Egzersizler

1. Sıfıra bölen `bol` fonksiyonunu yaz. `throw new Error("sıfıra bölme")` etsin. Çağrıyı `try/catch` ile sar. `message`ı yazdır. `bol(8, 2)` de dene, `4` gör, `catch`e girme.
2. `finally` içine `let adim = 0` yerine dışarıda bir sayaç koy, `finally`de artır. Hem hata olunca hem olmayınca sayacın arttığını gör.
3. `"{ad:}"` metnini `JSON.parse` ile çöz. `name` ve `message` yazdır.
4. Tanımsız bir fonksiyon çağır: `yokBoyledBirFonksiyon()`. `ReferenceError` geldiğini gör. `try` dışındaysa alttaki satırlar çalışmaz. `try` içine alınca alttaki satırın çalıştığını gör.
5. `const kisi = null` olsun. `kisi.ad` oku. Gelen tür `TypeError` olsun. `catch` içinde bunu yazdır.
6. `StokHatasi` sınıfını kur. Ürün adı `"Van çayı"` olsun. `catch` içinde yalnız bu türü yakala, `message` `Van çayı kalmadı` olsun. Başka bir `Error` fırlatıldığında yeniden `throw` edildiğini de bir kez dene. O denemede program yine kırılır. Bu doğrudur. Bilinmeyen hata gizlenmemelidir.
7. Bilerek boş bir `catch` yaz, hatanın kaybolduğunu gör. İçine `console.error` ekle, geri gelsin.

---

[← Önceki gün](../13-console-methods/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../15-classes/ders.md)
