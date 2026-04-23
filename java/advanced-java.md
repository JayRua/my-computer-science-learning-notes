# Java Advanced Programming Notes

Higher Diploma in Science in Computing, Java Module

This document summarises the core Java concepts I learned in the Advanced Java module.

Topics covered:  
	- ArrayLists  
	- JavaFX GUI development  
	- JavaFX layouts and controls  
	- Event-driven programming  
	- Handling user input from GUI controls  

## Week 1 – ArrayLists
ArrayLists are dynamic containers from the java.util package used to store collections of objects.
Unlike arrays, ArrayLists can grow or shrink during runtime.
Key features:
- Stores objects only (not primitive types).
- Resizable container.
- Provides built-in methods for manipulation.
### Creating an ArrayList:
```
//To use ArrayList, import the class
import java.util.ArrayList;

//Declare an ArrayList
ArrayList<String> names = new ArrayList<>();

//Example to create an ArrayList containing objects of the Employee Class:
ArrayList<Employee> employees = new ArrayList<>();
```
### Common Methods:
- add() – adds an element
```
//Elements are added using add().
names.add("John");
names.add("Paul");

//Add at specific index:
names.add(2, "George");

//Example with objects:
employees.add(new Employee(101, "Mary", 25000));
```  
- get(index) – retrieves element
```
//Use get(index).
String name = names.get(0);
//Example:
System.out.println(names.get(0));
//
```
- size() – returns number of elements  
Returns number of elements currently stored.
```
names.size();
```
- set(index,value) – replaces element
```
names.set(1, "Mick");
```
- remove(index) – deletes element
```
names.remove(2);
```
After removal: remaining elements shift left AND size decreases by one 
### Example iteration:
```
for(int i = 0; i < names.size(); i++)
{
    System.out.println(names.get(i));
}
```
For‑each loop version:
```
for(String name : names)
{
    System.out.println(name);
}
```
Searching example:
```
for(int i = 0; i < accounts.size(); i++)
{
    if(accounts.get(i).getAccountNumber() == 1234)
    {
        position = i;
    }
}
```
Finding maximun values or minimum values:
```
double largest = accounts.get(0).viewBalance();

for(int i = 0; i < accounts.size(); i++)
{
    if(accounts.get(i).viewBalance() > largest)
    {
        largest = accounts.get(i).viewBalance();
    }
}
```
## Week 2 - JavaFX Introduction
JavaFX is Java's modern graphical interface framework for building desktop applications.
Basic GUI structure:
Stage → Scene → Layout → Controls
Stage:
Main application window.
Scene:
Container that holds graphical content.
Layouts:
Determine how controls are arranged.
Common layouts:
- VBox – vertical layout  
- HBox – horizontal layout  
- GridPane – grid layout  
- BorderPane – five region layout


### Parent / Child Node Hierarchy
In JavaFX, GUI elements form a tree structure:
```
Stage
  └ Scene
      └ Layout (root)
            └ Controls (children)
```
Layouts contain controls using:
```
root.getChildren().add(node);
root.getChildren().addAll(node1, node2, node3);
```
Example: 
```
root.getChildren().addAll(txtName, btnSubmit, lblOutput);
```
### Layout Alignment

Controls in layouts can be positioned using the Pos class.
```
import javafx.geometry.Pos;

VBox root = new VBox();
root.setAlignment(Pos.CENTER);
```

### Example JavaFX application:
```
//All JavaFX programs must extend the Application class and implement
the start(Stage stage) method.
public class FirstGUI extends Application
{
    public void start(Stage stage)
    {
        Label label = new Label("Hello World");
        VBox root = new VBox();
        root.getChildren().add(label);
        Scene scene = new Scene(root,300,200);
        stage.setScene(scene);
        stage.show();
    }
    public static void main(String[] args)
    {
        launch(args);
    }
}
```
### Common JavaFX imports:
```
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;

import javafx.scene.control.*;
import javafx.scene.layout.*;

import javafx.geometry.Pos;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
```
This saves time when starting a new JavaFX file.

### Common JavaFX Controls
```
Label lbl = new Label("Text");

Button btn = new Button("Click");

TextField txt = new TextField();

TextArea area = new TextArea();
```








JavaFX program starter template
```
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.layout.VBox;
import javafx.scene.control.*;

public class MyGUI extends Application
{
    public void start(Stage stage)
    {
        VBox root = new VBox();

        Label lbl = new Label("Hello");
        Button btn = new Button("Click");

        root.getChildren().addAll(lbl, btn);

        Scene scene = new Scene(root,300,200);
        stage.setScene(scene);
        stage.show();
    }

    public static void main(String[] args)
    {
        launch(args);
    }
}
```
## Week 3 and 4 – JavaFX Event Handling
In GUI applications user interactions generate events.
Examples:
- clicking a button  
- typing text  
- mouse movement  
Common event types:
MouseEvent  
KeyEvent  
ActionEvent  
WindowEvent  
Event handling defines what happens when an event occurs.
### Parsing Input From TextFields

