# Exercise 1
Based on the football team generation exercise, add the following functionality:
- Create a `Team` class that has a name and a collection of players
- Add static factory methods that create a team given a specific formation. A formation is the number of players each position has.
examples:
1 - GK, 4 - Defense, 4 - Middlefiled, 2 - Attack
1 - GK, 4 - Defense, 3 - Middlefiled, 3 - Attack
etc..
- Add static factory methods to the `Player` class to enable creating different type of players.
examples:
createGoalKeeper()
createDefender()
etc..
- Create a `NameGenerator` class that has a name dictionary injected upon creation, and use it to generate player names.
whoever is using the name generator will have to initialize it with a dictionary. the dictionary's type is up to you.
- Use at least two different name dictionaries in your code.
- Add a function to the `Team` class that writes all the team's data to a file.
Preferably, this will be the `toString()` function
