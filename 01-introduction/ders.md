# 1. Gün — Giriş

Bu gün kodun nerede yazıldığını, nasıl çalıştırıldığını ve bir değere nasıl isim verildiğini gösterir. Önceden programlama bilmeye gerek yoktur. Yapılacak iş, konsolu açıp aşağıdaki örnekleri tek tek denemektir. Her örneğin altında, çalışınca ne görüneceği yazıyor. O satır görünmüyorsa yazım hatası vardır.

## JavaScript ne işe yarar

Tarayıcıdaki sayfa tek başına durağandır. Bir düğmeye basınca bir şey olsun, bir kutu dolsun, bir hesap yapılsın diye sayfaya JavaScript eklenir. Aynı dil sonra mobil uygulamada, küçük oyunlarda ve sunucuda da kullanılır. Bu rehber ilk iş olarak tarayıcıdaki JavaScript’i ele alır.

Gerekli olanlar: bir bilgisayar, internet, Google Chrome ve bir metin editörü. Visual Studio Code yeterlidir.

## Konsolu açmak

Konsol, yazılan JavaScript’i hemen çalıştıran penceredir. Sonuç sayfada değil, bu pencerede görünür.

1. Chrome’u aç.
2. `F12` tuşuna bas. Mac’te menüden **Görünüm → Geliştirici → JavaScript Konsolu** da olur.
3. Üstte **Console** yazan sekmeyi seç.
4. Altta yanıp sönen imlecin olduğu yere kod yazılır. **Enter** kodu çalıştırır.

Kısa yol: Mac’te `Command + Option + J`, Windows ve Linux’ta `Ctrl + Shift + J`.

