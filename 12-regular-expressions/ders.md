# 12. Gün — Düzenli ifadeler

Düzenli ifade, metnin içini bir kalıpla tarar. “@ geçiyor mu”, “baştan sona rakam mı”, “bu kelimeyi değiştir” soruları buna girer. JavaScript’te bu işi `RegExp` görür. Kalıp, küçük bir dildir. Bu bölümde günlük kullanıma yeten kısmı ele alınır.

## İki yazım

Eğik çizgi en kısası. Sondaki harfler bayrak.

```js
const kalip = /cay/i
console.log(kalip.test("Bir Çay lütfen"))
```

Kurucu, kalıp değişkenden geliyorsa lazım. Metin olduğu için ters bölüleri iki kez kaçırırsın.

```js
const kelime = "ayva"
const dinamik = new RegExp(kelime, "i")
console.log(dinamik.test("Ayva kompostosu"))
```

Bayraklar:

- `g` — ilkiyle yetinme, hepsini ara
- `i` — büyük küçük harf umursama
- `m` — `^` ve `$` her satırda çalışsın

## test, match, search, replace

```js
const cumle = "raf 12, kutu 4"
console.log(/\d+/.test(cumle))
console.log(cumle.match(/\d+/g))
console.log(cumle.search(/\d+/))
console.log(cumle.replace(/\d+/g, "#"))
```

`test` doğru ya da yanlış. `match` yakalananları dizi yapar, `g` yoksa fazladan bilgiyle tek sonuç döner. `search` ilk indeks, yoksa `-1`. `replace` yenisini verir, aslı durur.

## Sık işaretler

| İşaret | Anlamı |
| --- | --- |
| `.` | yeni satır hariç bir karakter |
| `\d` | rakam |
| `\D` | rakam olmayan |
| `\w` | harf, rakam, alt çizgi |
| `\s` | boşluk |
| `+` | bir veya daha fazla |
| `*` | sıfır veya daha fazla |
| `?` | sıfır veya bir |
| `{2,4}` | en az 2, en çok 4 |
| `^` | baş |
| `$` | son |
| `[]` | bu karakterlerden biri |
| `[^]` | bunlar hariç |
| `()` | grup, yakala |
| `\|` | ya bu ya o |

Köşeli parantez içinde `^` “hariç” demektir. Dışarıda “satır başı” demektir. Yerine göre oku.

```js
console.log(/^[0-9]{2}$/.test("34"))
console.log(/^[0-9]{2}$/.test("345"))
console.log(/indirim|hediye/.test("bugün hediye var"))
```

Nokta her karaktere uyar. Gerçek nokta istiyorsan kaçır: `\.`

```js
console.log(/uc\.nl/.test("uc.nl"))
console.log(/uc.nl/.test("ucXnl"))
```

## Grup

Parantez, yakalanan parçayı saklar. `match` sonucu ve `replace` içindeki `$1`, `$2` oradan beslenir.

```js
const kod = "TR-3401"
const parca = kod.match(/^([A-Z]{2})-(\d{4})$/)
console.log(parca[1], parca[2])
console.log(kod.replace(/^([A-Z]{2})-(\d{4})$/, "$2 / $1"))
```

## Açgözlülük

`+` ve `*` olabildiğince uzun yer. En kısa yer için sonlarına `?` ekle: `+?`, `*?`. HTML veya iç içe tırnakta buna ihtiyaç duyarsın. Basit doğrulamada şart değil.

## Ölçü

E-posta, telefon ve “yalnızca rakam” gibi işlerde hazır kalıp kör kopyalanmaz. Önce izin verilen biçim yazılır, sonra kalıba dökülür. Kalıp her geçerli adresi yakalamak zorunda değildir. Formun kendi kuralını yakalaması yeter. 30. günde bir form bu yolla denetlenir.

Türkçe harfler `\w` içine girmez. `ıİğüşöç` için harf açık yazılır ya da `/.../u` bayrağıyla `\p{L}` denenir. Basit ad kontrolünde aralık `[a-zçğıöşü]` ve `i` bayrağı ile açılır. `i` ile `İ` her motorda aynı sonucu vermeyebilir. Şüpheli yerde metin önce `toLocaleLowerCase("tr-TR")` ile indirilir, sonra küçük harf kalıbı kullanılır.

## Egzersizler

1. Bir cümlenin içinde `kedi` geçiyor mu, büyük küçük umursamadan bak.
2. `"siparis no 4481"` içindeki sayıyı `match` ile çek.
3. Dizideki bütün sayıları `#` ile değiştir.
4. Tam iki harf, tire, tam dört rakam kuralını `^` ve `$` ile yaz. `"ab-1234"` geçsin, `"ab-12345"` kalmasın.
5. `"12.5 kg"` ifadesinden sayıyı ve birimi iki grupla ayır.
6. Boşlukları `\s+` ile tek boşluğa indir: `"a   b\tc"`.
7. `new RegExp` ile kullanıcıdan gelen bir kelimeyi ara. Kelimenin kendisinde nokta varsa onu `\.` yapman gerektiğini dene.

---

[← Önceki gün](../11-destructuring-and-spread/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../13-console-methods/ders.md)
