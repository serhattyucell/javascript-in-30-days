# 7. Gün — Fonksiyonlar

Aynı hesabı üç yerde kopyalamak, biri değişince üçünü de aramaktır. Fonksiyon, adı olan bir iş paketidir. Bir kez yazılır, adıyla çağrılır. İçeri giren değere parametre, dışarı çıkan değere dönüş denir.

## Bildirim

```js
function selam(kisi, sehir) {
  return `${kisi}, ${sehir}`
}

console.log(selam("Serhat", "Trabzon"))
```

```text
Serhat, Trabzon
```

`function` anahtarı, `selam` adı, parantezdeki iki parametre ve süslü gövde tanımdır. Tanım kendi başına çalışmaz. `selam("Serhat", "Trabzon")` çağrıdır. `"Serhat"` , `kisi`nin yerine geçer. `"Trabzon"` , `sehir`in yerine geçer. Sıra önemlidir. Ters yazılırsa şehir adın yerine geçer.

`return` sonucu dışarı bırakır. Ondan sonraki satır çalışmaz. `return` yoksa fonksiyon `undefined` bırakır.

```js
function sus() {
  console.log("içeriden")
}

console.log(sus())
```

```text
içeriden
undefined
```

İleti basıldı ama fonksiyon bir değer döndürmedi. `console.log`un içindeki ikinci satır o yüzden `undefined`dir. Ekrana basmak ile değer döndürmek ayrı iştir. Hesap yapan fonksiyon bassın diye değil, sonucu geri versin diye yazılır. Basma işini çağıran taraf yapar.

## Değişkene bağlamak

Fonksiyon bir değişkene de konur. Bu biçimde, satırın üstünden çağrılamaz. Klasik `function selam` bildirimi dosyada yukarı taşınır, tanımdan önce de çağrılabilir. Yeni kodda aşağıdaki biçim tercih edilir. Ne zaman kurulduğu dosyada görülen sıradır.

```js
const kare = function (n) {
  return n * n
}

console.log(kare(6))
```

```text
36
```

## Parametre ve varsayılan

Eksik argüman `undefined` gelir. Fazlası yok sayılır.

```js
function indir(fiyat, oran) {
  return fiyat - fiyat * oran
}

console.log(indir(200, 0.1))
```

```text
180
```

200’ün yüzde 10’u 20’dir. 200’den 20 düşünce 180 kalır.

Argüman unutulursa varsayılan devreye girer.

```js
function yer(kisi = "Serhat", sehir = "İzmir") {
  return `${kisi}, ${sehir}`
}

console.log(yer())
console.log(yer("Serhat", "Van"))
```

```text
Serhat, İzmir
Serhat, Van
```

## Kaç tane geleceği bilinmiyorsa

Üç nokta, gelenlerin hepsini bir listeye toplar. Buna rest denir. Son parametre olmak zorundadır.

```js
function toplam(...sayilar) {
  let sonuc = 0
  for (const n of sayilar) {
    sonuc += n
  }
  return sonuc
}

console.log(toplam(4, 5, 6, 7))
console.log(toplam())
```

```text
22
0
```

Hiç argüman gelmezse liste boştur, döngü dönmez, `sonuc` 0 kalır.

Eskiden `arguments` adlı gizli bir liste vardı. Ok fonksiyonunda o yoktur. Yeni kodda `...` kullanılır.

## Ok fonksiyonu

Aynı işin kısa yazılışıdır. Tek ifadede `return` ve süslü parantez düşer.

```js
const ikiKat = (n) => n * 2
console.log(ikiKat(8))
```

```text
16
```

Gövde bir satırdan uzunsa süslü parantez ve `return` geri gelir.

```js
const bol = (a, b) => {
  if (b === 0) {
    return "bölünmez"
  }
  return a / b
}

console.log(bol(10, 2))
console.log(bol(10, 0))
```

```text
5
bölünmez
```

Tek parametrede parantez de düşebilir: `n => n * 2`. Okunaklılık için parantez durabilir. Ok fonksiyonu ile klasik fonksiyon `this` bağında ayrılır. Ayrım 8. ve 15. günde görünür. Kısa hesapta ok, nesnenin kendi metodunda klasik fonksiyon yazılır.

## Kendi kendine bir kez çalışan

Tanımlandığı anda bir kez çalışır. Adı yoktur. Eski kodda kapsam kirletmemek için kullanılırdı. Sık gerekmez. Biçimi görmek yeter.

```js
;(function () {
  const gizli = 7
  console.log(gizli)
})()
```

```text
7
```

Sondaki `()` çağrıdır. Olmazsa fonksiyon hiç çalışmaz, yalnızca kurulur.

## Başka fonksiyona vermek

Fonksiyon da bir değerdir. Başka fonksiyona argüman olabilir. Verilen fonksiyona geri çağırma denir. 9. gün tamamı budur.

```js
function calistir(is) {
  is()
}

calistir(() => console.log("Serhat"))
```

```text
Serhat
```

`calistir` işin ne olduğunu bilmez. Kendisine verilen fonksiyonu çağırır.

Fonksiyon tek iş yapar. Adı fiildir: `hesaplaIndirim`, `yazSehir`. Hem hesaplayıp hem konsola basan fonksiyon ikiye bölünür.

## Egzersizler

1. `kare(n)` yaz. `kare(5)` sonucu `25` olsun. Fonksiyon konsola basmasın, `return` etsin. Basma işini dışarıdaki `console.log` yapsın.
2. `birlestir(a, b)` iki metni arada boşlukla birleştirsin. `b` gelmezse yalnız `a` dönsün. `birlestir("Serhat", "İstanbul")` ve `birlestir("Serhat")` dene.
3. `ortalama(...sayilar)` yaz. Toplamı uzunluğa böl. Liste boşsa `0` dönsün, sıfıra bölme olmasın.
4. Aynı ortalamayı ok fonksiyonuyla yaz.
5. Bir listedeki en büyük sayıyı döndüren fonksiyon yaz. Döngü kullan. İkinci çözüm `Math.max(...liste)` olsun. `[3, 11, 7]` ile ikisini de dene, ikisi de `11` vermeli.
6. `uygula(kisi, is)` yaz. `is` bir fonksiyon olsun ve `kisi` ile çağrılsın. `uygula("Serhat", (ad) => console.log(ad + ", Van"))` dene.
7. `kdvEkle(fiyat, oran = 0.2)` yaz. `kdvEkle(100)` sonucu `120` olsun. `kdvEkle(100, 0.1)` sonucu `110` olsun.
8. `return` koymadan bir fonksiyon çağır, sonucu `console.log`a ver. `undefined` gör.

---

[← Önceki gün](../06-loops/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../08-objects/ders.md)
