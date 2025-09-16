The for & for each loops are interchangeable in many cases.
Why use one and not the other? and when?
### For
```
      for (int i = 0; i < strings.size(); i++) {
          System.out.println(strings.get(i));
      }
```
### For each
```
      for (String str: strings){
          System.out.println(str);
      }
```
In most cases we should prefer for each loops to for loops.
### Why?
* For loops present another unnecessary variable (in our case `i`)
* For each loops use the actual item from the collection and save you some hussle
* For each loops are more readable
* When using nested iteration it can get really messy using a for instead of foreach

This is a function that creates a list of all available cards in a deck

### Using for:
```
    private Collection<Card> listAllCardsFor() {
        Collection<Suit> suits = Arrays.asList(Suit.values());
        Collection<Rank> ranks = Arrays.asList(Rank.values());
        Collection<Card> cards = new ArrayList<>();

        for (Iterator<Suit> i = suits.iterator(); i.hasNext(); ) {
            Suit currentSuit = i.next();
            for (Iterator<Rank> j = ranks.iterator(); j.hasNext(); ) {
                cards.add(new Card(currentSuit, j.next()));
            }
        }

        return cards;
    }
```

### Using for each:
```
    private Collection<Card> listAllCardsForEach() {
        Collection<Suit> suits = Arrays.asList(Suit.values());
        Collection<Rank> ranks = Arrays.asList(Rank.values());
        Collection<Card> cards = new ArrayList<>();

        for (Suit suit : suits) {
            for (Rank rank : ranks) {
                cards.add(new Card(suit, rank));
            }
        }

        return cards;
    }
```
You can clearly see that the second version is a lot cleaner and uses no extra variables


### When not to use for each?
When the function of the loop alters the collection.

```
    private void filterCards(Collection<Card> deck){
        for (Card card: deck) {
            if(card.suit.equals(Suit.HEART)){
                deck.remove(card);
            }
        }
        deck.stream().forEach(System.out::println);
    }
```

This code will not cause any warnings but will throw `ConcurrentModificationException` when you try to run it since the collection is modified while it is being iterated.

Another case where you would prefer using for is when you actually need the index parameter for any reason.
```
    public int positionOfMaxValue(int[] numbers){
        int maxPosition = -1;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i]>max){
                maxPosition=i;
            }
        }
        return maxPosition;
    }
```