# A
1. What is amqp?
- Merupakan sebuah protocol yang digunakan untuk menghubungkan ke RabbitMQ server untuk dijalankan di local 
2. What does it mean? guest:guest@localhost:5672 , what is the first guest, and what
is the second guest, and what is localhost:5672 is for?
Untuk `guest:guest` merupakan username dan password  dan untuk `localhost:5762` untuk menghubungkan ke server local atau ke local machine

## Simulation Slow Subscriber
![alt text](image2.png)
Jika dilihat dari chart RabbitMQ diatas, Queued messages mencapai hingga 75, Ini terjadi karena saya melakukan perintah cargo run pada publisher sebanyak 4 kali. Karena publisher mengirim data 5 sekaligus dan saya mengirim data sebanyak 16 kali, maka dengan adanya thread::sleep(ten_millis); maka akan ada (16-1) * 5 data message yang queued.

## Simulate Many Subcriber
![alt text](image6.png)
![alt text](image5.png)

- Grafik pada RabbitMQ menunjukkan adanya burst pada proses publish dari publisher, sementara beberapa subscriber mulai mengonsumsi pesan dalam waktu yang hampir bersamaan. Publisher mengirim pesan lebih cepat daripada kemampuan subscriber untuk memprosesnya, sehingga antrean sempat menumpuk. Namun, antrean tersebut kemudian menurun karena subscriber memproses pesan secara bertahap, meskipun ada delay sleep(1000ms).

Beberapa perbaikan yang dapat dilakukan pada kode publisher dan subscriber antara lain adalah dengan menerapkan method get_handler_action untuk mencegah terjadinya panic serta mengurangi duplikasi kode pada publisher dengan menggunakan loop.

