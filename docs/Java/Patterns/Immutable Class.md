In java objects are passed as references. So even if you get a member variable from Class through a Getter, you can still mutate the state of the Class! To prevent this, one can use the "immutable class pattern". Here you make sure that you always perform a copy when accessing or sharing data, to avoid passing references to class members.
### Immutable class
1. Declare Class as **final**
2. Make all fields **private**
3. Don‘t provide setter methods
4. Make all mutable fields final
5. Initialize all fields using a construct method performing deep copy
6. Perform cloning of objects in Getter methods to return a copy 
