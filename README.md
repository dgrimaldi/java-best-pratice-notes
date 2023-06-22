# Java Guidelines

The style guidelines and best practices for our engineering team.

# Java Styles

---

- **[Access Modifier](https://www.geeksforgeeks.org/access-modifiers-java/)**
    
    ```jsx
    //make each class or member as inaccessible as possible
    // if a class is package-private or is a private nested
    	class, there is nothing inherently wrong with exposing its
    	data fields
    //public classes should not expose fields directly, use accessor methods instead
    ```
    
    ![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled.png)
    
- OOP concepts
    - Class represents the set of properties or methods that are common to all objects of one type. A class can be public or have default access, a class name should begin with the initial letter capitalized by convention, a class can extend another class, a class can implement an interface
    - Method is a set of code it can be public
    - A *singleton* is simply a class that is instantiated exactly once (it can be done with a private constructor)
    
    ```java
    public class Dog {
    	private static Dog = new Dog();
    	private Dog(string name, string age){
    		this.breed = breed;
    		this.age = age;
    	}
    	
    }
    ```
    
    - An immutable class is simply a class whose instances cannot be modified. Immutable classes are easier to design, implement, and use than mutable classes. They are less prone to error and are more secure. There are 5 points to do a class immutable
        - Don’t provide methods that modify the object’s state
        - Ensure that the class can’t be extended
        - Make all fields final
        - Make all fields private
        - Ensure exclusive access to any mutable components
    - When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object
        - Static variables are, essentially, global variables. All instances of the class share the same static variable.

```java
public class Dog {
    // Instance Variables
		// In a public class is important to use not-accesible variable
    private String name;
    private int age;

		// 1) Consider static factory methods (JavaBean) instead constructors when we have many parameters, it can has disadvantages
		// - may be in an inconsistent state partway through its construction
		// - precludes the possibility of making a class immutable
		// public void setAge(String age) { age = age }
		// public void setBreed(String breed) { breed = bredd }

		// 2) Consider Immutable class with static factories instead of constructors
		// private Dog...
		// public static Dog valueOf(String name, String age) { return new Dog(name, age) }
    public Dog(String name, String age){
        this.breed = breed;
        this.age = age;
    }

 
    // method 1
		//<access_modifier> <return_type> <method_name>( list_of_parameters) { body }
    public String getName(){
        return name;
    }
 
    @Override
    public String toString(){
        return("Hi dog name is "+ this.getName()+ "it's" + this.getAge()+ "years old";
    }

		// Factory method replace constructor with this, limitation 
		// - whitout public and protected classes cannot be subbclasses
		// - hard to find in the code
		// public static void String toString(String name, String age) {
		//  return("Hi my name is "+ this.getName()+ "i'm" + this.getAge()+ "years old";
		// }
		//
    public static void main(String[] args){
        Dog tuffy = new Dog("tuffy", 5);
        System.out.println(tuffy.toString());
    }
}
```

- **Inheritance -**  attributes and methods from one class to another : **subclass** (child) - the class that inherits from another class, **superclass** (parent) - the class being inherited from. To inherit from a class, use the `extend`     keyword and `super` to initiate  the variables of the parent class. Inheriting from ordinary concrete classes across package boundaries, however, is dangerous. Instead of extending an existing class, give your new class a private field that references an instance of the existing class. This design is called composition because the existing class becomes a component of the new one.

```jsx

!!!recheck
ITEM 18
https://en.wikipedia.org/wiki/Composition_over_inheritance

// Composition example
public class InstrumentedSet<E> extends ForwardingSet<E> {
	private int addCount = 0;
	public InstrumentedSet(Set<E> s) {
		super(s);
	}
	Override public boolean add(E e) {
		addCount++;
		return super.add(e);
	}
	@Override public boolean addAll(Collection<? extends E> c) {
		addCount += c.size();
		return super.addAll(c);
	}
	public int getAddCount() {
		return addCount;
	}
}

// Inheritance is appropriate only in circumstances where the
//	subclass really is a subtype of the superclass. In other words, a
//	class B should extend a class A only if an “is-a” relationship exists
//	between the two classes. It is often the case that B should
contain a private instance of A and expose a different API: A is not
an essential part of B, merely a detail of its implementation.
```

- **Data Type** – Is a Wrapper class is a class whose object wraps or contains primitive data types. When we create an object to a wrapper class, it contains a field and in this field, we can store primitive data types. The classes convert primitive data in we

![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled%201.png)

- **Object** – class provides multiple methods which are as follows:
    - tostring() (method returns a string representation of the object)
    - hashCode() (JVM unique number)
    - equals(Object obj) (indicates whether some other object is "equal to" this one)
    - finalize() (A subclass overrides the finalize method to dispose of system resources or to perform other cleanups)
    - getClass() (method returns the runtime class of an object)
    - clone() (creates and returns a copy of this object)
    - wait(), notify() notifyAll()
    - Utils that can be used with objects are:
        - 
- **************Generic************** – defined a type and then you tell the compiler what types of objects are permitted in each collection. Each generic type defines a set of parameterized types, which consist of the class or interface name followed by an angle-bracketed, for example List<String> (read “list of string”). Each generic type defines a raw type, which is the name of the generic type used without any accompanying type parameters. For example, the raw type corresponding to List<E> is List. If youuserawtypes, you lose all the safety and expressiveness benefits of generics

![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled%202.png)

```jsx

```

- **Array** – is a direct superclass of an array type is Object. Array declaration is: `type var-name[];` or `type[] var-name;`, to create an array we create: `var-name = new type [size];`
    - `init[] intArray = new int[] {1,2,3};` Prefer list to array `List<type>[] listName = new List<type>[size];`
- **************Interface and Abstract class************** – is defined as an abstract type used to specify the behavior of a class. Prefer interface to abstract class
    
    Abstract class and interface both are used to achieve abstraction  where we can declare the abstract methods. Abstract class and interface both can't be instantiated.
    
    But there are many differences between abstract class and interface that are given below.
    
    | Abstract class | Interface |
    | --- | --- |
    | 1) Abstract class can have abstract and non-abstract methods. | Interface can have only abstract methods. Since Java 8, it can have default and static methods also. |
    | 2) Abstract class doesn't support multiple inheritance. | Interface supports multiple inheritance. |
    | 3) Abstract class can have final, non-final, static and non-static variables. | Interface has only static and final variables. |
    | 4) Abstract class can provide the implementation of interface. | Interface can't provide the implementation of abstract class. |
    | 5) The abstract keyword is used to declare abstract class. | The interface keyword is used to declare interface. |
    | 6) An abstract class can extend another Java class and implement multiple Java interfaces. | An interface can extend another Java interface only. |
    | 7) An abstract class can be extended using keyword "extends". | An interface can be implemented using keyword "implements". |
    | 8) A Java abstract class can have class members like private, protected, etc. | Members of a Java interface are public by default. |
    | 9)Example: public abstract class Shape{public abstract void draw();} | Example: public interface Drawable{void draw();} |

