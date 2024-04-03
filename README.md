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
- Dari soal diatas yaitu mencari tau total attemp login, dimana pasti ada percobaan menginputkan password, saya mencoba mencari melalui filter dengan kunci paket ftp karena dari soal diminta untuk mencari response. Lalu di dapatkan kunci lagi yaitu response dengan code 331 dan pesan *please specify the password*
- Lalu kita coba filter dengan lengkap yaitu `ftp.response.code == 331`. Dari pencarian tersebut kita lihat bagian bawah yang menunjukkan `display = 934` dimana itu adalah jumlah semua attemp login yang dimaksut soal.
- Setelah mendapatkan angka tersebut, coba inputkan angka tersebut di dalam jawaban pada `nc 10.15.40.20 10005` dan di dapatkan flag dengan format yang diberikan
  
