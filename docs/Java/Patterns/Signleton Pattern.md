A Singleton is used when only a single instance of the class is needed globally. Achieve this by making the constructor private and writing a public getter which lazily initializes the instance.
#### Example
This is a very simple implementation. It works but is not thread safe! To achieve thread safety the get method could be marked with **synchronized**, or **Double Checked Locking** could be used for more performance.
```java
class Singleton {
	private static Singleton instance;

	private Singleton() {}

	public static Singleton get() {
		if(instance == null)
			instance = new Singleton();
		return instance;
	}
}
```
