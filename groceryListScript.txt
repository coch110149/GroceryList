function onEdit()
{
  /*----//opens the spreadsheet we are working with----*/
  var shoppingList = SpreadsheetApp.getActiveSpreadsheet(); 
  
  /*-----ensures script will not run while editing the ALL sheet-----*/
  if (shoppingList.getActiveSheet().getSheetName() != "ALL")
  {
    /*----only run the function if between range C:30-C:END-----*/
    var curRow = shoppingList.getActiveSheet().getActiveCell().getRow();
    var curCol = shoppingList.getActiveSheet().getActiveCell().getColumn();
    if (curRow > 30 && curCol == 3)
    {
      seekAndFind(shoppingList,curRow);
    }//end if
  }//end if
}//end function



function seekAndFind(shoppingList,curRow) 
{
  
    /*-----get the Range and values that are being edited-----*/
    var curRange = shoppingList.getActiveSheet().getRange(curRow, 1, 1, 3);  
    var toFind = shoppingList.getActiveSheet().getRange(curRow,1,1,3).getValues();  
  
    /*--store values of All sheet into an array--*/
    var all = shoppingList.getSheetByName("ALL");
    var foundFlag = false; //set to true when a match is found
  
    for(var i =2; i < all.getLastRow()+1; i++)
    {
      var allValue = all.getRange(i,1).getValue();
      if (allValue == toFind[0][0])
      {    
        /*----a match has been found----*/
        var allRange = all.getRange(i,1,1,3); //needed to set values
        var allArray = allRange.getValues();
        foundFlag = true;
        
        if ((allArray[0][2]/parseInt(allArray[0][1], 10)) >= (toFind[0][2]/parseInt(toFind[0][1],10)))
        {
          /*---user has entered a lower price. Must update ALL list---*/
          allRange.setValues(toFind);//set values to toFind's values
          curRange.setBackground("white");
        }
        else
         /*--user has entered a greater price. Tell the user--*/
        shoppingList.getActiveSheet().getRange(curRow, 3, 1, 1).setBackground("#ffedcc");
      break;
      } 
    }//end for
    if (foundFlag == false)
    {
      all.insertRowBefore(2);
      all.getRange(2,1,1,3 ).setValues(toFind);
      all.getRange(2,1,1,3 ).setBackgroundRGB(204, 255, 204);
    }
}









/*bugs:
throw exception if price or size is blank
    add function that will call seekAndFind if price,size,and quanity are not blank
    if any are blank then highlight them in red
after the ALL sheet has been opened sort it A->Z
    after opening the all sheet, wait 2 miniuits
    call sort 

change color based on stores
    new column called store
    conditional formatting
    k = red
    w = blue
    f = yellow

*/
