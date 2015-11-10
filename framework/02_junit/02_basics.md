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
