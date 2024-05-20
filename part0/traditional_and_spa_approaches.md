<h1>Traditional Approach</h1>
<h2>Loading Page</h2>
<p>
All resources such as HTML, CSS, JavaScript and data are load.
</p>

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the<br/> JavaScript code that fetches the<br/> JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback<br/> function that renders the notes
```

<h2>Post New Note</h2>
<p>
In the traditional approach, a POST request involves sending data to the server, which then processes the request and responds by reloading and rendering the entire webpage. This method refreshes the entire page, requiring the browser to reload all resources such as HTML, CSS, and JavaScript, which can result in longer loading times and a less seamless user experience.
</p>

```mermaid
sequenceDiagram
    actor user
    participant browser
    participant server

    user->>browser: Write "New Note" in Textbox
    user->>browser: Click Button Save
    activate browser

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note {"note": "New note"}
    activate server
    server-->>browser: Response 302: Redirect to Location /notes
    deactivate server

    Note right of browser: The browser starts all requests again

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    browser-->>user: Notes List Updated
    deactivate browser
```
<br/>
<br/>

<h1>Single Page Application (SPA)</h1>
<h2>Loading Page</h2>
<p>
When loading the webpage for the first time, it must perform the same queries as the traditional approach, retrieving the HTML document and subsequently the CSS, JS script, and JSON data.
</p>

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the<br/> JavaScript code that fetches the<br/> JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback<br/> function that renders the notes
```

<h2>Post New Note</h2>
<p>
Since it follows the AJAX approach, it doesn't reload the entire page. Instead, it updates specific parts of the page dynamically, which leads to a faster and smoother user experience compared to the traditional approach where the whole page is re-rendered.
</p>

```mermaid
sequenceDiagram
    actor user
    participant browser
    participant server

    user->>browser: Write "New Note" in Textbox
    user->>browser: Click Button Save
    activate browser

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa {"note": "New note"}
    activate server
    server-->>browser: Response 204: {"message":"note created"}
    deactivate server

    Note right of browser: After receiving the successful response, the<br/>browser proceeds to insert the item to the<br/> list using the input data given by the user

    browser-->>user: Notes List Updated
    deactivate browser
```
