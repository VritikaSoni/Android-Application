# Android-Application
Some basics about enabling and desabling Bluetooth.


 <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:tools="http://schemas.android.com/tools"
   android:layout_width="match_parent"
   android:layout_height="match_parent"
   android:background="#024" >
<Button
   android:id="@+id/button1"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:layout_centerHorizontal="true"
   android:layout_centerVertical="true"
   android:onClick="action"
   android:text="Enable and disable bluetooth"
   android:textSize="18sp" />
</RelativeLayout>

Now open your Java file and initialize all objects. Simply use enable() and disable() method and we can use Intent to start bluetooth service which will ask permission to enable bluetooth. The code of android Java file is given below with explanation:


package innosen.com;

import android.os.Bundle;
import android.view.View;
import android.widget.Toast;
import android.app.Activity;
import android.bluetooth.BluetoothAdapter;

public class MainActivity extends Activity {
  BluetoothAdapter bt=null;
  @Override
  protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   setContentView(R.layout.activity_main);
   //initialize bluetooth adapter object
   bt=BluetoothAdapter.getDefaultAdapter();
  }
  //this method will call when we click on button
  public void action(View v)
  {
  //if bluetooth not found
  if(bt==null)
  {
   Toast.makeText(this, "No bluetooth found.."+bt, Toast.LENGTH_LONG).show();
   }
   else
   {
     if(!bt.isEnabled())
    {
     /*****first method to enable bluetooth*****/
     //enable bluetooth without pop-up any dialog box
     bt.enable();
     /*****Second method to enable bluetooth*****/
     //Pop-up dialog box to confirm to enable bluetooth
     /*Intent i=new Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE);
     startActivity(i); */
     //Display blutooth device value on Toast
     Toast.makeText(this, "bluetooth found.."+bt, Toast.LENGTH_LONG).show();
    }
    else
    {
     //disable bluetooth
     bt.disable();
    }
   }
  }
}

Now open your AndroidManifest.xml file to take permission to use bluetooth and changing the state of bluetooth. The code of AndroidManifest.xml fiel is given below:

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
   package="innosen.com"
   android:versionCode="1"
   android:versionName="1.0" >
<uses-sdk
   android:minSdkVersion="10"
   android:targetSdkVersion="10" />
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
<application
   android:allowBackup="true"
   android:icon="@drawable/ic_launcher"
   android:label="@string/app_name"
   android:theme="@style/AppTheme" >
<activity
   android:name="sel.bil.MainActivity"
   android:label="@string/app_name" >
  <intent-filter>
   <action android:name="android.intent.action.MAIN" />
   <category android:name="android.intent.category.LAUNCHER" />
  </intent-filter>
  </activity>
</application>
</manifest>

Now run your project and install .apk of this project in your android mobile and test application. This application can't test on the emulator but will not give error on emulator.

