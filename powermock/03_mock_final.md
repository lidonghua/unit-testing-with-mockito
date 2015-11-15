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

	when(finale.method()).thenReturn("mock");

	assertEquals("mock", finale.method());

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.mock;
	// @PrepareForTest(FinalClass.class)

	FinalClass finale = mock(FinalClass.class);

	finale.method();

	verify(finale).method();
