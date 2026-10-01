# 4. Gün — Koşullar

Program, bir ifadeye göre farklı bir iş yapacaksa koşul kullanılır. Üçlü operatör kısa seçim içindir. Bu bölümde `if`, `else`, `else if` ve `switch` ele alınır.

Koşulun gövdesi süslü paranteze alınır. Tek satırda parantezsiz `if` yazılabilir; sonradan eklenen satır koşulun dışında kalır ve hata sessizce oluşur.

## if

Koşul doğruysa blok çalışır. Yanlışsa hiçbir şey olmaz.

```js
const stok = 3
if (stok > 0) {
  console.log("rafta var")
}
```

## if else

İki kapı. Biri kapanınca öteki açılır.

```js
const saat = 21
if (saat < 18) {
  console.log("gün ışığı")
} else {
  console.log("lamba yak")
}
```

## else if

Kapı ikiden fazlaysa zincir kur. Motor ilk doğru koşulda durur, altını okumaz. Sıralama bu yüzden önemli. Dar aralığı geniş aralığın üstüne yaz.

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

`not >= 90` kontrolü en alta konursa 95 puan da daha üstteki gevşek koşula yakalanır. Aralıklar yüksekten düşüğe yazılır.

## İç içe

Bazen ikinci soru ancak birinci doğruysa anlamlıdır.

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

İç içe üç kattan derinleşirse okunmaz. O zaman koşul `&&` ile yan yana yazılır ya da iş fonksiyona bölünür.

## switch

Tek bir değer birçok sabitle kıyaslanacaksa `switch` daha düz durur. Her kola `break` konur. Konmazsa alttaki kollar da çalışır. Buna kasıtlı düşme denir; istenmedikçe bırakılmaz.

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

`default`, hiçbir `case` tutmazsa çalışır. `else` ile aynı işi görür.

`switch` `===` ile kıyaslar. `"1"` ile `1` eşleşmez.

## Üçlü operatör, bir daha

Tek satırlık seçim:

```js
const acik = true
const tabela = acik ? "girebilirsin" : "kapalıyız"
```

İç içe ikinci bir üçlü yazılmaz. Okunması zorlaşır. O durumda `if` daha uygundur.

## Egzersizler

1. Bir hava sıcaklığı alın. 0 altı “don”, 0–15 “serin”, 16–28 “ılık”, üstü “sıcak” desin.
2. `Serhat` adlı değişken boşsa konsola “ad gerekli” yazın. Doluysa `İzmir` ile birlikte selamlayın. `if else` kullanın.
3. 1’den 7’ye bir sayı tutun. `switch` ile haftanın gün adını yazın.
4. İki koşulu birleştirin: bilet var **ve** yaş 12’den büyükse “salona”, değilse “uygun değil”.
5. Bir sayının pozitif, negatif veya sıfır olduğunu söyleyen kısa bir kontrol yazın.
6. Aynı işi üçlü operatörle de yazın. Hangisinin daha okunur olduğunu not edin.
7. Not aralığını yanlış sırayla yazın (önce `>= 50`, sonra `>= 90`). 95’te çıkan sonucu görün, sonra sırayı düzeltin.

---

[← Önceki gün](../03-booleans-operators-date/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../05-arrays/ders.md)
