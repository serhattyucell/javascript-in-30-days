# 4. Gün — Koşullar

Program her seferinde aynı satırları çalıştırmak zorunda değildir. Bir değer belli bir aralıktaysa bir yol, değilse başka yol seçilir. Dünkü karşılaştırma burada karar haline gelir.

Koşulun gövdesi süslü paranteze alınır. Parantezsiz tek satırlık `if` yazılabilir ama sonradan eklenen ikinci satır koşulun dışında kalır ve sessizce bozulur. Süslü parantez her zaman durur.

## if

Koşul doğruysa blok çalışır. Yanlışsa hiçbir satırı çalışmaz, program bloktan sonra devam eder.

Serhat’ın biletinden 3 tane kalmış. Rafta varsa haber ver.

```js
const stok = 3
if (stok > 0) {
  console.log("rafta var")
}
```

```text
rafta var
```

`stok` 0 yapılırsa konsol susar. Hata yoktur. Koşul tutmamıştır.

## if else

İki kapı vardır. Biri kapanınca öteki açılır. İkisi birden çalışmaz.

```js
const saat = 21
if (saat < 18) {
  console.log("gün ışığı")
} else {
  console.log("lamba yak")
}
```

```text
lamba yak
```

21, 18’den küçük olmadığı için birinci blok atlanır, `else` çalışır. `saat` 9 yapılsaydı `gün ışığı` çıkardı.

## else if

Kapı ikiden fazlaysa zincir kurulur. JavaScript ilk doğru koşulda durur, altını okumaz. Bu yüzden dar aralık, geniş aralığın üstüne yazılır. Not ölçeği yüksekten düşüğe dizilir.

```js
const not = 76
let harf

if (not >= 90) {
  harf = "A"
} else if (not >= 80) {
  harf = "B"
} else if (not >= 70) {
  harf = "C"
} else if (not >= 60) {
  harf = "D"
} else {
  harf = "kaldı"
}

console.log(harf)
```

```text
C
```

76, 90’ın ve 80’in altındadır, 70’in üstündedir. Zincir `C`de durur. `D` satırına bakılmaz.

Sıra ters olursa bozulur. Önce `not >= 60` yazılırsa 95 puan da o kapıdan girer ve `D` olur. Yüksek puan bir daha kontrol edilmez. Ölçek her zaman yüksekten aşağı yazılır.

## İç içe

İkinci soru ancak birinci doğruysa anlamlıdır. Üye değilse borca bakmaya gerek yoktur.

```js
const uye = true
const borc = 0

if (uye) {
  if (borc === 0) {
    console.log("ödünç alabilir")
  } else {
    console.log("önce borcu kapat")
  }
} else {
  console.log("önce üye ol")
}
```

```text
ödünç alabilir
```

Üç kattan derin iç içe okunmaz. Aynı iş tek koşula da sığar: `uye && borc === 0`. İki yol da doğrudur. Derinlik artınca tek satırlık `&&` daha az yer kaplar.

## switch

Tek bir değer birçok sabitle kıyaslanacaksa `switch` düz durur. `if` zinciri de olur. Fark, okuma kolaylığıdır.

Her kolun sonuna `break` konur. Konmazsa eşleşen koldan aşağısı da çalışır. Buna düşme denir. İstenmiyorsa `break` unutulmaz.

Haftanın günü `getDay()` ile gelir. Pazar 0, cumartesi 6’dır.

```js
const gun = new Date().getDay()
let ad

switch (gun) {
  case 0:
    ad = "pazar"
    break
  case 6:
    ad = "cumartesi"
    break
  default:
    ad = "hafta içi"
}

console.log(ad)
```

Bugün hafta içiyse `hafta içi` çıkar. Cumartesi çalıştırılırsa `cumartesi` çıkar. `default`, hiçbir `case` tutmazsa çalışan koldur. `else` ile aynı işi görür.

`switch` `===` ile kıyaslar. `case "1"` ile sayı `1` eşleşmez.

## Üçlü operatör yine

Tek bakışta okunan seçim üçlü ile yazılır. İçine ikinci bir üçlü konmaz. Okunmaz. O zaman `if` kullanılır.

```js
const acik = true
const tabela = acik ? "girebilirsin" : "kapalıyız"
console.log(tabela)
```

```text
girebilirsin
```

## Egzersizler

1. Bir `sicaklik` değişkeni al. 0’ın altı “don”, 0–15 “serin”, 16–28 “ılık”, üstü “sıcak” desin. 30, 10 ve -2 ile üç kez dene. Üç metin de doğru kola düşsün.
2. `ad` değişkeni boş metinse konsola “ad gerekli” yaz. Doluysa `Serhat, İzmir` gibi selamla. `if else` kullan. Boş metinle ve `"Serhat"` ile iki kez çalıştır.
3. 1’den 7’ye bir sayı tut. `switch` ile pazartesiden pazara gün adını yaz. `break` satırını bir koldan sil, alttaki kolun da çalıştığını gör, sonra `break`i geri koy.
4. Bilet varsa **ve** yaş 12’den büyükse “salona”, değilse “uygun değil” yaz. `&&` kullan. Yaşı 10 ve bileti `true` yap, ikinci metni gör.
5. Bir sayının pozitif, negatif veya sıfır olduğunu söyleyen kontrol yaz. `-4`, `0` ve `9` dene.
6. Aynı işi üçlü operatörle yaz. Hangisi daha okunuyor, bir cümle not et. Üç kola bölünmüş seçim üçlüye sığmayabilir. Sığmıyorsa `if`te kal.
7. Not aralığını yanlış sırayla yaz. Önce `>= 50`, sonra `>= 90`. 95’te ne çıktığını gör. Sonra sırayı yüksekten düşüğe düzelt.

---

[← Önceki gün](../03-booleans-operators-date/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../05-arrays/ders.md)
