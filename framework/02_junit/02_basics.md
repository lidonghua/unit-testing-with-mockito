!SLIDE
## SUT (System Under Test)
	@@@ Java
	public class Calculator {
	  public int evaluate(String expression) {
	    int sum = 0;
	    for (String summand: expression.split("\\+"))
	      sum += Integer.valueOf(summand);
	    return sum;
	  }
	}

!SLIDE
## Test
	@@@ Java
	import org.junit.Test;

	public class CalculatorTest {
	  @Test
	  public void evaluatesExpression() {
	    // Test goes here
	  }

	  @Test public void anotherTest() {}
	}

!SLIDE
### Test Structure
# 3A

!SLIDE
# Arrange
# Act
# Assert

!SLIDE
	@@@ Java
	import static org.junit.Assert.assertEquals;

	@Test
	public void evaluatesExpression() {
	  // Arrange
	  Calculator calculator = new Calculator();
	  // Act
	  int sum = calculator.evaluate("1+2+3");
	  // Assert
	  assertEquals(6, sum);
	}

!SLIDE
	@@@ Java
	@Test public void addOneNumber() {
	  Calculator calculator = new Calculator();
	  int sum = calculator.evaluate("0");
	  assertEquals(0, sum);
	  calculator.close();
	}

	@Test public void addTwoNumbers() {
	  Calculator calculator = new Calculator();
	  int sum = calculator.evaluate("1+2");
	  assertEquals(3, sum);
	  calculator.close();
	}

!SLIDE
## Set Up
## and
## Tear Down

!SLIDE
	@@@ Java
	private Calculator calculator;

	@Before public void setUp() {
	  calculator = new Calculator();
	}
	@Test public void addOneNumber() {
	  int sum = calculator.evaluate("0");
	  assertEquals(0, sum);
	}
	@Test public void addTwoNumbers() {
	  int sum = calculator.evaluate("1+2");
	  assertEquals(3, sum);
	}
	@After public void tearDown() {
	  calculator.close();
	}

!SLIDE
	@@@ Java
	@BeforeClass
	public static void init() {}

	@Before
	public void setUp() {}

	@After
	public void tearDown() {}

	@AfterClass
	public static void destroy() {}

!SLIDE
	@@@ Java
	private Calculator calculator = new Calculator();

	@Test public void addOneNumber() {
	  int sum = calculator.evaluate("0");
	  assertEquals(0, sum);
	}

	@Test public void addTwoNumbers() {
	  int sum = calculator.evaluate("1+2");
	  assertEquals(3, sum);
	}

!SLIDE
# It works!
	@@@ Java
	public class TestThis {
	  @Test public void test1() {
	    System.out.println(this);
	  }

	  @Test public void test2() {
	    System.out.println(this);
	  }
	}
