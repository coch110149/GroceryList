This script will help us keep track of our grocery prices. 

We have a spreadsheet (collection of sheets) in Google Sheets that holds monthly grocery sheet containing :item name, size, price, quantity, and total, for each item for the 12 months of the year. I also have a sheet in the spreadsheet that holds all of the items we have purchased and how much it was at that time. 

The script will check the ALL spreadsheet for an item when the price field is changed in a month sheet, there are three cases that could happen.

1) The unit price entered is less than or equal to the price previously recorded in the ALL list
    -The script will update the information in the ALL list to match the new lower price
2) The unit price entered is greater than the price in the ALL list
    -The script will change the color of the price field of that item in the month sheet to orange.
    I did this because there are two reasons we would enter a higher price:
      1) we are making a mistake in purchasing a item that costs more
      2) we don't have a choice because the price of the item went up
3) The item entered is not in the ALL list
   -We add it to the top of the ALL list and highlight it green so we know there was a new item. 
  *I'm working on a function that will sort and remove the highlight after 2 minutes after we've opened the all list


