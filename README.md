# Modul 9 - High Level Networking
**Samuel Farrel Bagasputra - 2206826614 - Adpro C**
<br><br>

## Reflection
1. ***What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?***
    - **Unary RPC** adalah metode yang paling sederhana, di mana client mengirimkan satu request dan server merespons dengan satu response. Unary RPC cocok digunakan ketika client hanya perlu mengirimkan satu request dan menerima satu response.
    - **Server streaming RPC** adalah metode di mana client mengirimkan satu request dan server merespons dengan stream data. Server streaming RPC cocok digunakan ketika client membutuhkan data dalam jumlah besar dari server.
    - **Bi-directional streaming RPC** adalah metode di mana client dan server saling mengirimkan stream data. Bi-directional streaming RPC cocok digunakan ketika client dan server membutuhkan komunikasi dua arah yang real-time.<br><br>

2. ***What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?***
    - **Authentication** : gRPC mendukung beberapa metode autentikasi, seperti SSL/TLS, OAuth2, token-based authentication, ataupun sesimpel username dan password.
    - **Authorization** : Diperlukan adanya pemberian permission yang sesuai setelah melewati proses autentikasi. gRPC mendukung beberapa metode otorisasi, seperti role-based access control (RBAC) dan attribute-based access control (ABAC).
    - **Data Encryption** : Data yang ditransfer melalui network perlu dienkripsi untuk melindungi dari tampering dan eavesdropping. Untuk mengamankan gRPC service, kita dapat menggunakan SSL/TLS untuk mengenkripsi data yang ditransfer.<br><br>

3. ***What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?***
    - **Concurrency** : Client mungkin mengirim dan menerima pesan yang banyak secara bersamaan, sehingga kita perlu memperhatikan concurrency ketika mengimplementasikan bidirectional streaming di Rust gRPC.
    - **Error Handling** : Rust memiliki sistem error handling yang ketat, sehingga kita perlu memperhatikan error handling ketika mengimplementasikan bidirectional streaming di Rust GPRC.
    - **Message Ordering** : Terdapat kemungkinan adanya hambatan yang terjadi ketika proses berjalan, sehingga kita perlu memperhatikan urutan pesan tetap sesuai ketika mengimplementasikan bidirectional streaming di Rust GPRC.<br><br>

4. ***What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?***
    - **Advantages** : 
        - Convenience : `ReceiverStream` menyederhanakan penanganan streaming dengan memberikan wrapper untuk `tokio::sync::mpsc::Receiver`, membuatnya lebih mudah untuk bekerja dengan asynchronous streams.
        - Compatibility : `ReceiverStream` kompatibel dengan `tonic::Streaming`, sehingga kita dapat menggunakan `ReceiverStream` untuk mengirimkan stream response di Rust gRPC services.
        - Error Handling : Dengan return hasil yang wrapped oleh `ReceiverStream`, kita dapat lebih mudah melakukan error handling pada stream response.
    - **Disadvantages** :
        - Error Handling : `ReceiverStream` tidak memberikan error handling bawaan sehingga kita perlu mengimplementasikan error handling secara manual ketika menggunakan `ReceiverStream`.
        - Dukungan : `ReceiverStream` hanya mendukung koneksi satu arah, sehingga tidak cocok digunakan untuk bidirectional streaming di Rust gRPC services.<br><br>

5. ***In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?***
    - Mendefinisikan service dan message pada file `.proto` yang berbeda sehingga message definition dapat digunakan kembali oleh service lain.
    - Menentukan reusable function dan struct pada file `.rs` yang berbeda sehingga dapat digunakan oleh service lain.
    - Mengatur implementasi service dan message pada file `.rs` yang berbeda sehingga memudahkan dalam melakukan maintenance dan extensibility. Hal ini memungkinkan penambahan, perubahan, atau penghapusan fungsionalitas tanpa mempengaruhi kode lain dalam sistem Anda.<br><br>

