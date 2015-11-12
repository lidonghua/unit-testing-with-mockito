!SLIDE
## How to deal with
## network & database?

!SLIDE
# Collaborators

!SLIDE
# Isolation

!SLIDE
# Test Double

!SLIDE
## Pretend object used
## in place of a real object
## for testing purposes

!SLIDE
## Dummy/Fake/Stub/Mock/Spy

!SLIDE
	@@@ Java
	public interface MailService {
	  public void send(Message msg);
	}

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
	  MailService mailer = ???
	  order.setMailer(mailer);
	  order.confirm();
	  // How to verify?
	}

!SLIDE
	@@@ Java
	public class MailServiceStub implements MailService {
	  private List<Message> messages = new ArrayList<>();
	  public void send(Message msg) {
	    messages.add(msg);
	  }
	  public int numberSent() {
	    return messages.size();
	  }
	}

!SLIDE
	@@@ Java
	public void itShouldSendMailAfterConfirmed() {
	  Order order = new Order(...);
	  MailServiceStub mailer = new MailServiceStub();
	  order.setMailer(mailer);
	  order.confirm();
	  assertEquals(1, mailer.numberSent());
	}
