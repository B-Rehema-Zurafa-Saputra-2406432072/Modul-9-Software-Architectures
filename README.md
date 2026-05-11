Subscriber:
1. AMQP adalah singkatan dari Advanced Message Queuing Protocol. Ini adalah protokol jaringan standar terbuka di *application layer* yang dirancang khusus untuk komunikasi middleware yang *message-oriented*. Protokol ini memungkinkan aplikasi *Client* (seperti program subscriber) untuk saling berkomunikasi dan bertukar pesan dengan message broker (seperti RabbitMQ).
2. Format tersebut adalah format URL koneksi standar. guest pertama merupakan username bawaan (default) untuk melakukan autentikasi ke dalam RabbitMQ. guest kedua: Merupakan password bawaan (default) untuk autentikasi ke RabbitMQ. localhost:5672: Menunjukkan lokasi host dan port. localhost berarti message broker berjalan secara lokal, dan 5672 adalah port default yang digunakan oleh RabbitMQ untuk mendengarkan koneksi masuk.

Publisher:
1. Program publisher akan mengirimkan 5 buah data (event) ke message broker dalam satu kali eksekusi. Hal ini dapat dilihat dari kode program publisher di mana terdapat 5 kali pemanggilan fungsi p.publish_event("user_created"... untuk 5 user_id dan nama yang berbeda (Rehema, Budi, Cica, Dira, Emir) secara berurutan.
2. URL yang sama berarti program publisher dan program subscriber sama-sama terhubung ke instans message broker (RabbitMQ) yang sama. Ini  agar arsitektur event-driven ini bisa berjalan dengan benar dengan publisher mempublikasikan pesan ke sebuah tempat dan subscriber mendengarkan di tempat yang sama sehingga pesan dari publisher bisa diterima dan diproses oleh subscriber.

## Running RabbitMQ
![Running RabbitMQ](assets\running-rabbitmq.png)