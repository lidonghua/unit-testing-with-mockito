!SLIDE
# Assertions

!SLIDE
## <del>Assert.assertEquals</del>
	@@@ Java
	// ALWAYS use static import
	import static org.junit.Assert.*;

!SLIDE
## Types
	@@@ Java
	// T in { byte, char, short, int, long, Object }
	assertEquals(T expected, T actual)

	// T in { long, Object }
	assertNotEquals(T expected, T actual)

!SLIDE
## Floating-point
	@@@ Java
	// T in { float, double }
	assertEquals(T expected, T actual,
	             T epsilon)

	assertNotEquals(double expected, double actual,
	                double epsilon)

!SLIDE
	@@@ Java
	assertTrue(boolean condition)
	assertFalse(boolean condition)

!SLIDE
	@@@ Java
	assertNull(Object object)
	assertNotNull(Object object)

!SLIDE
	@@@ Java
	assertSame(Object expected, Object actual)
	assertNotSame(Object expected, Object actual)

!SLIDE
	@@@ Java
	// T in { byte, char, short, int, long, Object }
	assertArrayEquals(T[] expected, T[] actual)

	// T in { float, double }
	assertArrayEquals(T[] expected, T[] actual,
	                  T epsilon)

!SLIDE
	@@@ Java
	fail()

!SLIDE
	@@@ Java
	// Note: expected and actual are reversed
	assertThat(T actual, Matcher expected)

!SLIDE
# Matcher

!SLIDE
	@@@ Java
	import static org.junit.matchers.JUnitMatchers.*;

	assertThat("albumen",
	           both(containsString("a"))
	             .and(containsString("b")));

	assertThat(Arrays.asList("one", "two", "three"),
	           hasItems("one", "three"));

	assertThat(Arrays.asList("fun", "ban", "net"),
	           everyItem(containsString("n")));

!SLIDE
	@@@ Java
	import static org.hamcrest.CoreMatchers.*;

	assertThat("good", allOf(equalTo("good"),
	                         startsWith("good")));

	assertThat("good", not(allOf(equalTo("bad"),
	                             equalTo("good"))));

	assertThat("good", anyOf(equalTo("bad"),
	                         equalTo("good")));

!SLIDE
	@@@ Java
	import org.hamcrest.core.CombinableMatcher;

	assertThat(7, not(CombinableMatcher
	                    .<Integer>either(equalTo(3))
	                    .or(equalTo(4))));

!SLIDE
## Custom Message
	@@@ Java
	assertEquals(T expected, T actual)
	assertEquals(String message, T expected, T actual)
