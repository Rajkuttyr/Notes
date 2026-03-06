client and serveer establishes a connection to communicate 
Sockets are used to establish a connection
Java socket is used to on client to start a communication 
Java server scoket is used to establish a communication on the server

# UDP
In UDP no connection between the server and client
client send the data and server may or may not recive the data

Socket creation
>[!important]
>Socket socket = new Socket("78.46.84.171", 80);
`

To write to a Java `Socket` you must obtain its [`OutputStream`](https://jenkov.com/java-io/outputstream.html). Here is how that is done:
```java
Socket socket = new Socket("jenkov.com", 80);
OutputStream out = socket.getOutputStream();

out.write("some data".getBytes());
out.flush();
out.close();

socket.close();
```

>[!note]
>flush method is used to send the data to the server through the internet