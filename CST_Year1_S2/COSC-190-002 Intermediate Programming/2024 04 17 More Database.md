# Notes
### `estGridPane`
Bryce was trying to add this but it just looks weird
`obGrid.getChildren().forEach(x->x.setStyle("-fx-border-style: solid; -fx-padding: 10px"));`

Change it from Labels to `TextField`s
```java
TextField txtMake = new TextField(sMake);  
txtMake.setDisable(true);  
TextField txtModel = new TextField(sModel);  
txtModel.setDisable(true);  
TextField txtYear = new TextField(Integer.toString(nYear));  
txtYear.setDisable(true);  
TextField txtPrice = new TextField(sPrice);  
txtPrice.setDisable(true);  
  
obGrid.add(txtMake,0,nCount);  
obGrid.add(txtModel,1,nCount);  
obGrid.add(txtYear,2,nCount);  
obGrid.add(txtPrice,3,nCount);
```
Make an edit button that lets you edit the text fields
currently you can't disable them again
*Logic for this would probably be if a disabled property is set to false when the button is pressed, then update the values for that record in the database and set all the disabled properties back to true so you can't edit them*
```java
Button cmdEdit = new Button("Edit");  
cmdEdit.setOnAction(e-> {  
    // IDK why he did these in such a weird order  
    txtPrice.setDisable(false);  
    txtMake.setDisable(false);  
    txtModel.setDisable(false);  
    txtYear.setDisable(false);  
});
```
### `createConnection`
When you're making the Statement for the connection, replace it with this
`this.obStmt = obCon.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);`
### `getMoveOptions`
Put this for the Left button to decrease the records it's displaying
*Basically, just sets the `next` object to whatever `curCursorPos` is*
*I thought i would need to up `curCursorPos` somewhere else but it seems to just work for some reason*
`curCursorPos` is a private int variable FYI
```java
obLeft.setOnAction(e-> {  
    if(curCursorPos >= 20){  
        curCursorPos-=20;  
        try {  
            obRes.absolute(curCursorPos);  
        } catch (SQLException exp) {  
            exp.printStackTrace();  
        }  
    }  
    obBP.setCenter(estGridPane());  
});
```
# Code






