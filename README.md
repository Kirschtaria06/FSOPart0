%% Notes App Diagrams - GitHub Markdown with Mermaid

%% 1️⃣ Traditional Page - Initial Load
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: Browser executes JS code that fetches notes JSON
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: Browser executes callback and renders notes

%% 2️⃣ Traditional Page - New Note Creation
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes a note in the text field and clicks "Save"

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    Note right of server: Server stores the new note in data.json
    server-->>browser: 201 Created (confirmation)
    deactivate server

    Note right of browser: Browser fetches updated notes
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, { "content": "New note", "date": "2023-2-28" }]
    deactivate server

    Note right of browser: Browser executes callback and renders updated notes

%% 3️⃣ Single Page App (SPA) - Initial Load
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: Browser executes JS code that fetches notes JSON
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: Browser renders notes dynamically

%% 4️⃣ SPA - New Note Creation
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes a new note and clicks "Save"

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    Note right of server: Server adds note to data.json
    server-->>browser: 201 Created
    deactivate server

    Note right of browser: Browser updates the page dynamically
    Note right of browser: JS adds the new note to the DOM without reloading
