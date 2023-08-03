## Keywords
### Visibility
- **protected**: declarations are visible within the package or all subclasses
- **default**: declarations are visible only within the package (package private)
- **private**: declarations are visible within the class only
- **public**: declarations are visible everywhere
### Other useful things
- **super(args...)**: calls constructor of base class
- **abstract**: Class contains abstract and implemented methods, the class cannot be instantiated, it can only be subclassed
- **interface**: only abstract methods
- a **extends** b: adds everything from class b to a 
- a **implements** b: a implements methods of interface b 

## UML-Stuff
![[uml.png]]
### Association
Associations are just relationships between classes.
### Aggregation vs Composition
Aggregation and Composition are used when Classes are composed from other classes. The difference between them is in their lifetime. 
**Aggregation**: Destroying the class does not destroy its parts
**Composition**: Destroying the class also destroys the parts 


## Patterns
### Immutable class
1. Declare class as **final**
2. Make all fields **private**
3. Don‘t provide setter methods
4. Make all mutable fields final
5. Initialize all fields using a construct method performing deep copy
6. perform cloning of objects in getter methods to return a copy 

### Decorator-Pattern
The Decorator-Pattern is used to modify the functionality of a specific object at runtime.
This pattern includes a Base Interface, an Implementation of that Interface, an abstract base decorator and a concrete Decorator which actually adds more functionality.

The base decorator acts as a proxy, which enables us to add functionality before and after the actual method call.

1. **Component Interface**: Any interface
2. **Component Implementation**: Any Implementation of interface (1)
3. **Base Decorator**
	- Has Implementation (2) as member Variable (init through constructor)
	- Implements Interface (1) as well

4. **Concrete Decorator**
	- Extends Base Decorator (3)
	- Adds additional functionality in the overridden method calls
#### Example
1. **Component Interface**
```java
public interface DataSource {
    void writeData(String data);

    String readData();
}
```

2. **Component Implementation**
```java
public class FileDataSource implements DataSource {
    private String name;

    public FileDataSource(String name) {
        this.name = name;
    }

    @Override
    public void writeData(String data) {
        File file = new File(name);
        OutputStream out = new FileOutputStream(file)
        out.write(data.getBytes(), 0, data.length());
    }

    @Override
    public String readData() {
        char[] buffer = null;
        File file = new File(name);
        buffer = new char[(int) file.length()];
        reader.read(buffer);
        return new String(buffer);
    }
}
```

3. **Base Decorator**
```java
public class DataSourceDecorator implements DataSource {
    private DataSource wrappee;

    DataSourceDecorator(DataSource source) {
        this.wrappee = source;
    }

    @Override
    public void writeData(String data) {
        wrappee.writeData(data);
    }

    @Override
    public String readData() {
        return wrappee.readData();
    }
}
```

4. **Concrete Decorator**
```java
public class EncryptionDecorator extends DataSourceDecorator {

    public EncryptionDecorator(DataSource source) {
        super(source);
    }

    @Override
    public void writeData(String data) {
	    // Encode functionality is added, before writeData is called
        super.writeData(encode(data));
    }

    @Override
    public String readData() {
        return decode(super.readData());
    }

    private String encode(String data) {
        byte[] result = data.getBytes();
        // ... Do some magic ...
        return Base64.getEncoder().encodeToString(result);
    }

    private String decode(String data) {
        byte[] result = Base64.getDecoder().decode(data);
        // ... Do some magic ...
        return new String(result);
    }
}
```


### Composite-Pattern
The Composite-Pattern represents data in a tree-like structure, and allows to treat a group of objects the same way as a single instance. 

This pattern consists of four parts:
- **Component**: Declares the interface used for objects in the composition
- **Leaf**: Defines behavior for objects in the composition (implements Component interface)
- **Composite**: Stores all the child components and also implements the interface on the child components
#### Example
##### Component
```java
public interface Employee {
	public void showDetails();
}
```

##### Leaf
**Developer "leaf"**:
```java
public class Developer implements Employee {
	private String name;

	public Developer(String name) {
		this.name = name;
	}

	@override
	public void showDetails() {
		System.out.println(name);
	}
}
```

**Manager "leaf"**
```java
public class Manager implements Employee {
	private String name;
	private int money;

	public Developer(String name, int money) {
		this.name = name;
		this.money = money;
	}

	@override
	public void showDetails() {
		System.out.println(name  + " " + money);
	}
}
```

##### Composite
```java
public class CompanyDirectory implements Employee {
	private List<Employee> employees = new ArrayList<Employee>;

	@override 
	public void showDetails() {
		for(var e : employees)
			e.showDetails();
	}

	public void addEmployee(Employee e) {
		employees.add(e);
	}
}
```
##### Main Program
```java
public static void main(String[] args) {
	Developer dev1 = new Developer("Epic Dev");
	Developer dev2 = new Developer("average java dev");

	dev2.showDetails();

	CompanyDirectory devDir = new CompanyDirectory();
	devDir.addEmployee(dev1);
	devDir.addEmployee(dev2);

	Manager man1 = new Manager("Very useful manager", 20000);
	Manager man2 = new Manager("Very manager", 20010);

	CompanyDirectory manDir = new CompanyDirectory();
	manDir.addEmployee(man1);
	manDir.addEmployee(man2);

	CompanyDirectory dir = new CompanyDirectory();
	dir.addEmployee(devDir);
	dir.addEmployee(manDir);
	dir.showDetails();
}
```

### Singleton-Pattern


### FactoryMethod-Pattern


### Observer-Pattern


## Frameworks
### Collections
![[java.collections.diagram.png]]