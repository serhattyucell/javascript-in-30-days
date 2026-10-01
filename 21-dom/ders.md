# 21. Gün — DOM: bulmak ve şekillendirmek

Şimdiye kadar sonuç konsoldaydı. Bundan sonra sonuç sayfadadır. DOM, tarayıcının HTML’den kurduğu ağaçtır. Her etiket bir düğümdür. JavaScript o ağaca uzanır, metni değiştirir, sınıf ekler, rengi oynatır.

Kod, HTML çizildikten sonra çalışır. `script` etiketi `body` sonunda durur. Başta durursa ağaç daha yokken aranır, sonuç `null` olur. `null` üstünden `.textContent` okumak `TypeError` verir.

Aşağıyı `index.html` diye kaydet. Aynı klasöre `main.js` koy. Dosyayı Chrome’da aç, `F12` ile konsola bak.

```html
<!DOCTYPE html>
<html lang="tr">
  <head>
    <meta charset="UTF-8" />
    <title>Gün 21</title>
  </head>
  <body>
    <main id="sahne">
      <h1 id="baslik">Durak</h1>
      <p class="not">İzmir</p>
      <p class="not">Van</p>
      <p class="not">Trabzon</p>
      <button type="button" data-islem="sil">sil</button>
    </main>
    <script src="main.js"></script>
  </body>
</html>
```

## Bulmak

```js
const sahne = document.getElementById("sahne")
const baslik = document.querySelector("#baslik")
const ilkNot = document.querySelector(".not")
const notlar = document.querySelectorAll(".not")
const sil = document.querySelector("[data-islem='sil']")

console.log(baslik.textContent)
console.log(notlar.length)
console.log(ilkNot.textContent)
```

```text
Durak
3
İzmir
```

`getElementById` tek düğüm verir. Yoksa `null`. `querySelector` CSS seçicisiyle ilkini verir. `#baslik` id, `.not` sınıftır. `querySelectorAll` durağan bir liste verir. Üç paragraf vardır, `length` 3 olur. Liste dizi değildir. Dizi metodu istenirse `[...notlar]` yapılır. Liste boş olabilir, `null` olmaz. Boş listenin uzunluğu `0`dır.

Eski API’ler de durur: `getElementsByClassName`, `getElementsByTagName`. Canlı listedir, DOM değişince kendileri de değişir. Yeni kodda `querySelector` kullanılır.

## Metni değiştirmek

```js
baslik.textContent = "Serhat, İstanbul"
ilkNot.textContent = "yeniden yazıldı"
```

Sayfada başlık ve ilk paragraf değişir. `textContent` düz metindir. İçine `<b>` yazılırsa etiket olarak değil, yazı olarak görünür.

`innerHTML` etiketi gerçekten basar. Dışarıdan gelen metin oraya konmaz. Biri etiket enjekte edebilir. Kullanıcı metninde `textContent` kullanılır.

```js
ilkNot.innerHTML = "<strong>İzmir</strong>"
```

İlk paragraf kalın görünür. Aynı yere `textContent = "<strong>İzmir</strong>"` yazılırsa kalın olmaz, etiketler ekranda yazı olarak durur. İkisini de dene.

Girdi kutusunun yazısı ayrıdır. `input.value` okunur. `textContent` kutu için boş kalabilir.

## Öznitelik, veri, sınıf

```js
const dugme = document.querySelector("button")
console.log(dugme.getAttribute("data-islem"))
dugme.dataset.islem = "arsiv"
console.log(dugme.dataset.islem)
```

```text
sil
arsiv
```

HTML’de `data-islem`, JavaScript’te `dataset.islem` olur. Tire, camelCase’e döner. `data-kullanici-id` , `dataset.kullaniciId` olur.

`dugme.setAttribute("disabled", "")` düğmeyi kilitler. Tıklanmaz.

Sınıfın tamamını `className` ezer. Parça parça oynamak için `classList` vardır.

```js
ilkNot.classList.add("soluk")
console.log(ilkNot.classList.contains("soluk"))
ilkNot.classList.toggle("soluk")
```

`toggle` varsa çıkarır, yoksa ekler. `contains` evet/hayır döndürür.

`style` satırında bir sınıf tanımla. Kod yalnız sınıfı eklesin.

```css
.soluk {
  opacity: 0.4;
}
```

Bu kuralı `head` içindeki `style` etiketine koy. `soluk` eklenince paragraf solar. Kural yoksa sınıf eklenir ama gözle bir şey değişmez. İkisi birlikte gerekir.

## Doğrudan renk

Acil deneme için `style` kullanılır. Kalıcı görünüm CSS sınıfında durur.

```js
sahne.style.backgroundColor = "#f4efe6"
sahne.style.padding = "16px"
```

CSS’te `background-color`, JavaScript’te `backgroundColor` yazılır. Tire düşer, sonraki harf büyür. `cssText` birçok özelliği birden basar ama var olan satır içi biçimi siler.

## Egzersizler

Hepsi gerçek sayfada olsun. Konsola yazmak yetmez. Gözle değişimi gör.

1. Başlığı `querySelector("#baslik")` ile bul. Metnini `Serhat, Van` yap.
2. Üç paragrafı `querySelectorAll(".not")` ile al. `forEach` ile sonuna sıra numarası ekle. Ekranda `İzmir 0`, `Van 1`, `Trabzon 2` görünsün. Numara indekstir, 0’dan başlar.
3. Düğmeye `classList.add("hazir")` ekle. CSS’te `.hazir { color: #9a3412; }` yaz. Yazı rengi değişsin. `remove` ile rengin geri geldiğini gör.
4. Düğmenin `data-islem` değerini oku, konsola yaz. Sonra `dataset` ile `goster` yap. HTML’de özniteliğin değiştiğini Öğeler sekmesinden gör.
5. `querySelector("#yok")` dene. `null` olduğunu yazdır. Üstünden `textContent` okumayı `if (dugum)` ile koru. Korumazsan `TypeError` gelir. İkisini de gör.
6. Bir paragrafa `innerHTML` ile `<strong>Trabzon</strong>` bas, kalın olsun. Aynı paragrafa `textContent` ile aynı etiketi bas, kalınlığın gittiğini gör.

---

[← Önceki gün](../20-clean-code/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../22-dom-manipulation/ders.md)
