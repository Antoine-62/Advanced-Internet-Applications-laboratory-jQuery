# Advanced Internet Applications – laboratory - jQuery

Description : The aim of this labotory was to learn some functionalities of jQuery, such as using various selector, using json data, using promise..., by doing some exercices.  
Important : In every code, there are comments which describe the functionalities.  

## Selectors

The code related to this part is contained in Selector.html

### Question 3

```
 $('div').css('color', 'green');
 $('.c').css('font-size', 'x-large');
 $('tr + tr').css('color', 'aqua');
```

* The first line will change all div elements in green
* The second line will set the size as X-large for each element with class ".c"
* The last line will set color as aqua for each table row other than the first row


### Question 4

```
$('table tr:first').css('color', 'yellow');
$('tr:last').css('color', 'yellow');
$('p:even').css('color', 'orange');
```

* The first line will select the first row of the table, to set its color as yellow
* The second line will select the last row of the table, to set its color as yellow
* The last line will select each row with an even index number

### Question 5

```
$('[href]').css('border', '1px solid black').css('padding', '3px');
$('a[href*=kalaka]').css('border', '1px solid pink');
$('a[href$=\'.pdf\']').css('border', '1px solid red');
```

* The first line selects every links
* The second line selects every links which contains "kalaka"
* The third line selects every links which redirect to a pdf

## Style

The code related to this part is contained in Style.html

### Question 6

```
alert('The color of an element withid="a" is'+ $('#a').css('color'));
```

We get the color of every elements from class ".a".

### Question 7

```
$('button:contains(\'A\')').click(function() { //We add 'asdf' class to #classic when we click on a button which contain "A" 
                    $('#classic').addClass('asdf');
                });
                
$('button:contains(\'B\')').click(function() { //We remove 'asdf' class to #classic when we click on a button which contain "B" 
                    $('#classic').removeClass('asdf');
                });
                
$('button:contains(\'C\')').click(function() {//Do the 2 functionalities before
                    $('#toggle').toggleClass('asdf');
                });
```

* The addClass method will add a class to selected element
* The removeClasss method will remove a class to selected element
* The toggleClass method toggles between adding and removinga class to selected element

### Question 8

```
$('tr:even').addClass('asdf');// set asdf class to every 2 row table
```

It will add the class "asdf" to every table row with an even index number

### Question 9

Our list with "a" class in our html file
```
<ol class ="a" type="1">
       <li>Coffee</li>
       <li class ="b">Tea</li>
       <li>Milk</li>
</ol> 
```
Our script, which will add "asf" class for each element of the list with "a" class, other than element from "b" class.

```
$('.a li').addClass('asdf');
$('.b').removeClass('asdf');
```
## Events

The code related to this part is contained in Events.html

### Question 10
Our edit function
```
                function edit()
                {
                    var Edit = document.createElement("input");//create an input
                    Edit.setAttribute("type", "text");//set attribute text to input
                    Edit.setAttribute("id","edit");//Set "edit" as id
                    var br = $(this).text();//Retrieve the current of the row
                    this.innerHTML="";//remove the text
                    Edit.setAttribute("value",br);//We set the retrieved text in our input
                    $(this).append(Edit);//We add the input to the row
                    let test = $(this);//we store the current element selected in a variable
                    
                    $("#edit").focus();// we set focus on our created input
                    
                    $("#edit").blur(function(){//When our input element loses its focus
                        var name= $("#edit").val();//we retrieve the value in the element
                        $("#edit").remove();//we remove our input
                        test.append(name);//we add the value as text - we use test and no this because we click on another element
                        test.one('click', edit);//we assign the edit function to the click event for  one-time execution.       
                    });
                }
```

Everythings is explained with the comments.
Some additionals explanations :
* We have to be careful with the reference *this*, we easily forget we are not in the same context. For example, here, we must store our row selected before we set focus on the input, because after we set focus on our input, "this" will refer to the input, and no our row.
* To get value from of the <input> field, we will use val() method
* To get text from an inner content, we will use text() method
* To get text with html balises from an inner content, we will use text() method

### Question 11
When we add the following code to our script, an alert will be trigged each time we click edit on table row. Not very funny.
```
$('button').bind('asdf', function() { alert('The cake is a lie!'); });
```
```
$('button').trigger('asdf');
```

The following code will disable all events of our script.
```
$('*').unbind();//disable all events
```
## Ajax

