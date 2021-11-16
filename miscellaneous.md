# **Miscellaneous Interview Questions**
<br />

## ***`Question :- What is Cache Busting?`***

```
> Cache busting is the process of uploading a new file to replace an existing file that is already cached. This is useful because the cache will often take a long time to expire from all of its various locations and cache busting properly ensures that any changes to a file be visible to end users sooner, rather than later.
```

### _`1. Filename Versioning :- `_ 

```
> It is the method of including the version in the file name, before the type.

    {
        background-image:url(‘back.png’);
    }
    {
        background-image:url(‘back-2.png’);
    }
    {
        background-image:url(‘back-3.png’);
    }
```

### _`2. File Path Versioning :- `_ 
```
> It is the process of including the version in the directory or path for the file.

    a. styles/v1/style.css 
        {
            background-image:url(‘back.png’);
        }
    b. styles/v2/style.css
        {
            background-image:url(‘back-new.png’);
        }
    c. styles/v3/style.css
        {
            background-image:url(‘back-newest.png’);
        }
```

### _`3. Versioning with Query Strings :- `_ 
```
> A Query String is a unique set of parameters that can identify separate files within the same file hierarchical path. This is usually done by adding a '?' followed by the string that indicates the differences to the end of the file. This can be used for cache busting because most cache mechanisms will use the query string as a separate file.

    a. style.css
        {
            background-image:url(‘back.png’);
        }
    b. style.css?back=2
        {
            background-image:url(‘back-new.png’);
        }
    c. style.css?back=3
        {
            background-image:url(‘back-newest.png’);
        }
```

<br />

## ***`Question :- What is Semantic Versioning?`***

```
> Semantic versioning or SemVer is the ideal way of versioning packages. They are usually written like 1.4.5 (major.minor.patch)
```

### _`1a. Bug fix/patch version :- `_ 
```
Includes bug fixes/documentation spelling mistakes etc.
```
### _`1b. Minor version :- `_ 
```
Includes additions of functions or API which does not break anything from the older versions So anything that runs on v1.1.0 should work on v1.9.0 as well.
```
### _`1c. Major version :- `_ 
```
Includes version which breaks stuff. It can include removing APIs or changing names of functions so anything that works on v1.0.0 may not necessarily work on v2.0.0
```

<br />

## ***`Question :- What is API Versioning?`***

```
API versioning is the practice of transparently managing changes to your API. Versioning is effective communication around changes to your API, so consumers know what to expect from it. You are delivering data to the public in some fashion and you need to communicate when you change the way that data is delivered.
```

### _`Q. When to version? :- `_ 
```
APIs only need to be up-versioned when a breaking change is made.
```
> Breaking changes include:
```
> a change in the format of the response data for one or more calls
> a change in the request or response type (i.e. changing an integer to a float)
> removing any part of the API.
```

```
--- Breaking changes should always result in a change to the major version number for an API or content response type.

--- Non-breaking changes, such as adding new endpoints or new response parameters, do not require a change to the major version number.
```

### _`Q. How to version a REST API? :- `_

> 1a. URI Versioning
```
Using the URI is the most straightforward approach (and most commonly used as well) though it does violate the principle that a URI should refer to a unique resource. You are also guaranteed to break client integration when a version is updated.
```
```
http://api.example.com/v1
http://apiv1.example.com
```
```
The version need not be numeric, nor specified using the “v[x]” syntax.

Alternatives include dates, project names, seasons, or other identifiers that are meaningful enough to the team producing the APIs and flexible enough to change as the versions change.
```

> 1b. Versioning using Custom Request Header
```
A custom header (e.g. Accept-version) allows you to preserve your URIs between versions though it is effectively a duplicate of the content negotiation behavior implemented by the existing Accept header.
```
```
Accept-version: v1
Accept-version: v2
```

> 1c. Versioning using “Accept” header
```
Content negotiation may let you preserve a clean set of URLs, but you still have to deal with the complexity of serving different versions of content somewhere.

This burden tends to be moved up the stack to your API controllers which become responsible for figuring out which version of a resource to send.

The result tends to be a more complex API as clients have to know which headers to specify before requesting a resource.
```
```
Accept: application/vnd.example.v1+json
Accept: application/vnd.example+json;version=1.0
```

```
In the real world, an API is never going to be completely stable. So it’s important how this change is managed.

A well-documented and gradual deprecation of API can be an acceptable practice for most APIs.
```

<br /><br />

## ***`Question :- What is Content Negotiation?`***
```
Generally, the REST resources can have multiple presentations, mostly because there may be different clients expecting different representations. Asking for a suitable presentation by a client is referred to as content negotiation.

HTTP has provisions for several mechanisms for “content negotiation” — the process of selecting the best representation for a given response when there are multiple representations available.
```

