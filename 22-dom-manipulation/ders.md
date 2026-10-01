# 22. Gün — DOM: üretmek ve silmek

21. günde var olan yazı değişti. Bu gün ağaçta düğüm üretilir ve silinir. Liste, kart ve ızgara bu yolla kurulur. HTML’de boş bir `ul` durur. Şehirler JavaScript’ten gelir.

```html
<button id="ekle" type="button">ekle</button>
<ul id="liste"></ul>
<script src="main.js"></script>
```

## Üretmek

`createElement` düğümü bellekte kurar. Sayfada henüz görünmez. Bir ebeveyne takılınca görünür.

```js
const madde = document.createElement("li")
madde.textContent = "İzmir"
madde.classList.add("sehir")
document.querySelector("#liste").append(madde)
```

Sayfada bir madde belirir: İzmir.

`append` sona koyar, metin de kabul eder. `prepend` başa koyar. `appendChild` daha eski olanıdır, yalnız düğüm alır.

Çok düğme tek tek `append` edilirse tarayıcı her seferinde sayfayı yeniden ölçer. Yüz kartta `DocumentFragment` kullanılır. Parça bellekte birikir, sayfaya bir kez takılır.

```js
const liste = document.querySelector("#liste")
const parca = document.createDocumentFragment()
;["Van", "İstanbul", "Trabzon"].forEach((ad) => {
  const li = document.createElement("li")
  li.textContent = ad
  parca.append(li)
})
liste.append(parca)
```

Ekranda üç şehir daha görünür. Önceki İzmir duruyorsa dört olur. Temiz deneme için sayfayı yenile, parçayı tek başına çalıştır.

## Silmek

```js
const ilk = liste.querySelector("li")
ilk.remove()
```

İlk madde kaybolur. `null.remove` patlar. Seçici tutmamışsa önce `if (ilk)` bak.

Listenin içini boşaltmak:

```js
liste.replaceChildren()
```

Eski tarayıcılarda `liste.innerHTML = ""` de boşaltır. `replaceChildren` niyeti daha açık gösterir.

## Tıklayınca satır eklemek

Olayın ayrıntısı 23. gündedir. Bu örnekte yalnız `click` yeter. Sayacı dışarıda tut. Her tıklama bir artırır.

```js
const ekle = document.querySelector("#ekle")
const liste2 = document.querySelector("#liste")
let sira = 1

ekle.addEventListener("click", () => {
  const li = document.createElement("li")
  li.textContent = "satır " + sira
  sira += 1
  liste2.append(li)
})
```

Düğmeye üç kez bas. `satır 1`, `satır 2`, `satır 3` alt alta durur. `sira` fonksiyonun içinde `let` ile kurulsaydı her tıklamada 1’e dönerdi. Dışarıda durduğu için hatırlar. Bu, 19. gündeki closure’dur.

## Egzersizler

Üçü de ayrı `index.html` sayfası olsun. Konsolda çalıştırmak yetmez.

### Sayı ızgarası

0’dan 99’a kadar kutular üret, bir ızgaraya diz.

```css
.izgara {
  display: grid;
  grid-template-columns: repeat(10, 2.5rem);
  gap: 4px;
}
.kutu {
  text-align: center;
  padding: 0.25rem;
}
.cift { background: #86efac; }
.tek { background: #fde68a; }
.asal { background: #fca5a5; }
```

- Çift sayıya `cift` sınıfı. Zemin yeşil.
- Tek sayıya `tek`. Zemin sarı.
- Asal sayıya `asal`. Zemin kırmızı. Çift ve tek kuralının üstüne yazılır, çünkü asal sınıfı en son eklenir.

Asallık fonksiyonu 6. gündeki mantıktır. 0 ve 1 asal değildir. 2 asaldır. Rengi `style.background` ile tek tek gömme. Üç sınıf yeter. Kutunun metni sayının kendisidir.

### Şehir tahtası

```js
const urunler = [
  { ad: "İzmir", tur: "kıyı" },
  { ad: "Van", tur: "doğu" },
  { ad: "İstanbul", tur: "kıyı" },
  { ad: "Trabzon", tur: "kıyı" },
]
```

Her kayıt bir kart olsun. Türü küçük bir etiket olsun. Kartlar `grid-template-columns: repeat(auto-fill, minmax(10rem, 1fr))` ile dizilsin. Sayfa daralınca alta kaysın. Dört kartı HTML’e elle yazma. Döngü kursun.

### Açılır notlar

Veri JavaScript’te dursun.

```js
const notlar = [
  { baslik: "İzmir", metin: "Kıyı, ilk durak." },
  { baslik: "Van", metin: "Doğu, ikinci durak." },
  { baslik: "Trabzon", metin: "Kıyı, son durak." },
]
```

Her kayıt için `details` ve içinde `summary` üret. `summary` başlık, geri kalan metin olsun. Biri açıkken ötekiler kapanmak zorunda değildir. Bir düğme bütün kartları `replaceChildren` ile silsin. Silince sayfada not kalmasın.

---

[← Önceki gün](../21-dom/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../23-events/ders.md)
