!SLIDE
## Capturing arguments
## for further assertions
	@@@ Java
	ArgumentCaptor<Person> argument =
	  ArgumentCaptor.forClass(Person.class);
	verify(mock).doSomething(argument.capture());
	assertEquals("John", argument.getValue().getName());
