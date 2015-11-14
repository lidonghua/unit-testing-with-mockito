!SLIDE
# Differences

!SLIDE
	@@@ Java
	// JUnit
	assertEquals(expected, actual)

	// TestNG
	assertEquals(actual, expected)

!SLIDE
	@@@ Java
	// JUnit
	@Before
	@After

	// TestNG
	@BeforeMethod
	@AfterMethod

!SLIDE
	@@@ Java
	// JUnit
	@Ignore

	// TestNG
	@Test(enable=false)

!SLIDE
	@@@ Java
	// JUnit
	@Test(expected=Exception.class)

	// TestNG
	@Test(expectedExceptions=Exception.class)

!SLIDE
## It may be broken in TestNG!
	@@@ Java
	class CalculatorTest {
	  Calculator calculator = new Calculator();

	  @Test void test1() {
	    // Use calculator
	  }

	  @Test void test2() {
	    // Use calculator
	  }
	}
