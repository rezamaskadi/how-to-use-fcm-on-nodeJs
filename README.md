# How to title?

How to setup FCM on nodeJs using fcm-push modules

# Created by ?

Muhamad Reza Anugrah Maskadi, Technical Lead Divisi Web
PT. GITS Indonesia

# Created at ?

15 Mei 2018

# Update by ?

1. --

# Updated at ?

1. --

# Type ? 

Panduan atau tutorial

# Description ?

How - To Setup FCM bisa digunakan sebagai panduan untuk setup firebase untuk pemula,
disini disertakan panduan dan screenshot yang semoga dapat membantu.
kritik dan saran atau mau menambahkan bisa dan silahkan saja.
Semangat menulis ya guys!

# How - to?
## why ?

Firebase atau FCM banyak digunakan saat ini karena sangat berhubungan dengan notifikasi baik pada aplikasi mobile atau aplikasi website

## How-to-use ?

### How-to-get ServerKey
1. Syarat yang wajib yaitu punya akun gmail ya dan kalau sudah punya silahkan login gmail nya.
2. Setelah itu bisa akses firebase console https://console.firebase.google.com

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856384/how-to1.png)

3. Setelah itu buat satu project dengan mengisi data berikut

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856386/how-to2.png)
    
4. Masuk ke dalam project yang sudah dibuat

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526942034/how-to3-1.png)

5. Masuk pada halaman setting dengan klik pada icon setting lalu pilih option project setting

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856384/how-to4.png)
    
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856384/how_-_to_5.png)
    
6. Pilih toolsbar 'CloudMessaging' dan dapatkan 'Serverkey'

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526859509/how-to6.png)

### How-to-implement on NodeJs (Menggunakan framework GITS)
1. Pertama instal modules fcm-push dengan melakukan 'npm install fcm-push --save'
2. Simpan ServerKey yang sudah didapat di dalam .env dan environment_variables

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856384/how-to7.png)

3. Tambahkan 'FCMPUSH: require('fcm-push')' pada ../configs/modules.js

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526856383/how-to8.png)

4. Setelah itu lakukan inisiasi module FCMPUSH dengan menambahkan ServerKey yang sebelum nya sudah di dapatkan,
   dengan menambahkan code seperti berikut "var FCM = new MODULES.FCMPUSH([SERVER KEY HERE]);" atau sample "TOOLS.FCM = new MODULES.FCMPUSH(process.env.SETTINGS_FCM_SERVERKEY);"

5. Lalu cara menggunakan nya seperti berikut, tambahkan inisiasi FCM di dalam file yang akan disimpan code notification misal 'NotificationInterface'
   "let FCM = TOOLS.FCM;"

6. Terakhir lakukan code untuk FCM dengan format sebagai berikut

        let message = {
            to: token, // Token untuk tujuan device atau target device yang akan dikirimkan notification
            collapse_key: 'collapse_key', // Colapse key untuk menggabungan dua atau lebih notification yang memiliki colapsekey yang sama
            data: { // Data yang akan digunakan
                your_custom_data_key: 'Notification', // Data_key, optional
                nick: name, // Nick, optional
                body: body, // Body, data payload yang akan dikirimkan atau digunakan oleh mobile atau frontEnd
                name: name // Name, optional
            },
            notification: { // referensi notification, sebetulnya fungsi nya sama dengan object-data, namun disarankan tetap mencantumkan object notification 
                title: 'Notification', // Title, judul notification
                body: body, // Body, Body, data payload yang akan dikirimkan atau digunakan oleh mobile atau frontEnd
                name: name // Name, optional
            }
        };

        FCM.send(message, function (err, response) { //FCM.send code atau intruksi untuk melakukan send notification
            if (err) { //Validasi error
                next(err, null); //return error optional, anda bisa melakukan custom untuk ini
                console.log('Failed to send push notification : ', err); //log error for check log in server or local, anda bisa melakukan custom untuk ini
            } else {
                next(null, {result: previousData.result}, true); //return success optional, anda bisa melakukan custom untuk ini
                console.log('Success send push notification : ', response); //log success for check log in server or local, anda bisa melakukan custom untuk ini
            }
        });

# Link

https://firebase.google.com/docs/admin/setup?hl=id
and
https://firebase.google.com/docs/cloud-messaging/server?hl=id

NodeModules for FCM :
https://www.npmjs.com/package/fcm-push