The code related to this part is contained in AJAX.html

### Question 12
**When I tried to use load() method, I've had some errors with my browsers (FireZilla, and Chrome), by watching the solutions, uncle Google told me that I need a web server for running my code, so I store my code in wampserver, that I already used before for some projects**

When I use back button, I leave the page.


## Animations

The code related to this part is contained in AJAX.html

### Question 13
The following code should works as following :
* First, the code disappears (we hide the element)
* Then, we load the content
* Finally, we display the elements with the loaded content

However, it runs like following :
* It load and add the content
* It hide the element
* It display the element

Jquery will first load the content, and then run the code.
```
$('#content').fadeOut();
$('#content').load('AJAX'+ $(this).attr('href'));
$('#content').fadeIn()
```
The following code works well 

```
$('a').click(function() {
            let thisA = $(this);
            $('#content').fadeOut('medium', function() {//here, the content (the div) "disappear" directly, it doesn't wait to load data
                $('#content').load('AJAX'+ thisA.attr('href'), function() {//load some contents and then append to content (the div)
                    $('#content').fadeIn();//Show the content (the div)
                    });
                });
                return false;
            });
```
The program will first wait the element is hidden, and then it will load the content.  
We cannot use the *this* reference, because we select the div content, and then the *this* will refer to the div content, no our url address.
### Question 14
```
 $('a').click(function() {
                $('#content').animate({height: '0px', width: '0px'}, ()=>{//The height and width of the content "shrink"(with animation) to 0px for both
                    $('#content').load('AJAX'+ $(this).attr('href'), () => {//we load some contents to append to content (the div) - Here we can use this because we are still in the same function 
                        $('#content').animate({ height: '500px', width: '500px'//the height and widht "grow up"(with animation) to 500px
                        });
                    });//Here we couldn't use the this reference, but it's good because we don't need it here :)
                });
            return false;});//if we remove it, the function become obsolete, and the link will be an normal link (actually, you will be redirected to url)
        });
```

Here we could use the *this* reference because we are still the in the function following the selected element (Please read comments, you will understand better).  
If we remove the *false*, the function will become obsolete, and then our link become single link (we'll be redirected to another page).
## JSON

The code related to this part is contained in json.html
### Question 15

Our function to load  the data from a json file, and then display it in a form of a list
```
 $("button").click(function(){//when we click on the button
        $.getJSON("guitars.json", function(data){//we retrieve json data from url, and then we store them in the variable "data"
           console.log(data.Guitars.Guitar);//Display in the console the data contained in guitar->a test to see how we can accsess to objects contained in json data
           var list = data.Guitars.Guitar;
           $(list).each(function(index) {//For each elements in the object guitar
               let tr = document.createElement("tr");//we create a tr element
               let td = document.createElement("td");//we create a td element
               td.append(list[index]['Brand']);//we add the element 'brand' of our guitar to our td 
               tr.append(td);//we add td to our row
               let td2 = document.createElement("td2");//We create a second td element for the model
               td2.append(list[index]['Model']);//We add the element 'Model' of our guitar to our td
               tr.append(td2);//we add the second td to our row
               $("#tab").append(tr);//finally, we add the row to our table
             });
        });
        });
```
Everything is explained in the code comments.  

## Promises

The code related to this part is contained in Promise.html

### Question 16

Our function which for a given url address parameter, will return a promise which makes an HTTP call to the given address.
```
function get(url) {
      // Return a new promise.
      return new Promise(function(resolve, reject) {
       // Do the usual XHR stuff
       var req = new XMLHttpRequest();
       req.open('GET', url);

     req.onload = function() {
      // This is called even on 404 etc
      // so check the status
      if (req.status == 200) {//if our statut is 200
        // then resolve the promise with the response text
        resolve(req.response);
      }
      else {
        // Otherwise reject with the status text
        // which will hopefully be a meaningful error
        reject(Error(req.statusText));
      }
    };

    // Handle network errors
    req.onerror = function() {
      reject(Error("Network Error"));//we say the errors come from network
    };

    // Make the request
    req.send();
     });
    }
```
Everything is explained in the code comments. I don't have additionals explanations here.
## Conclusion
In this exercice, I improved my skills with jQuery, and I understood a lot better the promises (before I used it without really know what is it, like a black box). I didn't met serious problems.  
I thank my teacher, sir Piernik, for this exercice and new skills acquired.
