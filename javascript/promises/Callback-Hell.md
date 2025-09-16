Your code should look something like this:

```
getRandomWord(function (word) {
    getSynonyms(word, function (synonyms) {
        getSentiment(synonyms[0], function (sentiment) {
            console.log(
                `The word ${word} has a synonym ${synonyms[0]}                which has a ${getSentimentDescription(sentiment)} sentiment`)
        })
    })
})
```

We have to write our code like this because the second operation ( `getSynonyms` ) depends on the response of the first operation `getRandomWord`.

We also need the third operation to be nested because we ultimately want to console log everything out together.

And if you're being responsible and wish to handle errors as well, we would have to pass each function an errorHandling function and the code would look **even worse**:
```

getRandomWord(
    function (word) {
        getSynonyms(word,
            function (synonyms) {
                getSentiment(synonyms[0],
                    function (sentiment) {
                        console.log(`The word ${word} has a synonym ${synonyms[0]} which has a 
            ${getSentimentDescription(sentiment)} sentiment`)
                    }, function (error) {
                        console.log(error);
                    }
                )
            }, function (error) {
                console.log(error);
            }
        )
    }, function (error) {
        console.log(error);
    }
) 
```
  

And that, ladies and gentlemen, is a **callback hell** - a callback inside of a callback inside of a callback inside of a... yeah.

It's just awful, and this is what **promises** are coming to help with.