```jsx
// If a top-level class or interface can be made package-private, it should be
```

- **Enum** – is a data type which contains a fixed set of constants. It can be used for days of the week (SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, and SATURDAY). Java Enums can be thought of as classes which have a fixed set of constants (a variable that does not change).
- **Annotation**– [https://dev.to/kylec32/effective-java-prefer-annotations-to-naming-patterns-52lk](https://dev.to/kylec32/effective-java-prefer-annotations-to-naming-patterns-52lk) check out
- **Lambda—** In Java 8, the language formalized the notion that interfaces with a single abstract method are special and deserve special treatment. These interfaces are now known as functional interfaces, and the language allows you to create instances of these interfaces using lambda expressions, or lambdas for short. Lambdas are similar in function to anonymous classes, but far more concise.
- **Method Reference —** Java provides a way to generate function objects even more succinct than lambdas: method references.

![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled%203.png)

```jsx
numbers.stream().sorted((a, b) -> a.compareTo(b));
numbers.stream().sorted(Integer::compareTo);
```

 Existing 6 different interfaces in java.utiil.function that make this job

![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled%204.png)

# Others

---

Return empty collections or arrays, not nulls

Throws exception if empty

Prefer for-each loops to traditional for loops

Beware the performance of string concatenation, to achieve acceptable performance, use a StringBuilder in place of a String

Naming conventions

![Untitled](Java%20Guidelines%2057fe79f104994c89b72c67dca0d74bb8/Untitled%205.png)

# Spring

****The Spring Data Generated DAO (Data Access Object)**** 

[Introduction to Spring Data JPA | Baeldung](https://www.baeldung.com/the-persistence-layer-with-spring-data-jpa)

# SQL

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;

SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;

SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;

SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;

INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;

UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

DELETE FROM table_name WHERE condition;

SELECT MIN/MAX(column_name)
FROM table_name
WHERE condition;

SELECT COUNT/AVG/SUM(column_name)
FROM table_name
WHERE condition;

SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;

WHERE CustomerName LIKE 'a%' 	Finds any values that start with "a"
WHERE CustomerName LIKE '%a' 	Finds any values that end with "a"
WHERE CustomerName LIKE '%or%' 	Finds any values that have "or" in any position
WHERE CustomerName LIKE '_r%' 	Finds any values that have "r" in the second position
WHERE CustomerName LIKE 'a_%' 	Finds any values that start with "a" and are at least 2 characters in length
WHERE CustomerName LIKE 'a__%' 	Finds any values that start with "a" and are at least 3 characters in length
WHERE ContactName LIKE 'a%o' 	Finds any values that start with "a" and ends with "o"

SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);

SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);

SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

SELECT column_name(s)
FROM table_name AS alias_name;

SELECT column_name(s)
FROM table1
INNER JOIN table2 //Intersection
ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;

SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2 //All
ON table1.column_name = table2.column_name
WHERE condition;

SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;

SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

GROUP BY Syntax
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);

CREATE DATABASE databasename;

DROP DATABASE/TABLE databasename/table_name;

CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
   ....
);
// -datatype https://www.w3schools.com/sql/sql_datatypes.asp
// -constraint https://www.w3schools.com/sql/sql_constraints.asp

CREATE INDEX index_name
ON table_name (column1, column2, ...);
```