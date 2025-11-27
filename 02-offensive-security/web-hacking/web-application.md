# Web Application Basics - Short Summary

## Web Application Architecture

## Front End (Client-Side)

- **HTML** - Structure and content (what to display)
    
- **CSS** - Styling and layout (how it looks)
    
- **JavaScript** - Interactivity and dynamic behavior (how it responds)
    

## Back End (Server-Side)

- **Database** - Stores and retrieves data
    
- **Web Server** - Processes requests and delivers content
    
- **Infrastructure** - Networking, storage, supporting software
    
- **Web Application Firewall** - Optional security layer filtering malicious requests
    

## URL Structure

`scheme://user@host:port/path?query#fragment`

|Component|Example|Description|
|---|---|---|
|Scheme|https://|Protocol (HTTP/HTTPS)|
|Host|example.com|Domain name|
|Port|:443|Service endpoint (80=HTTP, 443=HTTPS)|
|Path|/api/users|Resource location|
|Query|?id=123|Parameters|
|Fragment|#section|Page anchor|

## HTTP Communication

## Request Structure

`METHOD /path HTTP/version` 

`Headers (key: value)`

`Body (optional)`

**Common Methods:**

- **GET** - Retrieve data
    
- **POST** - Submit data
    
- **PUT** - Update resource
    
- **DELETE** - Remove resource
    

**Key Request Headers:**

- Host, User-Agent, Referer, Cookie, Content-Type
    

## Response Structure

`HTTP/version STATUS_CODE Reason`

`Headers (key: value)`

`Body`

**Status Code Categories:**

- **1xx** - Informational
    
- **2xx** - Success (200 OK)
    
- **3xx** - Redirect (301 Moved)
    
- **4xx** - Client Error (404 Not Found)
    
- **5xx** - Server Error (500 Internal)
    

**Key Response Headers:**

- Date, Content-Type, Server, Set-Cookie, Cache-Control, Location
    

## Request/Response Body Formats

|Format|Content-Type|Use Case|
|---|---|---|
|URL Encoded|application/x-www-form-urlencoded|Simple forms|
|Form Data|multipart/form-data|File uploads|
|JSON|application/json|APIs|
|XML|application/xml|Legacy systems|

## Security Headers

**Content-Security-Policy (CSP)**

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com`

Prevents XSS by defining allowed content sources.

**Strict-Transport-Security (HSTS)**

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

Forces HTTPS connections.

**X-Content-Type-Options**

`X-Content-Type-Options: nosniff`

Prevents MIME-sniffing attacks.

**Referrer-Policy**

`Referrer-Policy: strict-origin-when-cross-origin`

Controls information leakage when following links.

## Security Considerations

- Validate all user input (query strings, headers, body)
    
- Sanitize output to prevent XSS
    
- Use HTTPS and implement HSTS
    
- Set secure cookie flags (HttpOnly, Secure)
    
- Implement CSP to prevent code injection
    
- Verify authorization before processing requests
    
- Watch for typosquatting domains
    
- Validate redirect locations to prevent open redirects
    
- Never expose sensitive info in URLs or error messages
    

## Key Takeaways

✅ Web apps = Front End (user interface) + Back End (server logic + database)  
✅ HTTP = Request/Response protocol with methods, headers, and bodies  
✅ Status codes indicate success (2xx), redirect (3xx), client error (4xx), or server error (5xx)  
✅ Security headers provide defense against common attacks  
✅ Always validate input and sanitize output

---
# Web Application Components - Long Summary

## Front End (Client-Side)

What users see and interact with in the browser:

**HTML (Hypertext Markup Language)**

- Defines what content to display
    
- Provides structure to web pages
    

**CSS (Cascading Style Sheets)**

- Controls visual appearance (colors, fonts, layouts)
    
- Makes web pages look styled and professional
    

**JavaScript (JS)**

- Enables interactivity and dynamic content
    
- Allows the browser to make decisions and respond to user actions
    

## Back End (Server-Side)

Components running behind the scenes:

**Database**

- Stores, modifies, and retrieves information
    
- Saves user preferences, login data, content, etc.
    

**Infrastructure**

- Web servers, application servers
    
- Networking devices and supporting software
    
- Delivers content to users
    

**WAF (Web Application Firewall)** _(Optional)_

- Filters malicious requests
    
- Provides security protection layer
    

## Summary

- **Front End** = User interface (HTML, CSS, JavaScript)
    
- **Back End** = Server logic, databases, infrastructure
    
- Together they create a complete web application


# URL (Uniform Resource Locator)

A URL is a web address that lets you access online content (webpages, videos, photos, etc.).

## URL Components

**Format:**

`scheme://user@host:port/path?query#fragment`

