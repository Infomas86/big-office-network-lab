# Troubleshooting Log - Big Office Network Lab

## 1. Error Interface Range pada SW-CORE
- **Masalah:** Saat memasukkan perintah `interface range gigabitEthernet1/0/2-6`, muncul error `interface range not validated - command rejected`.
- **Penyebab:** 
  1. Kurangnya spasi sebelum dan sesudah tanda hubung (`-`).
  2. Port pada switch SW-CORE ternyata menggunakan interface `FastEthernet`, bukan `GigabitEthernet`.
- **Solusi:** Mengganti perintah dengan menambahkan spasi dan menggunakan interface yang tepat sesuai fisik switch, yaitu `interface range FastEthernet0/2 - 6`.

## 2. Invalid Input (Typo) pada SW-FIN
- **Masalah:** Muncul pesan `% Invalid input detected at '^' marker` saat mengkonfigurasi mode access.
- **Penyebab:** Terjadi salah ketik (typo), perintah diketik `swichport mode access` (kurang huruf 't').
- **Solusi:** Mengetik ulang perintah dengan ejaan yang benar: `switchport mode access`.

## 3. Kesalahan Pembuatan VLAN pada SW-FIN
- **Masalah:** Terdapat peringatan `% Access VLAN does not exist. Creating vlan 20`.
- **Penyebab:** Salah memasukkan ID VLAN untuk SW-FIN, yang diketik adalah VLAN 20, padahal seharusnya VLAN 30.
- **Solusi:** Langsung menimpa konfigurasi sebelumnya dengan perintah yang benar: `switchport access vlan 30` di dalam mode interface range.