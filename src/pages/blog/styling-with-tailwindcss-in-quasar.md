---
layout: "../../layouts/BlogPost.astro"
title: "Styling with Tailwind CSS in Quasar"
pubDate: "Feb 15, 2022"
---

I’ve been working with Quasar and Tailwind CSS for some projects, both are really helpful tools, sometimes I need to style my Quasar app with Tailwind CSS because I feel more comfort with Tailwind CSS for styling and I love how it works.

It’s quite simple to integrate Tailwind CSS to Quasar, you just need to do some little configurations.

Open your Quasar project in terminal and run these commands.

```shell
yarn add -D tailwindcss & npx tailwindcss init
```

There will be a new file named tailwind.config.js created. Open the file and add new property “prefix” with value “tw-“, then change value of content property to ["./src/*/*.{html,js,vue}"].

```javascript
module.exports = {
  prefix: "tw-",
  content: ["./src/**/*.{html,js,vue}"]
}
```

note: we have to use prefix to avoid clashes of Quasar classes and Tailwind CSS’s.

Now open scr/css/app.scss and add these to import utility classes of Tailwind CSS.

```css
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";
```

The last thing to do is add Tailwind CSS in .postcssrc.js file.

```javascript
require("tailwindcss")
```

```javascript
module.exports = {
  plugins: [
    require("tailwindcss"),
    require("autoprefixer"),
  ]
}
```

Alright, now you can use Tailwind CSS classes in your project, try to make a square div with red background and make it rounded at its every corner then place a text at center.

```javascript
<div 
  class="tw-h-24 tw-w-24 tw-bg-red-500 tw-rounded tw-flex tw-justify-center tw-items-center tw-text-white tw-text-lg"
>
  Hola!
</div>
```

![result](/blog/styling-with-tailwindcss-in-quasar/image.png)

You can also combine Quasar classes and Tailwind CSS when you need.