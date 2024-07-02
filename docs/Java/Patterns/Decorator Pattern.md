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
