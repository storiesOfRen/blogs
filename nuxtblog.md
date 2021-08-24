So I recently updated my personal resume website, and I thought it would be a good opportunity to refresh on Vue and learn [NuxtJs](https://nuxtjs.org/).  So I thought I'd give a run through of my experience.

The general setup of Nuxt is pretty self explanatory with in its stepper. They've got setup docs for `yarn`, `npx`, and `npm`.  I went through the `npx` choose your own adventure setup.

## Choose Your own adventure: `npx` style
```
npx create-nuxt-app <project-name>
```
As you journey through the `npx create-nuxt-app` route, you will be asked many questions.

- __What Package manager?__
  - `yarn`
  - `npm`
- __What programming language?__
  - JavaScript
  - TypeScript
- __Do you want a UI Framework?__
  - [Ant Design Vue](https://www.antdv.com/docs/vue/introduce/)
  - [BalmUI](https://material.balmjs.com/#/)
  - [Bootstrap](https://bootstrap-vue.org/)
  - [Buefy](https://buefy.org/)
  - [Chakra UI](https://chakra-ui.com/)
  - [Element](https://madewithvuejs.com/element-ui)
  - [Framevuerk](https://framevuerk.com/)
  - [Oruga](https://oruga.io/)
  - [Tachyons](https://tachyons.io/components/)
  - [Tailwind CSS](https://tailwindcss.com/docs/guides/vue-3-vite)
  - [Windi CSS](https://windicss.org/integrations/vue-cli.html)
  - [Vant](https://youzan.github.io/vant/#/en-US/)
  - [View UI](https://github.com/view-design/ViewUI)
  - [Vuetify](https://vuetifyjs.com/en/)
- __Nuxt.js modules:__
  - Axios - Promise based HTTP client
  - Progressive Web App (PWA)
  - Content - Git-based headless CMS
- __Linting tools:__
  - ESLint
  - Prettier
  - Lint staged files
  - StyleLint
  - Commitlint
- __Testing framework:__
  - None
  - Jest
  - AVA
  - WebdriverIO
  - Nightwatch
- __Rendering mode__
  - Universal (SSR / Static)
  - SPA
- __Deployment target__
  - Server (Node.js hosting)
  - Static (Static/JAMStack hosting)
- __Development tools__
  - jsconfig.json
  - Semantic PR
  - Dependabot (for GitHub only)
- __Continuous Integration__
  - GitHub Actions
  - Travis CI
  - CircleCI

### My route:
- `npm`
- JavaScript
- No UI framework
- Axios
- ESLint, Prettier, Stylelint, Lint staged files
- Like a horrible person I didn't add a testing library
- SPA
- Static (I deploy to github pages)
- jsConfig, Dependabot
- No CI 

I wanted a really clean slate to work with, but you can obviously manipulate or add in some of these options later if you find you need them.

Once you are all built, you can head into your directory!

```
cd <project-name>
npm run dev
``` 
### Me though, I chose a more dangerous and tedious route:

My previous code base was a `create-react-app`. I created a new branch and carefully removed that information making sure not to delete items that would remove my connection to `git` then copied over my new Nuxt project into the directory. Once everything was correctly manipulated then I could `npm run dev`. 
*There was probably an easier way to do this, but I sometimes just impulsively start things without thinking, when trying to learn new things... oops*

Up until this point, I had been using react based frameworks.  Most recently, I had been using [NextJS](https://nextjs.org/), which has a lot in common functionally as NuxtJS. Both have an opinionated routing system, meaning it's built in, which made setup go much faster.  It was kind of auto-magical! But because of my experience with Next it made working in Nuxt a bit easier.    

## Project Setup, Time to build
After getting my project setup and my new branch pushed to Github, I felt it was safe to start adding and adjusting content as I saw fit. 
...
### Cool things about Nuxt
Nuxt has a present directory structure that helps in the dynamic and auto importing.  
__My Fave Things__
- Components
  - The auto imports is available v2.13+
  - Easy to use Lazy loading, by just prefixing `Lazy` to the front of you component.
    - `<LazyTheFooter />`
    - Using the lazy prefix you can also dynamically import a component when an event is triggered.
- Layouts
  - So this may be more in line with liking the templating feature in Vue, but I dig the reusable layouts. On my personal resume site I really only extended the default layout, but the fact that I can create different layouts for specific templates is just cool.
- Pages
  - I mentioned before that Nuxt like Next has an opinionated routing system.  So the router is built-in, cool right? Well not half as cool as the router configurations being automatically created for me just by adding my files to the `Pages` Directory!!!! 

I'm using [Dependabot](https://github.com/dependabot), for the first time, I'm like it so far also.  It's kind of like how My cats tell me if they need fed, but plants don't... as in the Dependabot tells me about when my Dependencies need updating and if I relied on my own watchful eyes, the dependencies would probably die like any plants I've tried to keep.

Coolest thing about Nuxt, It has great Documentation! It's pretty understandable and followable.
 
### The things I needed to add or change

I needed to update a few things.  I needed to add a `.stylelintignore`, to ignore the `.nuxt` directory, it was not thrilled with how some of the css was being built out and was refusing to commit because of it.  I could have updated the rules to include it, but I actually like the rule it was breaking, in the end I guess that is a linting preference.  That being said, I'm thrilled that they included [stylelint](https://stylelint.io/) in the Nuxt template creation.  It's my go to for style linting now-a-days. 

## The site is built! Time to Deploy!
Well I mean the site has content.  That means it's time to generate the static build and publish. 


### Generate for static.

The first step in deploying is generating the build the static web app. And you do that by running the `generate` script:

```
npm run generate
```

This creates a `dist` directory.  It contains everything I needed to deploy to my Github pages site.

After running this script you will need to commit your changes at the very least, because if you try to deploy with the changes not committed, you will receive a error in deployment.

### [Deploy to `gh-pages`](https://nuxtjs.org/docs/2.x/deployment/github-pages#deploying-to-github-pages-for-repository)

The deploying documentation is stellar! It's also not limited to GitHub, so that's cool!
But for GitHub you want use [`push-dir`](https://github.com/L33T-KR3W/push-dir) 

```
npm install push-dir --save-dev
```
Then you add the `deploy` script:

```
"deploy": "push-dir --dir=dist --branch=gh-pages --cleanup"
},
```
Then like magic my site would be deployed and be live pretty quickly!  

## Last Impressions

Nuxt is cool and handy for getting a quick start!  I would recommend this more for refreshing on VueJS rather than trying to learn both how to work in Nuxt and writing VueJS templates.




   
