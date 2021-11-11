## [Server-side rendering](https://nuxtjs.org/docs/concepts/server-side-rendering)
* the ability of an application to contribute by displaying the web-page on the server instead of rendering it in the browser
* Server-side sends a fully rendered page to the client; the client's JavaScript bundle takes over which then allows the Vue.js app to hydrate (take over)

#### Extend and control the server
```vue
server-middleware/logger.js:
  export default function (req, res, next) {
    console.log(req.url)
    next()
  }

nuxt.config.js:
  export default {
    serverMiddleware: ['~/server-middleware/logger']
  }
```

#### Server vs Browser envs
* App has access to Node.js objects like `req` and `res` (because running in Node.js env)
* No access to `window` or `document` objects (because they belong to the browser)
  * can access `window` or `document` by using `beforeMount` or `mounted` hooks
  ```angular2html
    beforeMount() {
        window.alert('hello);
    }
  ```

#### Server-side Rendering steps with Nuxt
1. Browser to Server
   * Browser initial request -> Node.js server. Nuxt generates HTML and sends it back to the browser with results from executed functions/hooks
     * e.g. `asyncData`, `nuxtServerInit`, or `fetch`.
2. Server to Browser
  * Browser receives the rendered page. Content is displayed and Vue.js hydration starts. Afterwards, page is interactive
3. Browser to Browser
  * Navigating between pages with `<NuxtLink>` is done on client side unless hard refresh browser

#### Caveats
1. window or document undefined
   * due to server-side rendering, if need to import a resource only on the client-side, use `process.client`
    ```angular2html
        if (process.client) {
            require('external_library')
        }
    ```
2. iOS and phone numbers
   * some Safari versions automatically transform phone numbers into links. This triggers a `NodeMismatch warning`