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

##
<details>
<summary>Tugas-9</summary>

### 1.) Apakah bisa ambil JSON tanpa perlu membuat model?
Iya bisa, pengambilan data dengan JSON bisa dilakukan tanpa perlu adanya model terlebih dahulu, akan tetapi, jauh lebih baik membuat model sebelum mengambil JSON untuk code safety, code organization, dan validation.
### 2.) CookieRequest on Flutter?
- Sesuai namanya, CookieRequest adalah sebuah Class dalam flutter yang digunakan untuk mengambil Cookie dari aplikasi Flutter, bisa untuk data pengguna, data sesi, dan autentikasi. 
- CookieRequest perlu dibagikan ke semua komponen Flutter untuk memastikan Cookie digunakan dengan konsisten di keseluruhan aplikasi.
### 3.) JSON on Flutter?!
- Untuk mengambil data JSON dan menampilkannya ke dalam app Flutter, Flutter sudah menyediakan suatu library yaitu convert
- Kita akan ambil data dari website dan mengambil bagian json nya, lalu akan diambil dengan await http.get dan dengan dart convert, akan di json.decode
### 4.) Authentication on Both?!
- Buatlah sebuah modul authentication di Django dan buatlah sebuah fungsi untuk login dan logout seperti berikut:
```python
from django.shortcuts import render
from django.contrib.auth import authenticate, login as auth_login
from django.contrib.auth import logout as auth_logout
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Status login sukses.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login sukses!"
                # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, akun dinonaktifkan."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login gagal, periksa kembali email atau kata sandi."
        }, status=401)
    
@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logout berhasil!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout gagal."
        }, status=401)
```
- Buatlah fungsi login di dart yang akan menjadi bagian dari screens, dan login.dart tsb dihubungkan dengan django menggunakan package dari PBP
### 5.) Widgets
- AppBar: AppBar digunakan untuk menampilkan widget toolbar, title, dan actions
- Collumn: Menampilkan child darinya dalam wujud kolom (vertikal ke bawah
- Scaffold: Drawer, snackbar, dan lain-lain disediakan dengan menggunakan Scaffold.
- Container: Sesuai namanya, untuk meletakkan
- Textfield: Ini digunakan untuk menerima input dari keyboard pengguna, sudah digunakan dalam login.
- Snackbar: untuk popup message
### 6.) How to?
- Menyiapkan semua kebutuhan di Django dengan membuat modul baru untuk authentication serta menambahkan corsheaders, dan tidak lupa tambahkan url di app
- Dalam modul auth, tambahkan views untuk login dan logout di flutter
```py
@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Status login sukses.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login sukses!"
                # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, akun dinonaktifkan."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login gagal, periksa kembali email atau kata sandi."
        }, status=401)
    
@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logout berhasil!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout gagal."
        }, status=401)
```
- Setelah itu gunakan package untuk Django operation di Flutter yang sudah disediakan tim PBP dengan cara:
```dart
flutter pub add provider
flutter pub add pbp_django_auth
```
- Menggunakan package tadi, buatlah loginPage untuk flutter dengan mengimport auth dari django, seperti berikut:
```dart
import 'package:shopping_list/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

void main() {
    runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
const LoginApp({super.key});

@override
Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Login',
        theme: ThemeData(
            primarySwatch: Colors.blue,
    ),
    home: const LoginPage(),
    );
    }
}

class LoginPage extends StatefulWidget {
    const LoginPage({super.key});

    @override
    _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
    final TextEditingController _usernameController = TextEditingController();
    final TextEditingController _passwordController = TextEditingController();

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
            appBar: AppBar(
                title: const Text('Login'),
            ),
            body: Container(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                        TextField(
                            controller: _usernameController,
                            decoration: const InputDecoration(
                                labelText: 'Username',
                            ),
                        ),
                        const SizedBox(height: 12.0),
                        TextField(
                            controller: _passwordController,
                            decoration: const InputDecoration(
                                labelText: 'Password',
                            ),
                            obscureText: true,
                        ),
                        const SizedBox(height: 24.0),
                        ElevatedButton(
                            onPressed: () async {
                                String username = _usernameController.text;
                                String password = _passwordController.text;

                                // Cek kredensial
                                // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                                // Untuk menyambungkan Android emulator dengan Django pada localhost,
                                // gunakan URL http://10.0.2.2/
                                final response = await request.login("http://<APP_URL_KAMU>/auth/login/", {
                                'username': username,
                                'password': password,
                                });
                    
                                if (request.loggedIn) {
                                    String message = response['message'];
                                    String uname = response['username'];
                                    Navigator.pushReplacement(
                                        context,
                                        MaterialPageRoute(builder: (context) => MyHomePage()),
                                    );
                                    ScaffoldMessenger.of(context)
                                        ..hideCurrentSnackBar()
                                        ..showSnackBar(
                                            SnackBar(content: Text("$message Selamat datang, $uname.")));
                                    } else {
                                    showDialog(
                                        context: context,
                                        builder: (context) => AlertDialog(
                                            title: const Text('Login Gagal'),
                                            content:
                                                Text(response['message']),
                                            actions: [
                                                TextButton(
                                                    child: const Text('OK'),
                                                    onPressed: () {
                                                        Navigator.pop(context);
                                                    },
                                                ),
                                            ],
                                        ),
                                    );
                                }
                            },
                            child: const Text('Login'),
                        ),
                    ],
                ),
            ),
        );
    }
}
```
- Setelah itu, buatlah model di django menyesuaikan dengan model Produk, cara mudahnya adalah mengakses JSON products dengan 'json/' dan mengubah nya menggunakan quicktype
- Setelah itu, buatlah screen yang akan menampilkan semua product dari Products.dart
- Tambahkan ke left drawer
- Untuk integrasi form flutter dgn django bisa dilakukan seperti berikut: 
```dart
@csrf_exempt
def create_product_flutter(request):
    if request.method == 'POST':
        
        data = json.loads(request.body)

        new_product = Product.objects.create(
            user = request.user,
            name = data["name"],
            price = int(data["price"]),
            description = data["description"]
        )

        new_product.save()

        return JsonResponse({"status": "success"}, status=200)
    else:
        return JsonResponse({"status": "error"}, status=401)
```
- Dengan CookieRequest, kita bisa menambahkan product baru dengan form dari flutter.
- Tambahkan perintah onTap di shop_card untuk si Logout karena logout belum melakukan apa-apa.
</details>