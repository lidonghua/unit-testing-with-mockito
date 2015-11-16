!SLIDE
## The Mockito Solution
	@@@ Java
	public class Order {
	  private MailService mailer;
	  public void confirm() {
	    // ...
	    mailer.send(new Message(...));
	  }
	  // ...
	}

!SLIDE
	@@@ Java
	public void itShouldSendMailAfterConfirmed() {
	  Order order = new Order(...);
	  MailService mailer = mock(MailService.class);
	  order.setMailer(mailer);

	  order.confirm();

	  verify(mailer).send();
	}

!SLIDE
	@@@ Java
	public void itShouldDoXxxWhenSendingMailFailed() {
	  Order order = new Order(...);
	  MailService mailer = mock(MailService.class);
	  when(mailer.send(any()))
	    .thenThrow(new MailDeliveryException(...));
	  order.setMailer(mailer);

	  order.confirm();

	  // Verify do xxx
	}

!SLIDE
# Be Careful
### Mocks can couple the test
### to the implementation detail
