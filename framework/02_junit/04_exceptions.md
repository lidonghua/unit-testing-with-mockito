!SLIDE
## Expected Exceptions
	@@@ Java
	new ArrayList<Object>().get(0);

!SLIDE
	@@@ Java
	@Test(expected=IndexOutOfBoundsException.class)
	public void empty() {
	  new ArrayList<Object>().get(0);
	}

!SLIDE
## How about verifying
## the message?

!SLIDE
	@@@ Java
	@Rule
	public ExpectedException thrown =
	        ExpectedException.none();

	@Test
	public void shouldTestExceptionMessage()
	    throws IndexOutOfBoundsException {
	  List<Object> list = new ArrayList<Object>();

	  thrown.expect(IndexOutOfBoundsException.class);
	  thrown.expectMessage("Index: 0, Size: 0");

	  list.get(0);
	  // Execution will never get past the above line
	}

!SLIDE
## You can also use matchers
	@@@ Java
	// thrown.expectMessage("Index: 0, Size: 0");
	thrown.expectMessage(containsString("Size: 0"));

!SLIDE
## Inspect domain objects
	@@@ Java
	private class TestThing {
	  public void chuck() {
	    Response response =
	        Response
            .status(Status.NOT_FOUND)
            .entity("Resource not found")
            .build();
	    throw new NotFoundException("some Message",
	                                response);
	  }
	}

!SLIDE
	@@@ Java
	@Test
	public void shouldThrow() {
	  TestThing testThing = new TestThing();
	  thrown.expect(NotFoundException.class);
	  thrown.expectMessage(startsWith("some Message"));
	  thrown.expect(hasProperty(
	                  "response",
	                  hasProperty("status", is(404))));
	  testThing.chuck();
	}
