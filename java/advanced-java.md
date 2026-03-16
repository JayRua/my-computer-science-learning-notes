# Java Advanced Programming Notes

Higher Diploma in Science in Computing, Java Module

This document summarises the core Java concepts I learned in the Advanced Java module.

Topics covered:  
	- ArrayLists and Collections  
	- JavaFX GUI development  
	- Event-driven programming  
	- Exception handling  
	- File input and output  
	- Writing objects to files  

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
### Example JavaFX application:
```
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
## Week 3 – JavaFX Event Handling
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
