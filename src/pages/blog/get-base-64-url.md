---
layout: "../../layouts/BlogPost.astro"
title: "Get base64 from URL"
pubDate: "Jul 22, 2022"
published: false
---

```javascript
async function getBase64FromUrl(URL) {
  const data = await fetch(URL);
  const blob = await data.blob();
  return new Promise((resolve) => {
    const reader = new FileReader();
    reader.readAsDataURL(blob);
    reader.onloadend = () => {
      const base64data = reader.result;
      resolve(base64data);
    };
  });
};
```