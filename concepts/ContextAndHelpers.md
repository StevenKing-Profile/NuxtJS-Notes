## [Context and helpers](https://nuxtjs.org/docs/concepts/context-helpers)
* additional information about the current request to the application
* provide access to other parts of the Nuxt application
* Note: not to be confused with `context` object in Vuex Actions or `build.extend` function in `nuxt.config.js`

#### Context keys:
```angular2html
function (context) { // Could be asyncData, nuxtServerInit, plugins, middleware, ...
  // Always available
  const {
    app,
    store,
    route,
    params,
    query,
    env,
    isDev,
    isHMR,
    redirect,
    error,
    $config
  } = context

  // Only available on the Server-side
  if (process.server) {
    const { req, res, beforeNuxtRender } = context
  }

  // Only available on the Client-side
  if (process.client) {
    const { from, nuxtState } = context
  }
}
```

#### Using page parameters for your API query 
* exposes dynamic parameters via `context.params`
* Example (call an API using a dynamic page param as part of the url):
```vue
export default {
  async asyncData(context) {
    const id = context.params.id
    try {
      // Using the nuxtjs/http module here exposed via context.app
      const post = await context.app.$http.$get(
        `https://api.nuxtjs.dev/posts/${id}`
      )
      return { post }
    } catch (e) {
      context.error(e) // Show the nuxt error page with the thrown error
    }
  }
}
```