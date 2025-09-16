According to the following code snippet
```HTML
<html>
    <head>
    </head>
    <body>
        <header id="header">
            <h2>Cities</h2>
        </header>
        <section>
            <nav>
                <ul class="country">
                    <li><a class="cuntryName" id="lon" 
                         name="london" href="#">London</a></li>
                    <li>
                        <a class="cuntryName" 
                           id="par" 
                           name="paris" 
                           href="#">Paris
                        </a>
                    </li>
                    <li><a class="cuntryName" id="tok" name="tokyo" href="#">Tokyo</a></li>
                </ul>
            </nav>
    </body>
</html>
```

1. How to locate Header "Cities" - by tagName?
1. How to locate Name  "paris" - by name ?
1. How to locate id  "tokyo" - by id?
1. How to locate XPath "London" - by XPath?

<details>
  <summary>
    Solution
  </summary>

1. Header "Cities" => findElement(By.tagName('h2'))
1. Name  "paris" => findElement(By.name(‘paris'))
1. id  "tokyo" => findElement(By.id(‘tok'))
1. XPath "London" = > findElement(By.XPath(‘//li//a[@id="lon"]’))


</details>