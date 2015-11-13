!SLIDE
## Stubbing void methods
	@@@ Java
	// Impossible
	when(mockedList.clear())
	  .thenThrow(new RuntimeException())

	doThrow(new RuntimeException())
	  .when(mockedList).clear();

	mockedList.clear();

!SLIDE
## Stubbing consecutive calls
### (iterator-style stubbing)
	@@@ Java
	when(mock.someMethod("some arg"))
	  .thenThrow(new RuntimeException())
	  .thenReturn("foo");

	mock.someMethod("some arg");
	System.out.println(mock.someMethod("some arg"));
	System.out.println(mock.someMethod("some arg"));

	// when(mock.someMethod("some arg"))
	//   .thenReturn("one", "two", "three");

!SLIDE
## Stubbing with callbacks
### *Think carefully before using*
	@@@ Java
	when(mock.someMethod(anyString()))
	  .thenAnswer(new Answer() {
	    Object answer(InvocationOnMock invocation) {
	       Object[] args = invocation.getArguments();
	       Object mock = invocation.getMock();
	       return "called with arguments: " + args;
	    }
	  });

	System.out.println(mock.someMethod("foo"));
