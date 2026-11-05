
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by:SACHIN J M
Registeration Number :212225100041
*/
```

## OUTPUT
###Activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp"
    android:background="#FFFFFF">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="CONTACT DETAILS!!"
        android:textSize="25sp"
        android:textStyle="bold"
        android:textColor="#000000"
        android:gravity="center"
        android:padding="15dp" />

    <Button
        android:id="@+id/btnContacts"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="GET CONTACTS"
        android:textSize="18sp" />

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="15dp">

        <TextView
            android:id="@+id/txtContacts"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Contact details will appear here"
            android:textSize="18sp"
            android:textColor="#000000"
            android:padding="10dp" />

    </ScrollView>

</LinearLayout>

```
###MainActivity.java
```

package com.example.contactdetails;

import android.Manifest;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    Button btnContacts;
    TextView txtContacts;

    private static final int CONTACT_PERMISSION = 100;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnContacts = findViewById(R.id.btnContacts);
        txtContacts = findViewById(R.id.txtContacts);

        btnContacts.setOnClickListener(v -> {

            if (ContextCompat.checkSelfPermission(this,
                    Manifest.permission.READ_CONTACTS)
                    != PackageManager.PERMISSION_GRANTED) {

                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CONTACTS},
                        CONTACT_PERMISSION);

            } else {
                getContacts();
            }
        });
    }

    private void getContacts() {

        StringBuilder contacts = new StringBuilder();

        Cursor cursor = getContentResolver().query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null,
                null,
                null,
                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME
        );

        if (cursor != null) {

            int nameIndex = cursor.getColumnIndex(
                    ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME);

            int numberIndex = cursor.getColumnIndex(
                    ContactsContract.CommonDataKinds.Phone.NUMBER);

            while (cursor.moveToNext()) {

                String name = cursor.getString(nameIndex);
                String number = cursor.getString(numberIndex);

                contacts.append("Name: ").append(name)
                        .append("\nPhone: ").append(number)
                        .append("\n\n");
            }

            cursor.close();
        }

        if (contacts.length() == 0) {
            txtContacts.setText("No contacts found!");
        } else {
            txtContacts.setText(contacts.toString());
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           String[] permissions, int[] grantResults) {

        super.onRequestPermissionsResult(requestCode,
                permissions, grantResults);

        if (requestCode == CONTACT_PERMISSION) {

            if (grantResults.length > 0 &&
                    grantResults[0] == PackageManager.PERMISSION_GRANTED) {

                getContacts();

            } else {
                Toast.makeText(this,
                        "Permission Denied",
                        Toast.LENGTH_SHORT).show();
            }
        }
    }
}

```
###AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.READ_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.CONTACTDETAILS">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:windowSoftInputMode="adjustResize">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
<img width="1807" height="895" alt="Screenshot 2026-11-05 091619" src="https://github.com/user-attachments/assets/674b44df-af71-40c1-a291-aae112e39750" />
<img width="1917" height="793" alt="Screenshot 2026-11-05 091414" src="https://github.com/user-attachments/assets/35f96f54-e182-423e-9c6c-ac93351bfc6a" />
<img width="1917" height="1070" alt="Screenshot 2026-11-05 085311 - Copy" src="https://github.com/user-attachments/assets/ce2c6297-aa67-4b64-aa4b-6dd34366ab9d" />
<img width="1916" height="1016" alt="Screenshot 2026-11-05 085301" src="https://github.com/user-attachments/assets/d5dbef94-e141-45fc-bf86-81ef5e1555c3" />

## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
