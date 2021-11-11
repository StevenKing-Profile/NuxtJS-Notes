## [Rendering](https://nuxtjs.org/docs/features/rendering-modes)

#### Server-side
```angular2html
nuxt.config.js:

export default {
  ssr: true // default value
}
```

#### Client-side rendering only
* Rendering the content in the browser using JS, instead of on Node.
```angular2html
nuxt.config.js:

export default {
  ssr: false
}
```