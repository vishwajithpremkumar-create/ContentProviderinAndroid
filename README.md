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
Developed by: VISHWAJITH P
Registeration Number : 212225220122
*/
```

MainActivity.java
```java
package com.example.exp4;

import android.Manifest;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity{
    Button btnContacts;
    private static final int CONTACT_PERMISSION=101;

    protected void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnContacts=findViewById(R.id.btnContacts);
        btnContacts.setOnClickListener(v->{
            if(ContextCompat.checkSelfPermission(this,Manifest.permission.READ_CONTACTS)
                    != PackageManager.PERMISSION_GRANTED){
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CONTACTS},
                        CONTACT_PERMISSION);
            }
            else{
                loadContacts();
            }
        });
    }

    private void loadContacts(){
        Cursor cursor=getContentResolver().query(
                ContactsContract.CommonDataKinds.Phone.CONTENT_URI,
                null,
                null,
                null,
                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME+" ASC"
        );
        if(cursor!=null){
            Log.d("CONTACT_DETAILS","CONTACT DETAILS");
            while(cursor.moveToNext()){
                String name=cursor.getString(
                        cursor.getColumnIndexOrThrow(
                                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME
                        )
                );

                String phone=cursor.getString(cursor.getColumnIndexOrThrow(
                        ContactsContract.CommonDataKinds.Phone.NUMBER
                ));
                Log.d("CONTACT_DETAILS","Name: "+name);
                Log.d("CONTACT_DETAILS","Phone: "+phone);
                Log.d("CONTACT_DETAILS","---------------");
            }
            cursor.close();
        }
        else{
            Log.d("CONTACT_DETAILS","No Contacts Found");
        }
    }
    public void onRequestPermissionsResult(int requestCode,String[] permissions,
                                           int[] grantResults){
        super.onRequestPermissionsResult(requestCode,permissions,grantResults);
        if(requestCode==CONTACT_PERMISSION){
            if(grantResults.length>0 &&
                    grantResults[0] == PackageManager.PERMISSION_GRANTED){
                loadContacts();
            }
            else{
                Log.d("CONTACT_DETAILS","Permission Denied");
            }
        }
    }
}
```

activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#D500FF"
    tools:context=".MainActivity" >

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="serif"
        android:text="Contact Details"
        android:textColor="#00FFBB"
        android:textSize="34sp"
        app:layout_constraintBottom_toTopOf="@+id/btnContacts"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.822" />

    <Button
        android:id="@+id/btnContacts"
        style="@style/Widget.AppCompat.Button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="340dp"
        android:fontFamily="serif"
        android:text="Get Contacts"
        android:textColor="#4FF60D"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:rippleColor="#AFFA00" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

AndroidManifest.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.READ_CONTACTS"/>
    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Exp4">
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

## OUTPUT

<img width="1920" height="1020" alt="Screenshot 2026-11-04 203916" src="https://github.com/user-attachments/assets/7e3faa06-40e2-49c0-bc07-683376644e33" />

<img width="1920" height="1020" alt="Screenshot 2026-11-04 065851" src="https://github.com/user-attachments/assets/739028f2-cb17-42ba-b19a-65b0d9a1a124" />

<img width="1920" height="1020" alt="Screenshot 2026-11-04 065728" src="https://github.com/user-attachments/assets/1a10f236-0ae1-483d-9ad6-50f3010820ee" />

<img width="1807" height="457" alt="Screenshot 2026-11-04 070123" src="https://github.com/user-attachments/assets/e99e46f5-4108-46e5-a283-6dd866d16d0b" />



## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
