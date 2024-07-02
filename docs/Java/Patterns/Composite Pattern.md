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