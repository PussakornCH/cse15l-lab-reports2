# Lab Report 2 - Servers and SSH Keys
[Link](https://www.google.com/search?sca_esv=570462611&rlz=1C1ONGR_enUS939US939&sxsrf=AM9HkKkl37O5ZnMfqCblUa1W33AUWioiKw:1696377116311&q=anime&tbm=isch&source=lnms&sa=X&ved=2ahUKEwjUzrCbiduBAxWLLEQIHUDsCmUQ0pQJegQICRAB&biw=614&bih=571&dpr=1.56#imgrc=f4e_XJIpZO83HM)
## Part 1 "String Servers"

**StringServer.java**

``` bash
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler3 implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> s = new ArrayList<String>();
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("string: %s", s);
        }
        else {
            if (url.getPath().contains("/add-message")) { // decide the name of the function
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    
                    String print = ""; // make new string called print
                    // For loop to replace + with space
                    for(int i = 0; i < parameters[1].length(); i++){
                        if(parameters[1].charAt(i) == '+'){ // replace '+' with space
                            print = print + " ";  
                        }
                        else {
                            print += parameters[1].charAt(i); // add the character from the input.
                        }
                        // print now will contains new string make up of the user input without '+' character.
                    }
                    
                    s.add(print); // Assume that parameters[1] is string
                    num += 1; // for the number in front of the string
                    return String.format("%d. %s", num, print);
                }
            }
            return "404 Error";
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

        Server.start(port, new Handler3()); // Change the name of the Handler to Handler 3.
    }
}
```
**Screenshot from the two messages**

![Image](3-1.JPG)

![Image](3-2.JPG)

