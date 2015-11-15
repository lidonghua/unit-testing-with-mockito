!SLIDE
## Spying on real objects (1)
	@@@ Java
	List list = new LinkedList();
	List spy = spy(list);

	when(spy.size()).thenReturn(100);

	spy.add("one");
	spy.add("two");

	System.out.println(spy.get(0));
	System.out.println(spy.size());

!SLIDE
## Spying on real objects (2)
	@@@ Java
	List spy = spy(new LinkedList());

	spy.add("one");
	spy.add("two");

	verify(spy).add("one");
	verify(spy).add("two");

!SLIDE
## Spying on real objects (3)
	@@@ Java
	List spy = spy(new LinkedList());

	// Impossible
	when(spy.get(0)).thenReturn("foo");

	doReturn("foo").when(spy).get(0);

!SLIDE
## A copy is used when spying
	@@@ Java
	List list = new LinkedList();
	List spy = spy(list);

	spy.add(new Object());

	assertEquals(1, spy.size());
	assertEquals(0, list.size());
