# Notes
### Locks
`synchronized` - keyword to easily sync threads together, but it's not efficient because it locks and unlocks the whole method.
`Lock` - lets you lock specific areas of methods
`Condition` - lets you await/signal for when to do certain functions
- kind of like event based programming (waiting for something to happen)
### JavaFX
[Helpful JFX website](openjfx.io)
[Website to ask Bryce about](https://gluonhq.com/products/javafx/)
[JavaFX CSS style reference Guide](https://docs.oracle.com/javafx/2/api/javafx/scene/doc-files/cssref.html)

#### Stages and Scenes
Stage - Window
Scene - where you do shit, contains elements
Good idea to make a global stage
Scene can be a Pane or other root element
`mainStage.setResizable(false);` - Hacky workaround to make it so you can't resize it
- `mainStage.setMinHeight();` - also works with max height/width, better solution than `setResizable`
- `mainStage.setMinWidth();` 
# Code
### JavaFX
#### Making a global stage
```java
Stage mainStage = null;  
@Override  
public void start(Stage stage) throws Exception  
{  
    mainStage = stage;  
}
```