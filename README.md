# Mocha-jar
A tiny flexible web framework for Java

## Getting Started:

1. Download the framework located at the <a href="https://github.com/GabrielGavrilov/mocha-jar/releases">releases page.</a>

2. Start coding:
```Java
public class Server extends Mocha {
  public static void main(String[] args) {
    get("/", (request, response)-> {
      response.initializeHeader("200 OK", "text/html");
      response.send("<h1>Hello from Mocha!</h1>");
    });
  
    listen(3000, ()-> {
      System.out.println("Listening on port 3000...");
    });
  }
}
```
3. Run and view:
```
http://localhost:3000
```

## Routes

A Mocha route is made up of two components: 
- A path
- A callback method

Mocha supports the current routes:

```java
get("/", (request, response)-> {
  // Show something
});

post("/", (request, response)-> {
  // Create something
});

put("/", (request, response)-> {
  // Update something
});

delete("/", (request, response)-> {
  // Delete something
});
```

Routes also support parameters, and can be accessed by calling the ``parameter`` hashmap. 

```java
get("/greet/{name}", (request, response)-> {
  response.initializeHeader("200 OK", "text/html");
  String name = request.parameter.get("name");
  response.send("Hello, " + name + "!");
})
```

## Request

The Request class has the following information and functionality:
```java
request.payload()        // A MochaPayload class used to retrieve body payload information
request.parameter()      // A hashmap used to map a parameter's value by name
request.cookie()         // A hashmap used to map a cookie's value by name
request.header           // requested HTTP header
```

## Response
The Response class has the following information and functionality:
```java
response.initializeHeader()    // Used to intiialize the status and content-type for the response
response.addHeader()           // Appends a custom header to the response
response.status()              // Sets the HTTP status
response.contentType()         // Sets the content-type
response.cookie()              // Sets a cookie
response.send()                // Sends data to the response
response.render()              // Renders a given file
```

## Payloads

Mocha expects a body payload for the following routes:
- POST
- UPDATE
- DELETE

As of right now, Mocha only accepts ``raw`` and ``JSON`` payloads. Payloads can be accessed by using the Request's payload hashmap:
```java
request.payload.get("foo"); // bar
```

## Cookies

With Mocha, cookies are obtained through the request, and sent through the response. You can obtain a cookie by using the Request's cookie payload by calling the cookie's name:

```java
request.cookie.get("foo"); // bar
```

You can send a new cookie to the user by using the Response's cookie function. The first parameter for the function takes the cookie name, while the second parameter takes the cookie value.

```java
response.cookie("foo", "bar");
```

## Custom headers

You can add custom headers to the Response by using the Response's addHeader function. The first parameter for the function takes the header name, while the second parameter takes the header value.

```java
response.addHeader("Content-Type", "application/json")
```

## Parameters

You can create a route parameter by wrapping its desired name in curly brackets. Parameters can be accessed by using the Request's parameter hashmap:
```java
request.parameter.get("foo"); // bar
```

A route that utilizes a parameter like this:
```java
get("/greet/{name}", (request, response)-> {
  response.initializeHeader("200 OK", "text/html");
  String name = request.parameter.get("name");
  response.send("Hello, " + name + "!");
});
```