6. ***In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?***
    - Menambahkan fungsi-fungsi lain yang diperlukan untuk melakukan payment processing logic yang lebih kompleks.
    - Menambahkan error handling dan input validation untuk menangani error yang mungkin terjadi selama proses payment processing.
    - Menambahkan unit tests untuk memastikan bahwa payment processing logic berjalan dengan baik.
    - Menambahkan logging untuk memudahkan dalam melakukan debugging dan monitoring terhadap payment processing logic.
    - Koneksi langsung dengan database untuk menyimpan dan membaca informasi yang diperlukan untuk melakukan transaksi.<br><br>

7. ***What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?***
    - Penggunaan gRPC sebagai protokol komunikasi memiliki banyak keuntungan, seperti interoperabilitas antar layanan yang ditulis dalam berbagai bahasa pemrograman dan kinerja yang lebih efisien berkat penggunaan Protocol Buffers (protobuf) sebagai format pesan. Selain itu, dukungan untuk streaming dan desain berbasis kontrak juga memperkuat interaksi antara client dan server.
    - Namun, ada beberapa hambatan dan tantangan yang perlu diatasi terkait dengan penggunaan gRPC seperti kompleksitas setup, keterbatasan browser, interoperabilitas dengan Sistem yang Hanya Mendukung REST<br><br>

8. ***What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?***
    - **Advantages** :
        - Multiplexing : HTTP/2 mendukung multiplexing, yang memungkinkan multiple requests dan responses untuk dikirim secara bersamaan melalui satu koneksi TCP. Hal ini dapat meningkatkan kinerja dan efisiensi komunikasi antara client dan server.
        - Header Compression : HTTP/2 menggunakan HPACK untuk mengompresi header request dan response, yang dapat mengurangi overhead data dan meningkatkan kecepatan transfer data.
        - Server Push : HTTP/2 mendukung server push, yang memungkinkan server untuk mengirimkan resource tambahan kepada client tanpa diminta. Hal ini dapat meningkatkan performa aplikasi dengan mengurangi latensi.
    
    - **Disadvantages** :
        - Kompleksitas : HTTP/2 memiliki kompleksitas yang lebih tinggi dibandingkan HTTP/1.1, yang dapat membuat debugging dan troubleshooting lebih sulit.
        - Dukungan : Meskipun HTTP/2 semakin populer, masih ada beberapa platform dan library yang belum mendukung HTTP/2 sepenuhnya, yang dapat menyulitkan integrasi dengan sistem yang sudah ada.
        - Overhead : Meskipun header compression dapat mengurangi overhead data, namun ada beberapa kasus di mana overhead HTTP/2 lebih besar daripada HTTP/1.1, terutama untuk request-response yang kecil.<br><br>

9. ***How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?***
    - **REST APIs** : REST APIs menggunakan model request-response, di mana client mengirimkan request ke server dan server merespons dengan satu response. REST APIs tidak mendukung streaming, sehingga komunikasi real-time dan responsiveness terbatas.
    - **gRPC** : gRPC mendukung bidirectional streaming, di mana client dan server dapat saling mengirimkan stream data secara real-time. Hal ini memungkinkan komunikasi real-time dan responsiveness yang lebih baik daripada REST APIs, terutama untuk aplikasi yang membutuhkan komunikasi dua arah yang cepat dan efisien.<br><br>

10. ***What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?***
    - **Schema-based approach of gRPC** : gRPC menggunakan Protocol Buffers sebagai format pesan, yang memungkinkan definisi schema untuk message dan service. Hal ini memungkinkan validasi data secara otomatis dan interoperabilitas yang lebih baik antara client dan server.
    - **Schema-less nature of JSON in REST API payloads** : REST APIs menggunakan JSON sebagai format payload, yang memiliki sifat schema-less. Hal ini memberikan fleksibilitas dalam struktur data, namun juga dapat menyebabkan masalah validasi dan interoperabilitas antara client dan server.
    - **Implications** : Pendekatan berbasis skema dari gRPC memungkinkan validasi data otomatis dan interoperabilitas yang lebih baik, namun memerlukan definisi skema yang lebih ketat. Sementara itu, sifat tanpa skema dari JSON memberikan fleksibilitas dalam struktur data, namun dapat menyebabkan masalah validasi dan interoperabilitas jika tidak dikelola dengan baik. Pemilihan antara kedua pendekatan ini harus mempertimbangkan kebutuhan dari aplikasi yang dikembangkan.<br><br>
