# 22. Gün — DOM: üretmek ve silmek

Bir önceki günde var olan öğe değiştirildi. Bu bölümde ağaca düğüm eklenir ve çıkarılır. Liste, kart ve ızgara bu yolla kurulur.

## Üretmek

```js
const madde = document.createElement("li")
madde.textContent = "un"
madde.classList.add("urun")
```

Bu düğüm henüz sayfada değil. Bellekte durur. Bir ebeveyne takınca görünür.

## Takmak

```js
const liste = document.querySelector("#liste")
liste.append(madde)
```

`append` sona koyar, metin de kabul eder. `prepend` başa koyar. `appendChild` daha eski olanıdır, yalnız düğüm alır. `insertAdjacentHTML` bir konuma HTML metni basar: `"beforeend"`, `"afterbegin"` ve benzeri. Dışarıdan gelen metinde bu yol kullanılmaz.

Çok düğmeyi tek seferde kurup bir kez takmak daha ucuz. Ara ara `append` etmek, her seferinde sayfayı yeniden ölçtürür. Yüzlerce kart basacaksan `DocumentFragment` kullan:

```js
const parca = document.createDocumentFragment()
;["un", "tuz", "yağ"].forEach((ad) => {
  const li = document.createElement("li")
  li.textContent = ad
  parca.append(li)
})
liste.append(parca)
```

## Çıkarmak

```js
madde.remove()
```

Ebeveynden `removeChild` da olur. Çocuk yoksa `remove` sessiz ve düzgündür, düğümün kendi üstünden çağırırsın. Olmayan bir seçicide önce `null` kontrolü yap, çünkü `null.remove` patlar.

İçini boşaltmak:

```js
liste.replaceChildren()
```

Eski tarayıcılarda `liste.innerHTML = ""` de boşaltır. `replaceChildren` niyeti daha açık gösterir.

## Küçük bir örnek

Bir kutu ve bir düğme yeter. Düğmeye basılınca kutuya yeni bir satır düşer. Olayın ayrıntısı sonraki gündedir. Bu örnekte yalnız `click` vardır.

```html
<button id="ekle" type="button">ekle</button>
<ul id="liste"></ul>
```

```js
const ekle = document.querySelector("#ekle")
const liste = document.querySelector("#liste")
let sira = 1

ekle.addEventListener("click", () => {
  const li = document.createElement("li")
  li.textContent = `satır ${sira}`
  sira += 1
  liste.append(li)
})
```

## Egzersizler: üç küçük sayfa

Konsol bitti. Bunları gerçek dosyada kur. Görünümü sade tut, asıl ders ağaç.

### Sayı ızgarası

0’dan 99’a kadar kutular üret, bir ızgaraya diz. CSS grid işini görür.

- çift sayıların zemini yeşil
- tek sayıların zemini sarı
- asal olanların zemini kırmızı, çift-tek kuralının üstüne yazılsın

Asallık fonksiyonunu 6. gündeki mantıkla yaz. 0 ve 1 asal değil. Kutuyu üretirken sınıfı ona göre ver. Rengi JavaScript ile tek tek `style`’a gömmek yerine üç sınıf yaz.

### Ürün tahtası

Elinde şu dizi olsun (kopyala, isterken değiştir):

```js
const urunler = [
  { ad: "un", tur: "kuru" },
  { ad: "süt", tur: "soğuk" },
  { ad: "elma", tur: "taze" },
  { ad: "pirinç", tur: "kuru" },
]
```

Her ürün bir kart olsun. Türüne göre küçük bir etiket bas. Kartlar akışkan bir ızgarada dursun, sayfa daralınca alta kaysın.

### Açılır notlar

Üç başlık ve her birinin altında bir paragraf tanımla, veri JavaScript’te dursun. Ekranda `details` ve `summary` ile üret. Biri açıkken ötekiler kapanmak zorunda değil. Veriyi HTML’e elle yazma; döngü kursun.

```js
const notlar = [
  { baslik: "saklama", metin: "Kuru ürün üst rafta dursun." },
  { baslik: "serin", metin: "Süt dolaba, elmeyi dağınık bırakma." },
  { baslik: "süre", metin: "Pirinç ayakta, unu ağzı kapalı kutuda beklet." },
]
```

Bitince bir düğme ekle: bütün kartları `replaceChildren` ile silsin.

---

[← Önceki gün](../21-dom/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../23-events/ders.md)
