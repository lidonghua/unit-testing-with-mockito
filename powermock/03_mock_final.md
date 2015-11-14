!SLIDE
## Mocking Final
## Classes/Methods
	@@@ Java
	public final class FinalClass {
	  public final String method() {
	    return "real";
	  }
	}

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.mock;
	// @PrepareForTest(FinalClass.class)

	FinalClass finale = mock(FinalClass.class);

	doReturn("mock").when(finale).method();

	assertEquals("mock", finale.method());

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.mock;
	// @PrepareForTest(FinalClass.class)

	FinalClass finale = mock(FinalClass.class);

	finale.method();

	verify(finale).method();
