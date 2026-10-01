# 11. Gün — Parçalama ve yayma

Liste ve nesne tek satırda açılabilir. Parçalama, içinden seçip ada bağlamaktır. Yayma, içini başka bir yere sermektir. Üç nokta ikisinde de vardır. Durduğu yere göre anlam değişir.

- Solda, parantezin içinde `...geri` duruyorsa toplar. Buna rest denir.
- Yeni liste veya çağrı kurarken duruyorsa serer. Buna yayma denir.

## Listeyi parçalamak

Soldan sağa eşleşir.

```js
const sehirler = ["İzmir", "Van", "İstanbul", "Trabzon"]
const [ilk, ikinci] = sehirler
console.log(ilk)
console.log(ikinci)
```

```text
İzmir
Van
```

Atlamak için boş virgül konur. Varsayılan, o sıra yoksa devreye girer.

```js
const [, , ucuncu] = sehirler
console.log(ucuncu)

const [a = "yok", b = "yok"] = ["İzmir"]
console.log(a)
console.log(b)
```

```text
İstanbul
İzmir
yok
```

Kalan rest ile toplanır. Rest sonuncu olmak zorundadır. Ortada duramaz.

```js
const [bas, ...geri] = sehirler
console.log(bas)
console.log(geri)
```

```text
İzmir
["Van", "İstanbul", "Trabzon"]
```

İki değişkenin değerini takas etmek için üçüncü bir değişken gerekmez.

```js
let sol = "Van"
let sag = "Trabzon"
;[sol, sag] = [sag, sol]
console.log(sol)
console.log(sag)
```

```text
Trabzon
Van
```

Satırın başındaki noktalı virgül, bir önceki satır parantezsiz bittiyse yapışmasın diyedir. Ayrı satırda şaşırmazsan koyma.

Fonksiyon birden fazla değer döndürmek istiyorsa liste döndürür. Çağıran parçalar.

```js
function uclar(liste) {
  const sirali = liste.slice().sort((x, y) => x - y)
  return [sirali[0], sirali[sirali.length - 1]]
}

const [kucuk, buyuk] = uclar([4, 9, 1])
console.log(kucuk)
console.log(buyuk)
```

```text
1
9
```

Döngüde de aynı açılış vardır:

```js
for (const [sira, ad] of ["İzmir", "Van"].entries()) {
  console.log(sira + " " + ad)
}
```

```text
0 İzmir
1 Van
```

## Nesneyi parçalamak

Ad, anahtarla aynı olmalıdır. Sıra önemsizdir.

```js
const kayit = { ad: "Serhat", sehir: "İstanbul", aktif: true }
const { ad, sehir } = kayit
console.log(ad)
console.log(sehir)
```

```text
Serhat
İstanbul
```

Yeniden adlandırmak, iki noktanın sağındaki yeni addır.

```js
const { ad: kisi, sehir: yer } = kayit
console.log(kisi)
console.log(yer)
```

```text
Serhat
İstanbul
```

`ad` değişkeni kurulmaz. Kurulan ad `kisi`dir.

Varsayılan, anahtar yoksa veya değeri `undefined` ise devreye girer. `null` varsayılanı ezmez. `null` bir değerdir.

```js
const { not = "yok" } = kayit
console.log(not)
```

```text
yok
```

İç içe nesne de açılır. Önce dış kapı, sonra iç kapı yazılır.

```js
const siparis = { masa: 4, hesap: { tutar: 180, bahsis: 20 } }
const {
  hesap: { tutar },
} = siparis
console.log(tutar)
```

```text
180
```

## Parametrede parçalamak

Fonksiyon nesne bekliyorsa gövdede `siparis.ad` yazmak yerine parametre açılır. Hangi alanın kullanıldığı kapıda görünür. Kullanılmayan alan sessizce durur.

```js
function etiket({ ad, sehir }) {
  return ad + ", " + sehir
}

console.log(etiket({ ad: "Serhat", sehir: "Van", ekstra: true }))
```

```text
Serhat, Van
```

## Yayma

Üç nokta, değeri yerinde açar. Liste kopyalanır ve birleştirilir. Kopya sığdır. İçteki nesneler paylaşılır.

```js
const a = ["İzmir", "Van"]
const b = ["İstanbul", "Trabzon"]
const birlikte = [...a, ...b]
const kopya = [...a]
kopya.push("İstanbul")
console.log(a)
console.log(birlikte)
```

```text
["İzmir", "Van"]
["İzmir", "Van", "İstanbul", "Trabzon"]
```

`a` değişmedi. `push` kopyaya gitti.

Fonksiyon argümanına sermek, listedeki sayıları tek tek vermekle aynıdır.

```js
const notlar = [8, 3, 11]
console.log(Math.max(...notlar))
```

```text
11
```

`Math.max(notlar)` çalışmaz. `Math.max` sayı ister, liste istemez. Üç nokta listeyi `8, 3, 11` diye açar.

Nesne de serilir. Aynı anahtar iki kez gelirse **sonraki kazanır**.

```js
const temel = { ad: "Serhat", sehir: "İzmir" }
const ozel = { ...temel, sehir: "Trabzon" }
console.log(ozel)
console.log(temel)
```

```text
{ ad: "Serhat", sehir: "Trabzon" }
{ ad: "Serhat", sehir: "İzmir" }
```

`temel` durur. `ozel` yeni bir nesnedir. `sehir` sonra yazıldığı için Trabzon, İzmir’in üstüne yazar.

## Egzersizler

1. `["İzmir", "Van", "İstanbul", "Trabzon"]` içinden ilk ikisini ayrı değişkenlere al. Üçüncü ve dördüncüyü `...geri` ile tut. `geri.length` 2 olsun.
2. `sol = "Van"`, `sag = "İstanbul"` olsun. Parçalama ile takas et. `sol` İstanbul olmalıdır.
3. `{ ad: "Serhat" }` nesnesinden `ad` ve `sehir` çıkar. `sehir` yoksa `"bilinmiyor"` olsun.
4. `ad` alanını `tamAd` diye yeniden adlandırarak parçala.
5. `{ sehir: "İzmir", yil: 2020 }` ile `{ sehir: "Van" }` nesnelerini yayma ile birleştir. `sehir` Van kalsın, `yil` kaybolmasın. Sıra önemli. Van’ı sona yaz.
6. Bir listenin kopyasına şehir ekle. Asıl listenin uzunluğunun değişmediğini yazdır.
7. `Math.min(...[8, 3, 11])` dene. Sonuç `3` olsun. Üç noktasız `Math.min([8, 3, 11])` dene. `NaN` gör. Nedenini bir cümle yaz.
8. `etiket({ ad, sehir })` fonksiyonu yaz. `Serhat, Trabzon` döndürsün.

---

[← Önceki gün](../10-sets-and-maps/ders.md) · [İçindekiler](../README.md) · [Sonraki gün →](../12-regular-expressions/ders.md)