**Example:**

`https://www.example.com:443/products/search?q=laptop#reviews`

## Scheme

- Protocol used to access the website
    
- **HTTP** - Unencrypted (insecure)
    
- **HTTPS** - Encrypted (secure, recommended)
    

## User _(Rarely used)_

- Username for authentication
    
- ⚠️ Security risk - exposes credentials in URL
    

## Host/Domain

- Identifies which website you're accessing
    
- Must be unique
    
- ⚠️ Watch for typosquatting (fake domains used in phishing)
    

## Port

- Directs browser to correct service on server
    
- Range: 1-65,535
    
- Common ports:
    
    - **80** - HTTP
        
    - **443** - HTTPS
        

## Path

- Points to specific file/page on server
    
- Example: `/products/laptop`
    
- ⚠️ Must be secured to protect sensitive resources
    

## Query String

- Starts with `?`
    
- Used for search terms, form inputs, parameters
    
- Example: `?q=laptop&sort=price`
    
- ⚠️ User-modifiable - validate to prevent injection attacks
    

## Fragment

- Starts with `#`
    
- Points to specific section on webpage
    
- Example: `#reviews`
    
- ⚠️ User-modifiable - validate input
    

## Security Notes

- Always prefer HTTPS over HTTP
    
- Validate and sanitize query strings and fragments
    
- Be aware of typosquatting in domains
    
- Never put credentials directly in URLs


# HTTP Messages

HTTP messages are packets of data exchanged between client (user) and server.

## Types of HTTP Messages

**HTTP Request**

- Sent by client to trigger actions on server
    
- Example: User requesting a webpage
    

**HTTP Response**

- Sent by server in response to client's request
    
- Example: Server delivering the requested webpage
    

## Message Structure

## 1. Start Line

Identifies the message type and provides essential details:

- **Request:** Method (GET, POST, etc.) + URL + HTTP version
    
- **Response:** HTTP version + Status code (200, 404, etc.)
    

## 2. Headers

Key-value pairs providing additional information:

- Content type
    
- Authentication
    
- Cookies
    
- Security settings
    
- Caching instructions
    

**Example:**

`Content-Type: text/html Authorization: Bearer token123`

## 3. Empty Line

Separator between headers and body - marks where headers end and content begins.

## 4. Body _(Optional)_

Contains actual data:

- **Request body:** Form data, JSON, uploaded files
    
- **Response body:** HTML page, API data, images
    

## Why It Matters

- **Troubleshooting:** Understand web communication issues
    
- **Security:** Identify vulnerabilities and implement protection
    
- **Development:** Build and debug web applications effectively
    
- **Penetration Testing:** Analyze and exploit web application weaknesses


# HTTP Requests

An HTTP request is sent by a client to interact with a web server and trigger actions.

## Request Line Structure

`METHOD /path HTTP/version`

**Example:**

`GET /api/users/123 HTTP/1.1`

## HTTP Methods

## Common Methods

**GET**

- Fetches data without making changes
    
- ⚠️ Don't include sensitive data (tokens, passwords) - visible in plaintext
    

**POST**

- Sends data to create/update resources
    
- ⚠️ Validate and sanitize input to prevent SQL injection and XSS
    

**PUT**

- Replaces/updates entire resource
    
- ⚠️ Verify user authorization before accepting
    

**DELETE**

- Removes resource from server
    
- ⚠️ Ensure only authorized users can delete
    

## Less Common Methods

**PATCH** - Updates part of a resource (validate to avoid inconsistencies)

**HEAD** - Retrieves headers only (no body content)

**OPTIONS** - Shows available methods for a resource

**TRACE** - Debug method (often disabled for security)

**CONNECT** - Creates secure connection (HTTPS tunneling)

## URL Path

Points to specific resource on server.

**Example:** `/api/users/123`

## Security Considerations

- Validate path to prevent unauthorized access
    
- Sanitize to avoid injection attacks
    
- Protect sensitive data through proper access controls
    

## HTTP Versions

|Version|Year|Key Features|
|---|---|---|
|HTTP/0.9|1991|Only GET requests|
|HTTP/1.0|1996|Headers, content types, caching|
|HTTP/1.1|1997|Persistent connections, chunked encoding (widely used)|
|HTTP/2|2015|Multiplexing, header compression, faster performance|
|HTTP/3|2022|QUIC protocol, improved speed and security|

**Note:** HTTP/1.1 still most common, but HTTP/2 and HTTP/3 offer better performance and security.

## Security Best Practices

- Validate all user input
    
- Sanitize URL paths and parameters
    
- Implement proper authorization checks
    
- Use HTTPS for encrypted communication
    
