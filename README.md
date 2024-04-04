## Kelompok IT12

# Laporan Resmi Praktikum Jarkom - Modul 1 - Wireshark

### Anggota Kelompok
- Rehana Putri Salsabilla ( 5027221015 )
- Muhammad Rifqi Oktaviansyah ( 5027221067 )

## Soal 1 : ATM or ATP or FTP ? 🤔
Pradityo mencoba mengembangkan server ftp, tetapi seseorang mencoba melakukan bruteforce login, bisakah Anda menganalisis apa yang terjadi?

#### Solusi : 
- Menggunakan filter yang ada untuk memilih paket yang terkait dengan FTP.
  Menggunakan search *ftp* seperti dibawah ini
  ![Screenshot 2024-04-03 201017](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/a63b1119-6ddb-4949-9ba5-fc9188dbcc9f)

- Lakukan command *nc* di terminal untuk mencari clue dari soal dan untuk mendapatkan flag yang didapatkan dari soal tersebut `nc 10.15.40.20.10004`
  ![1004](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/ae26f6f6-4208-4a02-8bb6-a03850059b17)

- Follow semua paket dan cari flag yang berbentuk string sesuai dengan clue pada nc yang didapatkan. Dan didapatkan flag berupa string pada paket `tcp.stream eq 319`
  ![Screenshot 2024-03-30 214111](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/6ac00bf0-5f6e-493c-a52a-0004c883ccd7)

- Setelah di dapatkan flag tersebut, inputkan flag yang didapat berupa string tadi ke input jawaban pada `nc 10.15.40.20 10004`
dan akan didapatkan format flag yang diberikan seperti dibawah ini 
  ![10004](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/c63fa782-3bb0-4e48-990f-940936105f2c)

## Soal 2 : How Many Packets ?
Sebagai kewajiban untuk laporan, aku diminta untuk mencari tahu berapa kali attempt login yang dilakukan oleh hacker. Dapatkah kamu membantuku untuk menganalisanya?

#### Solusi : 
- Langkah pertama yaitu saya melihat clue dari nc soal ini yaitu `nc 10.15.40.20 10005`
  ![10005](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/8c70cfca-f073-42ec-aecb-11dd80a3cd3a)
  
- Dari soal diatas yaitu mencari tau total attemp login, dimana pasti ada percobaan menginputkan password, saya mencoba mencari melalui filter dengan kunci paket ftp karena dari soal diminta untuk mencari response. Lalu di dapatkan kunci lagi yaitu response dengan code 331 dan pesan *please specify the password*
  ![Screenshot 2024-04-03 212720](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/b5297cd6-a524-4b1c-8d36-07bc941111d9)

- Lalu kita coba filter dengan lengkap yaitu `ftp.response.code == 331`. Dari pencarian tersebut kita lihat bagian bawah yang menunjukkan `display = 934` dimana itu adalah jumlah semua attemp login yang dimaksut soal.
  ![Screenshot 2024-04-03 213324](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/7fb9102b-b450-48f8-a617-123ecfc663b1)
  ![Screenshot 2024-04-03 213343](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/ed5d987a-54a7-4a3f-a868-33c52a991e8b)
  
- Setelah mendapatkan angka tersebut, coba inputkan angka tersebut di dalam jawaban pada `nc 10.15.40.20 10005` dan di dapatkan flag dengan format yang diberikan
  ![10005](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/5c9641b3-7e40-43f4-ab08-70de73b0b94f)

## Soal 3 : Trace him 
Selain menghitung jumlah packet, coba lacak juga ip penyerang tersebut!

### Solusi : 
- Langkah pertama yaitu melihat soal dan clue yang di dapatkan dari `nc 10.15.40.20 10006` yang diberikan soal. Selanjutnya kita tau bahwa yang dimaksud adalah berbentuk *Alamat ip*
  ![10006](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/84aa48a5-2a76-4d03-8467-e2da65d9b166)

- Dan merujuk dari jawaban soal `*ATM or ATP or FTP ? 🤔*` disini kita bisa melihat destination pada jawaban soal `*ATM or ATP or FTP ? 🤔*`. Dan didapatkan destination pada paket `tcp.stream eq 319`
  ![Screenshot 2024-03-30 231642](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/35cc6464-a2eb-4240-9530-04eab88dd553)
  
- Dan setelah itu inputkan destination yang didapatkan pada `nc 10.15.40.20 10006`. Dan jawaban benar lalu didapatkan format flag yang diberikan seperti dibawah ini
  ![10006](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/6df5b145-f17c-4778-8d50-28916362f1fa)

## Soal 4 : Secret
Temukan pesan rahasia dari attacker

#### Solusi : 
- Langkah awal adalah melakukan command `nc 10.15.40.20 10010` pada terminal untuk melihat clue dari soal tersebut. Dan didapatkan jawaban flag berbentuk string.
  ![10010](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/901c2cf6-c27d-4abc-ace4-a6230f298c13)

- Ada clue yaitu *attachment: same as creds*. Dari hal tersebut kita coba lihat jawaban dari soal *creds* dan jawabannya berupa passwoard dan username. Disini mencoba mencari jawaban menggunakan aplikasi `FileZilla` dan menginputkan host (dari packet yang didapat creds), password dan username yang didapat pada soal creds.
  ![Screenshot 2024-04-03 220023](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/9d263d8c-9dfb-4b58-b34d-dd5163420486)

- Setelah menginputkan ketiga data tersebut akan muncul tampilan file gambar bernama `mirza` lalu download file tersebut untuk mengetahui isi file
  ![Screenshot 2024-04-03 220042](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/33356fd0-1092-40a2-80c1-10e4ab4c7078)
  
