---
layout: post
title: "Cyber Jawara 2015: CJ15"
---
### Pendahuluan
---
Tulisan singkat ini akan membahas soal "CJ15" pada cyberjawara 2015. Soal tersebut berupa aplikasi yang menggunakan format ELF 32-bit.


### Langkah-langkah
---
* Berikut ini adalah informasi dari file "CJ15":

```
% file cj15
cj15: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, \
interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=134d6b254d6198d5b012f7b76ecb32e9b16c2cb3, stripped
```

* Dan jika melihat printable string pada aplikasi tersebut, maka akan diperoleh informasi berikut ini:

```
% strings cj15
/lib/ld-linux.so.2
Mk%Ma
libc.so.6
_IO_stdin_used
puts
printf
calloc
__libc_start_main
free
__gmon_start__
GLIBC_2.0
PTRh
[^_]
Flag: [Aku Ada Di Mana Nih]
Yuhuuuu Ketemu Kang
Clue : 22
Cemungudhhh Ahh
;*2$"
...
```

* Bisa terlihat bahwa cluenya adalah 22 (desimal), dan jika diubah menjadi heksadesimal maka nilainya adalah 0x16.

* Load aplikasi tersebut menggunakan radare2 dan gunakan perintah "aaa" untuk melakukan analisis seperti ini:

```
% r2 cj15
 -- Enable ascii-art jump lines in disassembly by setting 'e asm.lines=true'. asm.linesout and asm.linestyle may interest you as well
[0x08048390]> aaa
```

* Masih pada prompt radare2, lanjutkan dengan melihat daftar fungsi yang terdapat pada aplikasi CJ15 tersebut:

```
[0x08048390]> afl
0x08048390  34  1  entry0
0x08048370  6  1  sym.imp.__libc_start_main
0x08048586  271  9  main
0x08048330  6  1  sym.imp.printf
0x08048340  6  1  sym.imp.free
0x08048350  6  1  sym.imp.puts
0x08048380  6  1  sym.imp.calloc
0x080483d0  43  4  fcn.080483d0
0x0804848b  40  4  fcn.0804848b
0x080484b3  98  4  fcn.080484b3
0x08048515  113  9  fcn.08048515
0x080483c0  4  1  fcn.080483c0
0x080482f4  35  3  section..init
0x08048360  6  1  sub.__gmon_start___244_360
```

* Disassemble fungsi main pada aplikasi tersebut dengan menggunakan perintah "pdf @ main":

