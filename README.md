Aplikasi Android yang dapat mendeteksi tingkat kecerahan cahaya menggunakan Ambient Light Sensor, sensor umum bawaan Smartphone berbasis Android. Untuk membuat aplikasi ini, menggunakan class Sensor dan SensorManager dari Android API.
Aplikasi dirancang menggunakan kerangka framework Kotlin Sensors dari Google untuk membuat aplikasi ini. Class SensorActivity digunakan sebagai bentuk inheritance dari Abstract Base Class Activity, digunakan sebagai blueprint untuk membuat class tersebut. Maka dibutuhkan perintah override untuk mendefinisikan ulang fungsi-fungsi dari class abstrak Activity untuk menyesuaikannya dengan aplikasi yang akan dibuat. Berikut ini adalah class dan interface penting yang digunakan pada Aplikasi:
1.	SensorManager Class: SensorManager digunakan untuk mengakses berbagai sensor yang ada pada perangkat Android.
2.	Sensor Class:  Class Sensor digunakan untuk mendapatkan informasi mengenai sensor seperti nama sensor, tipe sensor, resolusi sensor, dan tipe sensor yang ada pada perangkat Android.
3.	SensorEvent class: Class SensorEvent digunakan untuk mendapatkan informasi seperti jepretan waktu (time-stamp), akurasi dan log data sensor.
4.	SensorEventListener interface: Interface ini digunakan untuk melakukan aksi feedback ketika akurasi atau data pada sensor berubah.

Aplikasi sensor cahaya ini akan mendeteksi berapa lux dari cahaya yang dibaca oleh sensor smartphone kemudian menunjukkan nilai tersebut di layar berikut juga levelnya. Dengan skala sebagai berikut:
1. 0 -> "Tidak ada Cahaya sama sekali"
2. in 1..5 -> "Sangat Gelap"
3. in 6..10 -> "Gelap"
4. in 11..25 -> "Remang-remang"
5. in 26..50 -> "Cukup Terang"
6. in 51..1000 -> "Terang"
7. in 1001..5000 -> "Sangat Terang"
8. else -> "Terlalu Terang"

Aplikasi ini belum tentu bisa mendukung semua jenis smartphone khususnya yang tidak memiliki support Android Sensor API atau light ambience sensor. Untuk mencari tahu apakah smartphone yang digunakan mendukung aplikasi ini butuh menggunakan line ini pada onCreate.
Val deviceSensors: List<Sensor> =
sensorManager!!.getSensorList(Sensor.TYPE_ALL)
Log.i("SensorTag", deviceSensors.toString()
