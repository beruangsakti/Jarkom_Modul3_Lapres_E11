# Jarkom_Modul3_Lapres_E11

## Soal 1
Pada soal 1, diminta untuk membuat topologi jaringan sesuai dengan gambar yang diberikan.\
Pertama-tama hapus UML sebelumnya dengan menggunakan ``rm`` diikuti nama UML.\
Gunakan ```nano topologi.sh``` dan lakukan konfigurasi sesuai soal\
Lakukan ```bash topologi.sh``` , lalu lakukan login.\
Pada router SURABAYA, ketikkan perintah ```nano /etc/sysctl.conf``` dan hilangkan tanda pagar(#) di depan ```net.ipv4.ip_forward=1``` supaya packet forwarding dapat dilakukan:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1A.PNG)\
Ketikkan ```sysctl -p``` supaya perubahan yang dilakukan akan diaplikasikan\
![gambar1b](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1B.PNG)\
Dilakukan penyetinggan IP pada SURABAYA:\
![gambar1c](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1C.PNG)\
Dilakukan penyetinggan IP pada TUBAN:\
![gambar1d](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1D.PNG)\
Dilakukan penyetinggan IP pada MOJOKERTO:\
![gambar1e](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1E.PNG)\
Dilakukan penyetinggan IP pada MALANG:\
![gambar1f](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1F.PNG)\
Dilakukan penyetinggan IP pada GRESIK:\
![gambar1g](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1G.PNG)\
Dilakukan penyetinggan IP pada SIDOARJO:\
![gambar1h](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1H.PNG)\
Dilakukan penyetinggan IP pada BANYUWANGI:\
![gambar1i](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1I.PNG)\
Dilakukan penyetinggan IP pada MADIUN:\
![gambar1j](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/1J.PNG)\

## Soal 2-6
Diminta agar SURABAYA dijadikan perantara ( DHCP Relay ) antara DHCP Server dan client\
Lakukan ```apt-get update``` pada TUBAN, lalu install isc-dhcp-server dengan ```apt-get install isc-dhcp-server```.\
Lakukan konfigurasi DHCP Server dengan ```nano /etc/default/isc-dhcp-server```, lalu ubah isi dari file dengan menambahkan ```INTERFACES="eth0"``` seperti pada gambar:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2A.PNG)\
Lakukan ```apt-get update``` pada SURABAYA, lalu install dhcp relay dengan ```apt-get install isc-dhcp-relay -y```, kemudian masukkan IP server DHCP (TUBAN):\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2B.PNG)\
Isikan eth yang akan ditanggapi oleh DHCP, yaitu ```eth1 eth2 eth3``` sesuai pada soal:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2C.PNG)\
Kosongkan bagian berikutnya dan tekan tombol ok.\
Pada SURABAYA, ```nano /etc/default/isc-dhcp-relay``` dapat digunakan untuk merubah konfigurasi:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2D.PNG)\
Pada TUBAN, buka file konfigurasi DHCP dengan ```nano /etc/dhcp/dhcpd.conf``` lalu tambahkan sesuai permohonan soal
```
subnet 'NID' netmask 'Netmask' {
    range 'IP_Awal' 'IP_Akhir';
    option routers 'iP_Gateway';
    option domain-name-servers 'DNS_yang_diinginkan';
    default-lease-time 'Waktu(dalam detik)';
    max-lease-time 'Waktu(dalam detik)';
}
```
yang mana berarti untuk client pada subnet 1:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2E.PNG)\
Untuk client pada subnet 3:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/2F.PNG)\
Lakukan restart DHCP server pada TUBAN ```service isc-dhcp-server restart```\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/3A.PNG)\
Pada client GRESIK dan SIDOARJO, lakukan restart network dengan ```service networking restart```, lalu digunakan ```ip a``` untuk memeriksa hasil konfigurasi\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/3B.PNG)\
Berikutnya akan dilakukan pengecekan terhadap BANYUWANGI dan MADIUN\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/4A.PNG)\
Pada client BANYUWANGI dan MADIUN, lakukan restart network dengan ```service networking restart```, lalu digunakan ```ip a``` untuk memeriksa hasil konfigurasi\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/4B.PNG)\
Pengecekan juga dapat dilakukan dengan ```cat /etc/resolv.conf``` pada masing-masing client:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/5B.PNG)\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/5C.PNG)

