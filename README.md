Subscriber:
1. AMQP adalah singkatan dari Advanced Message Queuing Protocol. Ini adalah protokol jaringan standar terbuka di *application layer* yang dirancang khusus untuk komunikasi middleware yang *message-oriented*. Protokol ini memungkinkan aplikasi *Client* (seperti program subscriber) untuk saling berkomunikasi dan bertukar pesan dengan message broker (seperti RabbitMQ).
2. Format tersebut adalah format URL koneksi standar. guest pertama merupakan username bawaan (default) untuk melakukan autentikasi ke dalam RabbitMQ. guest kedua: Merupakan password bawaan (default) untuk autentikasi ke RabbitMQ. localhost:5672: Menunjukkan lokasi host dan port. localhost berarti message broker berjalan secara lokal, dan 5672 adalah port default yang digunakan oleh RabbitMQ untuk mendengarkan koneksi masuk.

Publisher:
1. Program publisher akan mengirimkan 5 buah data (event) ke message broker dalam satu kali eksekusi. Hal ini dapat dilihat dari kode program publisher di mana terdapat 5 kali pemanggilan fungsi p.publish_event("user_created"... untuk 5 user_id dan nama yang berbeda (Rehema, Budi, Cica, Dira, Emir) secara berurutan.
2. URL yang sama berarti program publisher dan program subscriber sama-sama terhubung ke instans message broker (RabbitMQ) yang sama. Ini  agar arsitektur event-driven ini bisa berjalan dengan benar dengan publisher mempublikasikan pesan ke sebuah tempat dan subscriber mendengarkan di tempat yang sama sehingga pesan dari publisher bisa diterima dan diproses oleh subscriber.

## Running RabbitMQ
![Running RabbitMQ](assets\running-rabbitmq.png)

## Sending and Processing Event
![alt text](assets\send-process-event.png)
Penjelasan: Program publisher me-*send* data berupa UserCreatedEventMessage. Pesan tersebut diterima oleh message broker RabbitMQ. Saat ada subscriber yang aktif di RabbitMQ, maka pesannya akan diberikan ke subscriber tersebut yang lalu diprocess sesuai dengan yang diperlukan.

## Monitoring Chart based on Publisher
![alt text](assets\monitoring-publisher.png)
Penjelasan: Grafik message rates menvisualisasikan rate dari pesan yang diterima oleh RabbitMQ. Di program yang sudah dibuat, pesan ini dikirim oleh program publisher.

## Simulation Slow Subscriber
![alt text](assets\simulate-slow.png)
Penjelasan: Saat subscriber tidak kuat memprocess traffic yang datang, RabbitMQ akan menyimpan sementara sampai bisa diprocess oleh subscriber. Ini terlihat dari grafik queued message yang naik hingga 3. Ini memastikan data yang diterima benar-benar diprocess oleh subscriber dan tidak hilang.

## Running 3 Subscriber
![alt text](assets\3-sub.png)
![alt text](assets\rabbit-3-sub.png)
Penjelasan: Ketika menjalankan tiga program subscriber secara bersamaan, RabbitMQ secara otomatis mendistribusikan pesan-pesan dari publisher kepada ketiga subscriber tersebut secara bergantian. Terlihat bahwa RabbitMQ juga berfungsi ganda sebagai load balancer yang membuat tugas pemrosesan tidak dibebankan pada satu program saja, melainkan dibagi rata ke semua instance subscriber yang aktif. Pendekatan ini sangat penting dalam arsitektur skala besar untuk mempercepat waktu pemrosesan secara keseluruhan dan mencegah sistem kewalahan saat menghadapi antrean data yang besar.

## Reflection Tutorial A
Tutorial A memberikan saya pemahaman praktis yang kuat tentang bagaimana Event-Driven Architecture bekerja. Saya belajar menerapkan Evend-Driven Architechture menggunakan Rust dan RabbitMQ. Selain itu, saya belajar bagaimana memisahkan komponen sistem menjadi publisher yang memproduksi event dan subscriber yang memprosesnya secara asinkron tanpa harus saling terikat erat. Simulasi slow subscriber memberikan saya informasi pentingnya peran message broker sebagai buffer untuk menahan lonjakan traffic. Selain itu, eksperimen dengan menjalankan banyak subscriber mengajarkan saya tentang konsep pembagian beban kerja secara terdistribusi. Secara keseluruhan, pemahaman tentang message queuing ini menjadi fondasi untuk merancang arsitektur microservices yang kuat dan skalabel di kemudian hari.