### _`1. Server-driven Vs Agent-driven Content Negotiation :- `_ 
```
If the selection of the best representation for a response is made by an algorithm located at the server, it is called server-driven negotiation. If that selection is made at the agent or client-side, it is called agent-driven negotiation.

Practically, we will NOT find much usage of server-side negotiations because, in that way, we have to make a lot of assumptions about the client’s expectations.

Few things, like the client context or how the client will use the resource representation, are almost impossible to determine. Also, the server-driven negotiation makes the server-side code more complex, unnecessarily.

So, most REST API implementations rely on agent-driven content negotiations. Agent-driven content negotiation depends on the usage of HTTP request headers or resource URI patterns.
```

### _`1a. Using HTTP Headers :- `_ 
```
At server side, an incoming request may have an entity attached to it. To determine it’s type, server uses the HTTP request header Content-Type. Some common examples of content types are “text/plain”, “application/xml”, “text/html”, “application/json”, “image/gif”, and “image/jpeg”.
```
```
Content-Type: application/json
```
```
Similarly, to determine what type of representation is desired on the client-side, an HTTP header ACCEPT is used. It will have one of the values mentioned for Content-Type above.
```
```
Accept: application/json
```
```
Generally, if no Accept header is present in the request, the server can send pre-configured default representation type.
```
> Implementing Accept header based content negotiation is most used and recommened way.

### _`1b. Using URL Patterns :- `_ 
```
Another way to pass content type information to the server, the client may use the specific extension in resource URIs. For example, a client can ask for details using:
```
```
http://rest.api.com/v1/employees/20423.xml
http://rest.api.com/v1/employees/20423.json
```
```
In the above case, the first request URI will return an XML response whether the second request URI will return a JSON response.
```

### _`2. Defining Preferences :- `_ 

```
It is possible to have multiple values in Accept header using the ‘q’ parameter i.e. relative quality factor.

The client may want to provide multiple values in the accept header when the client is not sure if its desired representation is present or supported by the server at that time. [RFC 2296]

For example,
```
```
Accept: application/json,application/xml;q=0.9,*/*;q=0.8
```
```
Above Accept header allows you to ask the server a JSON format (first choice). If it can’t, perhaps it could return XML format (the second choice). If it’s still not possible, let it return what it can.

The preference order is defined through the q parameter with values from 0 to 1. When nothing is specified, the implicit default value is 1.
```
<br /><br />

## ***`Question :- What is REST API Compression?`***
```
REST APIs can return the resource representations in several formats such as XML, JSON, HTML, or even plain text. All such forms can be compressed to a lesser number of bytes to save bandwidth over the network.

Different protocols use different techniques to enable compression and notify the clients about the compression scheme – so that the client can decompress it before consuming the representations.
```
> Compression, like encryption, is something that happens to the resource representation in transit and must be undone before the client can use the representation.

```
HTTP is the most widely used protocol for REST – so we are taking the example of HTTP-specific response compression.
```

### _`1. Compression Related Request/Response Headers :- `_ 

### _`1a. Accept-Encoding :- `_ 
```
While requesting resource representations – along with an HTTP request, the client sends an Accept-Encoding header that says what kind of compression algorithms the client understands.

The two standard values for Accept-Encoding are compress and gzip.

A sample request with accept-encoding, the header looks like this :
```

```
GET        /employees         HTTP/1.1
Host:     www.domain.com
Accept:     text/html
Accept-Encoding:     gzip,compress
```

```
Another possible usage of accept-encoding may be:
```

```
Accept-Encoding: compress, gzip
Accept-Encoding:
Accept-Encoding: *
Accept-Encoding: compress;q=0.5, gzip;q=1.0
Accept-Encoding: gzip;q=1.0, identity; q=0.5, *;q=0
```

```
If an Accept-Encoding the field is present in a request, and if the server cannot send a response that is acceptable according to the Accept-Encoding header, then the server SHOULD send an error response with the 406 (Not Acceptable) status code.
```

### _`1b. Content-Encoding :- `_ 

```
If the server understands one of the compression algorithms from Accept-Encoding, it can use that algorithm to compress the representation before serving it. When successfully compressed, the server lets know the client of encoding scheme by another HTTP header i.e. Content-Encoding.
```

```
200 OK
Content-Type:     text/html
Content-Encoding:     gzip
```

```
If the content-coding of an entity in a request message is not acceptable to the origin server, the server SHOULD respond with a status code of 415 (Unsupported Media Type). If multiple content encodings have been applied to an entity, all the encodings MUST be listed in the order in which they were used.

Please note that the original media type for request and response are not impacted whether compression is requested or not.

Compression can save a lot of bandwidth, with minimal cost without additional complexity. Also, you may know that most web browsers automatically request compressed representations from website host servers – using the above headers.
```

<br /><br />

## ***`Question :- Difference between HTTP/2 vs. HTTP/1.1?`***