## Soal 7
Diminta membuat autentikasi user saat hendak mengakses proxy\
Pada MOJOKERTO, lakukan ```apt-get update```, lalu ```apt-get install apache2-utils```.
Buat user baru dengan ```htpasswd -c /etc/squid/passwd userta_e11```, lalu set passwordnya menjadi ```inipassw0rdta_e11```.\
Edit konfigurasi pada squid dengan ```nano /etc/squid/squid.conf``` seperti pada gambar:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/7A.PNG)\
Setelah itu, gunakan browser dan ubah settingan proxy browser. Ketika mencoba untuk mengakses internet, akan muncul halaman autentikasi dimana diperlukan user dan password yang sebelumnya telah diset untuk mengakses internet:\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/7B.PNG)

## Soal 8
Diminta agar akses internet dengan proxy hanya dapat dilakukan pada setiap hari Selasa-Rabu pukul 13.00-18.00. \
Buat file baru yang akan menampung pengaturan tersebut pada MOJOKERTO dengan ```nano /etc/squid/acl.conf```, lalu isikan:
```
acl AVAILABLE_WORKING time TW 13:00-18:00
```
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/8A.PNG)\
Tambahkan pengaturan pada squid.conf dengan membuka ```nano /etc/squid/squid.conf```, lalu tambahkan
```
include /etc/squid/acl/conf
http_access allow USERS TA
http_access deny all
``` 
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/8B.PNG)\
Internet akan dapat diakses pada jam yang telah ditentukan\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/8C.PNG)

## Soal 9
Buka kembali konfigurasi waktu akses dengan ```nano /etc/squid/acl.conf``` lalu tambahkan\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/9A.PNG)\
Buka ```nano /etc/squid/squid.conf``` lalu tambahkan 
```
http_access allow USERS BIMBINGAN01
http_access allow USERS BIMBINGAN02
```
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/9B.PNG)

## Soal 10
Diminta agar ketika hendak mengakses google.com, justru akan di redirect menuju monta.if.its.ac.id\
Buka ```nano /etc/squid/squid.conf``` lalu tambahkan 
```
acl BLKSite dstdomain google.com
deny_info http://monta.if.its.ac.id all
http_reply_access deny BLKSite all
```
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/10A.PNG)\
Simpan, lalu restart squid dengan ```service squid restart``` dan dicoba untuk mengakses google.com\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/10B.PNG)\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/10C.PNG)

## Soal 11
Diminta untuk membuat error page yang khusus\
Gunakan ```cd /usr/share/squid/errors/templates``` untuk mengakses direktori, lalu unduh file error page dengan ```wget 10.151.36.202/ERR_ACCESS_DENIED```\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/11a.PNG)\
Buka ```nano /etc/squid/squid.conf``` lalu ubah \
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/11B.PNG)

## Soal 12
(penjelasan soal)\
Pada MALANG, lakukan ```apt-get update``` dan install bind dengan ```apt-get install bind9 -y```\
Gunakan ```nano /etc/bind/named.conf.local```, lalu isikan 
```
zone "e11.pw" {
 	type master;
	file "/etc/bind/jarkom/e11.pw";
};
```
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/12A.PNG)\
Masukkan konfigurasi pada file e11.pw dengan ```nano /etc/bind/jarkom/e11.pw```\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/12B.PNG)\
Simpan, lalu restart bind dengan ```service bind9 restart```, lalu ubah pengaturan proxy\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/12C.PNG)\
Lakukan ping untuk mengetes apakah berhasil atau belum\
![gambar1a](https://github.com/beruangsakti/Jarkom_Modul3_Lapres_E11/blob/main/Screenshoot/12D.PNG)\

# Kesulitan Selama Pengerjaan
- Pada saat membuat laporan, gambar dari hasil pekerjaan lama tercampur dengan gambar setelah revisi, sehingga mungkin akan terdapat gambar/penjelasan yang berbeda
- Terlambat menyadari bahwa pada client, ```apt-get update``` tidak perlu/tidak bisa dilakukan karena memori, sehingga awal pengerjaan agak terhambat
- Apabila komunikasi antar praktikan kurang, ada kemungkinan ke-2 praktikan mencoba mengakses UML secara bersamaan
- Waktu(DATE) pada UML membuat pengerjaan dan pengecekan soal nomor 8 agak susah dilakukan, terutama karena sebelumnya praktikan belum tahu cara mengubah DATE
- Jumlah Client/Server yang lebih banyak dari biasanya membuat pengesetan untuk soal nomor 1 sedikit lebih lambat apabila tidak membuat catatan sebelumnya
- Diperlukan revisi untuk 1 buah soal
