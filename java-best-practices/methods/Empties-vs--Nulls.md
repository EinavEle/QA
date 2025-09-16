It is recommended that your methods return empty collections, rather than returning nulls.

Nulls require further handling by the user:
```
public void something(){
  List<String> list = makeAList();
  if(list == null){
    // handle nulls
  }else{
    //do your thing
  }
}
```
Note that if we allow returning nulls instead of empty lists, this bit of code will need to appear in many places.
This is why it is always recommended to return empties.