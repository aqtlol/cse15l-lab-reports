# Lab Report 2 - Week 3
## Part 1 - Simplest Search Engine
During lab we were tasked with creating a web server and then using the url to manipulate the webserver. We created a simple search engine. By typing `/add` into the url as the path of our server we could then include a query where we add words to our array. Then using `/search` we could query a string to search for any strings we added to our array. Here is my code!
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.Arrays;

class daHandler implements URLHandler {
    // Code copied and changed from NumberServer.java provided by CSE15l

    // Recieved help from Angela in my lab group
    
    int num = 0;
    ArrayList<String> sList = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } 
        else if (url.getPath().equals("/search")) {
            // return "search works";
            String searchChar = url.getQuery().split("=")[1];
            ArrayList<String> output = new ArrayList<>();
            for(int i = 0; i < sList.size(); i++) {
                if(sList.get(i).contains(searchChar)) {
                    output.add(sList.get(i));
                }
            }
            return Arrays.toString(output.toArray());
        } 
        else {
            // System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                // return "add works";
                String[] parameters = url.getQuery().split("="); // My changes are below to the add method.
                // if (parameters[0].equals("s")) {
                     sList.add(parameters[1]);
                    return Arrays.toString(sList.toArray());
               // }
            }
            return "Error bro";
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

        Server.start(port, new daHandler());
    }
}
```
Pretty cool right!
Here you can see me using the add command to add in my name, Matthew.
![Image](week-3-screenshots/myNameSS.png)
The method being called in the code is the only method in `daHandler` class which is the `handleRequest` method. 

The `handleRequest` method goes into a if, else if, else statement. In the else statement the method checks if the url path contains `/add`. Since it does, the method splits the query by the `=` and stores the 2 split strings into a string array `parameters`. Using `parameters[1]` the method accesses the string argument. The string argument is then added to the array of strings `sList`. 
> `sList` is an array list of type `String` outside of the method that stores all of the strings we are going to add into our array and display on our website. 

Finally the method returns `sList` demonstrating the string array on my website and revealing the string I added, in this case my name.

So what changed?
* `sList` went from being empty to containing the string `Matthew`

Next I added a few more strings.
![Image](week-3-screenshots/lotsOfAdds.png)
Here a similar request is being made to the one explained above since we are calling the `handleRequest` method again.

The same steps occur as explained above but the difference here is that `sList` is not empty, it has been filled with a bunch of other strings.

So what is changing?
* Again `sList` is changed. It now contains a new string at the end of the array, `tritons`

Finally I used to search to see what sorts of *goo*🦠 I had in my site.
![Image](week-3-screenshots/searchGoo.png)
Look at all that **goo**🦠🦠🦠

But in all seriousness we can see that I added lots of strings in my array that matched the search query `goo`

So what is going on here? We are actually still using the same `handleRequest` method, however, we are accessing a different part of the if, else if, else statements.

In the `else if` statement the method checks if the path of the url is equal to `/search` and it is. The url query is split and indexed at 1 to access the string arugment in the url. The string argument is set to the field `searchChar`. Now a new string array is created called `output`, this is where the strings the match our search will be added to. Next a for loop checks to see if each string element in `sList` contains the search string. If the string in `sList` contians the search string, then the string is stored into the new `output` array. Finally once the loop checks all of the strings in `sList`, the method returns `output` containing the strings that matched the search query.

So what changed?
* Well the else if statement created a new string array `output`
* The strings in `sList` that contained the search query `goo` were stored into `output`
* [googe, goop, goob, goober]
## Part 2
Here we were testing some code using J-unit and fixed bugs. I decided to fix the `reversed` method from `ArrayExamples.java` and the `blank` from `LinkedListExample.java`

------

**Reversed**

The failure-inducing input I typed up was: 
```
@Test
  public void testMyReversed() {
    int[] input = {1, 2, 3};
    assertArrayEquals(new int[] {3, 2, 1}, ArrayExamples.reversed(input));
  }
  ```
Symptom:
![Image](week-3-screenshots/reversedSymptom.png)
The symptom is that the expected array and the actual array have different elements at the index 0. The test is expecting index 0 to be 3 but instead it was 0.

Bug fix:
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[arr.length - i - 1] = arr[i];
    }
    return newArray;
  }
  ```
Why did the symptom occur from bug?

From what I think the previous code for the `reversed` method had 2 bugs that caused the symptom to occur. First off the code was originally returning `arr` which was not the `newArray` that was created. Secondly the code was storying ints from `newArray` into `arr`. Since `newArray` was a new array that did not contain anything there was nothing to store into `arr`, and so `arr` stored 0 for all of its indicies. That is why in the symptom the expected and actual values differ at index 0. That also explains why the actual value was 0 instead of being 3.


-------
**method**