### _`1a. What is HTTP? Why is HTTP/2 faster than HTTP/1.1?`_

```
HTTP stands for hypertext transfer protocol, and it is the basis for almost all web applications. More specifically, HTTP is the method computers and servers use to request and send information. For instance, when someone navigates to cloudflare.com on their laptop, their web browser sends an HTTP request to the Cloudflare servers for the content that appears on the page. Then, Cloudflare servers send HTTP responses with the text, images, and formatting that the browser displays to the user.

The first usable version of HTTP was created in 1997. Because it went through several stages of development, this first version of HTTP was called HTTP/1.1. This version is still in use on the web. In 2015, a new version of HTTP called HTTP/2 was created.

HTTP/2 solves several problems that the creators of HTTP/1.1 did not anticipate. In particular, HTTP/2 is much faster and more efficient than HTTP/1.1. One of the ways in which HTTP/2 is faster is in how it prioritizes content during the loading process.
```

### _`1a. What is prioritization?`_

```
In the context of web performance, prioritization refers to the order in which pieces of content are loaded. Suppose a user visits a news website and navigates to an article. Should the photo at the top of the article load first? Should the text of the article load first? Should the banner ads load first?

Prioritization affects a webpage's load time. For example, certain resources, like large JavaScript files, may block the rest of the page from loading if they have to load first. More of the page can load at once if these render-blocking resources load last.

In addition, the order in which these page resources load affects how the user perceives page load time. If only behind-the-scenes content (like a CSS file) or content the user can't see immediately (like banner ads at the bottom of the page) loads first, the user will think the page is not loading at all. If the content that's most important to the user loads first, such as the image at the top of the page, then the user will perceive the page as loading faster.
```

### _`1a. How does prioritization in HTTP/2 affect performance?`_

```
In HTTP/2, developers have hands-on, detailed control over prioritization. This allows them to maximize perceived and actual page load speed to a degree that was not possible in HTTP/1.1.

HTTP/2 offers a feature called weighted prioritization. This allows developers to decide which page resources will load first, every time. In HTTP/2, when a client makes a request for a webpage, the server sends several streams of data to the client at once, instead of sending one thing after another. This method of data delivery is known as multiplexing. Developers can assign each of these data streams a different weighted value, and the value tells the client which data stream to render first.

Imagine that Alice wants to read a novel that her friend Bob wrote, but both Alice and Bob only communicate through the regular mail. Alice sends a letter to Bob and asks Bob to send her his novel. Bob decides to send the novel HTTP/1.1-style: He mails one chapter at a time, and he only mails the next chapter after receiving a reply letter from Alice confirming that she received the previous chapter. Using this method of content delivery, it takes Alice many weeks to read Bob's novel.

Now imagine that Bob decides to send Alice his novel HTTP/2-style: In this case, he sends each chapter of the novel separately (to stay within the postal service's size limits) but all at the same time. He also numbers each chapter: Chapter 1, Chapter 2, etc. Now, Alice receives the novel all at once and can assemble it in the correct order on her own time. If a chapter is missing, she may send a quick reply asking for that specific chapter, but otherwise the process is complete, and Alice can read the novel in just a few days.

In HTTP/2, data is sent all at once, much like Bob when he sends Alice multiple chapters at once. And just like Bob, developers get to number the chapters in HTTP/2. They can decide if the text of a webpage loads first, or the CSS files, or the JavaScript, or whatever they feel is most important for the user experience.
```

### _`1a. What are the other differences between HTTP/2 and HTTP/1.1 that impact performance?`_
> Multiplexing
```
HTTP/1.1 loads resources one after the other, so if one resource cannot be loaded, it blocks all the other resources behind it. In contrast, HTTP/2 is able to use a single TCP connection to send multiple streams of data at once so that no one resource blocks any other resource. HTTP/2 does this by splitting data into binary-code messages and numbering these messages so that the client knows which stream each binary message belongs to.
```
> Server push
```
Typically, a server only serves content to a client device if the client asks for it. However, this approach is not always practical for modern webpages, which often involve several dozen separate resources that the client must request. HTTP/2 solves this problem by allowing a server to "push" content to a client before the client asks for it. The server also sends a message letting the client know what pushed content to expect – like if Bob had sent Alice a Table of Contents of his novel before sending the whole thing.
```
> Header compression
```
Small files load more quickly than large ones. To speed up web performance, both HTTP/1.1 and HTTP/2 compress HTTP messages to make them smaller. However, HTTP/2 uses a more advanced compression method called HPACK that eliminates redundant information in HTTP header packets. This eliminates a few bytes from every HTTP packet. Given the volume of HTTP packets involved in loading even a single webpage, those bytes add up quickly, resulting in faster loading.
```

