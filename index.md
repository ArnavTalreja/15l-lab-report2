# PART 1: Server StringServer
Following is the java code for StringServer:-
```Java
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {

    //private static final String WELCOME_MESSAGE = "Welcome!"; 
    String message = new String();    
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Welcome!");
        } else{
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    message += parameters[1] + "\n";
                    return String.format(message);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
The following is the output for the code:-



## Input 1:-
![Image](s1.png)
## Output 1:-
![Image](1.jpg)

We compile and run the StringServer.java file. The main method of the Java file is invoked, which in turn creates a new Server object.\
The server object uses the handleRequest method of the Handler class to handle all the URIs.\
The port number and a new handler object are passed as arguments to the server class. The URI is passed as arguments to the handleRequest method.\
The URI changes from `localhost:1983/` to `localhost:1983/add-message?s=My%20name%20is%20Arnav`\
The String `message` which was an empty string, now has `My name is Arnav` concatenated to it.



## Input 2:-
![Image](s2.png)
## Output 2:-
![Image](2.jpg)

We compile and run the StringServer.java file. The main method of the Java file is invoked, which in turn creates a new Server object.\
The server object uses the handleRequest method of the Handler class to handle all the URIs.\
The port number and a new handler object are passed as arguments to the server class. The URI is passed as arguments to the handleRequest method.\
The URI changes from `localhost:1983/add-message?s=My%20name%20is%20Arnav` to `localhost:1983/add-message?s=This%20is%20for%20lab%20report`\
The String `message` which had the string `My name is Arnav`in it, now has `This is for lab report` concatenated to it.


# PART 2: Fixing 🐛s!

