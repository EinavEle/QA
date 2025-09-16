How would you better reorganize this code?
```
    public void saveTestFile(String testName, Object data){
        String filename;
        String localDate = LocalDateTime.now().toString();
        String key = generateRandomString();
        filename = testName + "_" + localDate + "_" + key;
        saveFileData(filename, data);
    } 
```

<details><summary>Solution</summary>
declare `filename` only when using it and not before.
</details>