### _`1a. What is HTTP/3?`_
```
HTTP/3 is the next proposed version of the HTTP protocol. HTTP/3 does not have wide adoption on the web yet, but it is growing in usage. The key difference between HTTP/3 and previous versions of the protocol is that HTTP/3 runs over QUIC instead of TCP. QUIC is a faster and more secure transport layer protocol that is designed for the needs of the modern Internet.
```

<br /><br />



## ***`Question :- What is Tree Shaking in Webpack and how does it works?`***
```
Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. It relies on the static structure of ES2015 module syntax, i.e. import and export. The name and concept have been popularized by the ES2015 module bundler rollup.
```
### _`1a. Clarifying tree shaking and sideEffects :- `_
```
The sideEffects and usedExports (more known as tree shaking) optimizations are two different things.

sideEffects is much more effective since it allows to skip whole modules/files and the complete subtree.

usedExports relies on terser to detect side effects in statements. It is a difficult task in JavaScript and not as effective as straightforward sideEffects flag. It also can't skip subtree/dependencies since the spec says that side effects need to be evaluated. While exporting function works fine, React's Higher Order Components (HOC) are problematic in this regard.
```

<br /><br />

## ***`Question :- What is the Box Model?`***
```
All HTML elements can be considered as boxes.
```

### _`The CSS Box Model :- `_
```
In CSS, the term "box model" is used when talking about design and layout.

The CSS box model is essentially a box that wraps around every HTML element. It consists of: margins, borders, padding, and the actual content. The image below illustrates the box model:

```
### _`Explanation of the different parts :- `_

```
> Content - The content of the box, where text and images appear

> Padding - Clears an area around the content. The padding is transparent

> Border - A border that goes around the padding and content

> Margin - Clears an area outside the border. The margin is transparent

The box model allows us to add a border around elements, and to define space between elements. 
```
### _`Demonstration of the box model :- `_

```
div {
  width: 300px;
  border: 15px solid green;
  padding: 50px;
  margin: 20px;
}
```

<br /><br />

## ***`Question :- What are the different properties of position attribute in css?`***
```
There are five different position values:
    1. static.
    2. relative.
    3. fixed.
    4. absolute.
    5. sticky.
```

<br /><br />

## ***`Question :- What is Server Side Rendering? What are the uses of it?`***
```
Server-side rendering refers to an application’s ability to display the web-page on the server rather than rendering it in the browser. When a website’s JavaScript is rendered on the website’s server, a fully rendered page is sent to the client and the client’s JavaScript bundle engages and enables the Single Page Application framework to operate.
```

```
Server-side rendering (SSR) is an application’s ability to convert HTML files on the server into a fully rendered HTML page for the client. The web browser submits a request for information from the server, which instantly responds by sending a fully rendered page to the client. Search engines can crawl and index content prior to delivery, which is beneficial for Search Engine Optimization purposes.

Popular examples of server-side rendering JavaScript frameworks include: Angular server side rendering, ejs server side rendering, server side rendering Express, Gatsby server side rendering, Google server side rendering, NestJS server side rendering, Next server side rendering, Nuxt server side rendering, React server side rendering, and Vue server side rendering.
```

### _`Question. What are the Benefits of Server-Side Rendering?`_

```
Some server-side rendering advantages include:

    > A server-side rendered application enables pages to load faster, improving the user experience.

    > When rendering server-side, search engines can easily index and crawl content because the content can be rendered before the page is loaded, which is ideal for SEO. 

    > Webpages are correctly indexed because web browsers prioritize web pages with faster load times.

    > Rendering server-side helps efficiently load webpages for users with slow internet connection or outdated devices.
```

### _`Question. What are the Risks of Server-Side Rendering?`_

```
Server-side rendering disadvantages may include:

    > Rendering server-side can be costly and resource-intensive as it is not the default for JavaScript websites, and the server takes on the full burden of rendering content for users and bots.
    
    > While rendering static HTML server-side is efficient, rendering bigger, more complex applications server-side can increase load times due to the bottleneck.
    
    > Server-side rendering may not be compatible with third-party JavaScript code. 

    > Rendering server-side may be ideal for static site generation, but frequent server requests and full page reloads can result in overall slower page rendering in more complex applications.
```

### _`Question. Server-Side Rendering vs Client-Side Rendering?`_
```
In client-server rendering, rather than receiving all of the content from the HTML document, content is rendered in the browser using the client-side JavaScript library. The browser does not make a new request to the server when a new page is loaded. Search engine rankings may be negatively impacted as the content is not rendered until the page is loaded on the browser, however, website rendering tends to be faster in client-side rendered app. In considering server side vs client side rendering, the developer will assess factors such as the scale of the project, the complexity of the application, the number of users, and user experience priorities.
```

<br /><br />



## ***`Question :- What is Statelessness in REST APIs?`***

### _`1. Statelessness`_

