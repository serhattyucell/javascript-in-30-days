# 12. Gün — Düzenli ifadeler

Düzenli ifade, metnin içinde bir kalıp arar. “Van geçiyor mu”, “baştan sona rakam mı”, “bu parçayı değiştir”. JavaScript’te bu işi `RegExp` görür. Kalıp küçük bir dildir. Bu gün günlük kullanıma yeten kısmı vardır. Her işareti ezberlemek gerekmez. Önce ne arandığını Türkçe yaz, sonra kalıba dök.

## İki yazılış

Eğik çizgi en kısa olanıdır. Sondaki harf bayraktır.

```js
const kalip = /van/i
console.log(kalip.test("Serhat, Van"))
```

```text
true
```

`test` yalnız evet ya da hayır döndürür. `i` bayrağı büyük küçük harfi önemsemez. `Van` ile `van` eşleşir.

Kalıp bir değişkenden geliyorsa kurucu kullanılır. Metin içinde ters bölü iki kez yazılır, çünkü birincisi JavaScript metninin kaçışıdır.

```js
const kelime = "İzmir"
const dinamik = new RegExp(kelime, "i")
console.log(dinamik.test("yol İzmir üstünden"))
```

```text
true
```

Bayraklar:

| Bayrak | Anlamı |
| --- | --- |
| `g` | ilkiyle yetinme, hepsini bul |
| `i` | büyük küçük harf önemsiz |
| `m` | `^` ve `$` her satırda geçerli olsun |

## Dört araç

```js
const cumle = "raf 12, kutu 4"
console.log(/\d+/.test(cumle))
console.log(cumle.match(/\d+/g))
console.log(cumle.search(/\d+/))
console.log(cumle.replace(/\d+/g, "#"))
```

```text
true
["12", "4"]
4
raf #, kutu #
```

- `test` evet/hayır.
- `match` bulunanları liste yapar. `g` yoksa fazladan bilgiyle tek sonuç döner.
- `search` ilk bulunanın sırasını verir. Yoksa `-1`.
- `replace` yenisini verir, asıl cümle durur.

`\d` bir rakamdır. `+` “bir veya daha fazla” demektir. `\d+` peş peşe rakamların tamamını alır. `12` iki rakamdır, tek parça olarak bulunur.

## Sık işaretler

| İşaret | Anlamı |
| --- | --- |
| `\d` | rakam |
| `\D` | rakam olmayan |
| `\s` | boşluk |
| `.` | satır sonu hariç bir karakter |
| `+` | bir veya daha fazla |
| `*` | sıfır veya daha fazla |
| `?` | sıfır veya bir |
| `{2,4}` | en az 2, en çok 4 |
| `^` | baş |
| `$` | son |
| `[0-9]` | bu aralıktan biri |
| `[^0-9]` | bu aralık hariç |
| `()` | grup, yakala |
| `\|` | ya bu ya şu |

Köşeli parantezin içindeki `^` “hariç” demektir. Dışarıdaki `^` “satır başı” demektir. Yerine göre okunur.

Nokta her karaktere uyar. Gerçek nokta için `\.` yazılır.

```js
console.log(/^[A-Z]{2}-\d{4}$/.test("TR-3401"))
console.log(/^[A-Z]{2}-\d{4}$/.test("TR-340"))
console.log(/van|izmir/.test("yol van üstü"))
```

```text
true
false
true
```

`^` ve `$` olmazsa kalıp metnin ortasında da tutar. Onlar “tamamı bu olsun” der. `TR-340` dört rakam değildir, ikinci test yanlıştır.

## Grup

Parantez, yakalanan parçayı saklar. `replace` içinde `$1` birinci grup, `$2` ikinci gruptur.

```js
const kod = "TR-3401"
const parca = kod.match(/^([A-Z]{2})-(\d{4})$/)
console.log(parca[1])
console.log(parca[2])
console.log(kod.replace(/^([A-Z]{2})-(\d{4})$/, "$2 / $1"))
```

```text
TR
3401
3401 / TR
```

`match` sonucu bir listedir. `0` bütün eşleşmedir. `1` ve sonrası gruplardır.

`+` ve `*` olabildiğince uzun yer. En kısa yer için sonlarına `?` eklenir: `+?`. Basit doğrulamada gerekmez.

Türkçe harfler `\w` içine girmez. `İ` ve `ı` bayrakla her motorda aynı davranmayabilir. Ad kontrolünde metin önce `toLocaleLowerCase("tr-TR")` ile küçültülür, sonra küçük harf kalıbı kullanılır. Hazır bir e-posta kalıbını kör kopyalamak gerekmez. Formun kendi kuralı yeter. 30. günde bir form bu yolla denetlenir.

## Egzersizler

1. `"Serhat Van’a gitti"` içinde `van` geçiyor mu, `i` bayrağıyla bak. Sonuç `true` olsun.
2. `"siparis no 4481"` içindeki sayıyı `match` ile çek. Liste `["4481"]` olsun.
3. `"oda 12, kat 4"` içindeki bütün sayıları `#` yap. `g` bayrağını unutma. Unutursan yalnız ilk sayı değişir. İkisini de dene.
4. Tam iki büyük harf, tire, tam dört rakam kuralını yaz. `"TR-1234"` geçsin, `"TR-12345"` kalmasın.
5. `"12.5 kg"` ifadesinden sayıyı ve birimi iki grupla ayır. `12.5` ve `kg` ayrı ayrı yazdırılsın.
6. `"İzmir   Van\tTrabzon"` içindeki boşlukları tek boşluğa indir. Kalıp `\s+` olsun.
7. `new RegExp` ile `Van` kelimesini bir değişkenden ara. Kelimenin kendisinde nokta olsaydı onu `\\.` yapmak gerektiğini bir cümleyle not et.

---

[← Önceki gün](../11-destructuring-and-spread/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../13-console-methods/ders.md)
