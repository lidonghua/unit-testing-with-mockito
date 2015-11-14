!SLIDE
## Mocking Constructors
	@@@ Java
	public class MyDate {
	  public Date current() {
	    return new Date();
	  }
	}

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.whenNew;

	// Prepare the class CREATING the new instance
	// @PrepareForTest(MyDate.class)

	MyDate myDate = new MyDate();
	whenNew(Date.class).withNoArguments().thenReturn(
	  new GregorianCalendar(2015, 0, 1).getTime());

	assertEquals(
	  new GregorianCalendar(2015, 0, 1).getTime(),
	  myDate.current());

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.verifyNew;

	// @PrepareForTest(MyDate.class)

	MyDate myDate = new MyDate();
	whenNew(Date.class).withNoArguments().thenReturn(
	  new GregorianCalendar(2015, 0, 1).getTime());

	myDate.current();

	verifyNew(Date.class).withNoArguments();
