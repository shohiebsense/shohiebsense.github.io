say ur `UIController` implements some protocol like `UITableViewDelegate, UITableViewDataSource`  

just don't access the value from the view element, go to the variable you want to change  

override this one  

```.swift
public func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
 //do something on your element
self.itemList[indexPath.section].isExpanded = !self.itemList[indexPath.section].isExpand


}
```

as that function gets called whenever some tap gesture is executed.

