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
	assertThat(Matcher matcher)

!SLIDE
# Matcher

!SLIDE
## Custom Message
	@@@ Java
	assertEquals(expected, actual)
	assertEquals(String message, expected, actual)
