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
