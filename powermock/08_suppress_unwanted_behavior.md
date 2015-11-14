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
	  Whitebox.newInstance(ExampleWithEvilConstructor.class);
	example.doSomething();

!SLIDE
## Suppress method
	@@@ Java
	// @RunWith(PowerMockRunner.class)
	// @PrepareForTest(ExampleWithEvilMethod.class)

	suppress(method(ExampleWithEvilMethod.class, "init"));
	ExampleWithEvilMethod example = new ExampleWithEvilMethod();

!SLIDE
## Suppress static initializer
	@@@ Java
	// Don't use ExampleWithEvilStaticInitializer.class
	@RunWith(PowerMockRunner.class)
	@SuppressStaticInitializationFor(
	  "org.mycompany.ExampleWithEvilStaticInitializer")

!SLIDE
## Suppress fields
	@@@ Java
	public class MyClass {
    private MyObject myObject = new MyObject();
	}

	suppress(field(MyClass.class, "myObject"));
