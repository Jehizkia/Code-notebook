# Wordpress notebook


**Tailwindcss package.json**

Change the `custom-file.css` to include it in the tailwindcss build.
``` bash
  "scripts": {
    "tailwind": "./node_modules/.bin/tailwind build ./css/custom-file.css -c ./css/tailwind.js -o ./style.css"
  }
```
