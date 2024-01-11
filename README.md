

# Learning Workbox
## default structure
./project-root
├── build
│   ├── css
│   │   └── main.css
│   ├── index.html
│   └── js
│       └── app.js
└── package.json
## change scripts(package.json)
## index.html
    link main.css inside HEAD tag
    ```
        <link rel="stylesheet" href="css/main.css">
    ```
    SCRIPT tag and source app.js at the bottom of BODY tag
    ```
        <script async src="js/app.js"></script>
    ```
### main.css
### link to app.js(at bottom of body tag)





- make workbox-config.js at root
- make src-sw.js at root
    importScript('orkbox-sw.js')
    workbox.precaching.precacheAndRoute([])
    ├── build
│   ├── css
│   │   └── main.css
│   ├── index.html
│   ├── js
│   │   └── app.js
│   ├── manifest.json
│   ├── sw.js
│   ├── sw.js.map
│   ├── workbox-e24dcd3f.js
│   └── workbox-e24dcd3f.js.map
├── learning.md
├── package.json
└── workbox-config.js

