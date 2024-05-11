# Text-to-Speech-Android-Studio

## Aim:
Create an Android app that converts text entered by the user into speech output.

## Algorithm:

1. Initialize Project: Create a new project in Android Studio.
2. Design Layout: Set up the layout in activity_main.xml with an EditText for user input, a Button to trigger conversion, and a TextView to display converted speech.
3. Initialize Text-to-Speech Engine: In MainActivity.java, initialize the TextToSpeech engine and set its language.
4. Handle Button Click: Implement an OnClickListener for the Button to convert the text entered by the user to speech.
5. Speak Text: Use the TextToSpeech engine to convert the text entered by the user into speech.
6. Display Result: Show the converted speech in the TextView.

## Program Files:
### activity_main.xml:
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter text to convert"
        android:layout_margin="16dp"/>

    <Button
        android:id="@+id/convertButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Convert"
        android:layout_below="@id/editText"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="16dp"/>

    <TextView
        android:id="@+id/speechText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="18sp"
        android:textColor="@android:color/black"
        android:layout_below="@id/convertButton"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="16dp"/>
</RelativeLayout>
```
### MainActivity.java:
```java
import android.os.Bundle;
import android.speech.tts.TextToSpeech;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    private EditText editText;
    private Button convertButton;
    private TextView speechText;
    private TextToSpeech textToSpeech;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = findViewById(R.id.editText);
        convertButton = findViewById(R.id.convertButton);
        speechText = findViewById(R.id.speechText);

        textToSpeech = new TextToSpeech(getApplicationContext(), new TextToSpeech.OnInitListener() {
            @Override
            public void onInit(int status) {
                if (status != TextToSpeech.ERROR) {
                    textToSpeech.setLanguage(Locale.US);
                }
            }
        });

        convertButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String text = editText.getText().toString();
                textToSpeech.speak(text, TextToSpeech.QUEUE_FLUSH, null);
                speechText.setText(text);
            }
        });
    }

    @Override
    protected void onDestroy() {
        if (textToSpeech != null) {
            textToSpeech.stop();
            textToSpeech.shutdown();
        }
        super.onDestroy();
    }
}
```

## Output:
### Screenshot:
![image](https://github.com/BalaSathiesh/Text-to-Speech-Android-Studio/assets/128462891/557e1142-7ddb-4a5e-a9a0-1982a46ea53d)

### Demo Video:
![YtYoutubeGIF](https://github.com/BalaSathiesh/Text-to-Speech-Android-Studio/assets/128462891/b416b36c-98a0-4bfd-9d15-afa163bcc6d0)
https://youtu.be/5LJk_z40nkI

## Result:
The Android app successfully converts text entered by the user into speech output. Users can input any text into the EditText field, click the "Convert" button, and hear the text spoken aloud. Additionally, the converted speech is displayed in a TextView for reference. The app provides a simple and intuitive interface for text-to-speech conversion.



