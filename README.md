## TO-DO-LIST
## Aim:
The aim of the provided program is to create a simple to-do list application for Android with the ability to add tasks. Additionally, the program includes an animation XML file that creates a shaking effect on an EditText field if the user attempts to add an empty task.

## Algorithm:
1.Initialize the layout of the main activity, including EditText for inputting tasks, a Button to add tasks, and a ListView to display tasks.

2.Set up the ArrayList and ArrayAdapter to store and display the tasks in the ListView.

3.Load a shake animation from the XML resource file to provide visual feedback if the user tries to add an empty task.

4.Implement a click listener for the "Add Task" button.

5.Retrieve the task text from the EditText.

6.If the task is not empty, add it to the ArrayList, update the adapter, and clear the EditText.

7.If the task is empty, apply the shake animation to the EditText and display a Toast message prompting the user to enter a task.

8.Run the Android application, allowing users to input tasks, add them to the list, and observe the shaking animation when attempting to add an empty task.

## Program:

##  Main_Activity.java:
```java
package com.example.todolist;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
        private ArrayList<String> tasksList;
        private ArrayAdapter<String> tasksAdapter;
        private EditText editTextTask;
        private ListView listViewTasks;
        private Animation shakeAnimation;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.activity_main);

                editTextTask = findViewById(R.id.editTextTask);
                Button buttonAddTask = findViewById(R.id.buttonAddTask);
                listViewTasks = findViewById(R.id.listViewTasks);

                tasksList = new ArrayList<>();
                tasksAdapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1, tasksList);
                listViewTasks.setAdapter(tasksAdapter);

                shakeAnimation = AnimationUtils.loadAnimation(this, R.anim.shake);

                buttonAddTask.setOnClickListener(new View.OnClickListener() {
                        @Override
                        public void onClick(View v) {
                                String task = editTextTask.getText().toString().trim();
                                if (!task.isEmpty()) {
                                        tasksList.add(task);
                                        tasksAdapter.notifyDataSetChanged();
                                        editTextTask.setText("");
                                } else {
                                        editTextTask.startAnimation(shakeAnimation);
                                        Toast.makeText(MainActivity.this, "Enter a task", Toast.LENGTH_SHORT).show();
                                }
                        }
                });
        }
}

``` 
## Activity_main.xml:
```java

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.google.android.material.textfield.TextInputLayout
        android:id="@+id/textInputLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="16dp"
        app:layout_constraintTop_toTopOf="parent">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/editTextTask"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Enter task"
            android:inputType="text"/>
    </com.google.android.material.textfield.TextInputLayout>

    <Button
        android:id="@+id/buttonAddTask"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/textInputLayout"
        android:layout_alignParentEnd="true"
        android:layout_marginEnd="16dp"
        android:layout_marginTop="16dp"
        android:text="Add Task" />

    <ListView
        android:id="@+id/listViewTasks"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/buttonAddTask"
        android:layout_margin="16dp"
        android:layout_marginTop="8dp"
        android:clipToPadding="false"
        android:divider="@null"
        android:dividerHeight="0dp" />
</RelativeLayout>
```
## Shake.xml
```java
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <translate
        android:fromXDelta="-10"
        android:toXDelta="10"
        android:interpolator="@android:anim/cycle_interpolator"
        android:duration="50"
        android:repeatCount="5"/>

</set>
```
## Output:
![image](https://github.com/karthick960/TO-DO-LIST/assets/121215938/1df640c2-0bbf-4d3c-9b70-b56f1c10ac86)


## Result:
The result is a functional to-do list application with basic task management functionality. Users can easily add tasks and receive visual feedback if they try to add an empty task. The shaking animation draws attention to the input field, improving the user experience by indicating where the issue lies.
