!SLIDE
## Argument matchers
	@@@ Java
	when(mockedList.get(anyInt())).thenReturn("element");

	// Custom matcher: isValid()
	when(mockedList.contains(argThat(isValid())))
	  .thenReturn("element");

	System.out.println(mockedList.get(999));

	verify(mockedList).get(anyInt());

!SLIDE
## A lot of matchers (1)
	@@@ Java
	any(), any(Class<T>)
	isA(Class<T>) // with type check

	isNull/isNotNull()
	isNull/isNotNull(Class<T>)

	any+Boolean/Byte/Char/Short/Int/Long/Float/Double()
	any+Collection/List/Set/Map()
	any+Collection/List/Set+Of(Class<T>)
	anyMapOf(Class<T>, Class<T>)

!SLIDE
## A lot of matchers (2)
	@@@ Java
	anyString()
	contains/startsWith/endsWith/matches(String)

	eq(T)
	eq(boolean/byte/char/short/int/long/float/double)

 	// When equals() not implemented
	refEq(T, String... excludeFields)

!SLIDE
## A lot of matchers (3)
	@@@ Java
	argThat(ArgumentMatcher<T>)
	boolean/byte/char/short/int/long/float/double
	  +That(ArgumentMatcher<T>)

	same(T), anyVararg()

	// Alias: anyObject(), notNull(), notNull(Class<T>)

!SLIDE
## Custom matchers (1)
	@@@ Java
	class ListOfTwoElements
	    implements ArgumentMatcher<List> {

	  public boolean matches(Object list) {
	    return ((List) list).size() == 2;
	  }

	  public String toString() {
	    return "[list of 2 elements]";
	  }
	}

!SLIDE
## Custom matchers (2)
	@@@ Java
	List mock = mock(List.class);

	when(mock.addAll(argThat(new ListOfTwoElements)))
	  .thenReturn(true);

	mock.addAll(Arrays.asList("one", "two"));

	verify(mock).addAll(argThat(new ListOfTwoElements()));

!SLIDE
## Custom matchers (3)
	@@@ Java
	// Extract method to keep it readable
	class CustomMatchers {
	  public static ArgumentMatcher<List>
	      listOfTwoElements() {
	    return new ListOfTwoElements();
	  }
	}

	// import static CustomMatchers.listOfTwoElements;
	verify(mock).addAll(argThat(listOfTwoElements()));

!SLIDE
## Warning: if using matchers,
## use on *all* arguments
	@@@ Java
	// Incorrect
	verify(mock).method(anyInt(), anyChar(), "abc");

	verify(mock).method(anyInt(), anyChar(), eq("abc"));
