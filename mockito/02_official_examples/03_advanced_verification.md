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
