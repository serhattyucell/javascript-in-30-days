# 23. Gün — Olaylar

Sayfa dururken bir işin başlamasını olay dinleyicisi sağlar. Tıklama, yazı, tuş, fare ve formun gönderilmesi buna girer. Önceki günde bir `click` görüldü. Bu bölümde dinleyici kurulur, hedef okunur ve olayın yukarı yürümesi yönetilir.

```js
const dugme = document.querySelector("#ekle")
function bildir() {
  console.log("tık")
}
dugme.addEventListener("click", bildir)
```

Kaldırmak için aynı fonksiyon referansı lazım. Anonim ok fonksiyonunu sonra `removeEventListener` ile sökemezsin, elde isim yoktur.

```js
dugme.removeEventListener("click", bildir)
```

HTML’deki `onclick="..."` özniteliğini kullanmıyorum. Kod HTML’den ayrık kalsın.

## Olay nesnesi

Dinleyici bir nesne alır. İçinde ne oldu, hangi tuş, hangi hedef var.

```js
dugme.addEventListener("click", (olay) => {
  console.log(olay.type)
  console.log(olay.target)
})
```

`target` olayı ilk alan düğüm. `currentTarget` dinleyiciyi taşıyan düğüm. İç içe etikette ikisi ayrılır. Bir listenin tek dinleyicisi varsa çocuğun tıklanmasında `target` çocuk, `currentTarget` listedir. Buna olayın yukarı yürümesi denir.

## Girdi

```html
<input id="arama" type="search" placeholder="ürün" />
<p id="yansima"></p>
```

```js
const arama = document.querySelector("#arama")
const yansima = document.querySelector("#yansima")

arama.addEventListener("input", () => {
  yansima.textContent = arama.value
})
```

`input` her tuşta gelir. `change` kutudan çıkınca gelir. Canlı yansıma istiyorsan `input`.

Formda `submit` sayfayı yeniler. Yenilenmesin istiyorsan `preventDefault`.

```js
document.querySelector("form").addEventListener("submit", (olay) => {
  olay.preventDefault()
})
```

## Tuş ve fare

`keydown` basılınca, `keyup` bırakılınca. `olay.key` insanın okuduğu tuş (`"Enter"`, `"a"`). `olay.code` fiziksel tuş. Türkçe klavyede ikisini karıştırma: `key` karaktere, `code` konuma yakındır.

```js
document.addEventListener("keydown", (olay) => {
  if (olay.key === "Escape") {
    console.log("kaçış")
  }
})
```

Fare: `click`, `dblclick`, `mouseenter`, `mouseleave`, `mousemove`. `mousemove` çok sık gelir. Ağır iş bağlama.

## Taşma

Yüz kartın her birine ayrı dinleyici takma. Üst kutuya bir tane tak, `target` ile hangi kart olduğunu anla.

```js
liste.addEventListener("click", (olay) => {
  const kart = olay.target.closest("li")
  if (!kart || !liste.contains(kart)) return
  kart.remove()
})
```

Sonradan eklenen kartlar da bu dinleyiciye düşer. Dün ürettiğin düğümler için özellikle iyi.

## Egzersizler

### Sayı kutuları, bu kez tıklanınca

22. günün ızgarasını aç. Kutuya tıklanınca üstte tek bir satır “seçilen: 17” desin. Yüz dinleyici yok. Izgara kabına bir dinleyici, `closest` ile kutu.

Bir de üç düğme koy: yalnız çiftleri, yalnız tekleri, yalnız asalları göster. Ötekilere `hidden` özniteliği veya bir sınıf ver.

### Tuş kartı

Sayfada büyük bir alan olsun. Bir tuşa basınca o alan üç şeyi göstersin: `key`, `code`, ve basılı tutuluyorsa “tekrar” yazısı (`olay.repeat`). Escape temizlesin.

Girdi kutusunun içindeyken de sayfanın dinleyicisi çalışır. İstemiyorsan `olay.target` bir `input` ise erken çık.

### Canlı süzgeç

Bir ürün dizisi ve bir arama kutusu. Her `input` olayında listeyi `replaceChildren` ile yeniden kur. Metin, ürün adının içinde geçiyorsa kart kalsın. Büyük küçük harfi `toLocaleLowerCase("tr-TR")` ile eşitle.

Arama boşsa hepsi görünsün. Eşleşme yoksa tek bir “yok” paragrafı bas.

---

[← Önceki gün](../22-dom-manipulation/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../24-planet-weight/ders.md)
