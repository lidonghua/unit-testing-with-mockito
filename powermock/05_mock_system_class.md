!SLIDE
## Mocking System Class
### e.g. `java.util.Calendar`

!SLIDE
### It's impossible for PowerMock
### to prepare a system class
	@@@ Java
	@PrepareForTest(Calendar.class) // It's not working

!SLIDE
### Instead, you prepare
### *the class that use the system class*

!SLIDE
	@@@ Java
	public class MyCalendar {
	  public Calendar current() {
	    return Calendar.getInstance();
	  }
	}

!SLIDE
	@@@ Java
	// @PrepareForTest(MyCalendar.class)

	MyCalendar calendar = new MyCalendar();

	mockStatic(Calendar.class);
	when(Calendar.getInstance())
	  .thenReturn(new GregorianCalendar(2015, 0, 1));

	assertEquals(
	  new GregorianCalendar(2015, 0, 1),
	  calendar.current());
