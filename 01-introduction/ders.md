# 1. Gün — Giriş

Bu bölümde JavaScript’in çalıştırıldığı yerler, ilk çıktı, yorum satırı, aritmetik, sayfaya kod ekleme ve değişken tanıtılır. Dilin tarihini ezberlemek gerekmez. Konsolu açmak, bir satır çalıştırmak ve değişkene bir değer bağlamak yeterlidir.

## JavaScript nerede kullanılır

Düğme, form, animasyon ve tarayıcıda saklanan notlar bu dille yazılır. Masaüstü uygulamalar, mobil uygulamalar ve basit oyunlar da aynı dile dayanır. Rehberde önce tarayıcıdaki JavaScript ele alınır. Bu temel oturunca dilin diğer ortamlardaki kullanımı aynı kurallara bağlanır.

Önceden program bilmene gerek yok. Motivasyon, bir bilgisayar, internet, bir tarayıcı ve bir editör yetiyor.

## Kod nerede çalıştırılır

**Chrome konsolu.** Sağ üstteki üç noktadan *Diğer araçlar → Geliştirici araçları* seçilir ya da `F12` kullanılır. Konsol sekmesine Mac’te `Command + Option + J`, Windows ve Linux’ta `Ctrl + Shift + J` ile de geçilir. Kısa denemeler buraya yazılır. Enter ile kod hemen çalışır.

**Dosya.** Asıl çalışma ayrı bir dosyada yapılır. Bir klasör açılır, içine `index.html` ve `main.js` konur. Editör olarak Visual Studio Code yeterlidir. Live Server eklentisi kayıt sırasında sayfayı yeniler; zorunlu değildir. Dosyayı tarayıcıya sürüklemek de aynı işi görür.

Node.js bu aşamada zorunlu değildir. İleride komut satırından `node dosya.js` çalıştırmak gerekirse [nodejs.org](https://nodejs.org) üzerinden LTS sürümü indirilir. Kurulumu doğrulamak için terminalde `node -v` yazılır. Bir sürüm numarası görünüyorsa kurulum tamamdır.

## İlk çıktı

Konsola şu satır yazılır:

```js
console.log("Serhat, İzmir")
```

`console.log`, parantezin içindeki değeri konsola yazar. Bu çıktı sayfada görünmez. Hata ayıklarken ve ara değerleri izlerken kullanılır.

Birden fazla değer virgülle yan yana verilebilir:

```js
console.log("fincan", 2, true)
```

## Yorum ve sözdizimi

Motorun okumaması gereken satır `//` ile kapatılır. Birkaç satır için `/* ... */` kullanılır.

```js
// bu satır çalışmaz
console.log("bu çalışır")
```

JavaScript yazım kurallarına sıkı uyar. Parantez kapanmazsa veya tırnak unutulursa konsol kırmızı bir ileti basar. İleti satır numarasını gösterir. İlk bakılacak yer orasıdır.

Büyük küçük harf ayrıdır. `console` ile `Console` aynı şey değil.

## Aritmetik

Konsol hesap için de kullanılır. `+ - * / %` temel işlemlerdir. `%` bölümden kalanı verir. `**` üs alır.

```js
console.log(17 + 4)
console.log(17 % 4)
console.log(2 ** 5)
```

## Sayfaya JavaScript koymak

Üç yol vardır. Günlük işte üçüncüsü kullanılır. İlk ikisi, başka projelerde karşılaşıldığı için burada da yer alır.

**Satır içi.** Kod, etiketin üzerine yazılır. Kısa örnek dışında dağınık durur ve uzamaz.

```html
<button onclick="console.log('tıkladın')">Bak</button>
```

**Sayfanın içinde.** `script` etiketi `body` kapanmadan hemen önce durur. Önce HTML çizilir, sonra kod çalışır.

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="UTF-8" />
    <title>Gün 1</title>
  </head>
  <body>
    <h1>Mutfak</h1>
    <script>
      console.log("sayfa içinden")
    </script>
  </body>
</html>
```

**Dış dosya.** Tercih edilen yöntem budur. HTML sade kalır, kod ayrı dosyada durur.

```html
<script src="main.js"></script>
```

Birden fazla dosya eklenirse yukarıdan aşağı çalışırlar. `menu.js` içinde tanımlanan bir isim, ondan sonra gelen `main.js` içinde görünür. Sıra ters çevrilirse “tanımsız” hatası oluşur.

## Verinin kabaca türleri

Bu bölümde yalnızca adları geçer. Ayrıntı sonraki derstedir.

- Sayı: `4`, `3.5`
- Metin: `"çay"`, `'çay'`
- Mantıksal: `true`, `false`
- Tanımsız: `undefined` — henüz değer verilmemiş
- Boş: `null` — bilerek boş bırakılmış

Türünü sormak için `typeof` kullan:

```js
console.log(typeof 4)
console.log(typeof "çay")
console.log(typeof true)
console.log(typeof undefined)
```

`typeof null` sonucu `"object"` olur. Bu, dilin eski bir tutarsızlığıdır. `null` nesne değildir; bilinçli olarak boş bırakılmış bir değerdir. Aynı not bir sonraki derste de geçerlidir.

## Değişken

Değişken, bir değere verilen addır.

```js
let fincan = 2
const kaynama = 100
```

`let` sonradan değişebilir. `const` yeniden atanamaz. İçindeki nesneyi veya diziyi değiştirmek ayrı bir konudur; 5. ve 8. günlerde ele alınır. Değişmeyecek değer `const`, değişecek değer `let` ile yazılır. `var` eski sözdizimidir. Yeni kodda kullanılmaz. Eski dosyalarda `let` gibi okunur; kapsamı daha gevşektir.

Ad, taşıdığı işi söyler. `x` yerine `biletSayisi` yazılır. İlk karakter harf, `_` veya `$` olabilir. Rakamla başlanamaz. Araya boşluk konmaz; kelimeler `biletSayisi` gibi birleştirilir.

```js
let fincan = 2
fincan = fincan + 1
console.log(fincan)
```

## Egzersizler

1. Konsola `Serhat`, `İzmir` ve bir sayısal yaş değerini üç ayrı `console.log` ile yazın.
2. `//` ile bir satırı kapatın, sayfayı yenileyin ve o satırın çalışmadığını görün.
3. `18 * 4` ve `18 % 4` sonuçlarını konsola yazdırın.
4. `let bilet = 1` yazın, sonra `bilet` değerini 3 yapın ve tekrar yazdırın.
5. `const sehir = "Van"` satırından sonra `sehir = "Trabzon"` deneyin. Konsolun iletisini okuyun.
6. `typeof` ile bir sayı, bir metin ve `true` değerinin türünü yazdırın.
7. Boş bir `index.html` ve `main.js` oluşturun. HTML’den dosyayı çağırın, `main.js` içindeki bir cümleyi konsola yazdırın.

---

[İçindekiler](../README.md) · [Sonraki gün →](../02-data-types/ders.md)
