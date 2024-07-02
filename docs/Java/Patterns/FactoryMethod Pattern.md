The FactoryMethod-Pattern is used to create objects without specifying the exact class of object that will be created. This is useful when you need to decouple the creation of an object from its implementation.
#### Example
**Basic Interface**
```java 
public interface Button {
	public void draw();
	public void on_pressed();
}
```

**Implementations**
```java
public class LightModeButton implements Button {
	...
}
```

```java
public class DarkModeButton implements Button {
	...
}
```

**Factory**
Now to create a Button based on the current Theme we need a Factory:
```java
public enum Theme {
	DARK,
	LIGHT
}

public class ButtonFactory {
	public Button createButton(Theme theme) {	
		switch(theme) {
			case Theme.Dark:
				return new DarkModeButton();
			case Theme.Light:
				return new LightModeButton();
		}
	}
}
```
