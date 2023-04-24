# CSE15L LAB2
## PART 1
In part 1, I will be writing a web server called StringServer that supports the path and behavior described below. It should keep track of a single string that gets added to by incoming requests. <br>
<br>
*The following codeblock details the blocks of code written in StringServer.java* <br>
```ruby
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String print = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(print);
        } else if (url.getPath().equals("/add-message")) {
            System.out.println("Path: " + url.getPath());

            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                String str = parameters[1];
                print = print + str + "\n";
                return print;
            }
        }
        return "404 Not Found!";
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
*The following images details the server outputs:* <br>
<br>
It is important to note that the main method starts the server. This server is where all of our paths and behaviors will be supported on.
![Image](lab2_8.jpg) <br>
**1. After '/add-message'** <br>
*Which methods in your code are called?* The relevant method that is called to get this output is the 'handleRequest' method. <br>
*What are the relevant arguments to those methods, and the values of any relevant fields of the class?* Revelvant arguments to this method, and the values of any relevant fields of the class includes "/add-message" of the pathway, additionally the "s" in the query, and our URL. <br>
*How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.* 

![Image](lab2_10.jpg) <br>
**2. After second '/add-message' , the effect of this request is to concatenate a new line (\n) and the string after = to the running string, and then respond with the entire string so far.** <br>
Which methods in your code are called?
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
