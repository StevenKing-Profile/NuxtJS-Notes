## [Deployment Targets](https://nuxtjs.org/docs/features/deployment-targets)

#### Static Hosting
* `nuxt generate` generates a static version of your website

```angular2html
nuxt.config.js

export default {
  target: 'static' // default is 'server'
}
```

Running nuxt dev with the static target will improve the developer experience:
* Remove req & res from context
* Fallback to client-side rendering on 404, errors and redirects see SPA fallback
* $route.query will always be equal to {} on server-side rendering
* process.static is true


#### Server Hosting
* `nuxt build`

```angular2html
nuxt.config.js

export default {
  target: 'server'
}
```

You can still run Nuxt with server hosting with ssr: false but Nuxt will not fully render the HTML for each page - 
leaving that task to the browser. You might choose this option if you need serverMiddleware but do not want fully server-side rendered HTML.