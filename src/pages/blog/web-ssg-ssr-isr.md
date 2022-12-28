---
layout: "../../layouts/BlogPost.astro"
title: "SSG vs SSR vs ISR"
pubDate: "Dec 12, 2022"
---

**What are SSG, SSR, and ISR?**

- **SSG (Static Site Generation)**: SSG is a process in which a website is built as a set of static HTML pages. The content of the pages is generated at build time, and the pages are served to the user without any further processing on the server. This means that the website can be hosted on a simple web server, such as Apache or Nginx, without the need for a server-side language such as PHP or Node.js.
- **SSR (Server-Side Rendering)**: SSR is a process in which a server generates the HTML for a website on the fly and serves it to the user. This allows the website to be built using a server-side language such as PHP or Node.js, and the content of the website can be dynamic, as it is generated on the server.
- **ISR (Incremental Static Regeneration)**: ISR is a hybrid approach that combines the benefits of SSG and SSR. The website is built as a set of static HTML pages, but the content of the pages is generated on the server on demand, rather than at build time. This allows the website to be fast and scalable, like an SSG website, but with the ability to generate dynamic content, like an SSR website.

**Benefits of SSG, SSR, and ISR**

**SSG**: SSG websites are fast and scalable, as they are served as static HTML pages. They are also easy to host, as they do not require a server-side language.  
**SSR**: SSR websites can generate dynamic content on the server, which can be useful for websites that need to show personalized or changing content.  
**ISR**: ISR websites combine the benefits of SSG and SSR, allowing developers to build fast and scalable websites with the ability to generate dynamic content on demand.

Here are some examples of popular tools and frameworks for building SSG, SSR, and ISR websites:

- SSG: [Gatsby](https://www.gatsbyjs.com/), [Jekyll](https://jekyllrb.com/), [Hugo](https://gohugo.io/)
- SSR: [Next.js](https://nextjs.org/), [Nuxt.js](https://nuxtjs.org/), [Angular](https://angular.io/)
- ISR: [Gridsome](https://gridsome.org/), [Nuxt.js](https://nuxtjs.org/) (with the ISR mode)