- Disable unnecessary methods (TRACE, OPTIONS)


# HTTP Request Headers & Body

## Request Headers

Convey additional information about the request to the web server.

## Common Request Headers

|Header|Example|Description|
|---|---|---|
|**Host**|`Host: tryhackme.com`|Specifies the web server name|
|**User-Agent**|`User-Agent: Mozilla/5.0`|Browser/client information|
|**Referer**|`Referer: https://www.google.com/`|URL the request came from|
|**Cookie**|`Cookie: user_type=student`|Stored data from previous server response|
|**Content-Type**|`Content-Type: application/json`|Format of data in request body|

## Request Body

Contains data sent to server (used in POST, PUT, PATCH requests).

## URL Encoded (application/x-www-form-urlencoded)

Key-value pairs separated by `&`, special characters percent-encoded.

**Format:**

`name=Aleksandra&age=27&country=US`

**Example Request:**

`POST /profile HTTP/1.1`

`Host: tryhackme.com`

`Content-Type: application/x-www-form-urlencoded`

`Content-Length: 33`

`name=Aleksandra&age=27&country=US`

## Form Data (multipart/form-data)

Multiple data blocks separated by boundary string. Used for file uploads.

**Example Request:**

`POST /upload HTTP/1.1`

`Host: tryhackme.com`

`Content-Type: multipart/form-data; boundary=----WebKitFormBoundary`

`----WebKitFormBoundary Content-Disposition: form-data; name="username" aleksandra ----WebKitFormBoundary Content-Disposition: form-data; name="profile_pic"; filename="photo.jpg" [Binary Data] ----WebKitFormBoundary--`

## JSON (application/json)

Data in JavaScript Object Notation format. Name-value pairs in curly braces.

**Example Request:**

`POST /api/user HTTP/1.1`

`Host: tryhackme.com`

`Content-Type: application/json`

`Content-Length: 62`

`{     "name": "Aleksandra",    "age": 27,    "country": "US" }`

## XML (application/xml)

Data structured with opening/closing tags. Tags can be nested.

**Example Request:**

`POST /api/user HTTP/1.1`

`Host: tryhackme.com`

`Content-Type: application/xml`

`Content-Length: 124`

`<user>     <name>Aleksandra</name>    <age>27</age>    untry>US</country> </user>`

## Security Notes

- Validate all data from headers and body
    
- Sanitize input to prevent injection attacks
    
- Cookies can contain sensitive data - protect with HttpOnly and Secure flags
    
- Different body formats have different parsing vulnerabilities


# HTTP Responses

The server sends an HTTP response to indicate whether the request succeeded or failed.

## Status Line Structure

`HTTP/version STATUS_CODE Reason Phrase`

**Example:**

`HTTP/1.1 200 OK`

## Status Code Categories

## 1xx - Informational Responses (100-199)

Server received part of request, waiting for rest. "Keep going" signal.

**Common:**

- **100 Continue** - Server ready for rest of request
    

## 2xx - Successful Responses (200-299)

Request succeeded, server processed and returned requested data.

**Common:**

- **200 OK** - Request successful, resource returned
    
- **201 Created** - New resource successfully created
    
- **204 No Content** - Request successful, no content to return
    

## 3xx - Redirection Messages (300-399)

Resource moved to different location, new URL provided.

**Common:**

- **301 Moved Permanently** - Resource permanently moved, use new URL
    
- **302 Found** - Temporary redirect
    
- **304 Not Modified** - Cached version still valid
    

## 4xx - Client Error Responses (400-499)

Problem with the request (wrong URL, missing authentication, etc.)

**Common:**

- **400 Bad Request** - Malformed request syntax
    
- **401 Unauthorized** - Authentication required
    
- **403 Forbidden** - Server refuses to authorize request
    
- **404 Not Found** - Resource doesn't exist at given URL
    
- **405 Method Not Allowed** - HTTP method not supported
    

## 5xx - Server Error Responses (500-599)

Server encountered an error, not the client's fault.

**Common:**

- **500 Internal Server Error** - Generic server-side error
    
- **502 Bad Gateway** - Invalid response from upstream server
    
- **503 Service Unavailable** - Server temporarily overloaded/down
    

## Security Implications

- **401/403:** Test for authentication/authorization bypasses
    
- **404:** May reveal information about directory structure
    
- **500:** Can expose server details in error messages
    
- **3xx:** Check for open redirect vulnerabilities
    

## Status Code Quick Reference

|Code|Phrase|Meaning|
|---|---|---|
|100|Continue|Ready for rest of request|
|200|OK|Request successful|
|301|Moved Permanently|Resource permanently moved|
|404|Not Found|Resource doesn't exist|
|500|Internal Server Error|Server-side error|


