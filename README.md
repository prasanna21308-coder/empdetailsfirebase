
# Ex.No:1 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by: PRASANNA V
Registeration Number : 212225220072
*/
```
## MainActivity.java:
```

package com.example.firebase1;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

import java.util.HashMap;
import java.util.Map;

public class MainActivity extends AppCompatActivity {

    EditText nameInput, ageInput;
    Button saveButton;
    DatabaseReference databaseReference;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        nameInput = findViewById(R.id.nameInput);
        ageInput = findViewById(R.id.ageInput);
        saveButton = findViewById(R.id.saveButton);

        databaseReference = FirebaseDatabase.getInstance()
                .getReference("Users");

        saveButton.setOnClickListener(v -> saveData());
    }

    private void saveData() {
        String name = nameInput.getText().toString().trim();
        String ageText = ageInput.getText().toString().trim();

        if (name.isEmpty() || ageText.isEmpty()) {
            Toast.makeText(this,
                    "Please enter name and age",
                    Toast.LENGTH_SHORT).show();
            return;
        }

        int age;

        try {
            age = Integer.parseInt(ageText);
            if (age < 0 || age > 150) {
                throw new NumberFormatException();
            }
        } catch (NumberFormatException e) {
            ageInput.setError("Enter a valid age");
            return;
        }

        String userId = databaseReference.push().getKey();

        if (userId == null) {
            Toast.makeText(this, "Unable to create user ID",
                    Toast.LENGTH_SHORT).show();
            return;
        }

        Map<String, Object> user = new HashMap<>();
        user.put("name", name);
        user.put("age", age);

        saveButton.setEnabled(false);

        databaseReference.child(userId).setValue(user)
                .addOnSuccessListener(unused -> {
                    Toast.makeText(this,
                            "Data saved successfully!",
                            Toast.LENGTH_SHORT).show();

                    nameInput.setText("");
                    ageInput.setText("");
                    saveButton.setEnabled(true);
                })
                .addOnFailureListener(e -> {
                    Toast.makeText(this,
                            "Failed: " + e.getMessage(),
                            Toast.LENGTH_LONG).show();

                    saveButton.setEnabled(true);
                });
    }
}

```
## Activity_Main.Xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp"
    android:gravity="center_horizontal"
    android:background="#F5F7FA">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/title_user_details"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="#202124"
        android:layout_marginTop="60dp"
        android:layout_marginBottom="32dp" />

    <EditText
        android:id="@+id/nameInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/hint_enter_name"
        android:inputType="textPersonName"
        android:autofillHints="personGivenName"
        android:padding="14dp" />

    <EditText
        android:id="@+id/ageInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="@string/hint_enter_age"
        android:inputType="number"
        android:importantForAutofill="no"
        android:padding="14dp"
        android:layout_marginTop="16dp" />

    <Button
        android:id="@+id/saveButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/btn_save_to_firebase"
        android:layout_marginTop="24dp" />

</LinearLayout>

```

## OUTPUT

<img width="1920" height="1080" alt="Screenshot (672)" src="https://github.com/user-attachments/assets/4e513f47-19a9-4bb6-98a1-0846fb42e896" />

<img width="1917" height="1078" alt="Screenshot 2026-10-26 091137" src="https://github.com/user-attachments/assets/da0aa709-bc58-403a-8420-ab848f675ba3" />

<img width="1917" height="1078" alt="Screenshot 2026-10-26 091015" src="https://github.com/user-attachments/assets/8b47a029-919d-43c9-8327-368c836d359a" />





## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
