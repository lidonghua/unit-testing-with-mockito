!SLIDE
# Mocking Static Methods
	@@@ Java
	public class Constants {
	  public static double pi() {
	    return 3.14;
	  }
	  public static double pi(int n) {
	    return 3.14 * n;
	  }
	}

!SLIDE
## Required annotations
	@@@ Java
	@RunWith(PowerMockRunner.class)
	@PrepareForTest(Constants.class)
	public class YourTestCase {
	  // ...
	}

!SLIDE
## Mocking static method
	@@@ Java
	// import static o.p.a.m.PowerMockito.mockStatic;

	mockStatic(Constants.class);
	when(Constants.pi()).thenReturn(0);

	System.out.println(Constants.pi());

!SLIDE
## Verify static method
	@@@ Java
	// import static o.p.a.m.PowerMockito.verifyStatic;

	mockStatic(Constants.class);

	Constants.pi();

	verifyStatic();
	Constants.pi();

!SLIDE
### NOTE: You need to call verifyStatic()
### *per* method verification.
	@@@ Java
	mockStatic(Constants.class);

	Constants.pi();
	Constants.pi(2);

	verifyStatic();
	Constants.pi();
	verifyStatic();
	Constants.pi(2);

!SLIDE
## Use argument matchers
	@@@ Java
	mockStatic(Constants.class);

	Constants.pi(2);

	verifyStatic();
	Constants.pi(anyInt());

!SLIDE
## Verify number of calls
	@@@ Java
	mockStatic(Constants.class);

	Constants.pi();
	Constants.pi();

	verifyStatic(times(2));
	Constants.pi();

!SLIDE
## Stub void static method
## to throw exception
	@@@ Java
	// import static o.p.a.m.PowerMockito.doThrow;

	mockStatic(Constants.class);
	doThrow(new RuntimeException()).when(Constants.class);
	Constants.pi();

	Constants.pi();