# HTTP Response Headers & Body

## Response Headers

Key-value pairs providing information about the response and instructions on how to handle it.

## Required Response Headers

**Date**

`Date: Fri, 23 Aug 2024 10:43:21 GMT`

Shows when the response was generated.

**Content-Type**

`Content-Type: text/html; charset=utf-8`

Indicates content format (HTML, JSON, etc.) and character encoding.

**Server**

`Server: nginx`

Reveals server software handling the request.

- ⚠️ Can expose information useful to attackers - often removed or obscured
    

## Common Response Headers

**Set-Cookie**

`Set-Cookie: sessionId=38af1337es7a8`

Sends cookies from server to client for storage.

**Security flags:**

- `HttpOnly` - Prevents JavaScript access
    
- `Secure` - Only sent over HTTPS
    

**Cache-Control**

`Cache-Control: max-age=600`

Controls how long client can cache the response.

- Use `no-cache` for sensitive information
    

**Location**

`Location: /index.html`

Used in 3xx redirects to specify new resource location.

- ⚠️ Validate to prevent open redirect vulnerabilities
    

## Other Useful Headers

**Content-Length**

`Content-Length: 1024`

Size of response body in bytes.

**Content-Encoding**

`Content-Encoding: gzip`

Compression method used.

**Strict-Transport-Security (HSTS)**

`Strict-Transport-Security: max-age=31536000`

Forces HTTPS connections.

## Response Body

Contains actual data returned to client:

- HTML pages
    
- JSON data
    
- Images
    
- Files
    
- API responses
    

## Security Considerations

- **Sanitize user-generated content** - Prevent XSS attacks
    
- **Escape special characters** - Avoid injection vulnerabilities
    
- **Validate all output** - Ensure data integrity
    
- **Don't expose sensitive server info** - Remove/obscure Server header
    
- **Set secure cookie flags** - Use HttpOnly and Secure
    
- **Validate Location header** - Prevent open redirects
    

## Example Complete Response

`HTTP/1.1 200 OK`

`Date: Fri, 23 Aug 2024 10:43:21 GMT`

`Server: nginx`

`Content-Type: application/json; charset=utf-8`

`Content-Length: 62`

`Set-Cookie: sessionId=abc123; HttpOnly; Secure`

`Cache-Control: no-cache`

`{     "name": "Aleksandra",    "age": 27,    "country": "US" }`


# HTTP Security Headers

Security headers help protect web applications against attacks like XSS, clickjacking, and data leaks.

**Test website headers:** [https://securityheaders.io/](https://securityheaders.io/)

## Content-Security-Policy (CSP)

Mitigates XSS attacks by defining which domains are allowed to load content.

**Example:**

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

## Common Directives

- **default-src** - Default policy for all content types
    
- **script-src** - Where scripts can be loaded from
    
- **style-src** - Where CSS stylesheets can be loaded from
    
- **img-src** - Where images can be loaded from
    
- **'self'** - Special keyword meaning same domain only
    

## Strict-Transport-Security (HSTS)

Forces browsers to always connect over HTTPS.

**Example:**

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

## Directives

- **max-age** - Expiry time in seconds for this setting
    
- **includeSubDomains** - Apply setting to all subdomains (optional)
    
- **preload** - Include in browser preload lists (optional)
    

## X-Content-Type-Options

Prevents browsers from MIME-sniffing (guessing content types).

**Example:**

`X-Content-Type-Options: nosniff`

## Directive

- **nosniff** - Browser must use Content-Type header, not guess
    

## Referrer-Policy

Controls what information is sent when users click links to other sites.

**Examples:**

`Referrer-Policy: no-referrer`

`Referrer-Policy: same-origin`

`Referrer-Policy: strict-origin`

`Referrer-Policy: strict-origin-when-cross-origin`

## Directives

- **no-referrer** - Completely disables referrer information
    
- **same-origin** - Only send referrer info within same website
    
- **strict-origin** - Send origin only when protocol stays same (HTTPS→HTTPS)
    
- **strict-origin-when-cross-origin** - Full URL for same-origin, origin only for cross-origin
    

## Security Impact

|Header|Protects Against|
|---|---|
|CSP|XSS, code injection|
|HSTS|Protocol downgrade attacks, MITM|
|X-Content-Type-Options|MIME confusion attacks|
|Referrer-Policy|Information leakage|

## Best Practices

- Always implement CSP to prevent XSS
    
- Use HSTS with long max-age and includeSubDomains
    
- Set X-Content-Type-Options to nosniff
    
- Choose appropriate Referrer-Policy based on privacy needs