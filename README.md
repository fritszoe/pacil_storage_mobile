# pacil_storage

<details> 
<summary>Tugas - 7</summary>
<br>

### 1.) Stateless vs Stateful

- Stateless: Stateless widget adalah widget yang tidak memiliki keadaan internal (state). Ini berarti bahwa sekali widget tersebut dibuat, ia tidak bisa mengubah tampilannya berdasarkan perubahan data. Jadi tidak cocok untuk interface yang ada perubahan datanya
- Stateful: Stateful widget adalah widget yang memiliki keadaan internal (state) yang dapat berubah selama siklus hidup widget. Ini memungkinkan widget untuk merespons perubahan data dan memperbarui tampilannya sesuai kebutuhan. Ini cocok untuk interface yang ada perubahan data

### 2.) Apa saja widget di sini?

- MyApp: Yaitu widget utama yang jalanin aplikasi
- MyHomePage: Widget yang berupa home page dari aplikasi flutter ini
- ShopCard: Widget berbentuk card yang  menerima objek dari class ShopItem. widget inilah yang nantinya jika ditekan akan mengeluarkan snack bar "anda menekan tombol ini".

### 3.) How To?

- Pertama flutter create app
- Setelah itu, widget MyHomePage dari main akan dipindahkan ke dalam file baru bernama menu.dart, dari sini akan disambungkan dengan cara import
```dart
import 'package:pacil_storage/menu.dart';
```
- Setelah memindahkan MyHomePage beserta _MyHomePageState, mengubah widget MyHomePage menjadi stateless sehingga _MyHomePageState tidak lagi diperlukan.
- Membuat class Shop Item yang nantinya akan digunakan widget ShopCard sekaligus membuat object Shop Item tersebut.
- Membuat widget ShopCard yang akan menampilkan object Shop Item.
- Tidak lupa, atribut dari Shop Item ditambahkan, sehingga setiap object Shop Item bisa memiliki warna yang berbeda
```dart
final List<ShopItem> items = [
    ShopItem("Lihat Produk", Icons.checklist, Colors.indigo),
    ShopItem("Tambah Produk", Icons.add_shopping_cart, Colors.blueGrey),
    ShopItem("Logout", Icons.logout, Colors.deepPurple),
  ];
```
- Ubah bagian widget ShopCard sehingga menjadi warna dari masing-masing Shop Item
```dart
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color, //ganti color sesuai item
      ...
```
- Setelah itu harusnya selesai karena di main.dart, sudah disambungkan homepage nya, di bagian ini:
```dart
home: myHomePage(),
```
</details>
