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
![Image](lab2_8.jpg)<br>
**1. After `/add-message`**<br>
*Which methods in your code are called?*<br>
The `main` method of *StringServer* is called where the path is recognized by the `handleRequest` method. The `handleRequest` method is called every time the specific URL is requested into the browser.<br>
<br>
*What are the relevant arguments to those methods, and the values of any relevant fields of the class?*<br>
Relevant arguments to this method, and the values of any relevant fields of the class includes `add-message` of the pathway, additionally the `=s` in the query, our print value (what will be printed), in this case our value is `Nicki Minaj`, and our URL.<br>
<br>
*How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.*<br>
The "printOut" field is updated to include the latter portion of the query (in this example, `Nicki Minaj`) because both a valid path and query were provided in the request. Furthermore, the "printOut" field then becomes `Nicki Minaj` + `\n`. Furthermore, as a part of the handleRequest method, the `parameters` field is modified to {"s", "Nicki Minaj"}, which corresponds to the query in the URL.


![Image](lab2_10.jpg) <br>
**2. After second `/add-message` , the effect of this request is to concatenate a new line (\n) and the string after = to the running string, and then respond with the entire string so far.**<br>
*Which methods in your code are called?*<br>
The relevant method that is called to get this output is the `handleRequest` method.<br>
<br>
*What are the relevant arguments to those methods, and the values of any relevant fields of the class?* <br>
Revelvant arguments to this method, and the values of any relevant fields of the class includes `add-message` of the pathway, additionally the "s" in the query, our print value (what will be printed, in this case our value is "Nicki Minaj", and our URL.<br>
<br>
*How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.*<br>
Similar to the last question of question 1, since both a valid path and query were provided in the request, the "printOut" field is updated to include the latter portion of the query. This is such that it now contains both `Nicki Minaj` and `Is The Queen of Rap` where the "printOut" field is `Nicki Minaj\n Is the Queen of Rap\n`. It is also important to mention that the `parameters` within the `handleRequest` method is then updated to a split query with individual key-value pairs of {"s", "Is the Queen of Rap"}.

## Part 2
1. A failure-inducing input for the buggy program I implemented was:<br>
```ruby
  //two added tests
@Test
public void testReversed1() {
  int[] input1 = {2,4,6};
  assertArrayEquals(new int[]{6,4,2}, ArrayExamples.reversed(input1));
}
```
<br>
Here our first `int` array has the elements of `{1,1,1}` with the expected output to be `{1,1,1}`.<br>
<br>
2. An input that doesn't induce a failure, as a JUnit test and any associated code is:
```ruby
@Test
public void testReversed2() {
  int[] input2 = {1,1,1};
  assertArrayEquals(new int[]{1,1,1}, ArrayExamples.reversed(input2));
}
```
<br>
3. The sympton, as the output of running the tests was 0 when expected was 1.<br>
4. The bug, as the before-and-after code change required to fix it.<br>
*Before* <br>
![Image](lab3_4.jpg)<br>
*After* <br>
![Image](lab3_5.jpg)<br>
<br>
**The Bug Identified**<br>
The following is the block of code that contained the bug:<br>
```ruby
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
    }
}
```
In this implementation, the bug can be found in the for-loop that iterated `arr`. The method iterates over the entire list (`for(int i = 0; i < arr.length; i += 1)`) and substitutes each element with its corresponding element from the opposing element (`arr[i] = arr[arr.length - i - 1];`). A potential issue with this approach is that for any array greater than length 1, once the code reaches the halfway point, it replaces the second half of the array with the updated first half, resulting in the overwriting of the already modified values.
<br>
The following code is the corrected implementation of the code:
```ruby
static void reverseInPlace(int[] arr) {
    int temp;
    for(int i = 0; i < arr.length/2; i += 1) {
        temp = arr[i]
        arr[i] = arr[arr.length - i - 1] = temp;
    }
}
```
Here, through the implementation of `temp`, the values of `arr[i]` is saved such that it can be saved to the opposing element (`arr[i] = arr[arr.length - i - 1];`). Additionally, the for-loop has been changed such that rather than going through the entire array, it will iterate through only half of the array (`for(int i = 0; i < arr.length/2; i += 1)`) highlighted by `i < arr.length/2`. 
## Part 3
In this lab, I learned how to identify symptoms. I also learned the interworkings of servers and how to create a web server of my own. This includes writing pathways to the URL.