```
As per the REST (REpresentational “State” Transfer) architecture, the server does not store any state about the client session on the server-side. This restriction is called Statelessness.

Each request from the client to the server must contain all of the necessary information to understand the request. The server cannot take advantage of any stored context on the server.

The application’s session state is therefore kept entirely on the client. The client is responsible for storing and handling the session related information on its own side.

This also means that the client is responsible for sending any state information to the server whenever it is needed. There should not be any session affinity or sticky session between the client and the server.
```

> Statelessness means that every HTTP request happens in complete isolation. When the client makes an HTTP request, it includes all information necessary for the server to fulfill the request.

> The server never relies on information from previous requests from the client. If any such information is important then the client will send that as part of the current request.

```
To enable clients to access these stateless APIs, it is necessary that servers also should include every piece of information that the client may need to create/maintain the state on its side.

For becoming stateless, do not store even authentication/authorization details of the client. Provide authentication credentials with each request.

Thus each request MUST be stand alone and should not be affected by the previous conversation that happened with the same client in past.
```

### _`2. Application State vs Resource State`_

```
It is important to understand the between the application state and the resource state. Both are completely different things.

Application state is server-side data that servers store to identify incoming client requests, their previous interaction details, and current context information.

Resource state is the current state of a resource on a server at any point in time – and it has nothing to do with the interaction between client and server. It is what we get as a response from the server as the API response. We refer to it as resource representation.
```

> REST statelessness means being free from the application state.

### _`3. Advantages of Stateless APIs`_

```
There are some very noticeable advantages of having REST APIs stateless.

    > Statelessness helps in scaling the APIs to millions of concurrent users by deploying it to multiple servers. Any server can handle any request because there is no session related dependency.

    > Being stateless makes REST APIs less complex – by removing all server-side state synchronization logic.

    > A stateless API is also easy to cache as well. Specific softwares can decide whether or not to cache the result of an HTTP request just by looking at that one request. There’s no nagging uncertainty that state from a previous request might affect the cacheability of this one. It improves the performance of applications.

    > The server never loses track of “where” each client is in the application because the client sends all necessary information with each request.

```

<br /><br />

## ***`Question :- REST API Security Essentials?`***

```
REST API Security isn’t an afterthought. It has to be an integral part of any development project and also for REST APIs.

There are multiple ways to secure a RESTful API e.g. basic auth, OAuth, etc. but one thing is sure that RESTful APIs should be stateless – so request authentication/authorization should not depend on sessions.

Instead, each API request should come with some sort of authentication credentials that must be validated on the server for every request.
```

### _`1. REST Security Design Principles`_
> 1. Least Privilege: 
```
An entity should only have the required set of permissions to perform the actions for which they are authorized, and no more. Permissions can be added as needed and should be revoked when no longer in use.
```
> 2. Fail-Safe Defaults: 
```
A user’s default access level to any resource in the system should be “denied” unless they’ve been granted a “permit” explicitly.
```
> 3. The economy of Mechanism: 
```
The design should be as simple as possible. All the component interfaces and the interactions between them should be simple enough to understand.
```
> 4. Complete Mediation: 
```
A system should validate access rights to all its resources to ensure that they’re allowed and should not rely on the cached permission matrix. If the access level to a given resource is being revoked, but that isn’t reflected in the permission matrix, it would violate the security.
```
> 5. Open Design: 
```
This principle highlights the importance of building a system in an open manner—with no secret, confidential algorithms.
```
> 6. Separation of Privilege: 
```
Granting permissions to an entity should not be purely based on a single condition, a combination of conditions based on the type of resource is a better idea.
```
> 7. Least Common Mechanism: 
```
It concerns the risk of sharing state among different components. If one can corrupt the shared state, it can then corrupt all the other components that depend on it.
```
> 8. Psychological Acceptability: 
```
It states that security mechanisms should not make the resource more difficult to access than if the security mechanisms were not present. In short, security should not make worse the user experience.
```

### _`2. Best Practices to Secure REST APIs`_

