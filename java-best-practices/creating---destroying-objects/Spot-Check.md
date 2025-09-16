Create a `user` class that has name, email, and country.
Write three different static factory methods relevant for this class.

<details><summary>Summary</summary>


    public class User {
    enum Country {ISRAEL, POLAND, GERMANY, UNITED_STATES}

    private final String name;
    private final String email;
    private final Country country;

    private User(String name, String email, Country country) {
        this.name = name;
        this.email = email;
        this.country = country;
    }

    public static User newIsraeliUser(String name, String email) {
        return new User(name, email, Country.ISRAEL);
    }

    public static User newUserWithRandomName(String email, Country country) {
        return new User(randomString(), email, country);
    }

    public static User newUser(String name, String email, Country country) {
        return new User(name, email, country);
    }

    }

</details>