!SLIDE
## Mocking Private Methods
	@@@ Java
	class FooClass {
	  public String getPrivate() {
	    return privateMethod();
	  }
	  private String privateMethod() {
	    return "private";
	  }
	}

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.spy;
	// import static o.p.a.m.PowerMockito.doReturn;
	// @PrepareForTest(FooClass.class)

	FooClass foo = spy(new FooClass());

	doReturn("public").when(foo, "privateMethod");

	assertEquals("public", foo.getPrivate());

!SLIDE
	@@@ Java
	// import static o.p.a.m.PowerMockito.verifyPrivate;
	// @PrepareForTest(FooClass.class)

	FooClass foo = spy(new FooClass());

	foo.getPrivate();

	verifyPrivate(foo).invoke("privateMethod");
