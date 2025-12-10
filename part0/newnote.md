sequenceDiagram
    participant browser
    participant server

    Note over browser: User writes a note and clicks "Save"

    %% The Form Submit
    browser->>server: HTTP POST /new_note
    activate server
    Note right of server: Server receives input,<br/>saves to database
    server-->>browser: HTTP 302 (Location: /notes)
    deactivate server

    %% The Reload (Redirect)
    Note right of browser: Browser reads 302 code<br/>and reloads /notes
    
    browser->>server: HTTP GET /notes
    activate server
    server-->>browser: HTML Document
    deactivate server

    %% Asset Loading
    browser->>server: HTTP GET /main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: HTTP GET /main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    %% JS Execution & Data Fetching
    Note right of browser: Browser executes JS<br/>and requests data

    browser->>server: HTTP GET /data.json
    activate server
    server-->>browser: JSON Data (All notes)
    deactivate server

    Note right of browser: Browser renders the notes