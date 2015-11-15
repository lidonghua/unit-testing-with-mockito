!SLIDE
	@@@ Java
	public void confirm() {
	  Message message = new Message();
	  message.setText("confirmed");
	  mailer.send(message);
	}

!SLIDE
## Capturing arguments
### for further assertions
	@@@ Java
	ArgumentCaptor<Message> argument =
	  ArgumentCaptor.forClass(Message.class);

	verify(mockMailer).send(argument.capture());

	assertEquals("confirmed", argument.getValue().getText());
