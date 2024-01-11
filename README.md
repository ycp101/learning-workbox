

# 0. Learning Workbox
- [Learned from Youtube](https://www.youtube.com/watch?v=PL2DG9LJoVQ)
- [github](https://github.com/designcourse/vanillajs-workbox-pwa/blob/110b39d27431bfa8df7138a90ce8372e1e418202/package.json)
# 1. Directory structure
- make directory structure and files
    ```
        ./project-root
        ├── build
        │   ├── css
        │   │   └── main.css
        │   ├── index.html
        │   └── js
        │       └── app.js
        └── package.json
    ```
# 2. Configure npm
- Change scripts command in package.sjon

    ```javascript
    "scripts": {
    "serve": "http-server -p 1335 build -c-1"
    },
    ```
# 3. Edit index.html
- link main.css inside HEAD tag

    ```html
       <link rel="stylesheet" href="css/main.css">
    ```

- source app.js at the bottom of BODY tag

    ```html
        <script async src="js/app.js"></script>
    ```

# 4. Service worker
- install workbox

    ```bash
    $ npm install workbox-cli -g
    ```

- generate workbox-config.js

    ```bash
    $ workbox wizard
    ```

    ```javascript
    module.exports = {
        "globDirectory": "build/",
        "grobPatterns": [
            "**/*".{css,html,js}""
        ],
        "swDest": "build/sw.js"
    }
    ```
- generate sw.js

    ```bash
    $ workbox generateSW
    ```
    > This will generate sw.js. Do not modify sw.js

- add event listener to index.html for sw.js below app.js script

    ```javascript
    if('serviceWorker' in navigator) {
        window.addEventListener('load', () => {
            navigator.serviceWorker.register('/sw.js');
            });
    }
    ```

# 5. cache
- edit workbox-config.js
    ```javascript
    module.exports = {
        "globDirectory": "build/",
        "grobPatterns": [
            "**/*".{css,html,js}""
        ],
        "swDest": "build/sw.js"
        "swSRC": "src-sw.js"
    }
    ```
- write src-sw.js
    ```javascript
    importScripts('https://storage.googleapis.com/workbox-cdn/releases/3.0.0/workbox-sw.js');

    workbox.routing.registerRoute(
        new RegExp('https://jsonplaceholder.typicode.com/users'),
        workbox.strategies.cacheFirst()
    );

    // custom adjustment here
    workbox.routing.registerRoute(
        new RegExp('https://fonts.(?:googleapis|gstatic).com/(.*)'),
        workbox.strategies.cacheFirst({
          cacheName: 'google-fonts',
          plugins: [
            new workbox.expiration.Plugin({
              maxEntries: 30,
            }),
            new workbox.cacheableResponse.Plugin({
              statuses: [0, 200]
            }),
          ],
        }),
      );
    // end of custom adjustment

    workbox.precaching.precacheAndRoute([]);
    ```
    > this will cache google fonts

- run

    ```
    workbox injectManifest
    ```
    > this will generate manifest.json

# 6. Installable
- Generate Manifest file at Generate Manifest file](https://app-manifest.firebaseapp.com/)
- Add manifest file link to very top of HEAD tag of index.html
