# Notes
## AJAX
Asynchonous Javascript and XML

How is this different from Javascript?

`const` is used like a variable

DOM DOM DOMDOMDOMDOM lol

## DOM
Javascript can manip the DOM 

## WTF is ARROW FUNCTION
Atleast this teacher says it full name instead of just "arrow"

`=>`

In python and others this doesnt mean the same thing. Lets take a look elsewhere to get some answers atleast.

[Thank you MDN!](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

An arrow function expression is a compact alternative to a traditional function expression, with some semantic differences and deliberate limitations in usage:

    * Arrow functions don't have their own bindings to this, arguments, or super, and should not be used as methods.
    * Arrow functions cannot be used as constructors. Calling them with new throws a TypeError. They also don't have access to the new.target keyword.
    * Arrow functions cannot use yield within their body and cannot be created as generator functions.

It allows you to call a simple function without having to write a whole new function. The one good example I can find on MDN:

``` javascript
// Easy array filtering, mapping, etc.
const arr = [5, 6, 13, 0, 1, 18, 23];
const double = arr.map((v) => v * 2);
// [10, 12, 26, 0, 2, 36, 46]
```

In python we have handy tools like `is` and just better runtime functions. I assume this is being used the same way. When I see this again later I can try to pick at it some more. 

This video is more of an overview of Javascript so I will need to dedicate sometime to learning the blasted thing.

## Event Listeners
They do things that can listen to at an event. Makes the website seem more responsive.

## AJAX
Oh lord here we go. Before I try to comprehend whatever `$.ajax({})` means lets talk about the status of this tutorial. While the previous video I saw about React it used the Axios module this teacher is explaining that we are using jquery to process ajax methods. This might be old by now but it could also be preferrence and at this point it doesn't matter what I learn its all gonna be crazy Javascript to me anyways.

### ReadyStates
[MDN Doc](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState)

|Value|	State |	Description |
|-----|------|------|
|0| UNSENT| 	Client has been created. open() not called yet.|
|1|	OPENED| 	open() has been called.|
|2| HEADERS_RECEIVED| 	send() has been called, and headers and status are |available|
|3|	LOADING| 	Downloading; responseText holds partial data.|
|4|	DONE| 	The operation is complete.|

### Described three different methods to get api
1. jquery ajax method
2. XMLHttpRequest
3. fetch method

> jquery ajax 

What a weird syntax required to use this method, using the `$.ajax` function that kinda hurts my head and abit hard to follow

``` javascript
// 1. Jquery Ajax method <- what will be used in this project
const url = 'https://swapi.dev/api/people/'
$.ajax({
    type: 'GET',
    url: url
    success: function(response){
        console.log('jquery ajax', repsonse)
    },
    error: function(error){
        console.log(error)
    }
})
```

> XMLHttpRequest

Too long and silly

``` javascript
const url = 'https://swapi.dev/api/people/'

req.addEventListener('readystatechange', ()=>{
    if(req.readyState===4){
        console.log('xhttp', req.responseText)
    }
})

req.open('GET', url)
req.send()
```

> fetch

This one I really like how simple it is but uses a promise try-like method that isn't talked about much more but I love how small it is. Now that I understand how the arrow function `=>` works its not too scary to look at.

``` javascript
const url = 'https://swapi.dev/api/people/'
fetch(url)
.then(resp=> resp.json()).ten(data=> console.log('fetch', data))
.catch(err=> console.log(err))
```