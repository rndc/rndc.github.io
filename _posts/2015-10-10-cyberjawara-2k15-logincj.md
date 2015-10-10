---
layout: post
title: "Cyber Jawara 2015: LoginCJ"
---
### Pendahuluan
---

Tulisan singkat ini akan membahas soal "LoginCJ" pada cyberjawara 2015. Soal tersebut berupa executable yang dibuat menggunakan Visual Basic 6 dan proses pengerjaannya dilakukan menggunakan sistem operasi Linux.


### Langkah-langkah
---

* Gunakan perintah "strings" untuk melihat printable string pada aplikasi tersebut. Karena aplikasi tersebut dibuat menggunakan Visual Basic, maka string yang terdapat pada aplikasi tersebut menggunakan tipe karakter unicode 16-bit. Gunakan opsi "-e l" pada perintah "strings" untuk menampilkan printable string yang menggunakan format unicode 16-bit seperti ini:

```% strings -e l LoginCJ.exe
I*\AC:\Program Files (x86)\Microsoft Visual Studio\VB98\cjlogin\Project2.vbp
J4w4r4cyb3rrrr
2015j4w4racYb3RR
Coba Lagi Kang Sampai Berhasil
Oleh-Oleh Khas Jawa Tengah
Gagal Maning !!
JZJ(
VS_VERSION_INFO
VarFileInfo
Translation
StringFileInfo
040904B0
CompanyName
Microsoft
ProductName
Project2
FileVersion
1.00
ProductVersion
1.00
InternalName
LoginCJ
OriginalFilename
LoginCJ.exe
```

* Bisa terlihat, pada baris ke-2 dan ke-3 terdapat string yang cukup menarik. Selanjutnya, jalankan aplikasi "LoginCJ" menggunakan wine dan masukkan "J4w4r4cyb3rrrr" sebagai username dan "2015j4w4racYb3RR" sebagai password seperti pada gambar berikut ini:

>   ![Gambar 1](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/cj2k15-cjlogin-00.png)

* Hasilnya adalah sebagian flag berupa string "JC2015{LANTING" dengan huruf berwarna hijau pada gambar di sebuah form.

>   ![Gambar 1](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/cj2k15-cjlogin-01.png)

* Selain menggunakan cara di atas, Anda juga dapat menggunakan "binwalk" dan "dd" untuk mengekstrak gambar yang berisi flag tersebut. Jalankan "binwalk" seperti ini:

```% binwalk LoginCJ.exe
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             Microsoft executable, portable (PE)
25026         0x61C2          PNG image, 256 x 256, 8-bit/color RGBA, non-interlaced
25067         0x61EB          Zlib compressed data, default compression
500014        0x7A12E         JPEG image data, JFIF standard 1.01
714848        0xAE860         PNG image, 256 x 256, 8-bit/color RGBA, non-interlaced
714889        0xAE889         Zlib compressed data, default compression
```

* Bisa terlihat bahwa pada executable "LoginCJ" terdapat gambar dalam format JPEG yang ukurannya 214834 byte (714848 - 500014). Offset dimana file tersebut berada adalah 500014 hingga 714848. Selanjutnya, Anda dapat menggunakan perintah "dd" untuk mengekstrak gambar tersebut seperti ini:

```% dd if=LoginCJ.exe of=img.jpg bs=1 skip=500014 count=$((714848 - 500014))
214834+0 records in
214834+0 records out
214834 bytes (215 kB) copied, 0.533164 s, 403 kB/s
```

* Bisa terlihat bahwa gambar tersebut berhasil diekstrak:

```% file img.jpg
img.jpg: JPEG image data, JFIF standard 1.01, aspect ratio, density 1x1, segment length 16, baseline, precision 8, 703x703, frames 3
```

### Penutup
---
Sekian tutorial singkat kali ini, semoga bermanfaat. Terima kasih kepada Tuhan Yang Maha Esa, Maxindo, N3 dan Anda yang telah membaca tutorial ini.
