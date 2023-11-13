# pacil_storage

##
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

##
<details>
<summary>TUGAS-8</summary>

### 1.) Navigator.push() vs Navigator.pushReplacement()
- Navigator.push() menambahkan page atau halaman atau screen baru ke depan, seperti ditumpuk, ini memungkinkan pengguna untuk kembali ke hlm sebelumnya.
- Navigator.pushReplacement() menambahkan halaman ke tumpukan tapi dia tujuannya menggantikan halaman saat ini, jadi pengguna gak bisa balik ke halaman sebelumnya.
### 2.) Flutter layout widgets
- Container: bisa untuk tata letak dan styling atau dekorasi. Container bisa diisi widget lain, ada margin dan padding nya juga.
- Collumn: Mengatur childrennya secara vertikal, seperti kolom pada umumnya, bisa untuk form login yang biasanya berbentuk kolom.
- Row: Sama kayak collumn tapi horizontal (bentuknya baris)
- ListView: Untuk scrolling, jadi gak perlu menghabiskan banyak space di layar.
- GridView: Untuk menampilkan data secara grid
- Stack: Stacking widget, ditumpuk diatas satu sama lain
- Expanded:  Memberikan children sebanyak mungkin ruang yang tersedia. Ini berguna dalam Column atau Row untuk memberikan sebagian atau seluruh sisa ruang kosong.
- Flexible: Biasanya untuk row dan collumn supaya childrennya flexible, bisa menyesuaiakan ukuran berdasarkan proporsi.
### 3.) Elemen input dalam Form
- Nama produk
- Harga produk
- Deskripsi produk
- Semuanya menggunakan field TextFormField
### 4.) Penerapan clean architecture pada flutter
Clean architecture menerapkan pemisahan komponen-komponen berdasarkan fungsinya sehingga apabila ada perubahan-perubahan yang akan terjadi, atau adanya pergantian author, maka akan lebih memudahkan pemahaman terhadap code. 
- Contohnya di sini, bagian menu dan form dipisahkan ke dalam folder screens, artinya ini adalah bagian yang ditampilkan di layar.
- Contoh lain adalah pemisahan left_drawer dan shop_card yang ada di widgets 
### 5.) How To?
- Buatlah file left_drawer yang akan menjadi widget drawer di bagian kiri
- Drawer punya routing 2 tombol yang akan routing ke menu dan ke shopform page
- Membuat form dengan shoplist_form.dart, form akan menggunakan scaffold dan memiliki drawer juga di samping kiri dengan left_drawer tadi dan tambahkan juga widget Form di body
- Mengisi widget form dengan field TextFormField untuk ketiga attribut yaitu nama, harga, dan deskripsi.
- Ketiga TextFormField adalah child dari Column di shoplist_form
- Menambahkan tombol save yang akan memunculkan showDialog() produk yang dibuat.
- Navigate button tambah produk baik di drawer ataupun di menu untuk menuju ke shoplist_form.
</details>