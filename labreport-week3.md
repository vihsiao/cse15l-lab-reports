# Lab Report - Week 3

## **Part 1: Search Engine**

The Java code for my Search Engine is down below 

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    String s = "";

    ArrayList<String> queries = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Current list: %s", queries.toString());
        }

        else if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");
            queries.add(parameters[1]);
            return String.format("%s added to the list!", parameters[1]);
        }

        else {
            if (url.getPath().contains("/search")) {
                String[] parameters = url.getQuery().split("=");
                String return_str = "";

                for (int i = 0; i < queries.size(); i++) {
                    if (queries.get(i).contains(parameters[1])) {
                        return_str += (queries.get(i) + " ");
                    }
                }

                return return_str;
            }

            if (url.getPath().contains("/delete")) {
                
            }
        }

        return "404 Not Found!";
    }
}

public class SearchEngine {
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

After compiling the code (commands: `javac Server.java SearchEngine.java` and `java SearchEngine (port number)`), the domain will open at `http://localhost:(port number)/`

![](localhost.png)

The program Server.java allows the localhost to run

The method `handleRequest` is running while the localhost is active

It sees that there is no path, so it prints the line:  `Current list: []`

------

To add an item to the list, you enter the localhost link into the search bar, plus the path `add?s=valorant` (in this case, I added the item `valorant`)

![](additem.png)

Return to the main page, and the list will contain the item
you just inputted

![](updatedlist.png)

When you add the path `add?s=valorant` to the localhost, it calls the if statement looking for the keyword `add`, so it will get the part after the `=` and add it to the list

```
else if (url.getPath().contains("/add")) {
    String[] parameters = url.getQuery().split("=");
    queries.add(parameters[1]);
    return String.format("%s added to the list!", parameters[1]);
}
```
---

**Updated list:**

![](currentlist.png)

After adding some items, when searching for an item, you change the path to `search?s=` and after the equals sign you add the keyword (in this case `"f"`)

![](query.png)

This command returns all keywords with the character "f" in it

When using the search keyword it activates this if statement, and gets the keyword by pulling the url and getting the path after the `"="`

```
if (url.getPath().contains("/search")) {
    String[] parameters = url.getQuery().split("=");
    String return_str = "";

    for (int i = 0; i < queries.size(); i++) {
        if (queries.get(i).contains(parameters[1])) {
            return_str += (queries.get(i) + " ");
        }
    }

    return return_str;
}
```
---

## **Part 2: Catching Bugs**