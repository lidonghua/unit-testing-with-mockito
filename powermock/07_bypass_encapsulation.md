!SLIDE
## Bypass Encapsulation
	@@@ Java
	import org.powermock.reflect.Whitebox;

!SLIDE
### Accessing a private member
	@@@ Java
	class StringList {
	  private List<String> strings = new ArrayList<>();

	  public void addString(String string) {
	    strings.add(string);
	  }

	  public int count() {
	    return strings.size();
	  }
	}

!SLIDE
	@@@ Java
	StringList stringList = new StringList();
	stringList.addString("a");

	List<String> strings =
	  Whitebox.getInternalState(stringList, "strings");

	assertEquals("a", strings.get(0));

!SLIDE
	@@@ Java
	StringList stringList = new StringList();

	Whitebox.setInternalState(stringList, "strings",
	  Arrays.asList("a", "b"));

	assertEquals(2, stringList.count());

!SLIDE
### Invoking a private method
	@@@ Java
	private int sum(int a, int b) {
	  return a + b;
	}

	int sum = Whitebox.<Integer>invokeMethod(
	  myInstance, "sum", 1, 2);

!SLIDE
### Instantiate a class with a private constructor
	@@@ Java
	public class FooClass {
	  private final int state;

	  private FooClass(int state) {
	    this.state = state;
	  }
	}

	FooClass foo = WhiteBox.invokeConstructor(
	  FooClass.class, 10);
