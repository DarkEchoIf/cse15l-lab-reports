# CSE15L Lab Report Week 3: Search Engine and Buggy Methods
## Part1: Simplest Search Engine:
First, I am showing my implementation of a simple search engine.

```

import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class SearchEngineHandler implements URLHandler {
    ArrayList<String> list = new ArrayList<String>();
    ArrayList<String> searchList = new ArrayList<String>();
    public String handleRequest(URI url) {

        if (url.getPath().equals("/")) {
            return "We have these strings stored: " + list;
        } 

        else if (url.getPath().equals("/add")){
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                list.add(parameters[1]);
                return "" + list;
            }
            return "Invalid Operation";
        }
            else {
                if (url.getPath().contains("/search")){
                    String[] parameters = url.getQuery().split("=");
                    if (parameters[0].equals("s")) {
                        for (String word : list){
                            if (word.contains(parameters[1])){
                                searchList.add(word);
                            }       
                        }      
                    return "" + searchList;
                    }
                }
                return "404 not Found!";
            }
        
        }
    }


class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new SearchEngineHandler());
    }
}
```
It is a running program, but far from perfect. Instead of chasing for perfection, let's focus on the functions of the search engine first!
![Add](CSE15L-Week3-SearchEngine-Add.png)
In the first picture, I used 'add' as the path and 's=apple' as the query which decides what string to add to the 'list'. Since 'apple' was added to the list, when we request the page to print 'list' which I will demonstrate later, a list containing 'apple' will be printed.
![Home](CSE15L-Week3-SearchEngine-Home.png)
In the second pocture, I simply typed '/' and went to this 'home' page of the site. By coming to this site, after each time '/add' is called, the updated list with all its current contents will be printed. This feature may seem redundant since I make the program print the updated list whenever the '/add' page is visited, but this feature of '/add' would be removed if I am going to improve the program. Just calling '/' won't change any value in the program. It simply shows what has been changed by other methods.
![Search](CSE15L-Week3-SearchEngine-Search.png) 
Before calling '/search', I added 'pineapple' to the list so the purpose of '/search' will be more obvious. When we use path '/search' then query '?s=app', a method to find strings in list that contain substring 'app' was excuted. A list of valid strings will be returned as a result. This method does not change nor update the value in the program.
## Part2: Buggy Methods:
For the ‘reverInPlace’ method in ArrayExamples.java, the failure-inducing input is an array of integers that need to be reversed. Due to the false implementation of the method, as long as a list has a size larger than 1, does not have identical elements or mirrored elements, the test will be a failure: instead of having a reversed array, the method returns a mirrored array which has the second half of the original array on both sides. 
The bug for this method lies in the for loop
The
``` 
arr[i] = newArray[arr.length - i - 1];
```
This line can reverse the second the half of the array; however, since the reverse is in place, when it comes to the second half of the array, the method is making each elements to change to it self, resulting a mirrored array in the end.
