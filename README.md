https://codesandbox.io/p/devbox/nextjs-basic-app-k2yfy7
https://codesandbox.io/p/devbox/meals-app-starting-project-forked-cy8lk7?file=%2Fapp%2Fcommunity%2Fpage.js%3A6%2C1 (meals project)

nextjs 14

App Router

- nextjs uses app/ folder
- rendering is done on the server
- routing is done by creating folders inside app/ AND "page.js"
- page should return jsx of what to render
- need default exports
- When you use export default, it allows Next.js to import the component without specifying the exact name of the import. default exports make it easier for Next.js to work with file-based routing and generate routes automatically.

type of files:

pages.js - page content
layout.js - wrapper around pages
not-found.js - not found page
loading.js - shown while sibling or nested pages or layouts are fetching data
error.js - error page
route.js - create an api route (page which does not return jsx code but data in eg. json format)

filenames are only reserved when creating them inside of the app/ folder (or any subfolder).

---

SERVER COMPONENT VS CLIENT COMPONENT
to tell nextjs something is client component,
define 'use client';

---

DYNAMIC ROUTES
any string inside brackets [] eg. using [**placeholder**] folder:

blog/page.js
blog/[placeholder]/page.js

[placeholder]/page.js

//gets access to props to destructure a {params} object

- every [placeholder] will be a key in params object and its value will be the url concrete value (whatever was passed in)

```js
export default function SomePage({ param }) {
  console.log(params.placeholder); //note the naming is same as the folder [placeholder] to get the url data
}
```

```js
export default function MealDetailPage({params}){
  const meal = getMeal(params.mealSlug);

  meal.instructions = meal.instructions.replace(/\n/g, '<br/>');

  ...

  return (<>
    <h1>{meal.title}</h1>
    <main>
      <p className={} dangerouslySetInnerHTML={{__html: meal.instructions}}>
      </p>
    </main>
  </>)

}
```

---

LINKS

using links to prevent rerending of page

import Link from 'next/Link';

<Link href="/about">About us</Link>

---

IMAGES

supports lazy loading under the hood.
auto image size detection.
file format .webp - different sized images are loaded depending size of viewport
priority - loads image with priority
you can use 'fill' prop when you dont know the width and height of images ahead of time

```js
import Image from 'next/image';

<Image src={} alt="" priority fill/>
```

---

IMAGES ALT METHOD: HARDCODED ASSETS:
to use an import, access it via .src property in nextjs

to use images, eg. from assets/logo.jpg
import logoImg from '@/assets/logo.png';

<img src={logoImg.src} alt="logo"/>

---

NAVIGATION

<nav>
<ul>
  <li><Link href="/meals">Browser Meals</Link>
</ul>
</nav>

---

LAYOUTS

RESERVED FILENAME: 'layout.js'
Layout renders <html> and <body> tags
Layout - every nextjs app needs atleast 1 root layout.js

- the metadata variable is reserved name and is part of the <head> which is handled by nextJs

export const metadata = {
title:'',
description:''
};

export default function RootLayout({children}){
return (<html><body>{children}</body></html>)
}

---

GLOBAL STYLE

root dir has ./globals.css
import into layout:

import './globals.css'

---

FAVICON

./app/icon.png

---

PATH ALIAS

jsconfig.json using @ to target root folder

---

LOADING

Nextjs embraces React's suspense to show suspense fallback while it loads

```js
import { Suspense } from "react";

<Suspense>
  <SomeComponent fallback={<p className={classes.loading}>loading...</p>} />
</Suspense>;
```

PAGE

RESERVED FILENAME: 'page.js'

---

ERROR HANDLING

RESERVED FILENAME: 'error.js'

- 'error.js' handles errors in the sibling 'page.js' file or nested 'page' or 'layout'
- if put on root, handles all errors
- receives error prop
- REQUIRED: needs to be client component - so it can catch errors on client / and server

```js
"use client";

export default function Error({ error }) {
  return (
    <main className="error">
      <h1>Error</h1>
      <p>an error occured</p>
    </main>
  );
}
```

NOT FOUND

RESERVED FILENAME: 'not-found.js'

- catches

```js
export default function NotFound() {
  return (
    <main className="not-found">
      <h1>Not found</h1>
      <p>requested resource not found</p>
    </main>
  );
}
```

- you can trigger the not found page
- NOTE: will show closest 'not-found' OR 'error' page,
- so if error is closer than not-found page, it will show error page if its closer, unless a not-found page is put at same level as the error page to make them equally close.

```js
import { notFound } from "next/navigation";

if (!meal) {
  notFound();
}
```
