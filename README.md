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

DYNAMIC ROUTES
using [placeholder] folder:

blog/page.js
blog/[placeholder]/page.js

[placeholder]/page.js

//gets access to props to destructure a {params} object

- every placeholder will be a key in params object and its value will be the url concrete value (whatever was passed in)

export default function SomePage({param}) {
console.log(params.placeholder);  
}

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

import Image from 'next/image';

<Image src={} alt="" priority/>

HARDCODED ASSETS:
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
Layout renders <html> and <body> tags
Layout - every nextjs app needs atleast 1 root layout.js

- the metadata variable is reserved name and is part of the <head> which is handled by nextJs

export const metadata = {
title:'',
description:''
};

export default function RootLayout({children}{
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

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
