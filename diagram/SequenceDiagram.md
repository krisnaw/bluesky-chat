# Chat Sequence Diagrams

### What happen when user open the app
- Client(UI) -> localStorage: loadMessage()
- localStorage -> Client(UI): messages
- Client(UI) -> Client(UI) : Render the list of message

### What happen when user send a message from left chat box

- LeftChatPanel -> Client(UI) : submitMessage()
- Client(UI) -> Client(UI) : message(sender = "left", text, createdAt)
- Client(UI) -> SocketServer: emitMessage()
- Client(UI) -> localStorage: saveMessage()

### How does the message reach the other chat box?

- Client(UI) -> SocketServer : emitMessage(message)
- SocketServer -> Clients : broadcastMessage(message)
- Client(UI) -> Client(UI) : renderMessageAndFlashBasedOnSender()

### What happens when the page is refreshed or reopened?

- Client(UI) -> localStorage: loadMessages()
- localStorage -> Client(UI): messages
- Client(UI) -> Client(UI): restore conversation
- Client(UI) -> SocketServer: reconnect()




