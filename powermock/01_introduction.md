!SLIDE
## How to mock (stub)
## *static*/*private* methods?

!SLIDE
# *NEVER*
### for your own code

!SLIDE
### Avoid static methods in your class

!SLIDE
### Test private methods indirectly

!SLIDE
## But sometimes, you know,
# I really need to...

!SLIDE
# ¯\\\_( ツ )\_/¯

!SLIDE
![PowerMock Logo](powermock-logo.png)

!SLIDE
## A framework that extends
## other mock libraries
## with more *powerful* capabilities

!SLIDE
## Enable mocking of
### *static* methods,
### *constructors*,
### *final* classes and methods,
### *private* methods,
### removal of *static initializers*
### and more...

!SLIDE
## Maven (JUnit 4.4+)
	@@@ XML
	<dependency>
	  <groupId>org.powermock</groupId>
	  <artifactId>powermock-module-junit4</artifactId>
	  <version>1.6.3</version>
	  <scope>test</scope>
	</dependency>
	<dependency>
	  <groupId>org.powermock</groupId>
	  <artifactId>powermock-api-mockito</artifactId>
	  <version>1.6.3</version>
	  <scope>test</scope>
	</dependency>

!SLIDE
## Maven (TestNG)
	@@@ XML
	<dependency>
	  <groupId>org.powermock</groupId>
	  <artifactId>powermock-module-testng</artifactId>
	  <version>1.6.3</version>
	  <scope>test</scope>
	</dependency>
	<dependency>
	  <groupId>org.powermock</groupId>
	  <artifactId>powermock-api-mockito</artifactId>
	  <version>1.6.3</version>
	  <scope>test</scope>
	</dependency>