```
[0x08048390]> pdf @ main
/ (fcn) main 271
|           ; arg int arg_8        @ ebp+0x20
|           ; arg int arg_8_2      @ ebp+0x22
|           ; arg int arg_8_3      @ ebp+0x23
|           ; arg int arg_9_1      @ ebp+0x25
|           ; arg int arg_11_3     @ ebp+0x2f
|           ; arg int arg_16_2     @ ebp+0x42
|           ; arg int arg_22_2     @ ebp+0x5a
|           ; arg int arg_22_3     @ ebp+0x5b
|           ; arg int arg_28_3     @ ebp+0x73
|           ; arg int arg_29_3     @ ebp+0x77
|           ; arg int arg_30       @ ebp+0x78
|           ; arg int arg_30_1     @ ebp+0x79
|           ; arg int arg_30_3     @ ebp+0x7b
|           ; var int local_0_1    @ ebp-0x1
|           ; var int local_1      @ ebp-0x4
|           ; var int local_7      @ ebp-0x1c
|           ; DATA XREF from 0x080483a7 (main)
|           0x08048586    8d4c2404       lea ecx, [esp + 4]            ; 0x4
|           0x0804858a    83e4f0         and esp, 0xfffffff0
|           0x0804858d    ff71fc         push dword [ecx - 4]
|           0x08048590    55             push ebp
|           0x08048591    89e5           mov ebp, esp
|           0x08048593    51             push ecx
|           0x08048594    83ec24         sub esp, 0x24
|           0x08048597    89c8           mov eax, ecx
|           0x08048599    833802         cmp dword [eax], 2            ; [0x2:4]=0x101464c
|       ,=< 0x0804859c    7420           je 0x80485be
|       |   0x0804859e    8b4004         mov eax, dword [eax + 4]      ; [0x4:4]=0x10101
|       |   0x080485a1    8b00           mov eax, dword [eax]
|       |   0x080485a3    83ec08         sub esp, 8
|       |   0x080485a6    50             push eax
|       |   0x080485a7    6830870408     push str.Flag:__Aku_Ada_Di_Mana_Nih__n ; "Flag: [Aku Ada Di Mana Nih]." @ 0x8048730
|       |   0x080485ac    e87ffdffff     call sym.imp.printf           ; sym.imp.printf(unk, unk)
|       |   0x080485b1    83c410         add esp, 0x10
|       |   0x080485b4    b801000000     mov eax, 1
|      ,==< 0x080485b9    e9cf000000     jmp 0x804868d
|      ||   ; JMP XREF from 0x0804859c (main)
|      |`-> 0x080485be    c645e479       mov byte [ebp-local_7], 0x79  ; [0x79:1]=0 ; 'y'
|      |    0x080485c2    c645e55b       mov byte [ebp - 0x1b], 0x5b   ; [0x5b:1]=0 ; '['
|      |    0x080485c6    c645e623       mov byte [ebp - 0x1a], 0x23   ; [0x23:1]=0 ; '#'
|      |    0x080485ca    c645e75a       mov byte [ebp - 0x19], 0x5a   ; [0x5a:1]=0 ; 'Z'
|      |    0x080485ce    c645e822       mov byte [ebp - 0x18], 0x22   ; [0x22:1]=0 ; '"'
|      |    0x080485d2    c645e97b       mov byte [ebp - 0x17], 0x7b   ; [0x7b:1]=0 ; '{'
|      |    0x080485d6    c645ea73       mov byte [ebp - 0x16], 0x73   ; [0x73:1]=0 ; 's'
|      |    0x080485da    c645eb42       mov byte [ebp - 0x15], 0x42   ; [0x42:1]=4 ; 'B'
|      |    0x080485de    c645ec20       mov byte [ebp - 0x14], 0x20   ; [0x20:1]=56 ; "8." 0x00000020  ; "8." @ 0x20
|      |    0x080485e2    c645ed77       mov byte [ebp - 0x13], 0x77   ; [0x77:1]=0 ; 'w'
|      |    0x080485e6    c645ee78       mov byte [ebp - 0x12], 0x78   ; [0x78:1]=0 ; 'x'
|      |    0x080485ea    c645ef42       mov byte [ebp - 0x11], 0x42   ; [0x42:1]=4 ; 'B'
|      |    0x080485ee    c645f025       mov byte [ebp - 0x10], 0x25   ; [0x25:1]=0 ; '%'
|      |    0x080485f2    c645f178       mov byte [ebp - 0xf], 0x78    ; [0x78:1]=0 ; 'x'
|      |    0x080485f6    c645f22f       mov byte [ebp - 0xe], 0x2f    ; [0x2f:1]=0 ; '/'
|      |    0x080485fa    c645f300       mov byte [ebp - 0xd], 0
|      |    0x080485fe    8b4004         mov eax, dword [eax + 4]      ; [0x4:4]=0x10101
|      |    0x08048601    83c004         add eax, 4
|      |    0x08048604    8b00           mov eax, dword [eax]
|      |    0x08048606    83ec0c         sub esp, 0xc
|      |    0x08048609    50             push eax                      ; parameter 1: user_password
|      |    0x0804860a    e8a4feffff     call fcn.080484b3             ; fcn.080484b3(unk) <<< encrypt user_password
|      |    0x0804860f    83c410         add esp, 0x10                 ; stack cleanup
|      |    0x08048612    8945f4         mov dword [ebp - 0xc], eax    ; [ebp - 0xc] = encrypted user_password
|      |    0x08048615    83ec08         sub esp, 8
|      |    0x08048618    ff75f4         push dword [ebp - 0xc]        ; parameter 2: encrypted user_password
|      |    0x0804861b    8d45e4         lea eax, [ebp-local_7]        ; eax = encrypted cj15_password
|      |    0x0804861e    50             push eax                      ; parameter 1: encrypted cj15_password
|      |    0x0804861f    e8f1feffff     call fcn.08048515             ; fcn.08048515(unk, unk) <<< compare function
|      |    0x08048624    83c410         add esp, 0x10                 ; stack cleanup
|      |    0x08048627    85c0           test eax, eax                 ; apakah password benar?
|     ,===< 0x08048629    7410           je 0x804863b                  ; jika salah, maka lompat ke alamat 0x0804863b
|     ||    0x0804862b    83ec0c         sub esp, 0xc
|     ||    0x0804862e    684d870408     push str.Yuhuuuu_Ketemu_Kang  ; "Yuhuuuu Ketemu Kang " @ 0x804874d
|     ||    0x08048633    e818fdffff     call sym.imp.puts             ; sym.imp.puts(unk)
|     ||    0x08048638    83c410         add esp, 0x10
|     |     ; JMP XREF from 0x08048629 (main)
|     `---> 0x0804863b    83ec08         sub esp, 8
|      |    0x0804863e    ff75f4         push dword [ebp - 0xc]        ; parameter 2: encrypted user_password
|      |    0x08048641    8d45e4         lea eax, [ebp-local_7]        ; eax = encrypted cj15_password
|      |    0x08048644    50             push eax                      ; parameter 1: encrypted cj15_password
|      |    0x08048645    e8cbfeffff     call fcn.08048515             ; fcn.08048515(unk, unk) <<< compare function
|      |    0x0804864a    83c410         add esp, 0x10                 ; stack cleanup
|      |    0x0804864d    85c0           test eax, eax                 ; apakah password benar?
|    ,====< 0x0804864f    7412           je 0x8048663                  ; jika salah, maka lompat ke alamat 0x8048663
|    | |    0x08048651    83ec0c         sub esp, 0xc                  ;
|    | |    0x08048654    6862870408     push str.Clue_:_22            ; "Clue : 22" @ 0x8048762
|    | |    0x08048659    e8f2fcffff     call sym.imp.puts             ; sym.imp.puts(unk)
|    | |    0x0804865e    83c410         add esp, 0x10
|   ,=====< 0x08048661    eb10           jmp 0x8048673
|   ||      ; JMP XREF from 0x0804864f (main)
|   |`----> 0x08048663    83ec0c         sub esp, 0xc
|   |  |    0x08048666    686c870408     push str.Cemungudhhh_Ahh      ; "Cemungudhhh Ahh " @ 0x804876c
|   |  |    0x0804866b    e8e0fcffff     call sym.imp.puts             ; sym.imp.puts(unk)
|   |  |    0x08048670    83c410         add esp, 0x10
|   |       ; JMP XREF from 0x08048661 (main)
|   `-----> 0x08048673    83ec0c         sub esp, 0xc
|      |    0x08048676    ff75f4         push dword [ebp - 0xc]
|      |    0x08048679    e8c2fcffff     call sym.imp.free             ; sym.imp.free(unk)
|      |    0x0804867e    83c410         add esp, 0x10
|      |    0x08048681    c745f4000000.  mov dword [ebp - 0xc], 0
|      |    0x08048688    b800000000     mov eax, 0
|      |    ; JMP XREF from 0x080485b9 (main)
|      `--> 0x0804868d    8b4dfc         mov ecx, dword [ebp-local_1]
|           0x08048690    c9             leave
|           0x08048691    8d61fc         lea esp, [ecx - 4]
\           0x08048694    c3             ret
```

* Pada bagian awal fungsi main, bisa terlihat bahwa ada beberapa karakter terenkripsi yang disimpan pada stack. Dan pada alamat "0x0804860a" terdapat pemanggilan fungsi "fcn.080484b3" yang tugasnya untuk melakukan enkripsi terhadap password yang dimasukkan oleh user. Setelah melakukan enkripsi terhadap password yang dimasukkan oleh user, maka fungsi "fcn.08048515" akan melakukan perbandingan antara password user yang telah terenkripsi dengan password yang benar. Jika passwordnya tidak sesuai, maka "JUMP" pada alamat "0x804863b" akan dieksekusi dan dilanjutkan dengan menampilkan pesan kesalahan. Namun jika benar, maka password yang dimasukkan oleh user dan password yang benar akan diperiksa sekali lagi. Selanjutnya, kita akan melihat fungsi yang melakukan enkripsi terhadap password yang dimasukkan oleh user, yaitu fungsi "call fcn.080484b3":

```
[0x08048390]> pdf @ fcn.080484b3
/ (fcn) fcn.080484b3 98
|           ; arg int arg_2        @ ebp+0x8
|           ; var int local_0_1    @ ebp-0x1
|           ; var int local_3      @ ebp-0xc
|           ; var int local_4      @ ebp-0x10
|           ; CALL XREF from 0x0804860a (fcn.080484b3)
|           0x080484b3    55             push ebp
|           0x080484b4    89e5           mov ebp, esp
|           0x080484b6    83ec18         sub esp, 0x18
|           0x080484b9    ff7508         push dword [ebp+arg_2]
|           0x080484bc    e8caffffff     call fcn.0804848b             ; fcn.0804848b(unk)
|           0x080484c1    83c404         add esp, 4
|           0x080484c4    83c001         add eax, 1
|           0x080484c7    83ec08         sub esp, 8
|           0x080484ca    6a01           push 1
|           0x080484cc    50             push eax
|           0x080484cd    e8aefeffff     call sym.imp.calloc           ; sym.imp.calloc(unk, unk)
|           0x080484d2    83c410         add esp, 0x10
|           0x080484d5    8945f0         mov dword [ebp-local_4], eax
|           0x080484d8    c745f4000000.  mov dword [ebp-local_3], 0
|       ,=< 0x080484df    eb1c           jmp 0x80484fd
|       |   ; JMP XREF from 0x0804850e (fcn.080484b3)
|       |   0x080484e1    8b55f4         mov edx, dword [ebp-local_3]
|       |   0x080484e4    8b45f0         mov eax, dword [ebp-local_4]
|       |   0x080484e7    01d0           add eax, edx
|       |   0x080484e9    8b4df4         mov ecx, dword [ebp-local_3]
|       |   0x080484ec    8b5508         mov edx, dword [ebp+arg_2]    ; [0x8:4]=0
|       |   0x080484ef    01ca           add edx, ecx
|       |   0x080484f1    0fb612         movzx edx, byte [edx]
|       |   0x080484f4    83f216         xor edx, 0x16                 ; lakukan XOR terhadap setiap karakter password user dengan 0x16
|       |   0x080484f7    8810           mov byte [eax], dl
|       |   0x080484f9    8345f401       add dword [ebp-local_3], 1
|       |   ; JMP XREF from 0x080484df (fcn.080484b3)
|       `-> 0x080484fd    83ec0c         sub esp, 0xc
|       |   0x08048500    ff7508         push dword [ebp+arg_2]
|       |   0x08048503    e883ffffff     call fcn.0804848b             ; fcn.0804848b(unk)
|       |   0x08048508    83c410         add esp, 0x10
|       |   0x0804850b    3b45f4         cmp eax, dword [ebp-local_3]
|       `=< 0x0804850e    7fd1           jg 0x80484e1
|           0x08048510    8b45f0         mov eax, dword [ebp-local_4]
|           0x08048513    c9             leave
\           0x08048514    c3             ret
```

* Bisa terlihat bahwa instruksi pada alamat "0x080484f4" melakukan operasi XOR terhadap setiap karakter pada password yang diberikan oleh user dengan nilai 0x16 heksadesimal (22 desimal). Dari sini, kita dapat melakukan dekripsi terhadap password yang benar, yaitu dengan melakukan operasi XOR setiap karakter password yang benar dengan nilai 0x16 heksadesimal. Jika menggunakan python, caranya seperti ini:

```
% python -c "print ''.join([chr(x ^ 0x16) for x in [0x79,0x5b,0x23,0x5a,0x22,0x7b,0x73,0x42,0x20,0x77,0x78,0x42,0x25,0x78,0x2f]])"
oM5L4meT6anT3n9
```

* Dari langkah di atas, bisa terlihat, bahwa password yang benar adalah "oM5L4meT6anT3n9". Untuk mengujinya, jalankan aplikasi "CJ15" dengan menggunakan password tersebut:

```
% ./cj15 oM5L4meT6anT3n9
Yuhuuuu Ketemu Kang
Clue : 22
```


### Penutup
---
Sekian tulisan singkat kali ini, semoga bermanfaat. Terima kasih kepada Tuhan Yang Maha Esa, Maxindo, N3 dan Anda yang telah membaca tutorial ini.
