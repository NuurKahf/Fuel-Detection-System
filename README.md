# Vehicle Fuel Monitor

Nama : Muhammad Nur Kahfi

NIM : 2402905

Tim : 5 spaCy

# Pendahuluan :

Selamat datang di proyek Sensor Bensin Monitor! Proyek ini dirancang untuk membantu pengendara motor memantau tingkat bensin secara real-time dan memberikan peringatan suara saat bensin hampir habis. Selain itu, sistem ini juga dapat memperkirakan jarak yang dapat ditempuh dengan bensin yang tersisa, sehingga pengguna dapat merencanakan perjalanan dengan lebih baik dan menghindari kehabisan bahan bakar di jalan. Dalam pengembangan proyek ini, kami menggunakan sensor bahan bakar yang terhubung dengan mikrokontroler untuk mengukur level bensin di tangki. Data yang diperoleh kemudian diproses untuk memberikan notifikasi visual dan audio ketika tingkat bensin menurun di bawah ambang batas tertentu. Dengan informasi jarak yang dapat ditempuh, pengendara dapat lebih tenang saat berkendara, mengetahui kapan dan di mana mereka perlu mengisi ulang bensin.

# Deskripsi :

Proyek ini adalah sistem sensor untuk motor yang mengukur level bensin dan memberikan peringatan suara saat bensin hampir habis, karena banyak dari kita yang kurang aware ketika peringatan indikator bensin hanya berkedip, dan akhirnya kita kehabisan bensin di jalan. Selain itu, sistem ini juga memperkirakan jarak yang bisa ditempuh dengan sisa bensin yang ada karena kita tidak tahu sisa bensin kita itu kuat sampai jarak berapa lagi. 

# Fitur-Fitur :
1. Sensor Level Bensin: Mengukur level bensin dalam tangki.
2. Peringatan Suara: Mengeluarkan bunyi peringatan saat bensin mencapai level kritis.
3. Perkiraan Jarak: Menghitung estimasi jarak yang bisa ditempuh dengan sisa bensin.
4. Tampilan Antarmuka Sederhana: Menampilkan informasi level bensin dan estimasi jarak pada layar LCD (opsional).

# Komponen :
1. Sensor Level Bensin: (misal: sensor ultrasonik atau sensor tekanan)
2. Mikrokontroler: (misal: Arduino, Raspberry Pi)
3. Buzzer: Untuk peringatan suara.
4. LCD Display: (opsional) untuk menampilkan informasi.
5. Kabel dan Breadboard: Untuk penyambungan komponen.

# Instalasi :
1. Sambungkan sensor level bensin ke mikrokontroler.
2. Hubungkan buzzer ke pin output pada mikrokontroler.
3. (Opsional) Sambungkan LCD Display untuk menampilkan informasi.
4. Upload codingan ke mikrokontroler.

        #include <Arduino.h>

        const int sensorPin = A0; // Pin sensor level bensin
        const int buzzerPin = 9;   // Pin buzzer
        const float fuelConsumption = 0.05; // Konsumsi bahan bakar per km

        void setup() {
        pinMode(buzzerPin, OUTPUT);
        Serial.begin(9600);
        }

        void loop() {
        int sensorValue = analogRead(sensorPin);
        float fuelLevel = map(sensorValue, 0, 1023, 0, 100); // Konversi ke persen

        if (fuelLevel < 10) { // Batas minimal bensin
        digitalWrite(buzzerPin, HIGH); // Aktifkan buzzer
        Serial.println("Bensin hampir habis!");
        } else {
        digitalWrite(buzzerPin, LOW); // Nonaktifkan buzzer
       }

        float remainingDistance = (fuelLevel / 100) * (1 / fuelConsumption) * 100; // Jarak yang bisa ditempuh
        Serial.print("Jarak sisa: ");
        Serial.print(remainingDistance);
        Serial.println(" km");

        delay(1000); // Pembacaan setiap detik
        }
