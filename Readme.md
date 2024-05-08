#  Reflection

### Nama: Zaidan Naufal Ilmi
### Kelas: Adpro-A
### NPM: 2206081761

<details>
<summary>Understanding how it works.</summary>
  
  ![image](https://github.com/bangjai123/Advprog10-Timer/assets/120235144/01022b56-9dfe-4717-9caa-740817b7cf85)

  Pada gambar di atas terlihat bahwa perintah `println!("Zaidan's komputer: hey hey");` dieksekusi terlebih dahulu. Kita dapat melihat bahwa program ini bekerja dengan dimulai saat pemanggila fungsi main(). Dipanggilnya fungsi tersebut membuat spawner dipanggil dan meletakkan block asinkronus berisi perintah `println!("Zaidan's Komputer: howdy!");` dan menunggu selama dua detik dengan menggunakan `TimerFuture`. Setelah meletakkan block tersebut ke dalam executor, program tetap berjalan hingga bertemu perintah `println!("Zaidan's komputer: hey hey");` dan mencetak "Zaidan's komputer: hey hey". Setelah itu, spawner didrop yang berarti executor tidak akan menerima task baru. Lalu, Executor mengambil task dari `ready_queue` nya dan mencetaknya secara berurutan. Dengan demikian, tercetaklah `"Zaidan's Komputer: howdy!"` dan `"Zaidan's Komputer: done"`. Setelah itu, karena tidak ada task lagi, maka eksekusi program selesai.
</details>

<details>
  <summary>Experiment 1.3: Multiple Spawn and removing drop</summary>
  
  Sebelum `drop(spawner);` dihapus
  
![image](https://github.com/bangjai123/Advprog10-Timer/assets/120235144/bd1d1d41-3fab-4571-b924-709ef440b6ce)

  Setelah `drop(spawner);` dihapus
  
<img width="658" alt="Setelah dihapus" src="https://github.com/bangjai123/Advprog10-Timer/assets/120235144/ca49e1ab-df93-430d-9133-5a8d4ec969ea">

  Setelah `drop(spawner);` dikebmbalikan

  ![image](https://github.com/bangjai123/Advprog10-Timer/assets/120235144/32a8838b-2d28-401f-b4cb-2045afdc9e65)

Secara berurutan, gambar ketida gambar di atas merupakan gambar sebelum `drop(spawner);` dihapus, setelah `drop(spawner);` dihapus, dan setelah `drop(spawner);` dikebmbalikan. Dari ketiga gambar di atas, dapat diamati bahwa pada gambar kedua, program tetap berjalan setelah semua task dilakukan. Hal ini berkaitan dengan penghapusan perintah `drop(spawner)`. Perintah `drop(spawner)` sendiri berfungsi agar executor tahu bahwa tidak ada lagi task yang akan dilakukan sehingga program dapat berhenti ketika semua task telah dilakukan. Dengan menghapus `drop(spawner)` program akan terus menunggu adanya task baru. Dengan demikian, program tidak akan berhenti. 
  
</details>