> 1. Keep it Simple
```
Secure an API/System – just how secure it needs to be. Every time you make the solution more complex “unnecessarily,” you are also likely to leave a hole.
```
> 2. Always Use HTTPS
```
By always using SSL, the authentication credentials can be simplified to a randomly generated access token. The token is delivered in the username field of HTTP Basic Auth. It’s relatively simple to use, and you get a lot of security features for free.

If you use HTTP 2, to improve performance – you can even send multiple requests over a single connection, that way you avoid the complete TCP and SSL handshake overhead on later requests.
```
> 3. Use Password Hash
```
Passwords must always be hashed to protect the system (or minimize the damage) even if it is compromised in some hacking attempts. There are many such hashing algorithms that can prove really effective for password security e.g. PBKDF2, bcrypt, and scrypt algorithms.
```
> 4. Never expose information on URLs
```
Usernames, passwords, session tokens, and API keys should not appear in the URL, as this can be captured in web server logs, which makes them easily exploitable.
```
```
https://api.domain.com/user-management/users/{id}/someAction?apiKey=abcd123456789  //Very BAD !!
```
```
The above URL exposes the API key. So, never use this form of security.
```
> 5. Consider OAuth
```
Though basic auth is good enough for most of the APIs and if implemented correctly, it’s secure as well – yet you may want to consider OAuth as well.

The OAuth 2.0 authorization framework enables a third-party application to obtain limited access to an HTTP service, either on behalf of a resource owner by orchestrating an approval interaction between the resource owner and the HTTP service, or by allowing the third-party application to obtain access on its behalf.
```
> 6. Consider Adding Timestamp in Request
```
Along with other request parameters, you may add a request timestamp as an HTTP custom header in API requests.

The server will compare the current timestamp to the request timestamp and only accepts the request if it is after a reasonable timeframe (30 seconds, perhaps).

This will prevent very basic replay attacks from people who are trying to brute force your system without changing this timestamp.
```
> 7. Input Parameter Validation
```
Validate request parameters on the very first step, before it reaches application logic. Put strong validation checks and reject the request immediately if validation fails.

In API response, send relevant error messages and examples of correct input format to improve user experience.
```
<br /><br />

# **Incomplete Interview Questions**

## ***`Question :- What is Lazy & Eager Loading?`***
### _`1. What is Lazy Loading?`_
```
Lazy loading is the practice of delaying load or initialization of resources or objects until they’re actually needed to improve performance and save system resources. For example, if a web page has an image that the user has to scroll down to see, you can display a placeholder and lazy load the full image only when the user arrives to its location.
```
> The benefits of lazy loading include:
#### _`a. Reduces initial load time – `_
```
> Lazy loading a webpage reduces page weight, allowing for a quicker page load time.
```
#### _`b. Bandwidth conservation – `_
```
> Lazy loading conserves bandwidth by delivering content to users only if it’s requested.
```
#### _`c. System resource conservation – `_
```
> Lazy loading conserves both server and client resources, because only some of the images, JavaScript and other code actually needs to be rendered or executed.
```

### _`2. Lazy Loading vs. Eager Loading`_
```
While lazy loading delays the initialization of a resource, eager loading initializes or loads a resource as soon as the code is executed. Eager loading also involves pre-loading related entities referenced by a resource. For example, a PHP script with an include statement performs eager loading—as soon as it executes, eager loading pulls in and loads the included resources.

Eager loading is beneficial when there is an opportunity or need to load resources in the background. For example, some websites display a “loading” screen and eagerly load all the resources required for the web application to run.
```
### _`3. Lazy Loading Implementing Methods`_
```
There are several open source libraries that can be used to implement lazy loading, including:
```
#### _`a. blazy.js – `_
```
blazy.js is a lightweight JavaScript library for lazy loading and multi-serving images, iframes, video and other resources.
```
#### _`b. LazyLoad – `_
```
LazyLoad is a script that automatically loads images as they enter the viewport.
```

> Methods for implementing lazy loading in your code include:
#### _`a. Lazy initialization – `_
```
- This method sets objects to null. Object data is loaded only after and whenever invoking them, check if null, and if so, load object data.
```
#### _`b. Virtual proxy – `_
```
- when accessing an object, call a virtual object with same interface as the real object. When the virtual object is called, load the real object, then delegate to it.
```
#### _`c. Ghost – `_
```
- load an object in partial state, only using an identifier. The first time a property on the object is called, load the full data.
```
#### _`d. Value holder – `_
```
- create a generic object that handles lazy loading behavior. This object should appear in place of an object’s data fields.
```

> Examples - 
#### _`a. Lazy Loading Images – `_
```
To lazy load an image, display a lightweight placeholder image, and replace with the real full-size image on scroll.

    1. Inline <img> tags, using JavaScript to populate the tag if image is in viewport

    2. Event handlers such as scroll or resize

    3. The Intersection Observer API

    4. The CSS background-image property
```

#### _`b. Lazy Loading Video – `_
```
To lazy load a video that doesn’t autoplay, you can use the HTML5 video tag’s preload attribute.

For videos that autoplay, Google Chrome provides lazy loading automatically. In other browsers, you will need to declare the following attributes in the video tag:
```
```
<video autoplay muted loop playsinline width="xx" height="xx" poster="placeholder-image.jpg">
``` 
### _`3. Lazy Loading Best Practices - `_
```
When performing lazy loading, consider the following tips:

    1. Only lazy load resources that are displayed below the fold or outside the user’s viewport. In code, only lazy load objects that are not needed for initial or essential system operations.

    2. When lazy loading an image, asynchronously decode it using the JavaScript decode() method before inserting it into the DOM. Otherwise, large images can cause the browser to freeze.

    3. Handle errors in case the image or object fails to load.

    4. Offer a noscript in case JavaScript is not available. Otherwise users with JavaScript disabled will not see any lazy-loaded resources.
```

