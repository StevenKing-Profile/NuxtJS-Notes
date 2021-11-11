## [Nuxt Lifecycle](https://nuxtjs.org/docs/concepts/nuxt-lifecycle)

varies for client + server

1. nuxt ServerInit
2. Route Middleware
   * 3 types: 
     1. Global - `nuxt.config.js` 
     2. Layout - affects groups of routes defined in layouts
     3. Page - affects single route, defined on page components
3. validate()
   * validate things like dynamic route parameter before rendering page
4. asyncData() or fetch(context) - called every time before loading page components

##### --- Beginning of Vue Lifecycle Hooks. `beforeCreate` hook is called when Vue instance is initialised ---

5. created()
   * called when Vue instance is created 
6. fetch() 
  * called after Vue instance is created
  * `this` context available here
  * Handles errors at component level
7. mounted()
   * called when DOM is rendered and reactive
#### ... rest of Vue lifecycle hooks