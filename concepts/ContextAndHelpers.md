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
```vue
Example #1 - calling an API using a dynamic page param from the url:

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

```vue
Example 1.1 - destructuring the context object (ES6)
	* Pass in objects we want to access without using the word context

export default {
  async asyncData({ params, $http, error }) {
    const id = params.id

    try {
      // Using the nuxtjs/http module here exposed via context.app
      const post = await $http.$get(`https://api.nuxtjs.dev/posts/${id}`)
      return { post }
    } catch (e) {
      error(e) // Show the nuxt error page with the thrown error
    }
  }
}
```

#### Helpers
In addition to the context shortcuts, NuxtJS has many other helpers:

* `$nuxt` - improve user experience and an escape hatch in some scenarios
  * accessible via `this.$nuxt` in Vue components and via `window.$nuxt` on the client side
  * Features:
    1. Connection checker (`$nuxt.isOffline / $nuxt.isOnline`)
    2. Accessing root directory (`window.$nuxt`)
       * Use sparingly but can access things like axios outside Vue Components
    3. Refreshing page data (`this.$nuxt.refresh()`)
    4. Control loading bar (`this.$nuxt.$loading`)
* `window.onNuxtReady` - run a script after Nuxt application has loaded and is ready
* `process` object - three booleans to help determine where app was rendered
  1. `client`
  2. `server`
  3. `static`
    