<br /><br />

## ***`Question :- What is clickjacking?`***

```
Clickjacking is an attack that tricks a user into clicking a webpage element which is invisible or disguised as another element. This can cause users to unwittingly download malware, visit malicious web pages, provide credentials or sensitive information, transfer money, or purchase products online.

Typically, clickjacking is performed by displaying an invisible page or HTML element, inside an iframe, on top of the page the user sees. The user believes they are clicking the visible page but in fact they are clicking an invisible element in the additional page transposed on top of it.

The invisible page could be a malicious page, or a legitimate page the user did not intend to visit – for example, a page on the user’s banking site that authorizes the transfer of money.
```
> There are several variations of the clickjacking attack, such as:
#### _`1. Likejacking - `_
```
a technique in which the Facebook “Like” button is manipulated, causing users to “like” a page they actually did not intend to like.
```
#### _`2. Cursorjacking - `_
```
a UI redressing technique that changes the cursor for the position the user perceives to another position. Cursorjacking relies on vulnerabilities in Flash and the Firefox browser, which have now been fixed.
```
### _`2. Clickjacking attack example - `_

```
> The attacker creates an attractive page which promises to give the user a free trip to Tahiti.

> In the background the attacker checks if the user is logged into his banking site and if so, loads the screen that enables transfer of funds, using query parameters to insert the attacker’s bank details into the form.

> The bank transfer page is displayed in an invisible iframe above the free gift page, with the “Confirm Transfer” button exactly aligned over the “Receive Gift” button visible to the user.

> The user visits the page and clicks the “Book My Free Trip” button.

> In reality the user is clicking on the invisible iframe, and has clicked the “Confirm Transfer” button. Funds are transferred to the attacker.

> The user is redirected to a page with information about the free gift (not knowing what happened in the background).
```
### _`3. Clickjacking mitigation - `_
> There are two general ways to defend against clickjacking:

#### _`a. Client-side methods - `_
```
the most common is called Frame Busting. Client-side methods can be effective in some cases, but are considered not to be a best practice, because they can be easily bypassed.
```
#### _`b. Server-side methods - `_
```
the most common is X-Frame-Options. Server-side methods are recommended by security experts as an effective way to defend against clickjacking.
```

> Mitigating clickjacking with X-Frame-Options response header

```
The X-Frame-Options response header is passed as part of the HTTP response of a web page, indicating whether or not a browser should be allowed to render a page inside a <FRAME> or <IFRAME> tag.
```
#### _`a. There are three values allowed for the X-Frame-Options header: - `_
```
    > DENY – does not allow any domain to display this page within a frame

    > SAMEORIGIN – allows the current page to be displayed in a frame on another page, but only within the current domain

    > ALLOW - FROM URI – allows the current page to be displayed in a frame, but only in a specific URI – for example www.example.com/frame-page
```

#### _`b. Using the SAMEORIGIN option to defend against clickjacking - `_
```
X-Frame-Options allows content publishers to prevent their own content from being used in an invisible frame by attackers.

The DENY option is the most secure, preventing any use of the current page in a frame. More commonly, SAMEORIGIN is used, as it does enable the use of frames, but limits them to the current domain.
```

#### _`c. Limitations of X-Frame-Options - `_
```
> To enable the SAMEORIGIN option across a website, the X-Frame-Options header needs to be returned as part of the HTTP response for each individual page (cannot be applied cross-site).

> X-Frame-Options does not support a whitelist of allowed domains, so it doesn’t work with multi-domain sites that need to display framed content between them.

> Only one option can be used on a single page, so, for example, it is not possible for the same page to be displayed as a frame both on the current website and an external site.

> The ALLOW-FROM option is not supported by all browsers.

> X-Frame-Options is a deprecated option in most browsers.
```

#### _`d. Clickjacking test – Is your site vulnerable? - `_
```
A basic way to test if your site is vulnerable to clickjacking is to create an HTML page and attempt to include a sensitive page from your website in an iframe. It is important to execute the test code on another web server, because this is the typical behavior in a clickjacking attack.

Use code like the following, provided as part of the OWASP Testing Guide:
```

```
<html>
<head>
<title>Clickjack test page</title>
</head>
<body>
<p>Website is vulnerable to clickjacking!</p>
<iframe src="http://www.yoursite.com/sensitive-page" width="500" height="500"></iframe>
</body>
</html>
```

```
View the HTML page in a browser and evaluate the page as follows:

    > If the text “Website is vulnerable to clickjacking” appears and below it you see the content of your sensitive page, the page is vulnerable to clickjacking.

    > If only the text “Website is vulnerable to clickjacking” appears, and you do not see the content of your sensitive page, the page is not vulnerable to the simplest form of clickjacking.

However, additional testing is needed to see which anti-clickjacking methods are used on the page, and whether they can be bypassed by attackers.
```

