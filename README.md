## Kelompok IT12

# Laporan Resmi Praktikum Jarkom - Modul 1

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
 
  
