
[Index](https://zcashe.github.io/cse15l-lab-reports/index.html)
---
# Lab 2 Report 
---
# Part 1
## Code for Chat Server
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    
    String chatString = "";
    
    public String handleRequest(URI url) {
       
        if (url.getPath().equals("/")) {
            return chatString;
        } else if (url.getPath().contains("add-message")) {
            System.out.println(url.getPath());
            System.out.println(url.getQuery());
            String[] parameters = url.getQuery().split("[=&-]");
                if (parameters[0].equals("s")) {
                    chatString = chatString + parameters[3]+ ": " + parameters[1] + "\n";
                    chatString = chatString.replaceAll("\\+", " ");
                    
                    }
                    
                    
                    
                    return chatString;
        }else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
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


## Using add message first time
![Image](assets/Lab2-Message2.png)

### Methods Called:
1. HandleRequest(URI url)
> This is the very first method being called and all other methods are called within this method. This method takes in the url which is type URI as an argument, and then based on comparisons either returns chatString unupdated, "404 Not Found!", or the updated chatString.
 
2. url.getPath() - gets path of the URL
> This is not called on its own it is used in combination with other methods, but this method returns a string with the path of the url, so when we update the url with add-message?s=Hi bruh&user=Zac, this returns just "/message" which was unexpected as I thought it would include the query as well.
   
3. url.getQuery() - gets query from URL
> This also is not used on its own, but similar to getPath(), getQuery just returns the string with the query in the url so when we update the url with add-message?s=Hi bruh&user=Zac, "s=Hello breh&user=Zac" gets returned.


4. url.getPath().equals("/") - Returns true if the path is /
> This has an argument "/" and the method checks to see if the path is simply "/".
 
5. url.getPath().contains("add-message") - Returns true if add-message is contained in path
> This has an argument "add-message" and if the path contains this string, it will return true.

 
6. url.getQuery().split("[=&-]") - splits query based on input
  > This has the argument "[=&-]" which tells the split method to separate the query string into a string array based on the = and & signs.



7. chatString.replaceAll("\\+", " ") - replaces + in chatString with space
> This has the argument "\\+", " " which replaces all the + signs with space.




### Other relevant argument field values:

W have the empty chatString value, the string array parameters which will contain the split url query.


### Which values change:

When we load the new page with /add-message?s=Hi bruh&user=Zac the URI objects changes so now
the url query value is now changed to be ?s=Hi+bruh&user=Zac and url path value is /add-message 

Then parameters is updated to be the string array of the query split at the = and & signs, making it a length 4 array where

Parameters[0] = s

Parameters[1] = Hi+bruh

Parameters[2] = user

Parameters[3] = Zac

Then since parameters[0] = s, chatString gets updated
to append "Zac: Hi+Bruh" and the new line.

Then because of the url encoding, the space gets turned into +, so we change it back to a space before we display finally getting chatString = "Zac: Hi Bruh \n".

## Using add message second time
![Image](assets/Lab2-Message1.png)

### Methods Called:
1. HandleRequest(URI url)
> This is the very first method being called and all other methods are called within this method. This method takes in the url which is type URI as an argument, and then based on comparisons either returns chatString unupdated, "404 Not Found!", or the updated chatString.
 
2. url.getPath() - gets path of the URL
> This is not called on its own it is used in combination with other methods, but this method returns a string with the path of the url, so when we update the url with add-message?s=Yo Wassup&user=Lil bro, "/add-message" gets returned.
   
3. url.getQuery() - gets query from URL
> This also is not used on its own, but similar to getPath(), getQuery just returns the string with the query in the url so when we update the url with add-message?s=Hi bruh&user=Zac, "s=Yo+Wassup&user=Lil+bro" gets returned.


4. url.getPath().equals("/") - Returns true if the path is /
> This has an argument "/" and the method checks to see if the path is simply "/".
 
5. url.getPath().contains("add-message") - Returns true if add-message is contained in path
> This has an argument "add-message" and if the path contains this string, it will return true.

 
6. url.getQuery().split("[=&-]") - splits query based on input
> This has the argument "[=&-]" which tells the split method to separate the query string into a string array based on the = and & signs.



7. chatString.replaceAll("\\+", " ") - replaces + in chatString with space
> This has the argument "\\+", " " which replaces all the + signs with space.





### Other Relevant arguments and field values:


We have the current chatString value "Zac: Hi bruh \n", the string array parameters which will contain the split url query.


### Which values change:

When we reload the new page with /add-message?s=Yo Wassup&user=Lil bro the URI objects changes so now
the url query value is now changed to ?s=Yo+Wassup&user=Lil+bro. 
The url path value gets updated to /add-message again.

Once again the string array parameters is updated to be a string array of the query split at the = and & signs, making it a length 4 array where

Parameters[0] = s

Parameters[1] = Yo+Wassup

Parameters[2] = user

Parameters[3] = Lil+bro

Then since parameters[0] = s, chatString gets updated
to append "Lil bro: Yo Wassup" and the new line.


Once again because of the url encoding, the spaces got turned into +, so we change them back to a space before we display.

This gives the update chatString variable "Zac: Hi bruh \n Lil bro: Yo wassup \n" 
Where the \n represents new lines.

We then display this message.




---

# Part 2
---
## Absolute path to private key 
```
/Users/zac/.ssh/id_rsa
```


## Absolute pash to public key from ieng6 file system
```
/home/linux/ieng6/oce/9e/zelders/.ssh/authorized_keys
```
## LS and absolute path to  private key screenshot 
![Image](assets/Lab2-privateKey.png)
## LS and absolute path to public key screenshot
![Image](assets/Lab2-PublicKey.png)

## SSH in without password
![Image](assets/Lab2-ssh.png)

---
# Part 3
## What have I learned in the past 2 weeks?
> Before these last 2 labs, I had no idea that it was possible to generate a public and private ssh key, which I can use to log in without my password. I also learned about how queries work in java and how to run a web server. I think the web servers seem interesting and I want to see what else can be done with them. The concept of URIs and URI handling was new to me as well, however I think I have a good grasp of the concept now that I made my own system to handle changes in URLs.
---
