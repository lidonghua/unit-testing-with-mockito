!SLIDE
## Suppressing
## Unwanted Behavior
e.g.
### Extending a class in 3rd-party framework

!SLIDE
## Suppress super class constructors
	@@@ Java
	// @RunWith(PowerMockRunner.class)
	// @PrepareForTest(ExampleWithEvilParent.class)

	suppress(constructor(EvilParent.class));
	new ExampleWithEvilParent();

!SLIDE
## Suppress own constructor
	@@@ Java
	ExampleWithEvilConstructor example =
	  Whitebox.newInstance(
	    ExampleWithEvilConstructor.class);
	example.doSomething();

!SLIDE
## Suppress method
	@@@ Java
	public class ExampleWithEvilMethod {
	  public ExampleWithEvilMethod() { init(); ... }
	  private void init() { ... }
	}

	// @RunWith(PowerMockRunner.class)
	// @PrepareForTest(ExampleWithEvilMethod.class)

	suppress(method(ExampleWithEvilMethod.class, "init"));
	ExampleWithEvilMethod example =
	  new ExampleWithEvilMethod();

!SLIDE
## Suppress static initializer
	@@@ Java
	public class ExampleWithEvilStaticInitializer {
	  static {
	    ...
	  }
	}

	// Don't use ExampleWithEvilStaticInitializer.class
	@RunWith(PowerMockRunner.class)
	@SuppressStaticInitializationFor(
	  "org.mycompany.ExampleWithEvilStaticInitializer")

!SLIDE
## Suppress fields
	@@@ Java
	// @RunWith(PowerMockRunner.class)
	// @PrepareForTest(MyClass.class)

	public class MyClass {
	  private MyObject myObject = new MyObject();
	}

	suppress(field(MyClass.class, "myObject"));
