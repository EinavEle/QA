Write a service that uses mock (you can use a soccer exercise from the Java course)

<details>
  <summary>
    Solution
  </summary>

```java
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;

import static org.mockito.Mockito.*;

public class SoccerServiceTest {
    @Test
    public void createTeamTest() {
        NameGenerator nameGenerator = mock(NameGenerator.class);
        when(nameGenerator.generateName())
                          .thenReturn("Player 1", "Player 2", "Player 3");

        SoccerService soccerService = new SoccerService(nameGenerator);
        Team team = soccerService.createTeam("Test Team", 1, 2, 3, 4);
        // Assertions or verifications based on the expected behavior
        // ...
    }
    // More test cases...
}
```
</details>