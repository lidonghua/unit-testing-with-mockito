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
