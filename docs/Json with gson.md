## Complex Types
Abstract classes can be instanced using a TypeAdapter.

**Clique.java**
```java
public class Clique {
	private final List<Person> members = new LinkedList<>();

	public boolean addMember(Person p) {
		return members.add(p);
	}

	public void removeMember(int at) {
		members.remove(at);
	}
}
```

**Main.java**
```java
public class Main {  
	private static final GsonBuilder gsonBuilder;  
	private static final Gson gson;  
  
	static {  
		gsonBuilder = new GsonBuilder();  
		gsonBuilder.registerTypeAdapter(Person.class, new PersonAdapter());  
		gson = gsonBuilder.create();  
	}  
  
	public static void main(String[] args) throws FileNotFoundException {  
		Lad lad = gson.fromJson(new BufferedReader(new FileReader("resources/main/Lad.json")), Lad.class);  
		
		Lass lass = gson.fromJson(new BufferedReader(new FileReader("resources/main/Lass.json")), Lass.class);  
		
		Clique clique = gson.fromJson(new BufferedReader(new FileReader("resources/main/Clique.json")), Clique.class);  
	}  
}  
  
class PersonAdapter implements JsonDeserializer<Person> {  
	@Override  
	public Person deserialize(JsonElement json, Type typeOfT, JsonDeserializationContext context) throws JsonParseException {  

	var person = json.getAsJsonObject();  
	var isFemale = person.get("female").getAsBoolean();  
	var name = person.get("name").getAsString();  
  
	if (isFemale)  
		return new Lass(name);  
  
	return new Lad(name);  
	}  
}
```
