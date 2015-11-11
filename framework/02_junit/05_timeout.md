!SLIDE
# Test Performance

!SLIDE
	@@@ Java
	// Timeout in milliseconds
	@Test(timeout=1000)
	public void testWithTimeout() {
	  // ...
	}

!SLIDE
## Apply to entire test class
	@@@ Java
	public class HasGlobalTimeout {
	  // 5 seconds max per method tested
	  @Rule
	  public Timeout globalTimeout = Timeout.seconds(5);

	  @Test
	  public void testInfiniteLoop1() { for (;;) {} }

	  @Test
	  public void testInfiniteLoop2() { for (;;) {} }
	}
