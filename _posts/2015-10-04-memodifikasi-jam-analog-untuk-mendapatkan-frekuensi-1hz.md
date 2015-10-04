---
layout: post
title: "Memodifikasi Jam Analog Untuk Mendapatkan Frekuensi 1 Hz"
---
### Pendahuluan
---

Pada tutorial kali ini akan dibahas mengenai cara memanfaatkan jam analog yang sudah tidak terpakai. Jam analog yang akan digunakan pada tutorial kali ini adalah jam tangan analog, yang mungkin caranya tidak jauh berbeda dengan jam dinding analog.


### Langkah - langkah
---

* Berikut ini adalah bahan yang diperlukan :
  1. Jam tangan analog yang mesinnya masih berfungsi.
  2. Dioda 1N4148 (atau dioda penyearah lainnya seperti 1N4007) sebanyak 2 buah.
  3. FET BS170.
  4. LED.
  5. Resistor 1k sebanyak 2 buah.
  6. Resistor 270R.
  7. Kabel jumper secukupnya.

* Siapkan peralatan dan jam tangan analog, kemudian buka penutupnya.

>  ![Gambar 1](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-1.jpg)

* Keluarkan bagian mesin jam dari casingnya.

>  ![Gambar 2](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-2.jpg)

* Selanjutnya ambil bagian elektronik dari jam tangan tersebut. Hanya bagian ini yang kita butuhkan saat ini, jadi bagian lainnya dapat dibuang atau disimpan untuk keperluan lain:

>  ![Gambar 3](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-3.jpg)

* Untuk keperluan informasi, kita dapat mengamati bentuk gelombang dari rangkaian elektronik ini dengan cara merangkaianya dengan menghubungkan bagian catu daya + dan - ke sumber tegangan 3 volt, kemudian bagian outputnya (output 1 dan 2) pada probe osiloskop seperti pada gambar berikut ini:

>  ![Gambar 4](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-4.jpg)

* Perhatikan gambar sinyal pada osiloskop dibawah ini:

>  ![Gambar 5a](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-5a.jpg)

* Pada osiloskop, channel 1 merupakan sinyal dari output 1, sedangkan channel 2 merupakan sinyal dari output 2:

>  ![Gambar 5b](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-5b.jpg)

* Perhatikan kursor yang menunjukan besar perioda pada sinyal channel 1. Besar perioda tersebut adalah sebesar 2 detik atau 0,5 Hz:

>  ![Gambar 5c](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-5c.jpg)

* Perhatikan kursor yang menunjukan besar perioda pada sinyal channel 2. Besar perioda tersebut juga menunjukkan angka 2 detik atau 0,5 Hz:

>  ![Gambar 5d](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-5d.jpg)

* Sedangkan pada gambar diatas, kursor ditunjuk untuk mengukur ''delta'' antara sinyal channel 1 dan 2. Dapat dilihat bahwa besarnya adalah 1 detik atau 1 Hz. Dengan demikian, untuk menghasilkan sinyal sebesar 1 Hz. Kita harus mengkombinasikan sinyal dari output 1 dan 2 tersebut. Jika diperhatikan lagi, siklus positif lebih besar daripada siklus negatif. Menurut pendapat saya, outputnya harus dibuat ''inverting'' agar lebih cocok untuk perangkat aktif high.

* Perhatikan gambar rangkaian dibawah ini, kemudian rangkailah:

>  ![Gambar 6](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-6.jpg)

* Gambar selanjutnya adalah rangkaian yang telah disatukan sesuai rangkaian diatas secara bebas:

>  ![Gambar 7a](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-7a.jpg)

>  ![Gambar 7b](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-7b.jpg)

* Hubungkan probe osiloskop channel 1 pada output 1 atau 2 kemudian hubungkan probe osiloskop 2 pada kaki drain FET BS170. Selanjutnya hubungkan powersupply dan hidupkan. Sekarang saatnya kita lakukan pengujian dengan cara menghubungkannya seperti gambar dibawah ini.

>  ![Gambar 8](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-8.jpg)

* Dapat dilihat bahwa output dari FET memiliki frekuensi keluaran sebesar 1 Hz. Untuk lebih jelasnya, perhatikan gambar sinyal dari osiloskop dibawah ini:

>  ![Gambar 9](https://raw.githubusercontent.com/rndc/rndc.github.io/master/images/1hz-9.jpg)


### Penutup
---

Selanjutnya anda mungkin dapat mengembangkan tutorial ini dengan memanfaatkan sinyal keluarannya untuk keperluan pembuatan pewaktu digital, frekuensi counter, atau lainnya. Sekian tutorial singkat kali ini, semoga bermanfaat. Terima kasih kepada Tuhan Yang Maha Esa, Maxindo, N3 dan Anda yang telah membaca tutorial singkat ini.


### Referensi
---

* [One Second Timebase](http://josepino.com/circuits/index.php?one_second_timebase.jpc)
* [Diode-transistor Logic](https://en.wikipedia.org/wiki/Diode-transistor_logic)
