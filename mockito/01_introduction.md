!SLIDE
![Mockito Logo](mockito-logo.png)

!SLIDE
## Mockito library
## enables mocks creation,
## verification and stubbing.

!SLIDE
## Maven
	@@@ XML
	<dependency>
	  <groupId>org.mockito</groupId>
	  <artifactId>mockito-core</artifactId>
	  <version>2.0.31-beta</version>
	  <scope>test</scope>
	</dependency>

!SLIDE
## Some examples from
## [the official site](http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html)

!SLIDE
## Let's verify some behaviour!
	@@@ Java
	import static org.mockito.Mockito.*;

	List mockedList = mock(List.class);

	mockedList.add("one");
	mockedList.clear();

	verify(mockedList).add("one");
	verify(mockedList).clear();

!SLIDE
## How about some stubbing?
	@@@ Java
	LinkedList mockedList = mock(LinkedList.class);

	when(mockedList.get(0)).thenReturn("first");
	when(mockedList.get(1))
	  .thenThrow(new RuntimeException());

	System.out.println(mockedList.get(0));
	System.out.println(mockedList.get(1));
	System.out.println(mockedList.get(999));

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
	any+Collection/List/Map/Set()
	any+Collection/List/Map/Set+Of(Class<T>)

!SLIDE
## A lot of matchers (2)
	@@@ Java
	anyString(),
	contains/startsWith/endsWith/matches(String)

	eq(T)
	eq(boolean/byte/char/short/int/long/float/double)

	refEq(T, String...) // equals() not implemented

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

	verify(mock).addAll(listOfTwoElements());

!SLIDE
## Warning: if using matchers,
## use on *all* arguments
	@@@ Java
	// Incorrect
	verify(mock).method(anyInt(), anyChar(), "abc");

	verify(mock).method(anyInt(), anyChar(), eq("abc"));

!SLIDE
## Verifying number of invocations
	@@@ Java
	mockedList.add("once");

	verify(mockedList).add("once"); // times(1)

	verify(mockedList, times(2)).add("twice");

	// never() is an alias to times(0)
	verify(mockedList, never()).add("never happened");

	verify(mockedList, atLeastOnce()).add("three times");
	verify(mockedList, atLeast(2)).add("five times");
	verify(mockedList, atMost(5)).add("three times");

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
## Verification in order (1)
	@@@ Java
	List singleMock = mock(List.class);

	singleMock.add("was added first");
	singleMock.add("was added second");

	InOrder inOrder = inOrder(singleMock);

	inOrder.verify(singleMock).add("was added first");
	inOrder.verify(singleMock).add("was added second");

!SLIDE
## Verification in order (2)
	@@@ Java
	List firstMock = mock(List.class);
	List secondMock = mock(List.class);

	firstMock.add("was called first");
	secondMock.add("was called second");

	InOrder inOrder = inOrder(firstMock, secondMock);

	inOrder.verify(firstMock).add("was called first");
	inOrder.verify(secondMock).add("was called second");

!SLIDE
## Making sure interaction(s)
## never happened on mock
	@@@ Java
	// mockOne, mockTwo, mockThree

	mockOne.add("one");

	verify(mockOne).add("one");
	verify(mockOne, never()).add("two");

	verifyZeroInteractions(mockTwo, mockThree);

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

!SLIDE
## Spying on real objects (1)
	@@@ Java
	List list = new LinkedList();
	List spy = spy(list); // a copy of list is used

	// when(spy.size()).thenReturn(100);

	spy.add("one");
	spy.add("two");

	System.out.println(spy.get(0));
	System.out.println(spy.size());
	// verify(spy).add("one");
	// verify(spy).add("two");

!SLIDE
## Spying on real objects (2)
	@@@ Java
	List spy = spy(new LinkedList());

	// Impossible
	when(spy.get(0)).thenReturn("foo");

	doReturn("foo").when(spy).get(0);

NOTE: Not working on *final* methods

!SLIDE
## Capturing arguments
## for further assertions
	@@@ Java
	ArgumentCaptor<Person> argument =
	  ArgumentCaptor.forClass(Person.class);
	verify(mock).doSomething(argument.capture());
	assertEquals("John", argument.getValue().getName());

!SLIDE


!SLIDE
	@@@ Java
	public void itShouldSendMailAfterConfirmed() {
	  Order order = new Order(...);
	  MailService mailer = mock(MailService.class);
	  order.setMailer(mailer);
	  order.confirm();
	  verify(mailer).send();
	}

!SLIDE
	@@@ Java
	public void itShouldDoXxxWhenSendingMailFailed() {
	  Order order = new Order(...);
	  MailService mailer = mock(MailService.class);
		when(mailer.send(any()))
		  .thenThrow(new MailDeliveryException(...));
	  order.setMailer(mailer);
	  order.confirm();
	  // Verify do xxx
	}
