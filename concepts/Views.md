## [Views](https://nuxtjs.org/docs/concepts/views)
* describes everything you need to know to configure data and views for a specific route
* consist of:
  * App template
  * A layout
  * Actual page

### Pages
* Every page component is a Vue component (but with special attributes and functions)
```angular2html
<template>
  <h1 class="red">Hello World</h1>
</template>

<script>
  export default {
    head() {
      // Set Meta Tags for this Page
    }
    // ...
  }
</script>

<style>
  .red {
    color: red;
  }
</style>
```

### Layouts
* Change the look and feel of a Nuxt app
* default layout is defined in `default.vue`


* Make sure to add the `<Nuxt/>` component when creating a layout to actually include the page component.
* custom layouts need to set the `layout` property in the page component where we want to use the layout

  ```angular2html
  layouts/blog.vue:
  <template>
    <div>
      <div>My blog navigation bar here</div>
      <Nuxt />
    </div>
  </template>
  
  pages/posts.vue:
  <template>
    <!-- Your template -->
  </template>
  <script>
    export default {
      layout: 'blog'
      // page component definitions
    }
  </script>
   ```
  
### Error Page
* Special page component that always displays on error
* Goes in `layouts` folder but treated as a page
* Can customize the error page by adding a layouts/error.vue file

### Document: App.html
* Template to create actual HTML frame of your document
* NuxtJS injects content as well as variables for the head/body
* can customize to include scripts/conditional CSS classes by creating an `app.html` file in the root dir
```angular2html
Default template:
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>

Custom template:
<!DOCTYPE html>
<!--[if IE 9]><html class="lt-ie9 ie9" {{ HTML_ATTRS }}><![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--><html {{ HTML_ATTRS }}><!--<![endif]-->
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
  {{ APP }}
  </body>
</html>

```