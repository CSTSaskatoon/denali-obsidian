# Notes
## *If it says "plane" anywhere it's probably a typo*
### Process for making something in JavaFX
1. add the library (*Done in project level, not per program)
2. Create the JavaFX app
3. Add runtime config
### Basic Structure of a JavaFX application
- Application
- Override the state (stage) method
- Stage, scene, nodes

![300](Pasted%20image%2020240301101314.png)
#### Panes, UI controls and shapes
*Shapes like `Line`, `Circle`, `Ellipse`, `Rectangle`, `Path`, `Polygon`, `Polyline` and `Text` are subclasses of `Shape`*
![](Pasted%20image%2020240301101450.png)
Stage is a window, we add a scene to the stage
### Making our first JavaFX project
got the `javafx-sdk` from onedrive, put it in `E:\Intellij`
JavaFX applications will run without a main
You can create your own stages if you want, but one is made by default by the start method
`--module-path E:\Intellij\javafx-sdk\lib --add-modules=javafx.controls`
### Panes
Panes are where you have all your setup
#### Configurations
![](Pasted%20image%2020240301115044.png)
**Need to add "VM options" in the "modify options" dropdown**
Don't rename the library, if it's not named "lib" it won't work
#### Layout panes
*`Pane`* - Base class for layout panes, contains `getChildren()`
*`StackPane`* - most common, places nodes on top of each other in the center of the pane
*`FlowPane`* - Places the nodes row-by-row horizontally or column-by-column vertically (Basically works like flex from CSS)
*`GridPane`* - Places the nodes in the cells in a two-dimensional grid (Works like a grid layout in CSS)
*`BorderPane`* - Places the nodes in the top, right, bottom, left and center regions
*`HBox`* - Places the nodes in a single row
*`VBox`* - Places the nodes in a single column
Missed notes for `Pane, StackPane, and FlowPane`
##### `GridPane`
![500](Pasted%20image%2020240301111055.png)
Adding an element to `GridPane` - `add(WhatYouAreAdding,columnIndex,RowIndex)`
##### `BorderPane`
![300](Pasted%20image%2020240301110847.png)
Kind of simple cause you only have 5 options to add
*Keep in mind that left and right don't go all the way to the top/bottom*
##### `HBox` 
![500](Pasted%20image%2020240301111536.png)
##### `VBox`
![500](Pasted%20image%2020240301111555.png)
# Code
### Making the start tester/start method
```java
public class JavaFXTester extends Application // Will import javafx.application.Application
```
Needs this method
```java
@Override  
public void start(Stage stage)  
{  
      // Make sure you import the right one  
Button btnOK= new Button("OK");  
 
Scene scene = new Scene(btnOK, 200,250);  
stage.setTitle("Fuckity fuck mcfuck fuck");  
stage.setScene(scene);  
stage.show();
}
```
*This class is basically boiler plate code for all JavaFX projects*
Most code you make in JavaFX will go between making the button and making the scene
### Making Panes
#### `StackPane`
use the same boiler plate code from before
```java
StackPane pane = new StackPane();  
pane.getChildren().add(new Button("Fuck 1"));  
pane.getChildren().add(new Button("Fuck 2 is large 0_o"));  
pane.getChildren().add(new Button("Fuck 3"));  
  
Scene scene = new Scene(pane, 200,200);  
stage.setTitle("fuck");  
stage.setScene(scene);  
stage.show();
```
Output - ![](Pasted%20image%2020240301112642.png)
#### `FlowPane`
same code as `StackPane`, but change the stuff in the middle
```java
FlowPane pane = new FlowPane();  
pane.setHgap(25);  
pane.setVgap(15);
pane.getChildren().addAll(new Label("FirstName: "), new TextField(), new Label("MI: "), new TextField());  
pane.getChildren().addAll(new Label("LastName: "), new TextField());
```
Output - ![](Pasted%20image%2020240301113155.png)
#### `GridPane`
same boiler plate code, just change the stuff in the middle
for `GridPane` you don't need to do `.getChildren()`
```java
GridPane pane = new GridPane();  
pane.setAlignment(Pos.CENTER);  
pane.setHgap(5.0);  
pane.setVgap(15.0);  
  
// Remember it's columnIndex,rowIndex  
pane.add(new Label("FirstName: "),0,0);  
pane.add(new TextField(),1,0);  
pane.add(new Label("LastName: "),0,1);  
pane.add(new TextField(),1,1);  
  
Button btnAdd = new Button("Add Name");  
pane.add(btnAdd,1,2);  
GridPane.setHalignment(btnAdd, HPos.RIGHT);  
pane.addRow(3, new Label("Password: "), new TextField());
```
Output - ![](Pasted%20image%2020240301114315.png)
#### `BorderPane`
Again same boiler plate code, but add stuff in the middle
```java
BorderPane pane = new BorderPane();  
pane.setTop(new CustomPane("Top"));  
pane.setBottom(new CustomPane("Bottom"));  
pane.setLeft(new CustomPane("Left"));  
pane.setCenter(new CustomPane("Center"));  
pane.setRight(new CustomPane("Right"));
```
Output - ![](Pasted%20image%2020240301115204.png)
##### For this one we use another class so that we can see the borders
```java
class CustomPane extends StackPane  
{  
    public CustomPane(String title)  
    {  
        getChildren().add(new Label(title));  
        setStyle("-fx-border-color: red");  
        setPadding(new Insets(50));  
    }  
}
```
Basically just uses CSS styles in java