# 23. Gün — Olaylar

Sayfa dururken bir işin başlamasını olay dinleyicisi sağlar. Tıklama, yazı, tuş, fare, formun gönderilmesi buna girer. 22. günde bir `click` vardı. Bu gün dinleyici kurulur, hangi öğenin tıklandığı okunur, olayın yukarı yürümesi yönetilir.

```js
const dugme = document.querySelector("#ekle")

function bildir() {
  console.log("tık")
}

dugme.addEventListener("click", bildir)
```

Düğmeye her basışta konsola `tık` düşer. Kaldırmak için aynı fonksiyon gerekir. Anonim ok sonradan sökülemez, elde isim yoktur.

```js
dugme.removeEventListener("click", bildir)
```

HTML’deki `onclick="..."` kullanılmaz. Kod HTML’den ayrı kalır.

## Olay nesnesi

Dinleyici bir nesne alır. Ne olduğu, hangi tuş, hangi hedef oradadır.

```js
dugme.addEventListener("click", (olay) => {
  console.log(olay.type)
  console.log(olay.target)
})
```

`type` `"click"` olur. `target` olayı ilk alan düğümdür. `currentTarget` dinleyiciyi taşıyan düğümdür. İç içe etikette ikisi ayrılır. Listenin tek dinleyicisi varken çocuğa tıklanınca `target` çocuk, `currentTarget` liste olur. Olay çocukta başlar, yukarı yürür. Buna kabarcıklanma denir.

## Girdi

```html
<label>
  Şehir
  <input id="arama" type="search" />
</label>
<p id="yansima"></p>
```

```js
const arama = document.querySelector("#arama")
const yansima = document.querySelector("#yansima")

arama.addEventListener("input", () => {
  yansima.textContent = arama.value
})
```

Kutuya `Van` yazıldıkça alttaki paragraf da `Van` olur. `input` her tuşta gelir. `change` kutudan çıkınca gelir. Canlı yansıma `input` ile kurulur.

Form `submit` olunca sayfa yenilenir. Yenilenmesin deniyorsa `preventDefault` çağrılır.

```js
document.querySelector("form").addEventListener("submit", (olay) => {
  olay.preventDefault()
  console.log("form gitti sayılmadı, sayfa durdu")
})
```

`preventDefault` olmazsa konsol iletisi bir an görünür, sayfa yenilenir, konsol temizlenir. İleti kaybolursa engelleme unutulmuştur.

## Tuş ve fare

`keydown` basılınca, `keyup` bırakılınca gelir. `olay.key` insanın okuduğu tuştur: `"Enter"`, `"a"`. `olay.code` fiziksel konumdur. Türkçe klavyede ikisi ayrı olabilir.

```js
document.addEventListener("keydown", (olay) => {
  if (olay.target.matches("input, textarea")) {
    return
  }
  if (olay.key === "Escape") {
    console.log("kaçış")
  }
})
```

Odak bir kutudayken Escape sayfanın dinleyicisine de düşer. Kutunun içindeyken karışmasın deniyorsa `target` bir `input` ise erken çıkılır. Yukarıdaki `matches` bunu yapar.

Fare: `click`, `dblclick`, `mouseenter`, `mouseleave`, `mousemove`. `mousemove` çok sık gelir. Ağır iş bağlanmaz.

## Tek dinleyici, çok çocuk

Yüz kartın her birine ayrı dinleyici takılmaz. Üst kutuya bir tane takılır. `target` hangi kart olduğunu söyler. Sonradan eklenen kart da bu dinleyiciye düşer. 22. günde üretilen düğümler için bu yol daha sağlamdır.

```js
liste.addEventListener("click", (olay) => {
  const kart = olay.target.closest("li")
  if (!kart || !liste.contains(kart)) {
    return
  }
  kart.remove()
})
```

`closest("li")` tıklanan yerden yukarı, ilk `li`yi bulur. Maddeye basılınca o satır silinir. Boşluğa basılırsa `kart` yoktur, fonksiyon döner.

## Egzersizler

### Sayı kutuları

22. günün ızgarasını aç. Kutuya tıklanınca üstte tek bir satır `seçilen: 17` desin. Yüz dinleyici yok. Izgara kabına bir dinleyici, `closest` ile kutu.

Üç düğme daha koy: yalnız çiftler, yalnız tekler, yalnız asallar. Ötekilere `hidden` özniteliği ver. `hidden` olan kutu ekrandan gider. Düğme yeniden basılınca `hidden` kalksın, hepsi görünsün.

### Tuş kartı

Sayfada büyük bir alan olsun. Bir tuşa basınca o alan üç şeyi göstersin: `key`, `code`, ve basılı tutuluyorsa “tekrar”. `olay.repeat` basılı tutmayı söyler. Escape alanı temizlesin. Odak bir `input` içindeyse sayfanın dinleyicisi karışmasın. Yukarıdaki erken çıkışı kullan.

### Canlı süzgeç

```js
const sehirler = ["İzmir", "Van", "İstanbul", "Trabzon"]
```

Bir arama kutusu. Her `input` olayında listeyi `replaceChildren` ile yeniden kur. Metin, şehir adının içinde geçiyorsa kart kalsın. Karşılaştırma `toLocaleLowerCase("tr-TR")` ile olsun. `İ` ve `i` karışmasın.

Arama boşsa dördü de görünsün. Eşleşme yoksa tek bir “yok” paragrafı bas. `zz` yazınca “yok”, silince dört şehir geri gelsin.

---

[← Önceki gün](../22-dom-manipulation/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../24-planet-weight/ders.md)
