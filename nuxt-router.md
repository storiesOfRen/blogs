## How cool is Nuxt automatic routing???

To really understand how cool Nuxt's automatic routing is, you need to understand how to set up a router in a traditional Vue project. But why do you need to know that? It is because Nuxt uses [`vue-router`](https://router.vuejs.org/guide/#html). Now the fastest way to set up a router in a vue project is to use the [`Vue CLI` tool](https://cli.vuejs.org/guide/installation.html), so you can have template for setting up your router.

## Setting up a Vue app router

The file tree for the Vue router set up:

```
src/
--| assets/
--| components/
--| router/
-----| index.js
--| views/
-----| Home.vue
-----| About.vue
--| App.vue
--| main.js
```

Using the CLI tools helps setting up the router much faster by providing a template to follow, however whenever you need to add pages you need to manually add routes to the router configurations you see below.

### [`src/router/index.js`](https://router.vuejs.org/guide/#javascript)<sub> 1</sub>

```js
import { createRouter, createWebHashHistory } from "vue-router";
import Home from "../views/Home.vue";
import About from "../views/About.vue";

const routes = [
  {
    path: "/",
    name: "Home",
    component: Home,
  },
  {
    path: "/about",
    name: "About",
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import("../views/About.vue"),
  },
];

const router = createRouter({
  history: createWebHashHistory(),
  routes,
});

export default router;
```

### [`src/App.vue`](https://router.vuejs.org/guide/#html)<sub> 2</sub>

When adding navigation to the router you use a `<router-link/>` and use the `<router-view/>` for rending the component of the mapped path.

```VUE
<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
```

### [`src/main.js`](https://router.vuejs.org/guide/#html)<sub> 3</sub>

```js
import { createApp } from "vue";
import App from "./App.vue";
import router from "./router";

createApp(App).use(router).mount("#app");
```

Alright you probably thinking, with the CLI tool setting up a router doesn't seem tedious at all. Well that is true, it's just a little extra work to have to add to or adjust the route mapping and App template. Nuxt, which is based in Vue, has automatic routing, as in it Auto-magically adds to the route mapping and templates. So essentially all you need to do to make routing work is put `.vue` files in the `pages` directory and blam routing.

The file tree for Nuxt automatic routing:

## Basic Routes

```
components/
layouts/
pages/
--| index.vue
--| About.vue

```

In `vue-router` there's the `<router-link/>` to navigate to the app's internal pages within the router, in Nuxt the component is `<NuxtLink/>`, both have `to="#"` attribute, which acts like the `href` of the anchor tag `<a href="#" />`. That being said the `<NuxtLink/>` is only used for Internal navigation, any external navigation should use anchor tags.

So in terms of how the basic routes are generated, let's reference the Nuxt automatic routing file tree above, and explore the router object that would be created.

```js
const router = {
  routes: [
    {
      name: "index",
      path: "/",
      component: "pages/index.vue",
    },
    {
      name: "About",
      path: "/about",
      component: "pages/About.vue",
    },
  ],
};
```

When creating an `index.vue` file within the top level of the`pages` directory, this automatically will have the base path `/` assigned to it. When the files are named it will create a path associated with the what you've named the `.vue` file. Additionally you can create Dynamic routes and Nesting routes.

## Dynamic Routes

```
components/
layouts/
pages/
--| index.vue
--| _slug/
-----| index.vue
--| users/
-----| _id.vue

```

Dynamic routes are routes where the name of the route includes unique identifiers and/or are unknown. A good example of this is if you are going to specific user's profile page, like: `someSite.com/userID`. In Nuxt we create dynamic link by adding an underscore to the beginning of the name of the route, like we see in the file tree above with `_slug.vue` and `users/_id.vue`. You can have both dynamic directories and dynamic routes.

## Nested Routes

```
components/
layouts/
pages/
--| index.vue
--| users/
-----| _id.vue
--| users.vue

```

Nested routes are created when a directory and a `.vue` file are at the same level and named the same, you can see an example of this above in the file tree for nested routes.

Creating these more complex file trees for the routing system still creates a router object similar to the basic routes, but a little different, specifically in terms of the nested routes. Below is an example holding both a dynamic routes and nested.

```js
const router = {
  routes: [
    {
      name: "index",
      path: "/",
      component: "pages/index.vue",
    },
    {
      name: "About",
      path: "/about",
      component: "pages/About.vue",
    },
    {
      // this is the basic nested route
      path: "/blog",
      component: "pages/blog.vue",
      children: [
        {
          name: ":id",
          path: "/blog/:id",
          component: "pages/blog/_id.vue",
        },
      ],
    },
    {
      // this is the basic dynamic route
      name: "User",
      path: "/user/:id",
      component: "pages/user/_id.vue",
    },
  ],
};
```

And there are the basics surrounding the coolness of the Nuxt Automatic Routing system. If you wanted to learn more about Nuxt router you can checkout how to extend the Nuxt router, reading about it in the Nuxt Docs under the [File System Routing Feature: Extending the Router](https://nuxtjs.org/docs/features/file-system-routing#extending-the-router)!

Thanks for reading!

## Resources

1. [`vue-router` Router Javascript Example](https://router.vuejs.org/guide/#html)
2. [`vue-router` App.vue](https://router.vuejs.org/guide/#html)
3. [Example code for main.js is pulled for a test app made with the CLI tool](https://cli.vuejs.org/guide/)