## ***`Question :- What is a sticky session?`***
```
Session stickiness, a.k.a., session persistence, is a process in which a load balancer creates an affinity between a client and a specific network server for the duration of a session, (i.e., the time a specific IP spends on a website). Using sticky sessions can help improve user experience and optimize network resource usage.
```
```
With sticky sessions, a load balancer assigns an identifying attribute to a user, typically by issuing a cookie or by tracking their IP details. Then, according to the tracking ID, a load balancer can start routing all of the requests of this user to a specific server for the duration of the session.
```
```
This can prove very helpful, as HTTP/S is a stateless protocol that was not devised with session persistence in mind. Nevertheless, many web applications do have the need to serve personalized user data (e.g., keep logs of items in a shopping cart or chat conversations) over the course of a session.
```
```
Without session persistence, the web application would have to maintain this information across multiple servers, which can prove inefficient—especially for large networks.
```
### _`1. Session stickiness: Advantages and disadvantages `_
```
Session stickiness offers a number of benefits that can improve your web application’s performance, including:
```
#### _`a. Minimized data exchange `_
```
When using sticky sessions, servers within your network don’t need to exchange session data, a costly process when done on scale.
```
#### _`b. RAM cache utilization `_
```
Sticky sessions allow for more effective utilization of your application’s RAM cache, resulting in better responsiveness.
```

```
That said, sticky sessions also make it more difficult to keep servers in balance. A server can become overloaded if it accumulates too many sessions, or if specific sticky sessions require a high number of resources. This could result in your load balancer having to shift a client to a different server mid-session, resulting in data loss.
```

### _`2. Persistence using session cookies `_

> There are two types of cookie-based session persistence: duration-based and application-controlled.

#### _`a. Duration-based session persistence `_

```
Your load balancer issues a cookie that defines a specific timeframe for session stickiness. Each time the load balancer receives a client request, it checks whether this cookie is present.

After the specified duration elapses and the cookie expires, the session is not sticky anymore.
```

#### _`b. Application-controlled session persistence `_

```
Your application generates a cookie that determines the duration of session stickiness. The load balancer still issues its own session cookie on top of it, but it now follows the lifetime of the application cookie.

This makes sticky sessions more efficient, ensuring that users are never routed to a server after their local session cookie has already expired. However, it’s more complex to implement because it requires additional integration between the load balancer and the application.
```

<br /><br />

## ***`Question :- What is web application security?`***

```
Web application security is the process of protecting websites and online services against different security threats that exploit vulnerabilities in an application’s code. Common targets for web application attacks are content management systems (e.g., WordPress), database administration tools (e.g., phpMyAdmin) and SaaS applications.
```
> Perpetrators consider web applications high-priority targets due to:

```
    > The inherent complexity of their source code, which increases the likelihood of unattended vulnerabilities and malicious code manipulation.

    > High value rewards, including sensitive private data collected from successful source code manipulation.

    > Ease of execution, as most attacks can be easily automated and launched indiscriminately against thousands, or even tens or hundreds of thousands of targets at a time.
```

```
Organizations failing to secure their web applications run the risk of being attacked. Among other consequences, this can result in information theft, damaged client relationships, revoked licenses and legal proceedings.
```

### _`1. Web application vulnerabilities `_
```
Web application vulnerabilities are typically the result of a lack of input/output sanitization, which are often exploited to either manipulate source code or gain unauthorized access.
```
> Such vulnerabilities enable the use of different attack vectors, including:
 
### _`1. SQL Injection `_
```
Occurs when a perpetrator uses malicious SQL code to manipulate a backend database so it reveals information. Consequences include the unauthorized viewing of lists, deletion of tables and unauthorized administrative access.
```

### _`2. Cross-site Scripting (XSS) `_
```
XSS is an injection attack targeting users in order to access accounts, activate Trojans or modify page content. Stored XSS occurs when malicious code is injected directly into an application. Reflected XSStakes place when malicious script is reflected off of an application onto a user’s browser.
```

### _`3. Remote File Inclusion `_
```
A hacker uses this type of attack to remotely inject a file onto a web application server. This can result in the execution of malicious scripts or code within the application, as well as data theft or manipulation.
```
### _`4. Cross-site Request Forgery (CSRF) `_
```
An attack that could result in an unsolicited transfer of funds, changed passwords or data theft. It’s caused when a malicious web application makes a user’s browser perform an unwanted action in a site to which a user is logged on.
```
 
<br /><br />


## ***`Question :- Difference between web1 and web2 and web3?`***
<br /><br />


## ***`Question :- What is Client Side Rendering?`***



<br /><br />

## ***`Question :- What is a Singleton Design Pattern?`***

<br /><br />

## ***`Question :- What are the SOLID Principles?`***

<br /><br />

## ***`Question :- What are PSR Rules?`***

<br /><br />