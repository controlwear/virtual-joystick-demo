# Android Joystick Demo

_This is just a very simple demo which implement this [virtual joystick android Library](https://github.com/controlwear/virtual-joystick-android)._

![Alt text](/android-joystick-demo.png?raw=true "Double Android Joystick")

## Code
For those who don't want to browse the project or files, here it is...

#### Gradle file
Add library to dependencies.

```
dependencies {
    ...
    compile 'io.github.controlwear:virtualjoystick:1.9.2'
}
```

#### Manifest
Force activity to landscape.
```xml
<activity
    android:name=".MainActivity"
    android:screenOrientation="landscape">
    ...
```

####  Layout
Just a couple of TextView and JoystickView to activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="io.github.controlwear.joystickdemo.MainActivity"
    android:padding="16dp">

    <TextView
        android:id="@+id/textView_angle_left"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="0°"/>


    <TextView
        android:id="@+id/textView_strength_left"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@+id/textView_angle_left"
        android:text="0%"/>


    <io.github.controlwear.virtual.joystick.android.JoystickView
        xmlns:custom="http://schemas.android.com/apk/res-auto"
        android:id="@+id/joystickView_left"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_margin="32dp"
        android:background="@drawable/joystick_background"
        custom:JV_buttonImage="@drawable/pink_ball"
        custom:JV_fixedCenter="false"/>


    <TextView
        android:id="@+id/textView_angle_right"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:text="0°"/>


    <TextView
        android:id="@+id/textView_strength_right"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_below="@+id/textView_angle_right"
        android:text="0%"/>


    <TextView
        android:id="@+id/textView_coordinate_right"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_below="@+id/textView_strength_right"
        android:text="x050:x050"/>


    <io.github.controlwear.virtual.joystick.android.JoystickView
        xmlns:custom="http://schemas.android.com/apk/res-auto"
        android:id="@+id/joystickView_right"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:layout_marginTop="64dp"
        custom:JV_borderWidth="8dp"
        custom:JV_backgroundColor="#009688"
        custom:JV_borderColor="#00796B"
        custom:JV_buttonColor="#FF6E40"/>

</RelativeLayout>
```

#### Java
MainActivity.java
```java
public class MainActivity extends AppCompatActivity {


    private TextView mTextViewAngleLeft;
    private TextView mTextViewStrengthLeft;

    private TextView mTextViewAngleRight;
    private TextView mTextViewStrengthRight;
    private TextView mTextViewCoordinateRight;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mTextViewAngleLeft = (TextView) findViewById(R.id.textView_angle_left);
        mTextViewStrengthLeft = (TextView) findViewById(R.id.textView_strength_left);

        JoystickView joystickLeft = (JoystickView) findViewById(R.id.joystickView_left);
        joystickLeft.setOnMoveListener(new JoystickView.OnMoveListener() {
            @Override
            public void onMove(int angle, int strength) {
                mTextViewAngleLeft.setText(angle + "°");
                mTextViewStrengthLeft.setText(strength + "%");
            }
        });


        mTextViewAngleRight = (TextView) findViewById(R.id.textView_angle_right);
        mTextViewStrengthRight = (TextView) findViewById(R.id.textView_strength_right);
        mTextViewCoordinateRight = findViewById(R.id.textView_coordinate_right);

        final JoystickView joystickRight = (JoystickView) findViewById(R.id.joystickView_right);
        joystickRight.setOnMoveListener(new JoystickView.OnMoveListener() {
            @SuppressLint("DefaultLocale")
            @Override
            public void onMove(int angle, int strength) {
                mTextViewAngleRight.setText(angle + "°");
                mTextViewStrengthRight.setText(strength + "%");
                mTextViewCoordinateRight.setText(
                        String.format("x%03d:y%03d",
                                joystickRight.getNormalizedX(),
                                joystickRight.getNormalizedY())
                );
            }
        });
    }
}
```

#### Images
Here are the two images to put in drawable.

![Alt text](/app/src/main/res/drawable/pink_ball.png?raw=true "Android Joystick Button")
![Alt text](/app/src/main/res/drawable/joystick_background.png?raw=true "Android Joystick Background")

### And that's it.
The (quick) documentation of the library is [here](https://github.com/controlwear/virtual-joystick-android).
