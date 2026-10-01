# 21. Gün — DOM: bulmak ve şekillendirmek

Şimdiye kadar sonuç konsoldaydı. Bundan sonra sonuç sayfada. DOM, tarayıcının HTML’den kurduğu ağaçtır. Her etiket bir düğüm. JavaScript o ağaca uzanır, metni değiştirir, sınıf ekler, rengi oynatır.

Kod, HTML çizildikten sonra çalışsın. `script` etiketini `body` sonunda tut, ya da `defer` ile başa koy. Başta düz `script` yazarsan ağaç daha yokken ararsın, `null` alırsın.

## Bulmak

```html
<main id="sahne">
  <p class="not">ilk not</p>
  <p class="not">ikinci not</p>
  <button data-islem="sil">sil</button>
</main>
<script src="main.js"></script>
```

```js
const sahne = document.getElementById("sahne")
const ilkNot = document.querySelector(".not")
const notlar = document.querySelectorAll(".not")
const sil = document.querySelector("[data-islem='sil']")
```

`getElementById` tek düğüm veya `null`. `querySelector` CSS seçicisiyle ilkini verir, yoksa `null`. `querySelectorAll` durağan bir liste verir, diziye benzetmek için `[...notlar]` yaparım. Liste boş olabilir, `null` olmaz.

Eski API’ler de durur: `getElementsByClassName`, `getElementsByTagName`. Canlı liste döndürürler, DOM değişince kendileri de değişir. Yeni kodda `querySelector` ailesi kullanılır.

`null` üstünden `.textContent` okursan `TypeError`. Seçicinin tuttuğundan emin ol, ya da bir kez kontrol et.

## Metin ve HTML

```js
ilkNot.textContent = "yeniden yazıldı"
```

`textContent` metindir, etiketi yazı olarak gösterir. `innerHTML` etiketi gerçekten basar. Dışarıdan gelen metin `innerHTML` içine konmaz; etiket enjekte edilebilir. Kullanıcı metninde `textContent` kullanılır.

```js
ilkNot.innerHTML = "<strong>kalın</strong>"
```

Girdi kutusunun değeri ayrıdır: `input.value`.

## Öznitelik ve veri

```js
const dugme = document.querySelector("button")
dugme.setAttribute("disabled", "")
console.log(dugme.getAttribute("data-islem"))
dugme.dataset.islem = "arsiv"
```

`data-islem` HTML’de, `dataset.islem` JavaScript’te. Tire, camelCase’e döner: `data-kullanici-id` → `dataset.kullaniciId`.

Sınıf için `className` tüm listeyi ezer. Parça parça oynamak için `classList`:

```js
ilkNot.classList.add("soluk")
ilkNot.classList.remove("soluk")
ilkNot.classList.toggle("soluk")
console.log(ilkNot.classList.contains("soluk"))
```

## Biçim

Doğrudan `style` acil iştir. Kalıcı görünümü CSS sınıfında tut, kod yalnız sınıfı eklesin. Yine de acil yol şu:

```js
sahne.style.backgroundColor = "#f4efe6"
sahne.style.padding = "16px"
```

CSS’te `background-color`, JavaScript’te `backgroundColor` yazılır. Birden fazla özellik basılacaksa `cssText` kullanılabilir ama var olan satır içi biçimi siler. Kalıcı görünüm için sınıf tercih edilir.

```css
.soluk {
  opacity: 0.4;
}
```

## Egzersizler

Basit bir HTML kur: bir başlık, üç paragraf, bir düğme.

1. Başlığı `querySelector` ile bul, metnini değiştir.
2. Üç paragrafı `querySelectorAll` ile al, `forEach` ile sonuna sıra numarası ekle.
3. Düğmeye `classList` ile `hazir` sınıfı ekle. CSS’te o sınıf yazı rengini değiştirsin.
4. Düğmenin `data-rol` değerini oku, konsola yaz, sonra başka bir değerle değiştir.
5. Olmayan bir seçicide `null` aldığını gör. Üstünden metin okumayı `if` ile koru.
6. Bir paragrafa `innerHTML` ile kalın etiket bas. Aynı yere `textContent` ile `<b>deneme</b>` bas, etiketin yazıya döndüğünü gör.

---

[← Önceki gün](../20-clean-code/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../22-dom-manipulation/ders.md)