Daha uzun bir iş için klasör açılır, içine `index.html` ve `main.js` konur. Bu günün sonunda o dosya çifti de kurulacak. Node.js şimdilik gerekmez. İleride terminalden `node dosya.js` denmek istenirse [nodejs.org](https://nodejs.org) adresinden LTS sürümü indirilir. Kurulum `node -v` ile kontrol edilir. Bir sürüm numarası çıkıyorsa tamamdır.

## İlk satır

Konsola şunu yazıp Enter’a bas:

```js
console.log("Serhat, İzmir")
```

Parça parça:

- `console` tarayıcının konsoludur.
- Nokta, o nesnenin bir aracını seçer.
- `log` seçilen aracıdır. Parantezin içindeki değeri konsola yazar.
- Tırnak, içindeki şeyin metin olduğunu söyler. Tırnak olmazsa JavaScript bunu bir isim sanır ve hata verir.

Konsolda görünen:

```text
Serhat, İzmir
```

Bu yazı web sayfasında görünmez. Öğrenirken ve hata ararken değerin ne olduğunu görmek için kullanılır.

Virgülle birden fazla değer verilebilir. Her virgül konsolda bir boşluk gibi durur.

```js
console.log("Serhat", "Van", 3)
```

```text
Serhat Van 3
```

`"3"` metindir, `3` sayıdır. Tırnak farkı 2. günde ayrı işlenir.

## Yorum

Motorun okumaması gereken satırın başına `//` konur. Birkaç satır `/*` ile başlar, `*/` ile biter.

```js
// bu satır çalışmaz
console.log("bu çalışır")
```

Konsolda yalnız `bu çalışır` görünür. Yorum, yarın okuyacak kişiye “neden böyle” demek içindir. Kodun ne yaptığını tekrar etmek için değildir.

## Yazım kuralı

Parantez, tırnak ve büyük harf önemlidir. Aşağıdaki satır çalışmaz, çünkü tırnak kapanmamıştır:

```js
console.log("Serhat)
```

Konsol kırmızı bir ileti basar ve satır numarasını söyler. İlk bakılacak yer odur.

`console` ile `Console` aynı değildir. İkincisi tanımsızdır, hata verir.

## Aritmetik

Konsol hesap makinesi gibi de kullanılır.

| İşaret | Anlamı | Örnek | Sonuç |
| --- | --- | --- | --- |
| `+` | toplama | `17 + 4` | `21` |
| `-` | çıkarma | `17 - 4` | `13` |
| `*` | çarpma | `17 * 4` | `68` |
| `/` | bölme | `17 / 4` | `4.25` |
| `%` | bölümden kalan | `17 % 4` | `1` |
| `**` | üs | `2 ** 5` | `32` |

`17 % 4` şunu sorar: 17’nin içinde 4, 4 kez vardır, geriye 1 kalır. Çift sayıyı ayırt etmek için sonra lazım olur. Çift sayıda 2’ye bölümden kalan 0’dır.

Hepsini tek tek yazmak şart değildir. Şu üçü yeter:

```js
console.log(17 + 4)
console.log(17 % 4)
console.log(2 ** 5)
```

## Sayfaya JavaScript koymak

Üç yol vardır. Günlük işte üçüncüsü kullanılır.

**1. Satır içi.** Kod, düğmenin üzerine yazılır. Kısa deneme içindir, sayfa kalabalıklaşır.

```html
<button onclick="console.log('tıkladın')">Bak</button>
```

**2. Sayfanın içinde.** `script` etiketi, `body` kapanmadan hemen önce durur. Önce HTML çizilir, sonra kod çalışır. Başta durursa sayfa henüz yokken kod öğe arar ve `null` bulur.

Aşağıyı `gun1.html` diye kaydedip Chrome’da aç. `F12` ile konsola bak.

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="UTF-8" />
    <title>Gün 1</title>
  </head>
  <body>
    <h1>Serhat, İzmir</h1>
    <script>
      console.log("sayfa içinden")
    </script>
  </body>
</html>
```

**3. Dış dosya.** HTML ayrı, kod ayrı. Tercih edilen yol budur.

`main.js`:

```js
console.log("dosyadan geldim")
```

`index.html` içinde, yine `body` sonunda:

```html
<script src="main.js"></script>
```

`src`, dosyanın adıdır. İki dosya aynı klasörde durmalıdır. Birden fazla dosya eklenirse üstteki önce çalışır. `menu.js` içinde kurulan bir isim, ondan sonra gelen `main.js` içinde görünür. Sıra ters olursa “tanımlı değil” hatası çıkar.

## Verinin ilk türleri

Bir değerin türü, onunla ne yapılabileceğini belirler. Sayı toplanır. Metin birleştirilir. Bu gün yalnız isimler var. Yarın her biri tek tek açılır.

| Yazılış | Tür | Ne demek |
| --- | --- | --- |
| `4`, `3.5` | sayı | hesap yapılacak değer |
| `"çay"` veya `'çay'` | metin | tırnak içindeki yazı |
| `true`, `false` | mantık | evet ya da hayır |
| `undefined` | tanımsız | henüz değer verilmemiş |
| `null` | boş | bilerek boş bırakılmış |

Türü sormak için `typeof` kullanılır. Sonuç bir metindir.

```js
console.log(typeof 4)
console.log(typeof "çay")
console.log(typeof true)
console.log(typeof undefined)
```

```text
number
string
boolean
undefined
```

`typeof null` sonucu `"object"` çıkar. `null` nesne değildir. Dilin eski bir tutarsızlığıdır. Boş değer olarak kalır. 3. günde yine geçecek.

## Değişken

Değişken, bir değere verilen addır. Değer değişebilir, ad aynı kalır. Kasadaki fiyat değişince etiketi sökmek gerekmez.

```js
let bilet = 2
const sehir = "Trabzon"
```

- `let` sonradan başka bir değer alabilir.
- `const` bir kez bağlanır, yeniden atanamaz.
- `var` eski yazımdır. Yeni kodda kullanılmaz. Eski dosyada `let` gibi okunur ama kapsamı daha gevşektir. Kapsam 8. gündedir.

```js
let bilet = 2
bilet = bilet + 1
console.log(bilet)
```

```text
3
```

`const` ile aynı şeyi denemek hata verir:

```js
const sehir = "Van"
sehir = "Trabzon"
```

Konsol “atama sabite yapılamaz” anlamına gelen bir ileti basar. `sehir` bir daha değişmeyecekse `const` doğrudur. Bilet sayısı artacaksa `let` doğrudur.

Ad, işi söyler. `x` yerine `biletSayisi` yazılır. İlk karakter harf, `_` veya `$` olabilir. Rakamla başlanamaz. Boşluk konmaz. Kelimeler `biletSayisi` gibi birleşir. JavaScript’te bu biçime camelCase denir.

## Egzersizler

Her maddeyi konsolda ya da `main.js` içinde ayrı ayrı dene. Cevabı ezberleme, sonucu konsolda gör.

1. Üç ayrı `console.log` ile `Serhat`, `İzmir` ve bir yaş sayısı yazdır.
2. Bir satırı `//` ile kapat. Sayfayı yenile. O satırın susduğunu gör.
3. `18 * 4` ve `18 % 4` sonuçlarını yazdır. 18, 4’e bölününce kalan kaçtır, bir cümleyle not et.
4. `let bilet = 1` yaz. Sonra `bilet` değerini 3 yap. İkisinin arasında ve sonunda `console.log(bilet)` koy. Sıranın 1, sonra 3 olduğunu gör.
5. `const sehir = "Van"` satırından sonra `sehir = "Trabzon"` dene. Kırmızı iletiyi oku.
6. `typeof` ile bir sayı, bir metin ve `true` değerinin türünü yazdır.
7. `index.html` ve `main.js` kur. HTML dosyayı `script src` ile çağır. `main.js` içinde `console.log("Serhat, İstanbul")` olsun. Sayfayı aç, konsolda cümleyi gör.

---

[İçindekiler](../README.md) · [Sonraki gün →](../02-data-types/ders.md)
