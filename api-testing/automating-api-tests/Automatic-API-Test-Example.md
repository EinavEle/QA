Simple test example:
In our next test, we had to use an API call to find out stuff about a house in the Harry Potter world. We used an ID from the enumeration to do this.
 Once we got the info, we made sure we got the right house by matching up the ID and the name.

The test:
```Java
@Test
public void SimpleTest() {
    AutomatingAPITests.HttpResponse<HousesResponse> result = null;
    //Get the ID from the enum
    String id = HarryPotterHouses.GRYFFINDOR.id;
    //Create the API Call
    result = HttpUtil
              .get("https://wizard-world-api.herokuapp.com/Houses/" + id);
    //Assert the result
    Assert.assertEquals(result.getStatus(),200);
    Assert.assertEquals(result.getData().getId()
                                      ,HarryPotterHouses.GRYFFINDOR.id);
    Assert.assertEquals(result.getData().getName()
                                      ,HarryPotterHouses.GRYFFINDOR.name);

}
```
The response from API:
```Java
[
    {
        "id": "0367baf3-1cb6-4baf-bede-48e17e1cd005",
        "name": "Gryffindor",
        "houseColours": "Scarlet and gold",
        "founder": "Godric Gryffindor",
        "animal": "Lion",
        "element": "Fire",
        "ghost": "Nearly-Headless Nick",
        "commonRoom": "Gryffindor Tower",
        "heads": [
            {
                "id": "530da97d-5a83-4ea6-bc15-790edf5b5efc",
                "firstName": "Minerva",
                "lastName": "McGonagall"
            },
            {
                "id": "9915c5f8-9177-4f63-bba8-d04387a404f9",
                "firstName": "Godric",
                "lastName": "Gryffindor"
            }
        ]
       },
    {...}
]
```
The API Entity:
```Java
public class HousesResponse {
    public String id;
    public String name;
    public String houseColours;
    public String founder;
    public String animal;
    public String element;
    public String ghost;
    public String commonRoom;
    public List<Head> heads;
    public List<Trait> traits;
}
```
The ENUM:
```Java
public enum HarryPotterHouses {
    GRYFFINDOR("0367baf3-1cb6-4baf-bede-48e17e1cd005","Gryffindor"),
    HUFFLEPUFF("85af6295-fd01-4170-a10b-963dd51dce14","Hufflepuff"),
    SLYTHERIN("a9704c47-f92e-40a4-8771-ed1899c9b9c1","Slytherin"),
    RAVENCLAW("805fd37a-65ae-4fe5-b336-d767b8b7c73a","Ravenclaw");

    public final String id;
    public final String name;

    HarryPotterHouses(String id,String name){
        this.id=id;
        this.name = name;
    }
}
```
In our example we can see how we make a simple call to the api and get the response in json format after that it goes to the entity and then the necessary tests can be done, status and data.