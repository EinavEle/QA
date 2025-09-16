Is there an unnecessary object here?
What would you have done differently?
```
    public void print(String... strings){
        Printer printer = new Printer();
        for(String str: strings){
          printer.print(str);
        }
    }
```  
<details><summary>Solution</summary>
Printer can be initialized once and doesn't have to be initialized every time the method is called.
</details>