- Setelah didownload ternyata isi dari gambar tersebut ada kalimat `MIO MIRZA`
  ![mirza](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/cb398da0-a127-4ede-b48d-fa68dc9589cc)
  
- Inputkan kata tersebut kedalam jawaban pada `nc 10.15.40.20 10010`. Dan disini jawabannya benar lalu didapatkan format flag yang diberikan.
  ![10010](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/136863633/a38411c5-55a2-4a65-b968-02394a1dbbf7)

## Soal 5 : Fuzz

#### Solusi :
- Pertama-tama download file fuzz dan lakukan command 'nc 10.15.40.20 10001' pada terminal untuk melihat clue soal
- Pada pertanyaan pertama kita disuruh untuk mencari IP address attacker. Kita dapat melakukannya dengan cara melihat IP apa saja yang masuk melalui kolom destination

  ![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/abe3103d-b569-4888-8242-f93c16e6325a)

- Untuk clue soal ke 2 sampai 4 bisa kita temukan dengan cara mem follow TCP stream yang ada. Pada soal 2 web nya merupakan http maka port nya adalah 80. Lalu untuk soal 3 path yang digunakan adalah / atau root. Lalu untuk soal 4 terkait tools yang digunakan adalah ffuf versi 2.

  ![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/9907ca31-6bb6-4a1b-b100-b3dcda2fa1f6)

- Pada soal terakhir mengenai username dan password yang berhasil masuk dapat dilakukan langkah-langkah berikut. Pertama-tama kita cari TCP stream dengan length paling besar karena ketika berhasil login maka program akan mengoutput kode html

  ![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/ea672181-f41c-49f5-b016-ae2d922bf2c5)
  Setelah itu, kita tinggal mencari username dan password mana yang berhasil login

  ![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/f076a99a-fd38-4026-a4e4-d51dd1cb0ac8)

- Untuk keseluruhan pertanyaan dan flag dapat dilihat pada gambar dibawah

  ![Screenshot 2024-03-31 000627](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/6b9d2085-ad84-461a-ba86-1306660b5772)

## Soal 6 : Evidence

#### Solusi :
- Download file dan lakukan command 'nc 10.15.40.20 10002' pada terminal
- Untuk clue pertama dan kedua kita disuruh untuk mencari domain dan web server yang digunakan korban
- Tahapan yang dilakukan adalah buka paket, lalu urutkan kolom length dan lihat dari length yang terbesar. Setelah itu cari satu persatu info yang menampilkan HTTP/1.1 200 OK.

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/eb1cc9be-1d56-44b9-8a52-6b05e6c2a8b9)

- Dapat kita lihat bahwa domain dan web server yang digunakan adalah nanomate-solutions.com dan apache-2.4.56

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/f0ce6da3-3bf7-4b97-9302-b2408ca92e5a)

- Pada soal ke 3 dan ke 4 bisa kita lihat dengan cara mencari stream satu per satu hingga bertemu stream seperti tampilan dibawah

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/1b2225ed-cc37-42c7-b150-2954fb0b5a1c)

- Untuk tampilan soal-soal pada terminal dan flag dapat dilihat pada gambar dibawah

![Screenshot 2024-03-31 000156](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/0a144ca1-6c1f-46fd-95dd-5509e1c735d7)

## Soal 7 : Creds

#### Solusi :
- Pertama-tama download file dan buka 'nc 10.15.40.20 10007' pada terminal
- Untuk clue pertama dan kedua cari username dan password yang berhasil dilakukan oleh hacker
- Caranya adalah dengan mengikuti stream TCP hingga bertemu log yang mengoutput login succesful.

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/b1b1c1cf-d29a-48ae-99dc-dd98a4260a86)

- Untuk flag yang didapatkan seperti dibawah

![Screenshot 2024-03-30 235520](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/26f859de-793a-416d-be74-b4bc871b71a6)

## Soal 8 : Malwleowleo

#### Solusi :
- Buka file yang sama dengan creds lalu masukkan command 'nc 10.15.40.20 10008' di terminal
- Untuk soal yang kita cari hanya nama malware yang dikirim oleh attacker
- Caranya adalah dengan mengikuti stream hingga bertemu dengan nama malwarenya yaitu 'm4L1c10us_W4re.c'

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/e97eb39f-d175-498c-be1b-8b64a35f685d)

- Untuk flag yang didapatkan seperti dibawah

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/d699ef32-0d01-4703-ade5-4c3c32e81f2d) 

## Soal 9 : whoami

#### Solusi :
- Buka file yang sama dengan creds lalu input command 'nc 10.15.40.20 10009' di terminal
- Soal yang dicari adalah nama attacker
- Caranya adalah mengikuti stream hingga bertemu dengan file c yang sus seperti gambar dibawah

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/509b0b38-2d19-4539-9156-b38a0aff9ef3)

- Dapat kita lihat diatas kalau terdapat teks yang sudah terenkripsi
- Langkah selanjutnya adalah mendecode teks tersebut. Teks tersebut ternyata telah di enkripsi menggunakan base64.

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/afd3d96b-75e5-4f87-a457-d7bd89851b87)

- Dapat dilihat bahwa nama sang attacker adalah Paul Atreides
- Untuk tampilan terminal dan flag yang didapat seperti dibawah

![image](https://github.com/rehanasalsabilla/Jarkom-Modul-1-IT12-2024/assets/143682058/54aa5429-34d5-4c8c-a387-3babeb66dc4a)




