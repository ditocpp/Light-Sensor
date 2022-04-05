Merupakan aplikasi Android yang mendeteksi adanya cahaya menggunakan sensor bawaan Smartphone berbasis Android. Untuk membuat aplikasi ini, menggunakan class Sensor dan SensorManager dari Android API. Aplikasi ini akan menampilkan display animasi ketika tidak ada cahaya. Sensor yang digunakan adalah Android Ambient Light Sensor.
Aplikasi dirancang menggunakan kerangka framework Kotlin Sensors dari Google untuk membuat aplikasi ini. Class SensorActivity digunakan sebagai bentuk inheritance dari Abstract Base Class Activity, digunakan sebagai blueprint untuk membuat class tersebut. Maka dibutuhkan perintah override untuk mendefinisikan ulang fungsi-fungsi dari class abstrak Activity untuk menyesuaikannya dengan aplikasi yang akan dibuat. Berikut ini adalah class dan interface penting yang digunakan pada Aplikasi:
1.	SensorManager Class: SensorManager digunakan untuk mengakses berbagai sensor yang ada pada perangkat Android.
2.	Sensor Class:  Class Sensor digunakan untuk mendapatkan informasi mengenai sensor seperti nama sensor, tipe sensor, resolusi sensor, dan tipe sensor yang ada pada perangkat Android.
3.	SensorEvent class: Class SensorEvent digunakan untuk mendapatkan informasi seperti jepretan waktu (time-stamp), akurasi dan log data sensor.
4.	SensorEventListener interface: Interface ini digunakan untuk melakukan aksi feedback ketika akurasi atau data pada sensor berubah.
class SensorActivity : Activity(), SensorEventListener {
    private lateinit var sensorManager: SensorManager
    private var mLight: Sensor? = null

    public override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.main)

        sensorManager = getSystemService(Context.SENSOR_SERVICE) as SensorManager
        mLight = sensorManager.getDefaultSensor(Sensor.TYPE_LIGHT)
    }

    override fun onAccuracyChanged(sensor: Sensor, accuracy: Int) {
        // Do something here if sensor accuracy changes.
    }

    override fun onSensorChanged(event: SensorEvent) {
        // The light sensor returns a single value.
        // Many sensors return 3 values, one for each axis.
        val lux = event.values[0]
        // Do something with this sensor value.
    }

    override fun onResume() {
        super.onResume()
        mLight?.also { light ->
            sensorManager.registerListener(this, light, SensorManager.SENSOR_DELAY_NORMAL)
        }
    }

    override fun onPause() {
        super.onPause()
        sensorManager.unregisterListener(this)
    }
}
Sumber: https://developer.android.com/guide/topics/sensors/sensors_overview
Aplikasi sensor cahaya ini akan mendeteksi berapa lux dari cahaya yang dibaca oleh sensor smartphone kemudian menunjukkan nilai tersebut di layar berikut juga levelnya. Dengan skala sebagai berikut:
            0 -> "Tidak ada Cahaya sama sekali"
            in 1..5 -> "Sangat Gelap"
            in 6..10 -> "Gelap"
            in 11..25 -> "Remang-remang"
            in 26..50 -> "Cukup Terang"
            in 51..1000 -> "Terang"
            in 1001..5000 -> "Sangat Terang"
            else -> "Terlalu Terang"
Aplikasi ini belum tentu bisa mendukung semua jenis smartphone khususnya yang tidak memiliki support Android Sensor API atau light ambience sensor. Untuk mencari tahu apakah smartphone yang digunakan mendukung aplikasi ini butuh menggunakan line ini pada onCreate.
Val deviceSensors: List<Sensor> =
sensorManager!!.getSensorList(Sensor.TYPE_ALL)
Log.i("SensorTag", deviceSensors.toString()