Values entered into a TextField are always read as a String.

To use them as numbers they must be converted (parsed).

Convert to integer:
```
int num = Integer.parseInt(txtNum.getText());
```
Convert to double:
```
double value = Double.parseDouble(txtValue.getText());
```
### Example event handler:
```
EventHandler<ActionEvent> handler =
    new EventHandler<ActionEvent>()
{
    public void handle(ActionEvent e)
    {
        lblOutput.setText("Hello " + txtName.getText());
    }
};
//Attach to button:
btnName.setOnAction(handler);
```
### Lambda expression (modern approach):
```
btnName.setOnAction(e -> lblOutput.setText("Hello " + txtName.getText()));
```
Example multi‑line lambda:
```
btnAdd.setOnAction(e ->
{
    int num1 = Integer.parseInt(txtNum1.getText());
    int num2 = Integer.parseInt(txtNum2.getText());
    int result = num1 + num2;
    lblResult.setText(num1 + " + " + num2 + " = " + result);
});
```
### Shared Event Handlers (getSource)
If multiple buttons use the same handler, use `getSource()` to identify which button was clicked.
```
  if (e.getSource() == btnAdd) {
      // Add logic
```
Example: 
```
// Define one handler for multiple buttons
EventHandler<ActionEvent> calcHandler = e ->
{
	if (e.getSource() == btnAdd)
	{
		lblResult.setText("Adding...");
	} else if (e.getSource() == btnSubtract)
	{
		lblResult.setText("Subtracting...");
	}
};
   
// Assign the same handler to different buttons
btnAdd.setOnAction(calcHandler);
btnSubtract.setOnAction(calcHandler);
```

### Input Validation
Before parsing numbers, always check if the `TextField` is empty to prevent crashes.
```
  if (txtPrice.getText().isEmpty())
	{
      lblStatus.setText("Error: Please enter a price.");
    }

  // Better version that catches spaces only
  if (txtPrice.getText().trim().isEmpty())
	{
      // ...
    }
```
Example: 
```
// Comprehensive check for empty or whitespace-only input
   if (txtPrice.getText().trim().isEmpty())
	{
   		txtArea.setText("Error: You must enter a price.");
    } else
	{
   // Safe to attempt parsing once we know it's not empty
	double price = Double.parseDouble(txtPrice.getText());
    }
```
Example Try-Catch-Finally Block:
```
try
{
    // Risky code: might fail if text is "abc" or 0
    int input = Integer.parseInt(txtField.getText());
    int result = 100 / input;
    lblStatus.setText("Result is: " + result);
} 
catch (NumberFormatException e)
{
    // Runs if the user types letters instead of numbers
    lblStatus.setText("Error: Input must be a number.");
} 
catch (ArithmeticException e)
{
	// Runs if the user types 0
	lblStatus.setText("Error: Cannot divide by zero.");
} 
finally
{
	// This runs no matter what (even if an error happened)
	txtField.clear(); 
}

```

## Week 5 – Exception Handling
Exceptions are runtime errors that disrupt the normal flow of a program.

### The Throwable Hierarchy
- **Throwable**: The parent class of all errors.
- **Error**: Serious system problems (e.g., `OutOfMemoryError`). Do not catch.
- **Exception**: Problems your code can handle.
   - **RuntimeException (Unchecked)**: Logic errors like `ArithmeticException` or
      `NullPointerException`.
   - **Checked Exceptions**: Detected at **compilation**. You are forced to handle these (e.g.,
      `IOException`).
  
### Keywords
| Keyword | Purpose |
| :--- | :--- |
| `try` | Defines a block of code to be tested for errors. |
| `catch` | Handles the exceptions. It defines a block of code to execute if an error occurs. |
| `finally` | A block that **always** executes, regardless of an exception. Used for cleanup. |
| `throw` | Used to manually trigger an exception (e.g., `throw new Exception();`). |
| `throws` | Declared in a method header to warn that the method might fail. |

### Common Exceptions in GUI
- `NumberFormatException`: Thrown when `Integer.parseInt()` receives a non-numeric String.
- `ArithmeticException`: Thrown when dividing by zero.
- `NullPointerException`: Thrown when trying to use an object that hasn't been initialized.
- `ArrayIndexOutOfBoundsException`: Thrown when trying to access an index that doesn't exist (e.g.,
     index 10 in an array of size 5).
- `InputMismatchException`: Thrown by the Scanner class when the data provided by the user is the wrong
     type (e.g., entering a word when nextInt() was expected).
Example block handling ArrayList Exceptions:
```
try
{
   // Accessing an element from your properties list
   Property p = properties.get(index);
   txtArea.setText(p.toString());
}
catch (IndexOutOfBoundsException e)
{
   // Prevents crash if the property number doesn't exist in the list
   txtArea.setText("Error: That property index does not exist.");
}

```

